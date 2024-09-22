<script>
	import Checkbox from '../../checkbox.svelte';
	import Graph from '../../graph.svelte';
	import Legend from '../../legend.svelte';
	import Metric from '../../metric.svelte';
	import ProgressBar from '../../progressBar.svelte';
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';
	// firebase, firestore imports

	import { session } from '$lib/session';
	import { auth, db } from '$lib/firebase.client';
	import * as firestore from 'firebase/firestore';

	/**
	 * @type {firestore.DocumentData | null}
	 */
	let companyData = null;
	import TopLeft from '../../icons/topLeft.svelte';
	import BottomRight from '../../icons/bottomRight.svelte';

	onMount(async () => {
		if (!localStorage.getItem('uid')) {
			goto('/');
		}

		// @ts-ignore
		const docRef = firestore.doc(db, 'users', localStorage.getItem('uid'));
		const docSnap = await firestore.getDoc(docRef);
		
		if (docSnap.exists()) {
			companyData = docSnap.data();
			// find company in "businesses" collection with business_name == companyData.displayName
			const businessRef = firestore.collection(db, 'businesses');
			const businessQuery = firestore.query(businessRef, firestore.where('business_name', '==', companyData.displayName));
			const businessSnap = await firestore.getDocs(businessQuery);
			const businessData = businessSnap.docs[0].data();

			companyData = businessData;
		}
	});

	function signout() {
		localStorage.clear();
		session.set({loggedIn: false, user: null});
		goto('/');
	}


	// load
</script>

<div class="background-containers">
	<div class="topleft-container">
		<TopLeft />
	  </div>
	  
	  <div class="bottomright-container">
		<BottomRight />
	  </div>
</div>

<div class="dashboardContainer">
	<div class="dashboardLeft">
		<div class="dashboardTitle">
			<h1>Dashboard</h1>
			<!-- if companyData then show companyData.business_rating -->
			<!-- {#if companyData}
				<h2>{companyData.business_rating}</h2>
			{/if} -->
			<p>Review Average</p>
		</div>

		<div class="graphContainer">
			<Graph />
		</div>
	</div>

	<div class="dashboardRight">
		<div>
			<div class="right-top" style="display:flex;flex-direction:row;justify-content:space-between">
				<h2>Key Metrics</h2>
				<button on:click={signout}>Sign Out</button>
			</div>
			<div class="greyBox" style="display:flex;flex-direction:row;justify-content:space-between;">
				<Metric change={5.21} number={10.51} name="NPS" />
				<Metric change={5.21} number={10.51} name="Review Count" up={false} />
			</div>
		</div>
		<div class="middleSection">
			<div class="middleLeft">
				<p>Click on a company in the legend to start an in-depth comparison</p>
				<div class="checkboxes">
					<div class="check">
						<Checkbox />
						<p>Hide Competition</p>
					</div>
					<div class="check">
						<Checkbox />
						<p>Hide Average</p>
					</div>
				</div>
			</div>
			<div class="middleRight">
				<ProgressBar progress={0.4} barColor="#95E398" name="Food" />
				<ProgressBar progress={0.7} barColor="#F3A0F7" name="Environment" />
				<ProgressBar progress={0.5} barColor="#54bdff" name="Service" />
			</div>
		</div>
		<div>
			<h2>Legend</h2>
			<div class="legendBottom">
				<div>
					<Legend color="#95E398" name="You" />
					<Legend color="#DCF086" name="Comp Average" />
				</div>
				<div>
					<Legend color="#F3A0F7" name="Company A" route="/comp/a" />
					<Legend color="#54bdff" name="Company B" route="/comp/b" />
				</div>
			</div>
		</div>
	</div>
</div>

<style>
	@import '/src/styles.css';

	.dashboardContainer {
		display: flex;
		flex-direction: row;
		width: 100vw;
		height: 100vh;
		z-index:1;
	}

	.dashboardLeft {
		flex-grow: 1;
		padding: 55px;
		display: flex;
		flex-direction: column;
		z-index:1;
	}

	.dashboardRight {
		width: 600px;
		padding: 55px;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		margin-bottom: 30px;
		z-index:1;
	}

	.check {
		display: flex;
		flex-direction: row;
	}

	.graphContainer {
		width: 100%;
		height: calc(100vh - 30px);
		margin-top: 20px;
	}

	.dashboardTitle {
		margin-bottom: 30px;
	}

	:global(body) {
		height: 100%;
		overflow-y: hidden;
		margin: 0px;
		padding: 0px;
		width: 100vw;
		height: 100vh;
	}

	.background-containers {
		position: fixed;
		top: 0;
		left: 0;
		width: 100vw;
		height: 100vh;
		pointer-events: none;
		z-index: 0;
  	}

	.topleft-container {
		position: absolute;
		top: -200px;
		left: -170px;
	}

  	.bottomright-container {
		position: absolute;
		bottom: -300px;
		right: -50px;
	}

	.middleSection {
		display: flex;
		flex-direction: row;
	}

	.middleLeft {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	.middleRight {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		height: 220px;
		margin-left: 10px;
	}

	.checkboxes > .check {
		margin-top: 15px;
	}

	.legendBottom {
		display: flex;
		flex-direction: row;
	}

	.legendBottom > div {
		margin-right: 70px;
		display: flex;
		flex-direction: column;
		height: 70px;
		justify-content: space-between;
	}

	button {
		padding: 0;
		border: none;
		font-size: 23px;
		font-weight: 300;
		background: none;
	}
</style>

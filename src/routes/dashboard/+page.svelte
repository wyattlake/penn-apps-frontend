<script>
	import Checkbox from '../../checkbox.svelte';
	import Graph from '../../graph.svelte';
	import Legend from '../../legend.svelte';
	import Metric from '../../metric.svelte';
	import ProgressBar from '../../progressBar.svelte';
	import { auth, db } from '$lib/firebase.client';
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';

    onMount(async () => {
        if (!auth.currentUser) {
            goto('/');
        }
    });
</script>

<div class="dashboardContainer">
	<div class="dashboardLeft">
		<div class="dashboardTitle">
			<h1>Dashboard</h1>
			<p>Review Average</p>
		</div>

		<div class="graphContainer">
			<Graph />
		</div>
	</div>

	<div class="dashboardRight">
		<div>
			<h2>Key Metrics</h2>
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
				<ProgressBar progress={0.7} barColor="#F3A0F7" name="Cleanliness" />
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
					<Legend color="#F3A0F7" name="Company A" />
					<Legend color="#54bdff" name="Company B" />
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
	}

	.dashboardLeft {
		flex-grow: 1;
		padding: 55px;
		display: flex;
		flex-direction: column;
	}

	.dashboardRight {
		width: 600px;
		padding: 55px;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		margin-bottom: 30px;
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
</style>

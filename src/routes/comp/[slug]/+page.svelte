<script lang="ts">
	import { page } from '$app/stores';
	import MiniGraph from '../../../miniGraph.svelte';
	import { goto } from '$app/navigation';
	import { onMount } from 'svelte';

	import { session } from '$lib/session';
	import { auth, db } from '$lib/firebase.client';
	import * as firestore from 'firebase/firestore';

	let slug_id = $page.params.slug;

	let updateToggle = true;

	function signout() {
		localStorage.clear();
		session.set({ loggedIn: false, user: null });
		goto('/');
	}

	function compback() {
		goto('/dashboard');
	}

	let yname = '';
	let cname = '';
	let categories1: String[] = [];
	let categories2: String[] = [];
	let ydata1: number[] = [];
	let cdata1: number[] = [];
	let ydata2: number[] = [];
	let cdata2: number[] = [];

	onMount(async () => {
		if (!localStorage.getItem('uid')) {
			goto('/');
		}

		// @ts-ignore
		const docRef = firestore.doc(db, 'users', localStorage.getItem('uid'));
		const docSnap = await firestore.getDoc(docRef);

		if (docSnap.exists()) {
			const companyData = docSnap.data();
			// find company in "businesses" collection with business_name == companyData.displayName
			const businessRef = firestore.collection(db, 'businesses');
			const businessQuery = firestore.query(
				businessRef,
				firestore.where('business_name', '==', companyData.displayName)
			);
			const businessSnap = await firestore.getDocs(businessQuery);
			const r1 = businessSnap.docs[0].data();

			// @ts-ignore
			const d2 = firestore.doc(db, 'businesses', slug_id);
			let a2 = await firestore.getDoc(d2);
			let r2 = a2.data();

			let raw_categories = [
				'Sep 2023',
				'Oct 2023',
				'Nov 2023',
				'Dec 2023',
				'Jan 2024',
				'Feb 2024',
				'Mar 2024',
				'Apr 2024',
				'May 2024',
				'Jun 2024',
				'Jul 2024',
				'Aug 2024'
			].reverse();

			if (r1 != null && r2 != null) {
				yname = r1.business_name;
				cname = r2.business_name;
				for (let raw_category of raw_categories) {
					if (
						r1.moving_avg_rating[raw_category] != undefined &&
						r2.moving_avg_rating[raw_category] != undefined
					) {
						categories1.push(raw_category.substring(0, 3));

						ydata1.push(r1.moving_avg_rating[raw_category].toFixed(2));
						cdata1.push(r2.moving_avg_rating[raw_category].toFixed(2));

						if (categories1.length == 6) {
							break;
						}
					}
				}

				console.log(r1);

				for (let raw_category of raw_categories) {
					if (
						r1.monthly_reviews_count[raw_category] != undefined &&
						r2.monthly_reviews_count[raw_category] != undefined
					) {
						categories2.push(raw_category.substring(0, 3));

						ydata2.push(r1.monthly_reviews_count[raw_category]);
						cdata2.push(r2.monthly_reviews_count[raw_category]);

						if (categories2.length == 6) {
							break;
						}
					}
				}
			}

			updateToggle = !updateToggle;
		}
	});
</script>

<div class="graphSidebar">
	<div class="dataBox">
		<h2>Review Averages</h2>
		<div class="graphContainer">
			{#key updateToggle}
				<MiniGraph cdata={cdata1} ydata={ydata1} categories={categories1} {cname} />
			{/key}
		</div>
	</div>
	<div class="dataBox">
		<h2>Review Counts</h2>
		<div class="graphContainer">
			{#key updateToggle}
				<MiniGraph cdata={cdata2} ydata={ydata2} categories={categories2} {cname} />
			{/key}
		</div>
	</div>
</div>

<div class="article">
	<div style="display:flex;flex-direction:row;justify-content:space-between;align-items: flex-end;">
		<h1>Direct Comparison</h1>
		<div style="display:flex;flex-direction:row;gap:20px;margin-bottom:10px">
			<button on:click={compback}>Dashboard</button>
			<button on:click={signout}>Sign Out</button>
		</div>
	</div>

	<h2>AI Suggestions</h2>
	<p>
		Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut metus nisi, interdum id tempor sed,
		elementum vel turpis. Phasellus accumsan tempor libero, a porttitor nisl dictum quis. Quisque et
		dapibus nunc, eget convallis dolor. Donec sit amet blandit libero. Aenean purus sem, dignissim
		in mauris in, eleifend pretium metus. In in orci diam. Vestibulum rutrum eget ligula eget
		posuere. Sed maximus sollicitudin porttitor. Pellentesque ac molestie ligula. Fusce velit nisl,
		consequat nec semper nec, elementum a ante. In sit amet tellus id sem pretium molestie id a
		purus. Proin ac convallis arcu. Morbi dignissim imperdiet enim et congue. Cras ac tempor nisi,
		in semper ex. Phasellus scelerisque, quam vel congue rutrum, quam massa egestas diam, vitae
		gravida erat dui eu nunc. Suspendisse dapibus, nibh ut blandit vehicula, nulla tellus luctus
		velit, non ultricies lorem eros eget ex. Suspendisse sagittis tristique leo quis porttitor. Ut
		venenatis convallis venenatis. Nunc at ante sodales, sollicitudin dui sit amet, condimentum
		enim. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque posuere mi
		urna, sit amet dignissim lacus volutpat eu. Aenean sit amet neque ligula. Integer ut dui orci.
		Duis eget sem vestibulum, scelerisque ligula ultrices, laoreet velit. Fusce nec quam sit amet
		nisi tempor tempor ac at nulla. Donec suscipit condimentum aliquet. Mauris gravida elementum
		efficitur. Nunc ac nisi enim. Nullam volutpat ex cursus augue eleifend, at finibus nibh sodales.
		Nunc malesuada interdum accumsan. Mauris at velit sed leo molestie fermentum quis ut erat.
		Vestibulum quis leo tincidunt lorem varius cursus. Integer sed ante nisl. Aliquam sagittis
		bibendum ligula eu ultricies. Quisque sit amet nisl at mi scelerisque sodales. Nunc et odio eget
		augue volutpat lacinia malesuada ut arcu. Duis consectetur semper ex a porttitor. Nullam et sem
		dui. Suspendisse maximus lectus eu purus tristique, euismod gravida eros pellentesque. In
		vehicula sagittis orci vel dictum. Cras vel molestie enim. Vivamus semper vehicula nunc.
		Vestibulum eget nisi neque. Praesent tortor ante, aliquet non nisl faucibus, dapibus porta nisi.
		Aliquam bibendum mollis neque, ac rutrum orci lacinia at. Donec in lorem porttitor nisl faucibus
		pulvinar quis eu ipsum. Quisque iaculis urna ac quam placerat pulvinar. Maecenas eget ex vel sem
		luctus finibus vitae eu metus. Donec in massa eros. Suspendisse nunc erat, faucibus et nulla
		ultricies, rhoncus dapibus sapien. Quisque porta tristique sem at varius. Donec quis fringilla
		turpis. Aenean feugiat euismod felis quis sollicitudin.
	</p>

	<h2>AI Suggestions</h2>
	<p>
		Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut metus nisi, interdum id tempor sed,
		elementum vel turpis. Phasellus accumsan tempor libero, a porttitor nisl dictum quis. Quisque et
		dapibus nunc, eget convallis dolor. Donec sit amet blandit libero. Aenean purus sem, dignissim
		in mauris in, eleifend pretium metus. In in orci diam. Vestibulum rutrum eget ligula eget
		posuere. Sed maximus sollicitudin porttitor. Pellentesque ac molestie ligula. Fusce velit nisl,
		consequat nec semper nec, elementum a ante. In sit amet tellus id sem pretium molestie id a
		purus. Proin ac convallis arcu. Morbi dignissim imperdiet enim et congue. Cras ac tempor nisi,
		in semper ex. Phasellus scelerisque, quam vel congue rutrum, quam massa egestas diam, vitae
		gravida erat dui eu nunc. Suspendisse dapibus, nibh ut blandit vehicula, nulla tellus luctus
		velit, non ultricies lorem eros eget ex. Suspendisse sagittis tristique leo quis porttitor. Ut
		venenatis convallis venenatis. Nunc at ante sodales, sollicitudin dui sit amet, condimentum
		enim. Interdum et malesuada fames ac ante ipsum primis in faucibus. Pellentesque posuere mi
		urna, sit amet dignissim lacus volutpat eu. Aenean sit amet neque ligula. Integer ut dui orci.
		Duis eget sem vestibulum, scelerisque ligula ultrices, laoreet velit. Fusce nec quam sit amet
		nisi tempor tempor ac at nulla. Donec suscipit condimentum aliquet. Mauris gravida elementum
		efficitur. Nunc ac nisi enim. Nullam volutpat ex cursus augue eleifend, at finibus nibh sodales.
		Nunc malesuada interdum accumsan. Mauris at velit sed leo molestie fermentum quis ut erat.
		Vestibulum quis leo tincidunt lorem varius cursus. Integer sed ante nisl. Aliquam sagittis
		bibendum ligula eu ultricies. Quisque sit amet nisl at mi scelerisque sodales. Nunc et odio eget
		augue volutpat lacinia malesuada ut arcu. Duis consectetur semper ex a porttitor. Nullam et sem
		dui. Suspendisse maximus lectus eu purus tristique, euismod gravida eros pellentesque. In
		vehicula sagittis orci vel dictum. Cras vel molestie enim. Vivamus semper vehicula nunc.
		Vestibulum eget nisi neque. Praesent tortor ante, aliquet non nisl faucibus, dapibus porta nisi.
		Aliquam bibendum mollis neque, ac rutrum orci lacinia at. Donec in lorem porttitor nisl faucibus
		pulvinar quis eu ipsum. Quisque iaculis urna ac quam placerat pulvinar. Maecenas eget ex vel sem
		luctus finibus vitae eu metus. Donec in massa eros. Suspendisse nunc erat, faucibus et nulla
		ultricies, rhoncus dapibus sapien. Quisque porta tristique sem at varius. Donec quis fringilla
		turpis. Aenean feugiat euismod felis quis sollicitudin.
	</p>
</div>

<style>
	@import '/src/styles.css';

	:global(body) {
		margin: 0px;
		padding: 0px;
	}
	.graphContainer {
		height: 300px;
		margin: 20px;
	}

	.graphSidebar {
		width: 500px;
		display: flex;
		flex-direction: column;
		height: 100%;
		overflow-x: hidden;
		position: fixed;
		top: 0;
		right: 0;
		z-index: 1;
		background-color: white;
		border-left: 1px solid #c4c4c4;
		margin-left: 50px;
	}

	:global(html) {
		scrollbar-width: none;
	} /* Firefox */
	:global(body) {
		-ms-overflow-style: none;
	} /* IE and Edge */
	:global(body)::-webkit-scrollbar,
	:global(body)::-webkit-scrollbar-button {
		display: none;
	}

	.article {
		width: calc(100vw - 650px);
		margin-left: 75px;
		margin-top: 100px;
	}

	.dataBox > h2 {
		padding-left: 50px;
	}

	.graphSidebar {
		padding-top: 20px;
		padding-bottom: 20px;
		height: 100vh;
	}
	button {
		padding: 0;
		border: none;
		font-size: 23px;
		font-weight: 300;
		background: none;
	}
</style>

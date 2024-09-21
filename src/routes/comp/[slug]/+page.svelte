<script>
	import { page } from '$app/stores';
	import MiniGraph from '../../../miniGraph.svelte';

	let slug_id = $page.params.slug;
</script>

<div class="graphSidebar">
	<div class="dataBox">
		<h2>Review Averages</h2>
		<div class="graphContainer">
			<MiniGraph />
		</div>
	</div>
	<div class="dataBox">
		<h2>Review Counts</h2>
		<div class="graphContainer">
			<MiniGraph />
		</div>
	</div>
</div>

<div class="article">
	<h1>Direct Comparison</h1>

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
		margin: 0px;
		width: 400px;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		height: 100%;
		overflow-x: hidden;
		position: fixed;
		top: 0;
		right: 0;
		z-index: 1;
		background-color: white;
		border: 1px solid grey;
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
		width: calc(100vw - 550px);
		margin-left: 75px;
		margin-top: 100px;
	}
</style>

<script>
	import Typewriter from 'svelte-typewriter';
	import Logo from '../icons/logo.svelte';
	import Background from '../icons/background.svelte';
	import TitleGraphic from '../icons/titleGraphic.svelte';
</script>

<meta name="viewport" content="width=device-width, initial-scale=1.0" />

<div class="background-container">
	<Background />
</div>

<div class="background-graph-container">
	<TitleGraphic />
</div>

<div class="content-container">
	<header class="mb-2">
		<div class="logo">
			<Logo scale={0.38} />
		</div>
	</header>
	<main class="flex-grow flex items-center">
		<div class="text-container">
			<h1>
				Building
				<span class="gradient-text">data analytics</span>
				solutions for
				<span class="typewriter-container">
					<Typewriter mode="loop">
						<h1 class="gradient-text">small businesses</h1>
						<h1 class="gradient-text">nonprofits</h1>
						<h1 class="gradient-text">innovators</h1>
					</Typewriter>
				</span>
			</h1>
			<h2>
				We utilize web scraping and super fast AI technology to create competitive recommendations
				for your business
			</h2>
		</div>
		<div class="button-container" style="margin-top: 50px">
			<a href="/login" class="btn btn-secondary">Login</a>
			<a href="/signup" class="btn btn-primary">Sign Up</a>
		</div>
	</main>
</div>

<style>
	:global(body) {
		font-family: Arial, sans-serif;
		line-height: 1.2;
		overflow: hidden;
		margin: 0;
		padding: 0;
	}

	.btn {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		padding: 0.5rem 1rem;
		font-size: 1.4rem;
		font-weight: 500;
		text-decoration: none;
		border-radius: 1rem;
		transition: background-color 0.3s ease;
		width: 135px;
		height: 40px;
	}

	.btn:focus {
		outline: none;
		box-shadow: 0 0 0 3px rgba(66, 153, 225, 0.5);
	}

	.btn-primary {
		background-color: #a1eea4;
		color: white;
		border: 0.6px solid #a1eea4;
	}

	.btn-secondary {
		background-color: #edf4fb;
		color: #000000;
		width: 100px;
		border: 0.6px solid #808080;
	}

	.btn-secondary:hover {
		background-color: #e2e8f0;
	}

	.background-container {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		z-index: -1;
	}

	.background-container :global(svg) {
		width: 130vw;
		height: 160vh;
		transform: translate(-19%, -24%) rotate(0.51turn);
		object-fit: cover;
	}

	.background-graph-container {
		position: absolute;
		bottom: -150px;
		right: -70px;
	}

	.content-container {
		position: relative;
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		padding: 4rem;
	}

	.text-container {
		max-width: 1000px;
		margin-top: 100px;
		display: flex;
		flex-direction: column;
	}

	.button-container {
		display: flex;
		gap: 1rem;
		margin-top: 1rem;
	}

	.typewriter-container {
		--cursor-width: 3px;
		--cursor-color: #95e398;
		display: flex;
	}

	h1 {
		font-size: 3.5rem;
		margin: 0;
	}

	h2 {
		font-size: 1.6rem;
		font-weight: normal;
	}

	.gradient-text {
		display: inline-block;
		background: linear-gradient(180deg, #77c893, #a9f095, #c0f5aa);
		-webkit-background-clip: text;
		background-clip: text;
		-webkit-text-fill-color: transparent;
		background-size: 200% 200%;
	}

	@keyframes gradient {
		0% {
			background-position: 0% 50%;
		}
		50% {
			background-position: 100% 50%;
		}
		100% {
			background-position: 0% 50%;
		}
	}

	@media (max-width: 400px) {
		h1 {
			font-size: 2rem;
		}
	}
</style>

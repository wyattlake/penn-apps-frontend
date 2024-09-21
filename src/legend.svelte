<script>
	export let name = 'None';
	export let color = '#000000';
</script>

<div class="legendContainer" style="--color: {color}">
	<div class="colorDot"></div>
	<p>{name}</p>
</div>

<style>
	.colorDot {
		width: 25px;
		height: 25px;
		border-radius: 12.5px;
		background-color: var(--color);
	}

	.legendContainer {
		display: flex;
		flex-direction: row;
		align-items: center;
	}

	.legendContainer > p {
		margin-top: 0px;
		margin-bottom: 0px;
		font-size: 23px;
		margin-left: 10px;
		font-weight: 300;
	}
</style>

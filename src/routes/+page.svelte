<script>
	import { Canvas } from '@threlte/core'
    import { Studio } from '@threlte/theatre'
    import Scene from '../components/Scene.svelte';
</script>

<div class="scene">
	<Canvas dpr={1.0}>
        <Studio enabled={false} />
		<Scene />
	</Canvas>
</div>

<style>
	.scene {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
	}
</style>
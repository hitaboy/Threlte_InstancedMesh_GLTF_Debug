<script>
    import { Object3DInstance } from '@threlte/core'
    import { useGltf, useGltfAnimations } from '@threlte/extras'
    
    const { gltf } = useGltf('/models/Anim_Flagtail/Anim_Flagtail.gltf')
    useGltfAnimations(gltf, ({ actions }) => {
        actions.animation_0?.play()
        console.log(actions)
    })

    $: if ($gltf) {
        console.log($gltf)
        $gltf.materials['MI_Flagtail'].metalness = 0;
        $gltf.materials['MI_Flagtail'].roughness = 0;
        $gltf.materials['MI_Flagtail'].fog = false;
        $gltf.materials['MI_Flagtail'].color = {r:1,g:1,b:1,isColor:true};
    }
    
</script>

{#if $gltf}
    <Object3DInstance object={$gltf.nodes['SK_Flagtail_LOD11_(Copy)']} />
{/if}
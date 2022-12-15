<script>
    import { InstancedMesh, Instance, OrbitControls, useFrame, T } from '@threlte/core'
	import { BackSide, sRGBEncoding  } from 'three';
    import { Project } from '@threlte/theatre'
    import { useGltf } from '@threlte/extras'
    import state from './state.json'
    const { gltf } = useGltf('/models/Anim_Flagtail/Anim_Flagtail.gltf')
    let geometry
    let material
    $: if ($gltf) {
        /*
        $gltf.materials['MI_Flagtail'].metalness = 0;
        $gltf.materials['MI_Flagtail'].roughness = 0;
        $gltf.materials['MI_Flagtail'].fog = false;
        $gltf.materials['MI_Flagtail'].color = {r:1,g:1,b:1,isColor:true};
        */
        material = $gltf.materials['MI_Flagtail']
        geometry = $gltf.nodes['SK_Flagtail_LOD11_(Copy)'].geometry
    }

    $: console.log(material, geometry)
    // Definim una animació de Theatre.js i l'arrenquem
    let sequence
    
</script>

<Project name="UnderwaterProject" config={{ state }}>
<T.PerspectiveCamera makeDefault position={[0, -30, 45]} fov={100}>
    <OrbitControls autoRotate={false} enableZoom={true} target={{ y: 0.5 }} />
</T.PerspectiveCamera>

    <T.AmbientLight intensity={1.0} />

    {#if geometry && material}

       <InstancedMesh geometry={geometry.toNonIndexed()} material={material.clone()}>
            <Instance />
        </InstancedMesh>

    {/if}

    <T.Mesh>
        <T.SphereGeometry args={[55, 32, 16 ]}/>
        <T.MeshStandardMaterial color="#ffffff" side={BackSide} metalness={0} />
    </T.Mesh>

    <T.Mesh>
        <T.SphereGeometry args={[5, 32, 16 ]}/>
        <T.MeshStandardMaterial color="#ff0000" side={BackSide} metalness={0} />
    </T.Mesh>

    <!--
    <Sheet name="Box animation" bind:sequence>
    <T.Mesh receiveShadow castShadow position.y={0.5}>
        <Editable name="Box / Mesh" transform controls />
        <T.BoxGeometry args={[1, 1, 1]} />
        <T.MeshStandardMaterial color="#b00d03">
            <Editable name="Box / Material" color roughness metalness />
        </T.MeshStandardMaterial>
    </T.Mesh>
    </Sheet>
    -->
    
</Project>
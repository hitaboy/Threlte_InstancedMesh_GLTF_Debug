<script>
    import { InstancedMesh, Instance, OrbitControls, T } from '@threlte/core'
	import { BackSide, MeshStandardMaterial, SphereGeometry } from 'three';
    import { Project } from '@threlte/theatre'
    import Flagtail from './Fishes/Flagtail.svelte';
    import state from './state.json'
    
    const geometry = new SphereGeometry(4.5)
    const material = new MeshStandardMaterial()

    // Definim una animació de Theatre.js i l'arrenquem
    let sequence
    
</script>

<Project name="UnderwaterProject" config={{ state }}>
<T.PerspectiveCamera makeDefault position={[0, -30, 45]} fov={100}>
    <OrbitControls autoRotate={false} enableZoom={true} target={{ y: 0.5 }} />
</T.PerspectiveCamera>

    <T.AmbientLight intensity={1.0} />

       <InstancedMesh>
            <Instance position={{x:15,y:-10,z:-35}}>
                <Flagtail />
            </Instance>
            <Instance position={{x:-15,y:-2,z:0}}>
                <Flagtail />
            </Instance>
        </InstancedMesh>

    <T.Mesh>
        <T.SphereGeometry args={[55, 32, 16 ]}/>
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
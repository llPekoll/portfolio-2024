<script lang="ts">
  import type * as THREE from 'three'
  import { Group, Color, MeshLambertMaterial, FrontSide } from 'three'
  import { T, type Props, type Events, type Slots, forwardEventHandlers, useTask } from '@threlte/core'
  import { useGltf } from '@threlte/extras'
  import { useTexture } from '@threlte/extras'
  
  let scaleFactor=0;
  let color=0xb83609;
  $: innerWidth=0;
$: {
  if (innerWidth <= 640) {
    scaleFactor = 0.6;
    color = 0xb83609;
  } else {
    scaleFactor = 1;
    color = 0xea580b;
  }
}
  type $$Props = Props<THREE.Group>
  type $$Events = Events<THREE.Group>
  type $$Slots = Slots<THREE.Group> & { fallback: {}; error: { error: any } }

  export const ref = new Group()

  type GLTFResult = {
    nodes: {
      mesh: THREE.Mesh
    }
    materials: {
      material_0: THREE.MeshLambertMaterial
    }
  }

    const gltf = useGltf<GLTFResult>('/models/peko2.glb')
    const map = useTexture('/models/text_low.jpg')

  const assets = Promise.all([gltf, map]);


  
  const component = forwardEventHandlers()
  let rotation = 0
  let jose = 0
  useTask((delta) => {
    const f = 1 / 60 / delta
    rotation += 0.0003 * f
  })
  
</script>
<svelte:window bind:innerWidth />
<T is={ref} dispose={false} {...$$restProps} bind:this={$component}>
    {#await assets}
        <slot name="fallback" />
        {:then [gltf, map]}
        <T.Mesh  rotation.y={1.2+rotation} geometry={gltf.nodes.mesh.geometry} scale={39.9*1.2* scaleFactor} >
            <T.MeshLambertMaterial 
                map={map} 
                color={0x000000}
            />
        </T.Mesh>
            <T.Mesh  rotation.y={1.2+rotation} geometry={gltf.nodes.mesh.geometry} scale={40*1.2* scaleFactor} >
                <T.MeshLambertMaterial 
                    color={color}
                    side={FrontSide}
                    wireframe={true}
                    wireframeLinecap={'round'}
                    wireframeLinewidth={.2}
                    fog={true}
                />
            </T.Mesh>
        {:catch error}
            <slot name="error" {error} />
        {/await}
    <slot {ref} />
</T>
    
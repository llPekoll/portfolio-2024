<script lang="ts">
  import { T } from '@threlte/core'
  // import { Fog } from 'three'
  import Peko  from '$lib/components/models/Peko.svelte';
</script>
<T.PerspectiveCamera
  makeDefault
  position={[10, 7, 10]}
  on:create={({ ref }) => {
    ref.lookAt(0, 1.5, 0)
  }}
/>
<T.DirectionalLight
  intensity={25}
  
/>
<!-- <Fog color={'#dddddd'} /> -->
<T.AmbientLight intensity={0.25} />
<Peko />
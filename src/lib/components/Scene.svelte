<script lang="ts">
  import { T } from '@threlte/core'
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
  intensity={132}
  color={0xea580d}
  position={[-10, 0, 0]}
  
/>
<T.DirectionalLight
  intensity={132}
  color={0xea580d}
  position={[-10, 0, -130]}
  
/>
<T.AmbientLight intensity={0.05} />
<Peko />
<script>
  import * as THREE from "three";

  import Experience from "$lib/experience.svelte";
  let scene = new THREE.Scene();

  const geometry = new THREE.BoxGeometry(1, 1, 1);
  const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
  const cube = new THREE.Mesh(geometry, material);
  scene.add(cube);




</script>

<Experience scene = {scene} />

<style>
</style>

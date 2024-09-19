<script>
  import { browser } from "$app/environment";
  import { onMount } from "svelte";
  import * as THREE from "three";
  import { OrbitControls } from "three/addons/controls/OrbitControls.js";

  export let scene = new THREE.Scene();

  let root;

  onMount(() => {
    const canvas = root.querySelector(".webgl");

    
    // Do something with nd, such as adding event listeners, styles, etc.

    if (browser) {
      let width = canvas.getBoundingClientRect().width;
      let height = canvas.getBoundingClientRect().height;

      const renderer = new THREE.WebGLRenderer({
        canvas,
        antialias: true,
      });
      renderer.setSize(width, height);




      const camera = new THREE.PerspectiveCamera(
        45,
        width / height,
        1,
        10000
      );

      const controls = new OrbitControls(camera, renderer.domElement);

      //controls.update() must be called after any manual changes to the camera's transform
      camera.position.set(0, 20, 100);
      controls.update();

      function animate() {
        requestAnimationFrame(animate);

        // required if controls.enableDamping or controls.autoRotate are set to true
        controls.update();

        renderer.render(scene, camera);
      }
      animate();
    }
  });
</script>

<div bind:this={root}>
  <canvas class="webgl"></canvas>
</div>




<style>
  div{
    width: 100%;
    height: 100%;
  }
  canvas {
    width: 100%;
    height: 100%;
  }
</style>
<script>
  import { browser } from "$app/environment";
  import * as THREE from "three";
  import { onMount } from "svelte";

  import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";
  import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader.js";
  //import { gsap } from "gsap";

  let root;
  onMount(() => {
    const canvas = root.querySelector(".webgl");
    // Do something with nd, such as adding event listeners, styles, etc.

    if (browser) {
      const loadingManager = new THREE.LoadingManager(
        // Loaded
        () => {
          // Wait a little
          window.setTimeout(() => {
            // Animate overlay
            gsap.to(overlayMaterial.uniforms.uAlpha, {
              duration: 3,
              value: 0,
              delay: 1,
            });

            // Update loadingBarElement
            loadingBarElement.classList.add("ended");
            loadingBarElement.style.transform = "";
          }, 500);

          window.setTimeout(() => {
            sceneReady = true;
          }, 2000);
        },

        // Progress
        (itemUrl, itemsLoaded, itemsTotal) => {
          // Calculate the progress and update the loadingBarElement
          const progressRatio = itemsLoaded / itemsTotal;
          loadingBarElement.style.transform = `scaleX(${progressRatio})`;
        }
      );

      const gltfLoader = new GLTFLoader(loadingManager);
      const cubeTextureLoader = new THREE.CubeTextureLoader(loadingManager);

      const scene = new THREE.Scene();

      /**
       * Background
       */
      const params = {
        color: "#ffffff",
      };
      scene.background = new THREE.Color(params.color);

      /**
       * Models
       */

      gltfLoader.load("/models/BlockDiagram.gltf", (gltf) => {
        gltf.scene.scale.set(1, 1, 1);
        gltf.scene.rotation.set(0, 0, 0);
        scene.add(gltf.scene);

        updateAllMaterials();
      });

      const camera = new THREE.PerspectiveCamera(
        75,
        window.innerWidth / window.innerHeight,
        0.1,
        1000
      );
      /**
       * Lights
       */
      const directionalLight = new THREE.DirectionalLight("#ffffff", 3);
      directionalLight.castShadow = true;
      directionalLight.shadow.camera.far = 15;
      directionalLight.shadow.mapSize.set(1024, 1024);
      directionalLight.shadow.normalBias = 0.05;
      directionalLight.position.set(0.25, 3, -2.25);
      scene.add(directionalLight);

      // Controls
      const controls = new OrbitControls(camera, canvas);
      controls.enableDamping = true;

      /**
       * Renderer
       */

      const renderer = new THREE.WebGLRenderer({
        canvas: canvas,
        antialias: true,
      });

      renderer.toneMapping = THREE.ReinhardToneMapping;
      renderer.toneMappingExposure = 3;
      renderer.shadowMap.enabled = true;
      renderer.shadowMap.type = THREE.PCFSoftShadowMap;

      renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

      renderer.setSize(window.innerWidth, window.innerHeight);
      

      /**
       * Sizes
       */

      const sizes = {
        width: window.innerWidth,
        height: window.innerHeight,
      };

      window.addEventListener("resize", () => {
        // Update sizes
        sizes.width = window.innerWidth;
        sizes.height = window.innerHeight;

        // Update camera
        camera.aspect = sizes.width / sizes.height;
        camera.updateProjectionMatrix();

        // Update renderer
        renderer.setSize(sizes.width, sizes.height);
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
      });

      camera.position.z = 5;

      const tick = () => {
        controls.update()
        console.log("hey")
        if (true) {
          // TODO: Implement points and Loading
        }
        renderer.render(scene, camera)
        window.requestAnimationFrame(tick)
      };
      tick()

    }
  });
</script>

<div bind:this={root}>
  <canvas class="webgl"></canvas>
</div>

<style>
  .webgl {
    position: relative;
    top: 0;
    left: 0;
    outline: none;
    height: 100%;
    width: 100%;
    /*height: 10%;*/
  }

  .point {
    position: absolute;
    top: 50%;
    left: 50%;
    /* pointer-events: none; */
  }

  .point .label {
    position: absolute;
    top: 60px;
    left: -20px;
    /*width: 40px;*/
    /*height: 40px;*/
    padding-top: 0px;
    padding-left: 5px;
    padding-right: 5px;
    padding-bottom: -1px;
    border-radius: 4px;
    background: #d0c4c4df;
    border: 1px solid #ffffff77;
    color: #000000;
    font-family: Helvetica, Arial, sans-serif;
    text-align: center;
    line-height: 20px;
    font-weight: 100;
    font-size: 12px;
    cursor: help;
    transform: scale(0, 0);
    transition: transform 0.5s;
  }

  .point .text {
    position: absolute;
    top: 95px;
    left: -120px;
    width: 200px;
    padding: 20px;
    border-radius: 4px;
    background: #dbdbdbe7;
    border: 1px solid #ffffffbe;
    color: #000000;
    line-height: 1.3em;
    font-family: Helvetica, Arial, sans-serif;
    font-weight: 100;
    font-size: 14px;
    opacity: 0;
    transition: opacity 0.8s;
    pointer-events: none;
  }

  .point:hover .text {
    opacity: 1;
  }

  .point.visible .label {
    transform: scale(1, 1);
  }
</style>

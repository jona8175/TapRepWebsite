<script>
  import * as THREE from "three";

  import Experience from "$lib/experience.svelte";
  let scene = new THREE.Scene();

  const geometry = new THREE.BoxGeometry(1, 3, 1);
  const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
  const cube = new THREE.Mesh(geometry, material);
  scene.add(cube);




</script>

<Experience scene = {scene} />

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

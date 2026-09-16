<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- A-Frame -->
  <script src="https://aframe.io/releases/1.6.0/aframe.min.js"></script>

  <!-- MindAR Image Tracking -->
  <script src="https://cdn.jsdelivr.net/npm/mind-ar@1.2.5/dist/mindar-image-aframe.prod.js"></script>

  <!-- Animation Mixer -->
  <script src="https://cdn.jsdelivr.net/gh/c-frame/aframe-extras@7.5.4/dist/aframe-extras.min.js"></script>
</head>

<body>

<a-scene
  mindar-image="imageTargetSrc: https://thunyakorn6239.github.io/targets.mind;"
  vr-mode-ui="enabled: false"
  device-orientation-permission-ui="enabled: false"
  renderer="colorManagement: true;">

  <!-- =========================
       Assets
  ========================== -->
  <a-assets>

    <!-- 3D Model -->
    <a-asset-item
      id="model0"
      src="https://thunyakorn6239.github.io/MBEE.glb">
    </a-asset-item>

  </a-assets>


  <!-- =========================
       Target 1
  ========================== -->
  <a-entity mindar-image-target="targetIndex: 0">

    <a-gltf-model
      src="#model0"
      animation-mixer
      rotation="90 0 0"
      scale="2 2 2">
    </a-gltf-model>

  </a-entity>


  <!-- =========================
       Target 2
  ========================== -->
  <a-entity mindar-image-target="targetIndex: 1">

    <a-gltf-model
      src="#model0"
      animation-mixer
      rotation="90 0 0"
      scale="2 2 2">
    </a-gltf-model>

  </a-entity>


  <!-- =========================
       Target 3
  ========================== -->
  <a-entity mindar-image-target="targetIndex: 2">

    <a-gltf-model
      src="#model0"
      animation-mixer
      rotation="90 0 0"
      scale="2 2 2">
    </a-gltf-model>

  </a-entity>


  <!-- Camera -->
  <a-camera
    position="0 0 0"
    look-controls="enabled: false">
  </a-camera>

</a-scene>

</body>
</html>

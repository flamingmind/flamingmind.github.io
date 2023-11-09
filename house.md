<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://aframe.io/releases/1.2.0/aframe.min.js"></script>
</head>
<body>

    <a-scene>
        <!-- 3D model of a dog (replace with your own model) -->
        <a-entity id="dog" position="0 1.6 -3" scale="0.05 0.05 0.05" rotation="0 180 0" gltf-model="https://cdn.rawgit.com/KhronosGroup/glTF-Sample-Models/master/2.0/Duck/glTF/Duck.gltf"></a-entity>

        <!-- Night background -->
        <a-sky color="#000" material="src: https://images.unsplash.com/photo-1544505861-7142c2ce16e1?auto=format&fit=crop&q=80&w=1000&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8N3x8YW1iaWVudHxlbnwwfHwwfHx8MA%3D%3D"></a-sky>

        <!-- Lighting -->
        <a-light type="ambient" color="#888"></a-light>
        <a-light type="point" position="0 5 0" intensity="2" distance="20"></a-light>

        <!-- Ground plane -->
        <a-plane position="0 0 0" rotation="-90 0 0" width="20" height="20" color="#222"></a-plane>
    </a-scene>

</body>
</html>

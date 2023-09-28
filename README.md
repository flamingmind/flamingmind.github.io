<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Spinning Outlined Cube</title>
</head>
<body>
    <!-- Create a container for the 3D scene -->
    <div id="scene-container"></div>

    <!-- Include Three.js library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

    <script>
        // Set up the scene, camera, and renderer
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer();

        renderer.setSize(window.innerWidth, window.innerHeight);
        document.getElementById("scene-container").appendChild(renderer.domElement);

        // Create a rotating cube with an outlined material
        const geometry = new THREE.BoxGeometry();
        const outlineMaterial = new THREE.MeshBasicMaterial({ color: 0x000000, side: THREE.BackSide });
        const cube = new THREE.Mesh(geometry, outlineMaterial);
        scene.add(cube);

        // Create a solid material for the cube's faces
        const solidMaterial = new THREE.MeshPhongMaterial({ color: 0x00ff00 });
        const solidCube = new THREE.Mesh(geometry, solidMaterial);
        scene.add(solidCube);

        // Add lighting
        const light = new THREE.PointLight(0xffffff);
        light.position.set(5, 5, 5);
        scene.add(light);

        // Position the camera
        camera.position.z = 5;

        // Create an animation loop
        const animate = () => {
            requestAnimationFrame(animate);

            // Rotate the cube
            cube.rotation.x += 0.01;
            cube.rotation.y += 0.01;
            solidCube.rotation.x += 0.01;
            solidCube.rotation.y += 0.01;

            renderer.render(scene, camera);
        };

        animate();
    </script>
</body>
</html>
<head>
  <meta http-equiv='refresh' content='2; URL=https://flamingmind.github.io/'>
</head>

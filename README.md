<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Spinning Brain with Fire Effects</title>
    <!-- Include Three.js library -->
    <script type="module" src="path/to/three.module.js"></script>
</head>
<body>
    <script>
        // Wait for the DOM to be ready
        document.addEventListener('DOMContentLoaded', init);

        function init() {
            // Set up the scene
            const scene = new THREE.Scene();
            const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            const renderer = new THREE.WebGLRenderer();
            renderer.setSize(window.innerWidth, window.innerHeight);
            document.body.appendChild(renderer.domElement);

            // Load the brain model
            const loader = new THREE.GLTFLoader();
            loader.load('path/to/brain.gltf', (gltf) => {
                const brain = gltf.scene;
                scene.add(brain);
            });

            // Create fire effect material (replace 'path/to/fire.jpg' with your fire texture)
            const fireTexture = new THREE.TextureLoader().load('path/to/fire.jpg');
            const fireMaterial = new THREE.MeshBasicMaterial({ map: fireTexture, transparent: true, opacity: 0.7 });

            // Create a plane with fire material to simulate fire effects
            const firePlane = new THREE.Mesh(new THREE.PlaneGeometry(100, 100), fireMaterial);
            scene.add(firePlane);

            // Position the camera
            camera.position.z = 5;

            // Animation loop
            const animate = function () {
                requestAnimationFrame(animate);

                // Rotate the brain
                if (brain) {
                    brain.rotation.x += 0.01;
                    brain.rotation.y += 0.01;
                }

                // Rotate and move the fire plane
                firePlane.rotation.z += 0.005;
                firePlane.position.z = -2;

                renderer.render(scene, camera);
            };

            animate();
        }
    </script>
</body>
</html>

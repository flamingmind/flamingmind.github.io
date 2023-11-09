<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Brain with Fire Effects</title>
    <style>
        body { margin: 0; }
        canvas { display: block; }
    </style>
</head>
<body>
    <script type="module">
        import * as THREE from 'https://threejs.org/build/three.module.js';
        import { GLTFLoader } from 'https://threejs.org/examples/jsm/loaders/GLTFLoader.js';
        import { Fire } from 'https://threejs.org/examples/jsm/libs/Fire.js';

        // Initialize scene
        const scene = new THREE.Scene();

        // Create camera
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        camera.position.z = 5;

        // Create renderer
        const renderer = new THREE.WebGLRenderer();
        renderer.setSize(window.innerWidth, window.innerHeight);
        document.body.appendChild(renderer.domElement);

        // Load brain model
        const loader = new GLTFLoader();
        const brainUrl = 'HTTPS://BRAINURL___'; // Replace with the actual URL
        loader.load(brainUrl, (gltf) => {
            const brain = gltf.scene;
            scene.add(brain);

            // Add fire effect to the brain
            const fireOptions = {
                textureWidth: 512,
                textureHeight: 512,
                debug: false,
            };
            const fireEffect = new Fire(brain, camera, fireOptions);
            scene.add(fireEffect.mesh);
        });

        // Animation
        const animate = () => {
            requestAnimationFrame(animate);

            // Rotate the brain
            if (scene.children.length > 0) {
                const brain = scene.children[1];
                brain.rotation.x += 0.005;
                brain.rotation.y += 0.005;
            }

            // Update fire effect
            if (scene.children.length > 1) {
                const fireEffect = scene.children[2];
                fireEffect.update();
            }

            // Render the scene
            renderer.render(scene, camera);
        };

        // Handle window resize
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });

        // Start animation
        animate();
    </script>
</body>
</html>

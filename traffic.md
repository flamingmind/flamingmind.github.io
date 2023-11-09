<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>City Traffic Simulation</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
    }
    canvas {
      display: block;
    }
  </style>
</head>
<body>
  <script src="https://threejs.org/build/three.js"></script>
  <script src="https://threejs.org/examples/js/loaders/GLTFLoader.js"></script>
  <script src="https://threejs.org/examples/js/controls/OrbitControls.js"></script>

  <script>
    // Set up scene
    const scene = new THREE.Scene();
    
    // Set up camera
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.set(0, 50, 100);

    // Set up renderer
    const renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    // Add orbit controls for navigation
    const controls = new THREE.OrbitControls(camera, renderer.domElement);

    // Add skybox
    const skyboxTexture = new THREE.TextureLoader().load('https://images.unsplash.com/photo-1544505861-7142c2ce16e1?auto=format&fit=crop&q=80&w=1000&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8N3x8YW1iaWVudHxlbnwwfHwwfHx8MA%3D%3D');
    scene.background = skyboxTexture;

    // Load city models
    const loader = new THREE.GLTFLoader();
    
    loader.load('https://flamingmind.github.io/car.gltf', function (carModel) {
      const car = carModel.scene;
      car.scale.set(0.1, 0.1, 0.1); // adjust the scale
      car.position.set(0, 0, 0); // set initial position
      scene.add(car);
    });

    loader.load('https://flamingmind.github.io/tower.gltf', function (towerModel) {
      const tower = towerModel.scene;
      tower.scale.set(1, 1, 1); // adjust the scale
      tower.position.set(10, 0, 10); // set initial position
      scene.add(tower);
    });

    // Create ground (a simple cube for now)
    const groundGeometry = new THREE.BoxGeometry(200, 1, 200);
    const groundMaterial = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
    const ground = new THREE.Mesh(groundGeometry, groundMaterial);
    scene.add(ground);

    // Lights
    const ambientLight = new THREE.AmbientLight(0x404040);
    scene.add(ambientLight);

    const directionalLight = new THREE.DirectionalLight(0xffffff, 0.5);
    directionalLight.position.set(5, 5, 5);
    scene.add(directionalLight);

    // Animation loop
    const animate = function () {
      requestAnimationFrame(animate);

      // Add your simulation logic here

      renderer.render(scene, camera);
    };

    // Handle window resize
    window.addEventListener('resize', function () {
      const newWidth = window.innerWidth;
      const newHeight = window.innerHeight;

      camera.aspect = newWidth / newHeight;
      camera.updateProjectionMatrix();

      renderer.setSize(newWidth, newHeight);
    });

    animate();
  </script>
</body>
</html>

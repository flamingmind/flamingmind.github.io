<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Loading Screen</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background-color: #333;
        }

        .loading-container {
            width: 100vw;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            perspective: 800px;
        }

        .loading-cube {
            width: 100px;
            height: 100px;
            transform-style: preserve-3d;
            animation: spin 2s linear infinite;
        }

        .loading-face {
            position: absolute;
            width: 100px;
            height: 100px;
            background-color: #3498db;
            opacity: 0.8;
            border: 2px solid #fff;
        }

        .loading-face:nth-child(1) { transform: rotateY(0deg) translateZ(50px); }
        .loading-face:nth-child(2) { transform: rotateY(90deg) translateZ(50px); }
        .loading-face:nth-child(3) { transform: rotateY(180deg) translateZ(50px); }
        .loading-face:nth-child(4) { transform: rotateY(-90deg) translateZ(50px); }
        .loading-face:nth-child(5) { transform: rotateX(90deg) translateZ(50px); }
        .loading-face:nth-child(6) { transform: rotateX(-90deg) translateZ(50px); }

        @keyframes spin {
            0% { transform: rotateY(0deg); }
            100% { transform: rotateY(360deg); }
        }
    </style>
</head>
<body>
    <div class="loading-container">
        <div class="loading-cube">
            <div class="loading-face"></div>
            <div class="loading-face"></div>
            <div class="loading-face"></div>
            <div class="loading-face"></div>
            <div class="loading-face"></div>
            <div class="loading-face"></div>
        </div>
    </div>
</body>
</html>
<head>
  <meta http-equiv='refresh' content='2; URL=https://flamingmind.github.io/home'>
</head>
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
  
    <title>
        GeeksforGeeks
    </title>
  
    <!-- add icon link -->
    <link rel="icon" href=
"https://media.geeksforgeeks.org/wp-content/cdn-uploads/gfg_200X200.png" 
          type="image/x-icon">
</head>
  
<body>
    <h1 style="color:green;">
        GeeksforGeeks
    </h1>
  
    <p>
        Welcome to my website
    </p>
</body>
</html>

<meta http-equiv='refresh' content='2; URL=https://www.google.com'>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Centered 3D Loading Screen</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background-color: #333;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .loading-cube {
            width: 100px;
            height: 100px;
            perspective: 800px;
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
    <div class="loading-cube">
        <div class="loading-face"></div>
        <div class="loading-face"></div>
        <div class="loading-face"></div>
        <div class="loading-face"></div>
        <div class="loading-face"></div>
        <div class="loading-face"></div>
    </div>
</body>
</html>

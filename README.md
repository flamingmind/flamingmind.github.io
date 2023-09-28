<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Spinning Cube</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
        }

        .container {
            width: 100vw;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .cube {
            width: 200px;
            height: 200px;
            perspective: 800px;
        }

        .cube .face {
            position: absolute;
            width: 200px;
            height: 200px;
            background-color: transparent;
            border: 1px solid #fff;
            opacity: 0.8;
            transition: transform 2s;
        }

        .cube .face:nth-child(1) { transform: rotateY(0deg) translateZ(100px); }
        .cube .face:nth-child(2) { transform: rotateY(90deg) translateZ(100px); }
        .cube .face:nth-child(3) { transform: rotateY(180deg) translateZ(100px); }
        .cube .face:nth-child(4) { transform: rotateY(-90deg) translateZ(100px); }
        .cube .face:nth-child(5) { transform: rotateX(90deg) translateZ(100px); }
        .cube .face:nth-child(6) { transform: rotateX(-90deg) translateZ(100px); }

        .cube:hover .face {
            animation: spin 4s linear infinite;
        }

        @keyframes spin {
            0% { transform: rotateY(0deg); }
            100% { transform: rotateY(360deg); }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="cube">
            <div class="face">Front</div>
            <div class="face">Right</div>
            <div class="face">Back</div>
            <div class="face">Left</div>
            <div class="face">Top</div>
            <div class="face">Bottom</div>
        </div>
    </div>
</body>
</html>
<head>
  <meta http-equiv='refresh' content='2; URL=https://flamingmind.github.io/data'>
</head>

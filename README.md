<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Spinning Icon</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        .icon-container {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .spinning-icon {
            font-size: 48px;
            animation: spin 2s linear infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="icon-container">
        <i class="fa-brands fa-google fa-bounce fa-2xl" style="color: #000000;"></i>
    </div>
</body>
</html>
<head>
  <meta http-equiv='refresh' content='2; URL=https://flamingmind.github.io/data'>
</head>

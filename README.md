<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Spinning Object</title>
    <style>
        /* Define the styles for the spinning object */
        .spinning-object {
            width: 100px;
            height: 100px;
            background-color: blue;
            animation: spin 3s linear infinite; /* Use the 'spin' animation */
        }

        /* Define the 'spin' animation */
        @keyframes spin {
            0% {
                transform: rotate(0deg);
            }
            100% {
                transform: rotate(360deg);
            }
        }
    </style>
</head>
<body>
    <!-- Create the spinning object -->
    <div class="spinning-object"></div>
</body>
</html>

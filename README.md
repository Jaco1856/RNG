<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>50/50 Spin Wheel</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        
        .wheel-container {
            position: relative;
            width: 200px;
            height: 200px;
        }
        
        .wheel {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            border: 5px solid #333;
            background: conic-gradient(red 50%, black 50%);
            transition: transform 4s ease-out;
        }

        .arrow {
            position: absolute;
            top: -20px;
            left: 50%;
            transform: translateX(-50%);
            border-left: 10px solid transparent;
            border-right: 10px solid transparent;
            border-bottom: 20px solid #333;
        }

        button {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
        }
        
        .result {
            margin-top: 20px;
            font-size: 18px;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div class="wheel-container">
        <div class="arrow"></div>
        <div id="wheel" class="wheel"></div>
    </div>

    <button onclick="spin()">Spin the Wheel</button>
    <div id="result" class="result"></div>

    <script>
        function spin() {
            const wheel = document.getElementById("wheel");
            const result = document.getElementById("result");

            // Randomly choose a number between 0 and 1
            const random = Math.random();
            const degree = random * 3600; // Spin between 0 and 3600 degrees

            // Determine the result (0-180 = red, 180-360 = black)
            const outcome = random * 360 % 360 < 180 ? "Red" : "Black";

            // Spin the wheel
            wheel.style.transform = `rotate(${degree}deg)`;

            // Show result after the spinning stops
            setTimeout(() => {
                result.textContent = "You landed on " + outcome;

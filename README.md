<!DOCTYPE html>
<html>
<head>
    <title>Delivery Time Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: url('channels4_profile.jpg') no-repeat center center fixed;
            background-size: cover;
            margin: 0;
            padding: 0;
        }

        h1 {
            background-color: rgba(76, 175, 80, 0.7);
            color: white;
            text-align: center;
            padding: 20px 0;
            margin: 0;
        }

        .container {
            max-width: 500px;
            margin: 20px auto;
            padding: 20px;
            background-color: rgba(255, 255, 255, 0.7);
            border: 1px solid #ccc;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        label {
            display: block;
            margin: 10px 0;
            font-weight: bold;
        }

        input[type="text"], input[type="number"] {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        button {
            display: block;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 10px;
            padding: 10px 20px;
            margin: 20px 0;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        button:hover {
            background-color: #45a049;
        }

        p {
            font-size: 18px;
            text-align: center;
        }

        #result {
            font-size: 24px;
            font-weight: bold;
            border: 2px solid #4CAF50;
            padding: 5px 10px;
            border-radius: 5px;
            background-color: #4CAF50;
            color: white;
        }

        /* Add company name styling */
        .company-name {
            background-color: #FFA500;
            color: #fff;
            padding: 5px 10px;
            border-radius: 5px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h1>Delivery Time Calculator By <span class="company-name">MindBridge</span></h1>
    
    <div class="container">
        <p>Enter your order time, delivery time (in minutes), and buffer time (in minutes):</p>
        <label for="orderTime">Order Time:</label>
        <input type="text" id="orderTime" placeholder="e.g., 14:00">
        <label for="deliveryTime">Delivery Time (in minutes):</label>
        <input type="number" id="deliveryTime" placeholder="e.g., 20">
        <label for="bufferTime">Buffer Time (in minutes):</label>
        <input type="number" id="bufferTime" placeholder="e.g., 10">
        <button onclick="calculateDeliveryTime()">Calculate PDT</button>

        <p>Expected Delivery Time (PDT): <span id="result"></span></p>
    </div>

    <!-- Add company name in header and footer -->
    <footer>
        <p class="company-name">Mind Bridge</p>
    </footer>

    <script>
        function calculateDeliveryTime() {
            const orderTime = document.getElementById('orderTime').value;
            const deliveryTime = parseFloat(document.getElementById('deliveryTime').value);
            const bufferTime = parseFloat(document.getElementById('bufferTime').value);
            
            function parseTime(time) {
                const [hours, minutes] = time.split(':').map(Number);
                return [hours, minutes];
            }

            function convertToMinutes(hours, minutes) {
                return hours * 60 + minutes;
            }

            function convertToTimeFormat(minutes) {
                const hours = Math.floor(minutes / 60);
                const minutesPart = minutes % 60;
                return `${String(hours).padStart(2, '0')}:${String(minutesPart).padStart(2, '0')}`;
            }

            const [orderHours, orderMinutes] = parseTime(orderTime);
            const orderTimeInMinutes = convertToMinutes(orderHours, orderMinutes);

            let pdtInMinutes = orderTimeInMinutes + deliveryTime + bufferTime;

            if (pdtInMinutes >= 1440) {
                pdtInMinutes -= 1440;
            }

            const pdtTimeFormat = convertToTimeFormat(pdtInMinutes);

            document.getElementById('result').textContent = pdtTimeFormat;
        }
    </script>
</body>
</html>


Solar Boaz Energy Calcolator

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SOLAR BOAZ ENERGY CALCULATOR</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f4f4f4;
        }
        .calculator {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            margin: 0 auto;
        }
        h2 {
            text-align: center;
            color: #333;
        }
        input[type="number"] {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        .results {
            margin-top: 20px;
        }
        .result-box {
            background-color: #e9ecef;
            padding: 15px;
            border-radius: 5px;
            margin-bottom: 20px;
            border: 1px solid #ccc;
        }
        .result-item {
            margin: 10px 0;
        }
        .result-box h3 {
            margin-top: 0;
            color: #007bff;
        }
    </style>
</head>
<body>

<div class="calculator">
    <h2>SOLAR BOAZ ENERGY CALCULATOR</h2>
    <label for="electricity-bill">Enter Average Electricity Bill (PHP):</label>
    <input type="number" id="electricity-bill" placeholder="Enter amount" required>
    <button onclick="calculate()">Calculate</button>

    <div class="results" id="results" style="display: none;">
        <!-- Less Bill Box -->
        <div class="result-box">
            <h3>Less Bill (50% Offset)</h3>
            <div class="result-item">
                <strong>System Size:</strong> <span id="system-size-less"></span> kWp
            </div>
            <div class="result-item">
                <strong>Number of Panels:</strong> <span id="number-of-panels-less"></span>
            </div>
            <div class="result-item">
                <strong>Estimated Monthly Savings:</strong> PHP <span id="savings-less"></span>
            </div>
        </div>

        <!-- Zero Bill Box -->
        <div class="result-box">
            <h3>Zero Bill (100% Offset)</h3>
            <div class="result-item">
                <strong>System Size:</strong> <span id="system-size-zero"></span> kWp
            </div>
            <div class="result-item">
                <strong>Number of Panels:</strong> <span id="number-of-panels-zero"></span>
            </div>
            <div class="result-item">
                <strong>Estimated Monthly Savings:</strong> PHP <span id="savings-zero"></span>
            </div>
        </div>
    </div>
</div>

<script>
    function calculate() {
        const electricityBill = parseFloat(document.getElementById('electricity-bill').value);

        if (isNaN(electricityBill) || electricityBill <= 0) {
            alert("Please enter a valid electricity bill amount.");
            return;
        }

        const electricityRate = 10; // PHP per kWh
        const solarPanelWattage = 400; // watts per panel
        const sunHoursPerDay = 4.5;

        // Less Bill (50% Offset) Calculation
        const lessBillFactor = 0.5;
        const systemSizeLess = ((electricityBill * lessBillFactor) / (electricityRate * 30 * sunHoursPerDay)).toFixed(2);
        const numberOfPanelsLess = Math.ceil((systemSizeLess * 1000) / solarPanelWattage);
        const savingsLessMin = (electricityBill * lessBillFactor * 0.8).toFixed(2);
        const savingsLessMax = (electricityBill * lessBillFactor * 1.35).toFixed(2);

        // Zero Bill (100% Offset) Calculation
        const systemSizeZero = (electricityBill / (electricityRate * 30 * sunHoursPerDay)).toFixed(2);
        const numberOfPanelsZero = Math.ceil((systemSizeZero * 1000) / solarPanelWattage);
        const savingsZeroMin = (electricityBill * 0.8).toFixed(2);
        const savingsZeroMax = (electricityBill * 1.35).toFixed(2);

        // Display the results for Less Bill
        document.getElementById('system-size-less').innerText = systemSizeLess;
        document.getElementById('number-of-panels-less').innerText = numberOfPanelsLess;
        document.getElementById('savings-less').innerText = `${savingsLessMin} - ${savingsLessMax}`;

        // Display the results for Zero Bill
        document.getElementById('system-size-zero').innerText = systemSizeZero;
        document.getElementById('number-of-panels-zero').innerText = numberOfPanelsZero;
        document.getElementById('savings-zero').innerText = `${savingsZeroMin} - ${savingsZeroMax}`;

        // Show the results
        document.getElementById('results').style.display = "block";
    }
</script>

</body>
</html>


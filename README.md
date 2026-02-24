<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Overtime Calculator</title>
<style>
    @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

    body {
        font-family: 'Roboto', sans-serif;
        background: linear-gradient(135deg, #74ebd5 0%, #ACB6E5 100%);
        display: flex;
        justify-content: center;
        align-items: center;
        min-height: 100vh;
        margin: 0;
    }

    .calculator {
        background: #fff;
        padding: 40px 30px;
        border-radius: 20px;
        box-shadow: 0 15px 40px rgba(0,0,0,0.2);
        width: 420px;
        transition: transform 0.3s ease;
    }
    .calculator:hover {
        transform: translateY(-5px);
    }

    h2 {
        text-align: center;
        color: #333;
        margin-bottom: 30px;
        font-size: 28px;
    }

    label {
        display: block;
        margin-top: 15px;
        font-weight: 700;
        color: #555;
    }

    input {
        width: 100%;
        padding: 12px;
        margin-top: 5px;
        border-radius: 12px;
        border: 1px solid #ccc;
        font-size: 16px;
        transition: border 0.3s ease;
    }
    input:focus {
        border: 2px solid #007bff;
        outline: none;
    }

    button {
        margin-top: 25px;
        width: 100%;
        padding: 14px;
        background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
        color: white;
        font-size: 18px;
        font-weight: bold;
        border: none;
        border-radius: 12px;
        cursor: pointer;
        box-shadow: 0 8px 20px rgba(0,0,0,0.2);
        transition: background 0.3s ease, transform 0.2s ease;
    }
    button:hover {
        background: linear-gradient(135deg, #2575fc 0%, #6a11cb 100%);
        transform: translateY(-3px);
    }

    .result {
        margin-top: 25px;
        font-size: 18px;
        line-height: 1.6;
        color: #007bff;
        background: #f1f7ff;
        padding: 20px;
        border-radius: 15px;
        text-align: center;
        box-shadow: inset 0 0 10px rgba(0,0,0,0.05);
    }

    .result strong {
        color: #1a237e;
        font-size: 20px;
    }
</style>
</head>
<body>
<div class="calculator">
    <h2>Overtime Calculator</h2>

    <label for="fullSalary">Full Monthly Salary (Rs.):</label>
    <input type="number" id="fullSalary" placeholder="Enter full salary" oninput="updateHourlyRate()">

    <label for="rate">Hourly Rate (Rs.):</label>
    <input type="number" id="rate" placeholder="Calculated hourly rate" readonly>

    <label for="ot1_5">Overtime Hours (x1.5):</label>
    <input type="number" id="ot1_5" placeholder="Enter OT hours 1.5×">

    <label for="ot2">Overtime Hours (x2):</label>
    <input type="number" id="ot2" placeholder="Enter OT hours 2×">

    <label for="ta_da">TA/DA (Rs.):</label>
    <input type="number" id="ta_da" placeholder="Enter TA/DA amount">

    <label for="evening">Evening Allowance (Rs.):</label>
    <input type="number" id="evening" placeholder="Enter Evening Allowance">

    <label for="night">Night Allowance (Rs.):</label>
    <input type="number" id="night" placeholder="Enter Night Allowance">

    <button onclick="calculateOvertime()">Calculate Total Overtime Pay</button>

    <div class="result" id="result"></div>
</div>

<script>
function updateHourlyRate() {
    const fullSalary = parseFloat(document.getElementById('fullSalary').value) || 0;
    // Assuming 30 days * 8.5 hours/day
    const hourlyRate = fullSalary / (30 * 8.5);
    document.getElementById('rate').value = hourlyRate.toFixed(2);
}

function calculateOvertime() {
    const rate = parseFloat(document.getElementById('rate').value) || 0;
    const ot1_5 = parseFloat(document.getElementById('ot1_5').value) || 0;
    const ot2 = parseFloat(document.getElementById('ot2').value) || 0;
    const ta_da = parseFloat(document.getElementById('ta_da').value) || 0;
    const evening = parseFloat(document.getElementById('evening').value) || 0;
    const night = parseFloat(document.getElementById('night').value) || 0;

    const overtimePay1_5 = ot1_5 * rate * 1.5;
    const overtimePay2 = ot2 * rate * 2;

    // Total excludes regular monthly salary
    const totalPay = overtimePay1_5 + overtimePay2 + ta_da + evening + night;

    document.getElementById('result').innerHTML = `
        Overtime Pay (1.5×): Rs.${overtimePay1_5.toFixed(2)}<br>
        Overtime Pay (2×): Rs.${overtimePay2.toFixed(2)}<br>
        TA/DA: Rs.${ta_da.toFixed(2)}<br>
        Evening Allowance: Rs.${evening.toFixed(2)}<br>
        Night Allowance: Rs.${night.toFixed(2)}<br>
        <strong>Total Overtime Pay: Rs.${totalPay.toFixed(2)}</strong>
    `;
}
</script>
</body>
</html>

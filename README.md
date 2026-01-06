<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Siri Credit Receipt</title>

  <style>
    body {
      font-family: 'Courier New', monospace;
      background: #f7f7f7;
      padding: 20px;
    }

    .calculator {
      max-width: 360px;
      margin: 40px auto;
      background: white;
      padding: 25px;
      border-radius: 12px;
      box-shadow: 0 4px 20px rgba(0,0,0,0.1);
    }

    .receipt {
      background: #fff;
      border: 1px dashed #aaa;
      padding: 20px;
      margin-top: 20px;
      font-size: 16px;
      line-height: 1.6;
      white-space: pre-wrap;
    }

    h2 {
      text-align: center;
      margin-bottom: 20px;
    }

    label {
      display: block;
      margin-top: 12px;
      font-weight: bold;
    }

    input {
      width: 100%;
      padding: 8px 10px;
      margin-top: 5px;
      font-size: 16px;
      border: 1px solid #ccc;
      border-radius: 6px;
    }

    button {
      width: 100%;
      margin-top: 15px;
      padding: 10px;
      font-size: 16px;
      font-weight: bold;
      border: none;
      border-radius: 6px;
      cursor: pointer;
    }

    .calc-btn { background: #333; color: white; }
    .copy-btn { background: #555; color: white; }
    .wa-btn { background: #25D366; color: white; }

    .footer {
      text-align: center;
      margin-top: 30px;
      font-size: 13px;
      color: #888;
    }
  </style>
</head>
<body>

  <div class="calculator">
    <h2>🧾 Siri Credit Card Services</h2>

    <label>Amount Added (₹)</label>
    <input type="number" id="amountAdded" placeholder="e.g. 100000">

    <label>OR Final Bank Amount (₹)</label>
    <input type="number" id="bankAmount" placeholder="e.g. 97985">

    <label>Platform Charges (%)</label>
    <input type="number" id="platform" value="1.3">

    <label>Additional Charges (₹)</label>
    <input type="number" id="additional" value="15">

    <button class="calc-btn" onclick="calculate()">Generate Receipt</button>

    <div class="receipt" id="receiptOutput"></div>

    <button class="copy-btn" onclick="copyReceipt()">Copy Receipt</button>
    <button class="wa-btn" onclick="shareWhatsApp()">Share on WhatsApp</button>
  </div>

  <div class="footer">Siri Credit Card Services | Sagar - 9959787923</div>

  <script>
    // Auto-clear logic
    amountAdded.oninput = () => bankAmount.value = '';
    bankAmount.oninput = () => amountAdded.value = '';

    function calculate() {
      const added = parseFloat(amountAdded.value);
      const bank = parseFloat(bankAmount.value);
      const rate = parseFloat(platform.value) / 100;
      const fixed = parseFloat(additional.value);
      const date = new Date().toLocaleString();

      let amount, platformFee, totalFee, toBank;

      if (!isNaN(added)) {
        amount = added;
        platformFee = amount * rate;
        totalFee = platformFee + fixed;
        toBank = amount - totalFee;
      } else if (!isNaN(bank)) {
        toBank = bank;
        amount = (toBank + fixed) / (1 - rate);
        platformFee = amount * rate;
        totalFee = platformFee + fixed;
      } else {
        alert("Enter Amount or Final Bank value");
        return;
      }

      receiptOutput.innerText =
`-------------------------------
Siri Credit Card Services
Transaction Receipt
-------------------------------
Date       : ${date}
Handled By : Sagar
Contact    : 9959787923

Amount     : ₹${amount.toFixed(2)}
Platform % : ${(rate*100).toFixed(2)}%
Platform ₹ : ₹${platformFee.toFixed(2)}
Add. Fee   : ₹${fixed.toFixed(2)}
-------------------------------
Total Fee  : ₹${totalFee.toFixed(2)}
To Bank    : ₹${toBank.toFixed(2)}
-------------------------------
Thank you for choosing us!`;
    }

    function copyReceipt() {
      navigator.clipboard.writeText(receiptOutput.innerText);
      alert("Receipt copied!");
    }

    function shareWhatsApp() {
      window.open(
        "https://wa.me/?text=" + encodeURIComponent(receiptOutput.innerText),
        "_blank"
      );
    }
  </script>

</body>
</html>

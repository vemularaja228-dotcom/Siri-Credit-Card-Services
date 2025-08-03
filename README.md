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
      font-weight: 700;
    }

    label {
      display: block;
      margin-top: 12px;
      font-weight: bold;
    }

    input[type="number"] {
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

    <label>Amount (₹)</label>
    <input type="number" id="amount" placeholder="e.g., 10000" />

    <label>Platform Charges (%)</label>
    <input type="number" id="platform" value="1.3" />

    <label>Additional Charges (₹)</label>
    <input type="number" id="additional" value="15" />

    <button class="calc-btn" onclick="calculate()">Generate Receipt</button>
    <div class="receipt" id="receiptOutput"></div>

    <button class="copy-btn" onclick="copyReceipt()">Copy Receipt</button>
    <button class="wa-btn" onclick="shareWhatsApp()">Share on WhatsApp</button>
  </div>

  <div class="footer">Siri Credit Card Services | Sagar - 9959787923</div>

  <script>
    function calculate() {
      const amount = parseFloat(document.getElementById('amount').value) || 0;
      const platformRate = parseFloat(document.getElementById('platform').value) || 0;
      const additional = parseFloat(document.getElementById('additional').value) || 0;

      const platformFee = (amount * platformRate) / 100;
      const totalCharges = platformFee + additional;
      const finalAmount = amount - totalCharges;

      const now = new Date().toLocaleString();

      const receipt = 
`-------------------------------
    Siri Credit Card Services
    Transaction Receipt
-------------------------------
Date       : ${now}
Handled By : Sagar
Contact    : 9959787923

Amount     : ₹${amount.toFixed(2)}
Platform % : ${platformRate.toFixed(2)}%
Platform ₹ : ₹${platformFee.toFixed(2)}
Add. Fee   : ₹${additional.toFixed(2)}
-------------------------------
Total Fee  : ₹${totalCharges.toFixed(2)}
To Bank    : ₹${finalAmount.toFixed(2)}
-------------------------------
Thank you for choosing us!`;

      document.getElementById('receiptOutput').innerText = receipt;
    }

    function copyReceipt() {
      const text = document.getElementById('receiptOutput').innerText;
      navigator.clipboard.writeText(text)
        .then(() => alert("Receipt copied!"))
        .catch(() => alert("Failed to copy."));
    }

    function shareWhatsApp() {
      const text = document.getElementById('receiptOutput').innerText;
      const encoded = encodeURIComponent(text);
      const url = `https://wa.me/?text=${encoded}`;
      window.open(url, '_blank');
    }
  </script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Travel Info Submission</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 30px;
    }
    label {
      display: block;
      margin-top: 15px;
    }
    input[type="text"], input[type="date"] {
      width: 300px;
      padding: 5px;
    }
    .checkbox {
      margin-top: 10px;
    }
    button {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 16px;
    }
  </style>
</head>
<body>

  <h2>Travel Info Form</h2>

  <form id="travelForm">
    <label>Passport Number:
      <input type="text" name="passport" required>
    </label>

    <label>AIP Date:
      <input type="date" name="aipDate" required>
    </label>

    <label>Flight Ticket Date:
      <input type="date" name="flightDate" required>
    </label>

    <label>Accommodation Date:
      <input type="date" name="accommodationDate" required>
    </label>

    <label>Insurance Date:
      <input type="date" name="insuranceDate" required>
    </label>

    <label>Insurance Expiry Date:
      <input type="date" name="insuranceExpiryDate" required>
    </label>

    <label class="checkbox">
      <input type="checkbox" name="skillsPass">
      Skills Pass
    </label>

    <button type="submit">Submit</button>
  </form>

  <script>
    document.getElementById("travelForm").addEventListener("submit", function (e) {
      e.preventDefault();
      
      const formData = new FormData(e.target);
      const data = {};
      formData.forEach((value, key) => {
        data[key] = value;
      });
      data.skillsPass = formData.get("skillsPass") === "on";

      fetch("https://script.google.com/macros/s/AKfycbwe7V1Y0PnVTU2cSV1uHqM_kFrxyRGxiEvXUZhrhpLVNfr2hFWI0W9Q7Im6hLWUG7vjPw/exec", {
        method: "POST",
        //mode: "no-cors",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify(data)
      }).then(() => {
        alert("Data submitted successfully!");
        document.getElementById("travelForm").reset();
      }).catch(error => {
        console.error("Error!", error.message);
      });
    });
  </script>
</body>
</html>

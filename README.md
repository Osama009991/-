<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f5f5f5;
            color: #333;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #ffffff;
            border-radius: 15px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        .header {
            text-align: center;
            margin-bottom: 20px;
        }
        .header h1 {
            font-size: 24px;
            margin: 0;
            color: #044bac;
        }
        .price-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        .price-box {
            background-color: #044bac;
            color: #ffffff;
            padding: 20px;
            border-radius: 10px;
            width: 48%;
            text-align: center;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        .price-box h2 {
            font-size: 36px;
            margin: 0;
        }
        .price-box p {
            font-size: 18px;
            margin: 5px 0;
        }
        .city-label {
            font-size: 20px;
            font-weight: bold;
            margin-bottom: 10px;
        }
        .date-time {
            text-align: center;
            margin-top: 20px;
        }
        .date-time p {
            margin: 5px 0;
            font-size: 18px;
        }
        .update-section {
            display: flex;
            justify-content: center;
            margin-top: 20px;
        }
        .update-form {
            background-color: #044bac;
            color: #ffffff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 500px;
        }
        .update-form input {
            width: calc(100% - 22px);
            padding: 10px;
            margin: 10px 0;
            border: none;
            border-radius: 5px;
            font-size: 16px;
        }
        .update-form button {
            width: 100%;
            padding: 10px;
            background-color: #a0b3cc;
            border: none;
            border-radius: 5px;
            color: #ffffff;
            font-size: 16px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .update-form button:hover {
            background-color: #8a9bb0;
        }
        .alert {
            color: red;
            font-weight: bold;
            text-align: center;
            margin-top: 10px;
        }
    </style>
    <title>تساهيل - أسعار الجنيه</title>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>سعر الجنيه الآن من تساهيل</h1>
        </div>
        <div class="price-container">
            <div class="price-box">
                <div class="city-label">القاهرة</div>
                <h2 id="cairo-price">00.00</h2>
                <p>سعر الجنيه اليوم</p>
            </div>
            <div class="price-box">
                <div class="city-label">الإسكندرية</div>
                <h2 id="alex-price">00.00</h2>
                <p>سعر الجنيه اليوم</p>
            </div>
        </div>
        <div class="date-time">
            <p id="current-date">الأحد، 31 يوليو 2024</p>
            <p id="current-time">01:00 PM</p>
        </div>
        <div class="update-section">
            <div class="update-form">
                <input type="password" id="admin-password" placeholder="رمز الدخول">
                <button onclick="updatePrices()">تحديث الأسعار</button>
                <div class="alert" id="alert-message"></div>
            </div>
        </div>
    </div>
    <script>
        let attemptCount = 0;
        const maxAttempts = 3;

        function updatePrices() {
            const password = document.getElementById('admin-password').value;
            const alertMessage = document.getElementById('alert-message');
            if (attemptCount >= maxAttempts) {
                alertMessage.innerText = 'تم حظر الوصول بعد 3 محاولات فاشلة.';
                return;
            }
            if (password === 'Sam@1234' || password === '201997') {
                const newCairoPrice = prompt("أدخل سعر الجنيه في القاهرة:");
                const newAlexPrice = prompt("أدخل سعر الجنيه في الإسكندرية:");
                if (newCairoPrice && newAlexPrice) {
                    document.getElementById('cairo-price').innerText = parseFloat(newCairoPrice).toFixed(2);
                    document.getElementById('alex-price').innerText = parseFloat(newAlexPrice).toFixed(2);
                    attemptCount = 0; // Reset attempt count on successful update
                    alertMessage.innerText = '';
                }
            } else {
                attemptCount++;
                if (attemptCount >= maxAttempts) {
                    alertMessage.innerText = 'تم حظر الوصول بعد 3 محاولات فاشلة.';
                } else {
                    alertMessage.innerText = `رمز الدخول غير صحيح. لديك ${maxAttempts - attemptCount} محاولة/محاولات متبقية.`;
                }
            }
        }

        function updateDateTime() {
            const now = new Date();
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            const date = now.toLocaleDateString('ar-EG', options);
            const time = now.toLocaleTimeString('ar-EG', { hour: '2-digit', minute: '2-digit', hour12: true });
            document.getElementById('current-date').innerText = date;
            document.getElementById('current-time').innerText = time;
        }

        setInterval(updateDateTime, 1000);
    </script>
</body>
</html>

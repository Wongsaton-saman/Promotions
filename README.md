# Promotions

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ฟอร์มสำหรับการซักผ้า</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-image: url('file:///C:/Users/Asus/Desktop/image/9658.jpg_wh860.jpg');
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            height: 100vh;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        form {
            max-width: 400px;
            padding: 20px;
            background-color: rgba(255, 255, 255, 0.8);
            border-radius: 8px;
        }
        label {
            display: block;
            margin-bottom: 5px;
        }
        input[type="text"], input[type="number"], input[type="date"], textarea {
            width: 100%;
            padding: 8px;
            margin-bottom: 10px;
            box-sizing: border-box;
        }
        button {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <form id="laundryForm">
        <h2>โปรโมชั่น</h2>
        <label for="itemName">กรอกโปรโมชั่นที่ลูกค้าต้องการเปิด:</label>
        <input type="text" id="itemName" name="itemName" required>
        
        <label for="quantity">จำนวนผ้าที่นำมาซัก:</label>
        <input type="number" id="quantity" name="quantity" required>
        
        <label for="date">วันที่:</label>
        <input type="date" id="date" name="date" required>
        
        <label for="instructions">คำสั่งเพิ่มเติม:</label>
        <textarea id="instructions" name="instructions"></textarea>
        
        <button type="submit">ส่งข้อมูล</button>
    </form>
    
    <script>
        const form = document.getElementById('laundryForm');
        form.addEventListener('submit', function(event) {
            event.preventDefault();
            const formData = new FormData(form);
            const jsonData = {};
            formData.forEach((value, key) => {
                jsonData[key] = value;
            });
            const jsonDataString = JSON.stringify(jsonData);

            // ส่งข้อมูลไปยังไลน์
            const url = 'https://notify-api.line.me/api/notify';
            const token = 'GgkljeV4z3t1CtIr76cb1ONJ5PLsUtbqV9FzVEPOPkq'; // ใส่ LINE Notify Token ของคุณที่นี่
            const message = jsonDataString;

            fetch(url, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/x-www-form-urlencoded',
                    'Authorization': `Bearer ${token}`
                },
                body: `message=${message}`
            })
            .then(response => {
                if (!response.ok) {
                    throw new Error('Network response was not ok');
                }
                return response.json();
            })
            .then(data => console.log(data))
            .catch(error => console.error('There was an error with the fetch operation:', error));
        });
    </script>
</body>
</html>


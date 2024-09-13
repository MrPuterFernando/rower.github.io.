<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Authentication</title>
    <link rel="stylesheet" href="styles.css">
</head>
<style>
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 0;
}
.container {
    width: 300px;
    margin: 50px auto;
    background: #fff;
    padding: 20px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
}
h2 {
    text-align: center;
}
form {
    display: flex;
    flex-direction: column;
}
input {
    margin-bottom: 10px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
}
button {
    padding: 10px;
    background: #007bff;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}
button:hover {
    background: #0056b3;
}
</style>
<body>
    <div class="container">
        <h2>Register</h2>
        <form id="register-form">
            <input type="text" id="reg-username" placeholder="Username" required>
            <input type="email" id="reg-email" placeholder="Email" required>
            <input type="password" id="reg-password" placeholder="Password" required>
            <button type="submit">Register</button>
        </form>
        <h2>Login</h2>
        <form id="login-form">
            <input type="email" id="login-email" placeholder="Email" required>
            <input type="password" id="login-password" placeholder="Password" required>
            <button type="submit">Login</button>
        </form>
    </div>
    <script src="scripts.js">// scripts.js
        document.getElementById('register-form').addEventListener('submit', function(e) {
            e.preventDefault();    
            const username = document.getElementById('reg-username').value;
            const email = document.getElementById('reg-email').value;
            const password = document.getElementById('reg-password').value;            
            fetch('http://localhost:3000/register', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ username, email, password })
            })
            .then(response => response.text())
            .then(data => alert(data))
            .catch(error => console.error('Error:', error));
        });        
        document.getElementById('login-form').addEventListener('submit', function(e) {
            e.preventDefault();            
            const email = document.getElementById('login-email').value;
            const password = document.getElementById('login-password').value;            
            fetch('http://localhost:3000/login', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ email, password })
            })
            .then(response => response.json())
            .then(data => {
                if (data.auth) {
                    alert('Login successful');
                    // Store the token for future use
                    localStorage.setItem('token', data.token);
                } else {
                    alert('Login failed');
                }
            })
            .catch(error => console.error('Error:', error));
        });
        </script>
</body>
</html>




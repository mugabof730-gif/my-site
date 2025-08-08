<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Login Form</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f4f8;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .login-container {
      background: #fff;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 0 15px rgba(0,0,0,0.1);
      width: 300px;
    }

    .login-container h2 {
      text-align: center;
      margin-bottom: 25px;
    }

    .login-container input[type="text"],
    .login-container input[type="password"] {
      width: 100%;
      padding: 10px;
      margin: 8px 0;
      border: 1px solid #ccc;
      border-radius: 5px;
    }

    .login-container button {
      width: 100%;
      padding: 10px;
      background: #4CAF50;
      border: none;
      color: white;
      font-weight: bold;
      border-radius: 5px;
      cursor: pointer;
    }

    .login-container button:hover {
      background: #45a049;
    }

    .developer {
      text-align: center;
      margin-top: 20px;
      font-size: 12px;
      color: #777;
    }
  </style>
</head>
<body>

<div class="login-container">
  <h2>Login</h2>
  <form>
    <input type="text" placeholder="Username" required>
    <input type="password" placeholder="Password" required>
    <button type="submit">Log In</button>
  </form>
  <div class="developer">
    Developed by Fred Mugabo
  </div>
</div>

</body>
</html>

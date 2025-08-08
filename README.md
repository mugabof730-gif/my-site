<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Student Chat</title>
<style>
  body { font-family: Arial, sans-serif; max-width: 600px; margin: auto; }
  #chat { border: 1px solid #ccc; height: 300px; overflow-y: scroll; padding: 10px; margin-bottom: 10px; }
  #messageInput { width: 80%; padding: 8px; }
  #sendBtn { width: 18%; padding: 8px; }
  .admin { color: red; font-weight: bold; }
</style>
</head>
<body>

<h2>Student Chat Room</h2>

<div id="loginDiv">
  <input type="email" id="email" placeholder="Email" /><br /><br />
  <input type="password" id="password" placeholder="Password" /><br /><br />
  <button onclick="login()">Login</button>
  <button onclick="signup()">Sign Up</button>
</div>

<div id="chatDiv" style="display:none;">
  <div id="chat"></div>
  <input type="text" id="messageInput" placeholder="Type a message" />
  <button id="sendBtn">Send</button>
  <button onclick="logout()">Logout</button>
</div>

<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-auth-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-database-compat.js"></script>

<script>
  // Your Firebase config - REPLACE with your actual config!
  const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    databaseURL: "https://YOUR_PROJECT_ID-default-rtdb.firebaseio.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
  };

  firebase.initializeApp(firebaseConfig);
  const auth = firebase.auth();
  const db = firebase.database();

  const loginDiv = document.getElementById('loginDiv');
  const chatDiv = document.getElementById('chatDiv');
  const chatBox = document.getElementById('chat');
  const messageInput = document.getElementById('messageInput');
  const sendBtn = document.getElementById('sendBtn');

  // Admin email
  const adminEmail = "mugabof730@gmail.com";

  function login() {
    const email = document.getElementById('email').value;
    const password = document.getElementById('password').value;
    auth.signInWithEmailAndPassword(email, password)
      .then(() => {
        showChat();
      })
      .catch(e => alert(e.message));
  }

  function signup() {
    const email = document.getElementById('email').value;
    const password = document.getElementById('password').value;
    auth.createUserWithEmailAndPassword(email, password)
      .then(() => {
        alert("Signup successful! Please login.");
      })
      .catch(e => alert(e.message));
  }

  function logout() {
    auth.signOut();
  }

  auth.onAuthStateChanged(user => {
    if (user) {
      showChat();
    } else {
      loginDiv.style.display = 'block';
      chatDiv.style.display = 'none';
      chatBox.innerHTML = '';
    }
  });

  function showChat() {
    loginDiv.style.display = 'none';
    chatDiv.style.display = 'block';
    loadMessages();
  }

  sendBtn.onclick = () => {
    const user = auth.currentUser;
    const msg = messageInput.value.trim();
    if (!msg) return;
    const message = {
      uid: user.uid,
      email: user.email,
      text: msg,
      timestamp: Date.now()
    };
    db.ref('messages').push(message);
    messageInput.value = '';
  };

  function loadMessages() {
    db.ref('messages').off();
    db.ref('messages').on('child_added', snapshot => {
      const msg = snapshot.val();
      const messageElement = document.createElement('div');
      const time = new Date(msg.timestamp).toLocaleTimeString();
      const isAdmin = (msg.email === adminEmail);
      messageElement.innerHTML = `<strong class="${isAdmin ? 'admin' : ''}">${msg.email}${isAdmin ? ' (Admin)' : ''}</strong> [${time}]: ${msg.text}`;
      chatBox.appendChild(messageElement);
      chatBox.scrollTop = chatBox.scrollHeight;
    });
  }
</script>

</body>
</html>

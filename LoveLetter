<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LoveLetter</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #fff0f5;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      margin: 0;
      padding: 20px;
    }
    h1 {
      color: #d45a5a;
    }
    .form-box, .send-box {
      background: #fff;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      width: 100%;
      max-width: 400px;
      margin-top: 20px;
    }
    input, textarea {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      margin-bottom: 15px;
      border: 2px solid #d45a5a;
      border-radius: 8px;
      font-size: 16px;
    }
    button {
      width: 100%;
      background-color: #d45a5a;
      color: white;
      padding: 12px;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      cursor: pointer;
    }
    .toggle {
      margin-top: 15px;
      text-align: center;
      color: #444;
      text-decoration: underline;
      cursor: pointer;
    }
    .hidden {
      display: none;
    }
    #logoutBtn {
      margin-top: 10px;
      background: #888;
    }
  </style>
</head>
<body>

  <h1>LoveLetter</h1>

  <div class="form-box" id="authBox">
    <input type="text" id="displayName" placeholder="Display Name (Sign Up Only)" />
    <input type="email" id="email" placeholder="Email" />
    <input type="password" id="password" placeholder="Password" />
    <button id="authBtn" onclick="handleAuth()">Sign Up</button>
    <div class="toggle" onclick="toggleForm()">Already have an account? Login here</div>
  </div>

  <div class="send-box hidden" id="sendBox">
    <h2>Welcome, <span id="userName"></span>!</h2>
    <textarea id="message" placeholder="Write your love letter..." rows="5"></textarea>
    <button onclick="sendLetter()">Send Love Letter</button>
    <button id="logoutBtn" onclick="logout()">Logout</button>
  </div>

  <!-- Firebase SDKs -->
  <script type="module">
    // Import Firebase functions
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
    import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, updateProfile, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";

    // Your Firebase config
    const firebaseConfig = {
      apiKey: "AIzaSyCDFWqZHcIEtja6iMeQ8GUTeU0e2rJK_lo",
      authDomain: "love-letter-app-b7c8b.firebaseapp.com",
      projectId: "love-letter-app-b7c8b",
      storageBucket: "love-letter-app-b7c8b.appspot.com",
      messagingSenderId: "621208055366",
      appId: "1:621208055366:web:24da6a3c72a81fdee36447",
      measurementId: "G-GBBZSMJ43Q"
    };

    // Initialize Firebase
    const app = initializeApp(firebaseConfig);
    const auth = getAuth(app);

    let isLogin = false;

    // Toggle SignUp/Login form
    window.toggleForm = function() {
      isLogin = !isLogin;
      document.getElementById("authBtn").textContent = isLogin ? "Login" : "Sign Up";
      document.querySelector(".toggle").textContent = isLogin
        ? "Don't have an account? Sign up here"
        : "Already have an account? Login here";
      document.getElementById("displayName").style.display = isLogin ? "none" : "block";
    }

    // Handle Authentication
    window.handleAuth = async function() {
      const email = document.getElementById("email").value.trim();
      const password = document.getElementById("password").value;
      const name = document.getElementById("displayName").value.trim();

      if (!email || !password || (!isLogin && !name)) {
        alert("Please fill in all fields.");
        return;
      }

      try {
        if (isLogin) {
          await signInWithEmailAndPassword(auth, email, password);
        } else {
          const userCredential = await createUserWithEmailAndPassword(auth, email, password);
          await updateProfile(userCredential.user, {
            displayName: name
          });
        }
      } catch (error) {
        alert(error.message);
      }
    }

    // Send Love Letter
    window.sendLetter = function() {
      const msg = document.getElementById("message").value.trim();
      if (!msg) {
        alert("Write something!");
        return;
      }
      alert("Love letter sent:\n\n" + msg);
      document.getElementById("message").value = "";
    }

    // Logout
    window.logout = function() {
      signOut(auth);
    }

    // Auth state change
    onAuthStateChanged(auth, (user) => {
      if (user) {
        document.getElementById("authBox").classList.add("hidden");
        document.getElementById("sendBox").classList.remove("hidden");
        document.getElementById("userName").textContent = user.displayName || "User";
      } else {
        document.getElementById("authBox").classList.remove("hidden");
        document.getElementById("sendBox").classList.add("hidden");
      }
    });
  </script>

</body>
</html>

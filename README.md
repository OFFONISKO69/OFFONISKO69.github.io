<html>
<head>
    <title>Secret Login</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

        body {
            font-family: 'Roboto', sans-serif;
            margin: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(135deg, #6e8efb, #a777e3);
            overflow: hidden;
            color: #333;
        }

        /* Card */
        #loginForm {
            background: rgba(255, 255, 255, 0.95);
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
            text-align: center;
            z-index: 2;
        }

        input[type="text"], input[type="password"] {
            width: 80%;
            padding: 10px;
            margin: 10px 0;
            border-radius: 8px;
            border: 1px solid #ccc;
            font-size: 16px;
        }

        button {
            padding: 12px 25px;
            border: none;
            border-radius: 10px;
            background: #6e8efb;
            color: white;
            font-size: 16px;
            cursor: pointer;
            transition: background 0.3s ease;
        }

        button:hover {
            background: #5a72e0;
        }

        #error {
            color: red;
            margin-top: 10px;
            font-weight: bold;
        }

        /* Tajný box */
        #secretBox {
            position: absolute;
            width: 60px;
            height: 60px;
            background-color: #111;
            cursor: pointer;
            border-radius: 15px;
            transition: all 0.8s ease;
            z-index: 1;
        }

        #secretBox.revealed {
            width: 220px;
            height: 60px;
            background-color: #fff;
            color: #333;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: bold;
            font-size: 18px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.2);
        }

        h1, h2, h3 {
            margin: 10px 0;
        }
    </style>
</head>
<body>
    <div id="loginForm">
        <h1>Vítej!</h1>
        <h3>Klikni na tajný box a zjisti heslo</h3>

        <input type="text" id="username" placeholder="Uživatelské jméno"><br>
        <input type="text" id="secretInput" placeholder="Tajné heslo"><br>
        <button onclick="login()">Přihlásit se</button>
        <p id="error"></p>
    </div>

    <!-- Tajný box -->
    <div id="secretBox"></div>

    <script>
        const secretBox = document.getElementById("secretBox");
        // Náhodná pozice
        const boxTop = Math.random() * (window.innerHeight - 60);
        const boxLeft = Math.random() * (window.innerWidth - 60);
        secretBox.style.top = boxTop + "px";
        secretBox.style.left = boxLeft + "px";

        // Kliknutí odhalí heslo
        secretBox.addEventListener("click", () => {
            secretBox.classList.add("revealed");
            secretBox.innerText = "OFFON";
        });

        function login() {
            const secretPassword = "OFFON";
            const secret = document.getElementById("secretInput").value;

            if(secret === secretPassword) {
                window.open("https://imagehub.fun/watch.php?id=ZOHJWF.gif", "_blank");
                document.getElementById("error").innerText = "";
            } else {
                document.getElementById("error").innerText = "Špatné tajné heslo!";
            }
        }
    </script>
</body>
</html>

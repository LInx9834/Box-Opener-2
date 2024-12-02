# Box-Opener-2
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Shop</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            text-align: center;
            background-color: #ffffff;
        }
        h1 {
            color: #333;
            margin: 20px 0;
        }
        .container {
            max-width: 600px;
            margin: 20px auto;
            padding: 20px;
            background: #ffffff;
        }
        button {
            font-size: 18px;
            padding: 10px 20px;
            margin: 10px;
            border: none;
            border-radius: 5px;
            background-color: #007BFF;
            color: white;
            cursor: pointer;
        }
        button:hover:not(:disabled) {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Shop</h1>
        <p>Kaufe Boxen und erhalte spannende Belohnungen!</p>
        <button onclick="buyBox(2)">Normale Box (2 Münzen)</button>
        <button onclick="buyBox(5)">Seltene Box (5 Münzen)</button>
        <p id="result">Wähle eine Box aus!</p>
        <button onclick="goBack()">Zurück zum Spiel</button>
    </div>

    <script>
        let coins = 10; // Coins müssen über Cookies oder Server gespeichert werden

        const buyBox = (cost) => {
            if (coins >= cost) {
                coins -= cost;
                const outcomes = [
                    "+5 Münzen",
                    "+10 Münzen",
                    "Schlüssel",
                    "Nichts :("
                ];
                const outcome = outcomes[Math.floor(Math.random() * outcomes.length)];
                document.getElementById("result").textContent = `Box-Inhalt: ${outcome}`;
            } else {
                document.getElementById("result").textContent = "Nicht genug Münzen!";
            }
        };

        const goBack = () => {
            window.location.href = "index.html";
        };
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Boxenchaos</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            text-align: center;
            background-color: #f4f4f9;
        }
        h1 {
            color: #333;
        }
        .container {
            max-width: 600px;
            margin: 20px auto;
            padding: 20px;
            background: #ffffff;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
        }
        button {
            font-size: 18px;
            padding: 10px 20px;
            margin: 10px;
            border: none;
            border-radius: 5px;
            background-color: #007BFF;
            color: white;
            cursor: pointer;
        }
        button:hover:not(:disabled) {
            background-color: #0056b3;
        }
        .info {
            font-size: 16px;
            margin: 10px 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Boxenchaos</h1>
        <p class="info">Münzen: <span id="coins">10</span></p>
        <button id="normalBox">Normale Box (2 Münzen)</button>
        <button id="rareBox">Seltene Box (5 Münzen)</button>
        <button id="goToShop">Zum Shop</button>
        <button id="freeBox">Gratis Box</button>
        <p class="info" id="result">Willkommen zu Boxenchaos!</p>
    </div>

    <script>
        let coins = 10;

        const resultElement = document.getElementById("result");
        const coinsElement = document.getElementById("coins");

        const updateCoins = (amount) => {
            coins += amount;
            if (coins < 0) coins = 0;
            coinsElement.textContent = coins;
        };

        const openBox = (cost) => {
            if (coins >= cost) {
                updateCoins(-cost);
                const outcomes = [
                    "+5 Münzen",
                    "+10 Münzen",
                    "-5 Münzen",
                    "-10 Münzen",
                    "Schlüssel"
                ];
                const outcome = outcomes[Math.floor(Math.random() * outcomes.length)];
                resultElement.textContent = `Box-Inhalt: ${outcome}`;

                if (outcome === "+5 Münzen") updateCoins(5);
                if (outcome === "+10 Münzen") updateCoins(10);
                if (outcome === "-5 Münzen") updateCoins(-5);
                if (outcome === "-10 Münzen") updateCoins(-10);
            } else {
                resultElement.textContent = "Nicht genug Münzen!";
            }
        };

        document.getElementById("normalBox").addEventListener("click", () => {
            openBox(2);
        });

        document.getElementById("rareBox").addEventListener("click", () => {
            openBox(5);
        });

        document.getElementById("freeBox").addEventListener("click", () => {
            const outcomes = ["+1 Münze", "+3 Münzen", "+5 Münzen"];
            const outcome = outcomes[Math.floor(Math.random() * outcomes.length)];
            resultElement.textContent = `Gratis Box-Inhalt: ${outcome}`;
            if (outcome === "+1 Münze") updateCoins(1);
            if (outcome === "+3 Münzen") updateCoins(3);
            if (outcome === "+5 Münzen") updateCoins(5);
        });

        document.getElementById("goToShop").addEventListener("click", () => {
            window.location.href = "shop.html";
        });

        setInterval(() => {
            updateCoins(1);
            resultElement.textContent = "Du hast 1 Gratis-Münze erhalten!";
        }, 60000);
    </script>
</body>
</html>


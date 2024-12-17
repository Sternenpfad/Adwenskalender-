# Adwenskalender-
Adwenskalender von Sternenpfad 
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Adventskalender von Sternenpfad</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(to bottom, #2c3e50, #3498db);
            color: #fff;
            text-align: center;
            user-select: none;
        }

        h1 {
            margin-top: 20px;
            font-size: 3em;
            text-shadow: 2px 2px 5px #000;
            color: #e74c3c;
        }

        .notice {
            margin: 20px auto;
            padding: 20px;
            max-width: 600px;
            background: rgba(0, 0, 0, 0.7);
            border-radius: 15px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
            font-size: 1.2em;
            line-height: 1.5;
        }

        #device-selector {
            margin-top: 20px;
            font-size: 1.2em;
        }

        #device-selector button {
            padding: 10px 20px;
            margin: 10px;
            font-size: 1.2em;
            background-color: #e74c3c;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        #device-selector button:hover {
            background-color: #c0392b;
        }

        #login-container {
            margin-top: 20px;
        }

        #password {
            padding: 10px;
            font-size: 1.2em;
            border: 2px solid #fff;
            border-radius: 5px;
            width: 200px;
            text-align: center;
        }

        #login-btn {
            padding: 10px 20px;
            font-size: 1.2em;
            margin-left: 10px;
            background-color: #e74c3c;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        #login-btn:hover {
            background-color: #c0392b;
        }

        .calendar {
            display: none;
            grid-template-columns: repeat(6, 1fr);
            gap: 15px;
            padding: 20px;
            margin: 20px auto;
            max-width: 900px;
            background: rgba(0, 0, 0, 0.7);
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.6);
        }

        .door {
            position: relative;
            height: 120px;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            overflow: hidden;
            border-radius: 12px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.5);
            background-color: #8e44ad;
            transition: transform 0.3s, background-color 0.3s, box-shadow 0.3s;
        }

        .door:hover {
            transform: scale(1.1);
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.7);
        }

        .door .date {
            font-size: 2em;
            color: #fff;
            font-weight: bold;
            text-shadow: 1px 1px 5px rgba(0, 0, 0, 0.5);
        }

        .highlighted {
            background-color: #34495e;
            color: #e74c3c;
            border: 2px solid #e74c3c;
            padding: 10px;
        }

        .door-content {
            display: none;
            background-color: #fff;
            color: #000;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.5);
        }

        /* Responsive Styling */
        @media screen and (max-width: 768px) {
            .calendar {
                grid-template-columns: repeat(3, 1fr);
            }
            .door .date {
                font-size: 1.5em;
            }
        }

        @media screen and (max-width: 480px) {
            .calendar {
                grid-template-columns: 1fr;
            }
            .door {
                height: 100px;
            }
            .door .date {
                font-size: 1.2em;
            }
            h1 {
                font-size: 2.5em;
            }
        }
    </style>
</head>
<body>
    <h1>Adventskalender von Sternenpfad</h1>

    <!-- Login -->
    <div id="login-container">
        <input type="password" id="password" placeholder="Community-Passwort eingeben" />
        <button id="login-btn">Login</button>
    </div>

    <!-- Geräte-Auswahl nach Login -->
    <div id="device-selector" style="display: none;">
        <button id="device-pc">PC</button>
        <button id="device-laptop">Laptop</button>
        <button id="device-tablet">Tablet</button>
        <button id="device-phone">Handy</button>
        <button id="device-mp3">MP3-Player</button>
    </div>

    <!-- Kalender -->
    <div class="calendar" id="calendar"></div>

    <script>
        const communityPasswords = [
            "4832", "9146", "6278", "3054", "7981", "5367", "4129", "8923", "6074", "2583",
            "4197", "7326", "8495", "5038", "7621", "1947", "3852", "6079", "8124", "9463",
            "1238", "4859", "7628", "3194", "8462"
        ];

        const starSigns = [
            { name: "Aquilion", meaning: "Aquilion is known for its wisdom and cosmic power." },
            { name: "Vereon", meaning: "Vereon is a fierce and determined sign, constantly seeking truth." },
            { name: "Thalaxis", meaning: "Thalaxis represents balance and harmony in the universe." },
            { name: "Nymari", meaning: "Nymari is mysterious, with a deep connection to the ocean of stars." },
            { name: "Praxion", meaning: "Praxion is a sign of intellect, always searching for knowledge." },
            { name: "Zarvok", meaning: "Zarvok symbolizes strength and courage in times of adversity." },
            { name: "Flarith", meaning: "Flarith brings warmth and light to all those it touches." },
            { name: "Etheon", meaning: "Etheon represents the crossroads between fate and destiny." },
            { name: "Veris", meaning: "Veris is a sign of creativity, always in tune with the universe's flow." },
            { name: "Trilion", meaning: "Trilion is a fiery sign, passionate and always seeking adventure." },
            { name: "Galion", meaning: "Galion is known for its tranquility and peaceful presence." },
            { name: "Karex", meaning: "Karex thrives on challenges and is always growing stronger." },
            { name: "Solara", meaning: "Solara radiates energy and light, bringing hope to those around it." },
            { name: "Verecan", meaning: "Verecan is an ancient sign of wisdom and patience." },
            { name: "Taranis", meaning: "Taranis is a symbol of perseverance and enduring strength." },
            { name: "Miriath", meaning: "Miriath is a nurturing sign, always caring for others." },
            { name: "Hexilon", meaning: "Hexilon is a secretive sign, always plotting for greater purposes." },
            { name: "Lunara", meaning: "Lunara is a mystical sign, with deep connections to the night sky." },
            { name: "Corvex", meaning: "Corvex symbolizes strategy, always thinking ahead." },
            { name: "Syntar", meaning: "Syntar is a free spirit, moving with the winds of change." },
            { name: "Palliar", meaning: "Palliar is a sign of growth and prosperity, always flourishing." },
            { name: "Freyos", meaning: "Freyos is the embodiment of joy and celebration in all things." },
            { name: "Vynar", meaning: "Vynar is a mysterious and complex sign, ever-evolving." },
            { name: "Orionis", meaning: "Orionis is known for its bravery and dedication to its cause." },
            { name: "Elyndor", meaning: "Elyndor brings peace and calmness, offering solace to others." }
        ];

        const calendar = document.getElementById("calendar");
        const doors = [];
        let isLoggedIn = false;
        let device = "pc"; // Default ist die PC-Version

        // Kalender mit 24 Türchen erstellen
        for (let i = 0; i < 24; i++) {
            const door = document.createElement("div");
            door.classList.add("door");
            door.innerHTML = `<div class="date">${i + 1}</div>`;
            door.addEventListener("click", () => openDoor(i));
            doors.push(door);
            calendar.appendChild(door);
        }

        // Türchen-Öffnungs-Funktion
        function openDoor(i) {
            if (!isLoggedIn) return;

            const sign = starSigns[i];
            const contentDiv = document.createElement("div");
            contentDiv.classList.add("door-content");
            contentDiv.innerHTML = `<h3>${sign.name}</h3><p>${sign.meaning}</p>`;
            
            // Türchen wird sichtbar und Text wird angezeigt
            doors[i].innerHTML = "";
            doors[i].appendChild(contentDiv);
            contentDiv.style.display = "block";

            doors[i].addEventListener("click", () => closeDoor(i)); // Schließen-Funktion
        }

        // Türchen schließen
        function closeDoor(i) {
            doors[i].innerHTML = `<div class="date">${i + 1}</div>`;
        }

        // Login-Funktion
        document.getElementById("login-btn").addEventListener("click", function() {
            const password = document.getElementById("password").value;
            if (communityPasswords.includes(password)) {
                alert("Login erfolgreich!");
                isLoggedIn = true;
                document.getElementById("login-container").style.display = "none";
                document.getElementById("device-selector").style.display = "block"; // Geräteauswahl anzeigen
            } else {
                alert("Falsches Passwort. Bitte versuche es erneut.");
            }
        });

        // Gerätewahl
        document.getElementById("device-pc").addEventListener("click", function() {
            device = "pc";
            setDeviceLayout();
        });

        document.getElementById("device-laptop").addEventListener("click", function() {
            device = "laptop";
            setDeviceLayout();
        });

        document.getElementById("device-tablet").addEventListener("click", function() {
            device = "tablet";
            setDeviceLayout();
        });

        document.getElementById("device-phone").addEventListener("click", function() {
            device = "phone";
            setDeviceLayout();
        });

        document.getElementById("device-mp3").addEventListener("click", function() {
            device = "mp3";
            setDeviceLayout();
        });

        // Layout-Anpassung basierend auf dem gewählten Gerät
        function setDeviceLayout() {
            switch(device) {
                case "pc":
                    calendar.style.gridTemplateColumns = "repeat(6, 1fr)";
                    break;
                case "laptop":
                    calendar.style.gridTemplateColumns = "repeat(5, 1fr)";
                    break;
                case "tablet":
                    calendar.style.gridTemplateColumns = "repeat(4, 1fr)";
                    break;
                case "phone":
                    calendar.style.gridTemplateColumns = "repeat(3, 1fr)";
                    break;
                case "mp3":
                    calendar.style.gridTemplateColumns = "1fr";
                    break;
            }
            alert(`${device.charAt(0).toUpperCase() + device.slice(1)}-Layout ausgewählt`);
            calendar.style.display = "grid"; // Kalender sichtbar machen
        }
    </script>
</body>
</html>

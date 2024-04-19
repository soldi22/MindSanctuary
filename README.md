<!DOCTYPE html>
<html lang="it">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MindSanctuary - Meditazione Guidata</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <div class="container">
        <h1>MindSanctuary</h1>
        <p class="intro-text">Scopri la pace interiore con la nostra app di meditazione, immersa in un sereno sfondo celeste blu. Lasciati avvolgere da un'atmosfera rilassante che ti guiderà verso un profondo stato di calma.</p>
        <h2>Seleziona una sessione di meditazione:</h2>
        <select id="sessionSelect">
            <option value="audio/session1.mp3">Meditazione Guidata 1</option>
            <option value="audio/session2.mp3">Meditazione Guidata 2</option>
        </select>
        <button id="startButton">Inizia Meditazione</button>
        <div id="meditationTimer">Tempo rimanente: --:--</div>
        <audio id="meditationAudio" src=""></audio>
    </div>

    <script src="script.js"></script>
</body>

</html>
/* Stile di base per la pagina */
body {
    font-family: Arial, sans-serif;
    text-align: center;
    padding: 50px;
    background-color: #e0f7fa; /* Celeste chiaro */
}

.container {
    max-width: 600px;
    margin: auto;
    background-color: #ffffff;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

h1 {
    color: #01579b; /* Blu scuro */
    margin-bottom: 20px;
}

.intro-text {
    margin-bottom: 20px;
    font-size: 18px;
    color: #0288d1; /* Blu medio */
}

h2 {
    color: #0288d1; /* Blu medio */
    margin-bottom: 10px;
}

select, button {
    padding: 10px 15px;
    margin-bottom: 20px;
    border-radius: 5px;
    border: none;
    color: white;
    background-color: #0288d1; /* Blu chiaro */
    font-weight: bold;
    cursor: pointer;
}

select:focus, button:hover {
    background-color: #0277bd; /* Blu medio */
}

#meditationTimer {
    margin-top: 20px;
    font-size: 18px;
    color: #01579b; /* Blu scuro */
}
// Seleziona gli elementi HTML
const startButton = document.getElementById('startButton');
const meditationTimer = document.getElementById('meditationTimer');
const meditationAudio = document.getElementById('meditationAudio');
const sessionSelect = document.getElementById('sessionSelect');

// Variabili per il timer
let timerInterval;
let timerDuration = 300; // 5 minuti

// Funzione per aggiornare il timer
function updateTimer() {
    const minutes = Math.floor(timerDuration / 60);
    const seconds = timerDuration % 60;
    meditationTimer.textContent = `Tempo rimanente: ${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;

    if (timerDuration > 0) {
        timerDuration--;
    } else {
        clearInterval(timerInterval);
        meditationAudio.pause();
        meditationTimer.textContent = "Meditazione conclusa";
        startButton.disabled = false; // Riabilita il pulsante alla fine della sessione
    }
}

// Funzione per avviare la meditazione
function startMeditation() {
    // Imposta l'audio della sessione selezionata
    meditationAudio.src = sessionSelect.value;
    
    // Avvia il timer
    timerDuration = 300; // 5 minuti
    timerInterval = setInterval(updateTimer, 1000);
    
    // Avvia l'audio
    meditationAudio.currentTime = 0;
    meditationAudio.play();

    // Disabilita il pulsante durante la meditazione
    startButton.disabled = true;
}

// Aggiungi un evento al pulsante di avvio
startButton.addEventListener('click', startMeditation);

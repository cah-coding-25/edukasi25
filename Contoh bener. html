<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Permainan Mencocokkan Hewan</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <!-- jsPDF CDN for PDF generation -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f0f4f8; /* Light blue-gray background */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
            box-sizing: border-box;
        }
        .game-container {
            background-color: #ffffff;
            border-radius: 20px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
            padding: 30px;
            width: 100%;
            max-width: 600px;
            text-align: center;
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        .input-field {
            padding: 12px 15px;
            border: 2px solid #cbd5e1; /* Light gray border */
            border-radius: 10px;
            font-size: 1rem;
            width: 100%;
            box-sizing: border-box;
            transition: border-color 0.3s ease;
        }
        .input-field:focus {
            outline: none;
            border-color: #3b82f6; /* Blue focus border */
        }
        .btn {
            background-color: #3b82f6; /* Blue button */
            color: white;
            padding: 12px 25px;
            border-radius: 10px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease;
            box-shadow: 0 4px 10px rgba(59, 130, 246, 0.3);
        }
        .btn:hover {
            background-color: #2563eb; /* Darker blue on hover */
            transform: translateY(-2px);
        }
        .btn:active {
            transform: translateY(0);
            box-shadow: 0 2px 5px rgba(59, 130, 246, 0.3);
        }
        .answer-option {
            background-color: #e2e8f0; /* Light gray option */
            color: #334155; /* Dark text */
            padding: 15px 20px;
            border-radius: 10px;
            font-size: 1rem;
            font-weight: 500;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease;
            text-align: left;
            width: 100%;
        }
        .answer-option:hover {
            background-color: #cbd5e1; /* Slightly darker gray on hover */
            transform: translateY(-2px);
        }
        .answer-option.correct {
            background-color: #4ade80; /* Green for correct */
            color: white;
        }
        .answer-option.incorrect {
            background-color: #ef4444; /* Red for incorrect */
            color: white;
        }
        .message-box {
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            padding: 20px;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 1000;
            display: none; /* Hidden by default */
            flex-direction: column;
            gap: 15px;
            align-items: center;
            max-width: 350px;
            width: 90%;
        }
        .message-box-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 999;
            display: none; /* Hidden by default */
        }
        .message-box-title {
            font-size: 1.5rem;
            font-weight: bold;
            color: #1e293b;
        }
        .message-box-content {
            font-size: 1rem;
            color: #475569;
            text-align: center;
        }
        .message-box-button {
            background-color: #3b82f6;
            color: white;
            padding: 10px 20px;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        .message-box-button:hover {
            background-color: #2563eb;
        }

        /* Shake animation for FAIZ_FAHMI_ID */
        @keyframes shake {
            0% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            50% { transform: translateX(5px); }
            75% { transform: translateX(-5px); }
            100% { transform: translateX(0); }
        }
        .shaking-text {
            animation: shake 0.5s infinite alternate; /* Adjust duration and iteration as needed */
            font-size: 1.2rem;
            font-weight: 700;
            color: #1d4ed8; /* Darker blue for visibility */
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
    <div class="game-container">
        <!-- Overlay and Message Box -->
        <div id="messageOverlay" class="message-box-overlay"></div>
        <div id="messageBox" class="message-box">
            <div id="messageBoxTitle" class="message-box-title"></div>
            <div id="messageBoxContent" class="message-box-content"></div>
            <button id="messageBoxButton" class="message-box-button">OK</button>
        </div>

        <!-- Start Screen -->
        <div id="startScreen" class="flex flex-col gap-5">
            <!-- FAIZ_FAHMI_ID text with shaking effect -->
            <div class="shaking-text">FAIZ_FAHMI_ID</div>
            <h1 class="text-3xl font-bold text-gray-800 mb-4">Permainan Mencocokkan Hewan</h1>
            <input type="text" id="playerName" placeholder="Masukkan Nama Anda" class="input-field" required>
            <input type="text" id="playerNISN" placeholder="Masukkan NISN Anda" class="input-field" required>
            <button id="startButton" class="btn">Mulai Permainan</button>
        </div>

        <!-- Game Screen -->
        <div id="gameScreen" class="hidden flex-col gap-5">
            <div class="flex justify-between items-center text-lg font-semibold text-gray-700">
                <p>Waktu: <span id="timerDisplay" class="text-blue-600">60</span> detik</p>
                <p>Skor: <span id="scoreDisplay" class="text-blue-600">0</span></p>
            </div>
            <h2 class="text-2xl font-bold text-gray-800 mt-4 mb-6">Hewan: <span id="animalName" class="text-blue-700"></span></h2>
            <div id="optionsContainer" class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <!-- Answer options will be loaded here by JavaScript -->
            </div>
            <p id="feedbackMessage" class="text-lg font-semibold mt-4"></p>
        </div>

        <!-- End Screen -->
        <div id="endScreen" class="hidden flex-col gap-5">
            <h2 class="text-3xl font-bold text-gray-800 mb-4">Permainan Selesai!</h2>
            <p class="text-xl text-gray-700">Nama: <span id="finalName" class="font-semibold text-blue-600"></span></p>
            <p class="text-xl text-gray-700">NISN: <span id="finalNISN" class="font-semibold text-blue-600"></span></p>
            <p class="text-xl text-gray-700">Skor Akhir: <span id="finalScore" class="font-semibold text-blue-600"></span></p>
            <p class="text-xl text-gray-700">Waktu Tersisa: <span id="timeRemaining" class="font-semibold text-blue-600"></span> detik</p>
            <div class="flex flex-col md:flex-row gap-4 mt-6 w-full justify-center">
                <button id="homeButton" class="btn bg-gray-500 hover:bg-gray-600">Beranda</button>
                <button id="restartButton" class="btn">Main Lagi</button>
                <button id="downloadPdfButton" class="btn bg-green-500 hover:bg-green-600">Unduh Laporan PDF</button>
            </div>
        </div>
    </div>

    <script>
        // Data hewan dan cara perkembangbiakannya (simulasi dari Google Sheet)
        const animalsData = [
            { animal: "Ayam", reproduction: "Bertelur" },
            { animal: "Sapi", reproduction: "Melahirkan" },
            { animal: "Katak", reproduction: "Bertelur" },
            { animal: "Ular", reproduction: "Bertelur" },
            { animal: "Kucing", reproduction: "Melahirkan" },
            { animal: "Ikan", reproduction: "Bertelur" },
            { animal: "Kuda", reproduction: "Melahirkan" },
            { animal: "Burung", reproduction: "Bertelur" },
            { animal: "Kelelawar", reproduction: "Melahirkan" },
            { animal: "Buaya", reproduction: "Bertelur" },
            { animal: "Kangguru", reproduction: "Melahirkan" },
            { animal: "Penyu", reproduction: "Bertelur" },
            { animal: "Lumba-lumba", reproduction: "Melahirkan" },
            { animal: "Bebek", reproduction: "Bertelur" },
            { animal: "Gajah", reproduction: "Melahirkan" },
            { animal: "Cicak", reproduction: "Bertelur" },
            { animal: "Singa", reproduction: "Melahirkan" },
            { animal: "Semut", reproduction: "Bertelur" },
            { animal: "Paus", reproduction: "Melahirkan" },
            { animal: "Kupu-kupu", reproduction: "Bertelur" }
        ];

        // Daftar cara perkembangbiakan unik untuk opsi jawaban
        const reproductionMethods = [...new Set(animalsData.map(item => item.reproduction))];

        // Elemen DOM
        const startScreen = document.getElementById('startScreen');
        const gameScreen = document.getElementById('gameScreen');
        const endScreen = document.getElementById('endScreen');
        const startButton = document.getElementById('startButton');
        const restartButton = document.getElementById('restartButton');
        const homeButton = document.getElementById('homeButton'); // New Home button
        const downloadPdfButton = document.getElementById('downloadPdfButton'); // New Download PDF button
        const playerNameInput = document.getElementById('playerName');
        const playerNISNInput = document.getElementById('playerNISN');
        const timerDisplay = document.getElementById('timerDisplay');
        const scoreDisplay = document.getElementById('scoreDisplay');
        const animalNameDisplay = document.getElementById('animalName');
        const optionsContainer = document.getElementById('optionsContainer');
        const feedbackMessage = document.getElementById('feedbackMessage');
        const finalNameDisplay = document.getElementById('finalName');
        const finalNISNDisplay = document.getElementById('finalNISN');
        const finalScoreDisplay = document.getElementById('finalScore');
        const timeRemainingDisplay = document.getElementById('timeRemaining');

        // Message Box elements
        const messageBox = document.getElementById('messageBox');
        const messageOverlay = document.getElementById('messageOverlay');
        const messageBoxTitle = document.getElementById('messageBoxTitle');
        const messageBoxContent = document.getElementById('messageBoxContent');
        const messageBoxButton = document.getElementById('messageBoxButton');

        // Variabel Game
        let score = 0;
        let timeLeft = 60; // Waktu dalam detik
        let gameInterval;
        let currentQuestion = null;
        let questionsAsked = []; // Untuk melacak pertanyaan yang sudah ditanyakan
        let playerName = '';
        let playerNISN = '';
        let finalTimeRemaining = 0; // To store time remaining at end of game

        // Fungsi untuk menampilkan kotak pesan kustom
        function showMessageBox(title, message, callback = null) {
            messageBoxTitle.textContent = title;
            messageBoxContent.textContent = message;
            messageBox.style.display = 'flex';
            messageOverlay.style.display = 'block';

            const closeMessageBox = () => {
                messageBox.style.display = 'none';
                messageOverlay.style.display = 'none';
                messageBoxButton.removeEventListener('click', closeMessageBox);
                if (callback) {
                    callback();
                }
            };
            messageBoxButton.addEventListener('click', closeMessageBox);
        }

        // Fungsi untuk mengacak array
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Fungsi untuk memulai permainan
        function startGame() {
            playerName = playerNameInput.value.trim();
            playerNISN = playerNISNInput.value.trim();

            if (!playerName || !playerNISN) {
                showMessageBox("Input Tidak Lengkap", "Nama dan NISN harus diisi sebelum memulai permainan.");
                return;
            }

            score = 0;
            timeLeft = 60;
            questionsAsked = []; // Reset pertanyaan yang sudah ditanyakan
            scoreDisplay.textContent = score;
            timerDisplay.textContent = timeLeft;
            feedbackMessage.textContent = '';

            startScreen.classList.add('hidden');
            gameScreen.classList.remove('hidden');
            gameScreen.classList.add('flex');

            loadQuestion();
            gameInterval = setInterval(updateTimer, 1000);
        }

        // Fungsi untuk memuat pertanyaan baru
        function loadQuestion() {
            optionsContainer.innerHTML = ''; // Bersihkan opsi sebelumnya
            feedbackMessage.textContent = ''; // Bersihkan pesan feedback

            // Pastikan semua pertanyaan sudah ditanyakan sebelum mengulang
            if (questionsAsked.length === animalsData.length) {
                questionsAsked = []; // Reset jika semua pertanyaan sudah ditanyakan
            }

            let availableQuestions = animalsData.filter(q => !questionsAsked.includes(q.animal));
            if (availableQuestions.length === 0) {
                // If somehow all questions are asked but not all animals are in questionsAsked, reset
                questionsAsked = [];
                availableQuestions = animalsData;
            }

            const randomIndex = Math.floor(Math.random() * availableQuestions.length);
            currentQuestion = availableQuestions[randomIndex];
            questionsAsked.push(currentQuestion.animal); // Tambahkan ke daftar pertanyaan yang sudah ditanyakan

            animalNameDisplay.textContent = currentQuestion.animal;

            // Buat opsi jawaban
            let options = [currentQuestion.reproduction];
            let incorrectOptions = reproductionMethods.filter(method => method !== currentQuestion.reproduction);

            // Tambahkan 3 opsi salah acak (atau kurang jika tidak cukup)
            shuffleArray(incorrectOptions);
            for (let i = 0; i < Math.min(3, incorrectOptions.length); i++) {
                options.push(incorrectOptions[i]);
            }

            // Acak opsi jawaban
            shuffleArray(options);

            options.forEach(option => {
                const button = document.createElement('button');
                button.textContent = option;
                button.classList.add('answer-option');
                button.addEventListener('click', () => checkAnswer(option, button));
                optionsContainer.appendChild(button);
            });
        }

        // Fungsi untuk memeriksa jawaban
        function checkAnswer(selectedAnswer, buttonElement) {
            // Nonaktifkan semua tombol opsi setelah jawaban dipilih
            Array.from(optionsContainer.children).forEach(btn => btn.disabled = true);

            if (selectedAnswer === currentQuestion.reproduction) {
                score += 20;
                feedbackMessage.textContent = 'Benar!';
                feedbackMessage.classList.remove('text-red-600');
                feedbackMessage.classList.add('text-green-600');
                buttonElement.classList.add('correct');
            } else {
                score = Math.max(0, score - 5); // Kurangi 5 poin, minimal 0
                feedbackMessage.textContent = `Salah! Jawaban yang benar adalah '${currentQuestion.reproduction}'.`;
                feedbackMessage.classList.remove('text-green-600');
                feedbackMessage.classList.add('text-red-600');
                buttonElement.classList.add('incorrect');

                // Highlight the correct answer
                Array.from(optionsContainer.children).forEach(btn => {
                    if (btn.textContent === currentQuestion.reproduction) {
                        btn.classList.add('correct');
                    }
                });
            }
            scoreDisplay.textContent = score;

            // Muat pertanyaan berikutnya setelah jeda singkat
            setTimeout(() => {
                // Aktifkan kembali tombol opsi
                Array.from(optionsContainer.children).forEach(btn => btn.disabled = false);
                loadQuestion();
            }, 1500); // Jeda 1.5 detik
        }

        // Fungsi untuk memperbarui timer
        function updateTimer() {
            timeLeft--;
            timerDisplay.textContent = timeLeft;

            if (timeLeft <= 0) {
                endGame();
            }
        }

        // Fungsi untuk mengakhiri permainan
        function endGame() {
            clearInterval(gameInterval); // Hentikan timer
            finalTimeRemaining = timeLeft > 0 ? timeLeft : 0; // Store the final time remaining

            gameScreen.classList.add('hidden');
            endScreen.classList.remove('hidden');
            endScreen.classList.add('flex');

            finalNameDisplay.textContent = playerName;
            finalNISNDisplay.textContent = playerNISN;
            finalScoreDisplay.textContent = score;
            timeRemainingDisplay.textContent = finalTimeRemaining;
        }

        // Fungsi untuk mengunduh laporan PDF
        function downloadPdfReport() {
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();

            doc.setFontSize(22);
            doc.text("Laporan Permainan Mencocokkan Hewan", 105, 20, null, null, "center");

            doc.setFontSize(12);
            doc.text(`Nama Pemain: ${playerName}`, 20, 40);
            doc.text(`NISN: ${playerNISN}`, 20, 50);
            doc.text(`Skor Akhir: ${score}`, 20, 60);
            doc.text(`Waktu Tersisa: ${finalTimeRemaining} detik`, 20, 70);

            doc.setFontSize(14);
            doc.text("Penjelasan Permainan:", 20, 90);
            doc.setFontSize(10);
            const explanationText = `
Permainan "Mencocokkan Hewan" ini dirancang untuk menguji pengetahuan siswa tentang cara perkembangbiakan berbagai jenis hewan. Setiap pertanyaan menampilkan nama hewan, dan siswa harus memilih cara perkembangbiakan yang benar dari opsi yang tersedia.

Aturan Permainan:
- Setiap jawaban benar akan mendapatkan 20 poin.
- Setiap jawaban salah akan mengurangi 5 poin dari total skor.
- Waktu permainan adalah 60 detik. Permainan akan berakhir ketika waktu habis atau semua pertanyaan telah dijawab (jika data pertanyaan terbatas).

Tujuan permainan ini adalah untuk membantu siswa memahami dan mengingat konsep perkembangbiakan hewan dengan cara yang interaktif dan menyenangkan. Laporan ini merangkum kinerja siswa dalam permainan ini.
            `;
            doc.text(explanationText, 20, 100, { maxWidth: 170 });

            doc.save(`Laporan_Permainan_${playerName}_${playerNISN}.pdf`);
        }

        // Event Listeners
        startButton.addEventListener('click', startGame);
        restartButton.addEventListener('click', () => {
            endScreen.classList.add('hidden');
            startScreen.classList.remove('hidden');
            startScreen.classList.add('flex');
            playerNameInput.value = ''; // Clear input fields
            playerNISNInput.value = '';
        });
        homeButton.addEventListener('click', () => { // Event listener for Home button
            endScreen.classList.add('hidden');
            startScreen.classList.remove('hidden');
            startScreen.classList.add('flex');
            playerNameInput.value = ''; // Clear input fields
            playerNISNInput.value = '';
        });
        downloadPdfButton.addEventListener('click', downloadPdfReport); // Event listener for Download PDF button


        // Ensure the game starts clean on load
        window.onload = () => {
            startScreen.classList.remove('hidden');
            startScreen.classList.add('flex');
            gameScreen.classList.add('hidden');
            endScreen.classList.add('hidden');
        };
    </script>
</body>
</html>

<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Detektif: Misteri Lukisan Hilang</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        body {
            background: linear-gradient(145deg, #0b1a2e 0%, #1c2f44 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Segoe UI', 'Roboto', system-ui, sans-serif;
            padding: 20px;
        }
        .game-container {
            max-width: 820px;
            width: 100%;
            background: rgba(22, 34, 48, 0.85);
            backdrop-filter: blur(4px);
            border-radius: 48px;
            padding: 24px 28px 32px;
            box-shadow: 0 25px 40px rgba(0, 0, 0, 0.7), 0 0 0 2px #7d9eb3 inset;
            color: #e9f2f0;
            transition: all 0.2s;
        }
        h1 {
            font-size: 2.6rem;
            font-weight: 700;
            letter-spacing: 2px;
            text-shadow: 0 4px 8px rgba(0,0,0,0.6);
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 6px;
            border-bottom: 2px solid #5f7f94;
            padding-bottom: 10px;
        }
        h1 small {
            font-size: 1rem;
            font-weight: 300;
            opacity: 0.8;
            margin-left: auto;
            background: #1e364a;
            padding: 4px 14px;
            border-radius: 40px;
            letter-spacing: 1px;
        }
        .case-header {
            background: #1d3142;
            border-radius: 60px;
            padding: 12px 24px;
            margin: 12px 0 18px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            box-shadow: inset 0 2px 6px rgba(0,0,0,0.5);
            border: 1px solid #4e6f85;
        }
        .case-title {
            font-weight: 600;
            font-size: 1.1rem;
            background: #253b4e;
            padding: 5px 16px;
            border-radius: 50px;
        }
        .case-status {
            background: #2d4a5e;
            padding: 5px 18px;
            border-radius: 40px;
            font-size: 0.9rem;
            border-left: 3px solid #b8d0dd;
        }
        .clue-panel {
            background: #14232f;
            border-radius: 28px;
            padding: 18px 20px;
            margin: 16px 0 20px;
            border: 1px solid #426277;
            box-shadow: 0 6px 0 #0b171f;
        }
        .clue-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 10px 14px;
            justify-content: center;
        }
        .clue-item {
            background: #1d3343;
            padding: 8px 20px;
            border-radius: 60px;
            border-left: 4px solid #b9d4e3;
            font-weight: 500;
            font-size: 0.95rem;
            box-shadow: 0 2px 0 #0a141c;
            cursor: default;
            transition: 0.1s;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }
        .clue-item span {
            opacity: 0.7;
            font-weight: 300;
        }
        .clue-item.new-clue {
            border-left-color: #f7d44a;
            background: #1f3f54;
            animation: glowPulse 1.2s infinite alternate;
        }
        @keyframes glowPulse {
            0% { box-shadow: 0 0 2px #f7d44a; }
            100% { box-shadow: 0 0 12px #f7b84a; }
        }
        .interrogation-area {
            background: #1b2e3d;
            border-radius: 30px;
            padding: 18px 20px;
            margin: 20px 0;
            border: 1px solid #47677c;
        }
        .suspect-list {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 15px;
            margin: 10px 0 12px;
        }
        .suspect-card {
            background: #1e3345;
            padding: 12px 16px;
            border-radius: 40px;
            min-width: 100px;
            text-align: center;
            border: 2px solid #2a4a5e;
            transition: all 0.15s;
            cursor: pointer;
            font-weight: 500;
            box-shadow: 0 3px 0 #0b161f;
        }
        .suspect-card:hover {
            transform: scale(1.02);
            background: #274b61;
            border-color: #80a9c2;
        }
        .suspect-card.selected {
            border-color: #f7c948;
            background: #1f4860;
            box-shadow: 0 0 16px #f7b53b;
        }
        .action-area {
            display: flex;
            flex-wrap: wrap;
            gap: 14px;
            justify-content: center;
            margin: 12px 0 8px;
        }
        .btn {
            background: #213a4b;
            border: none;
            padding: 12px 28px;
            border-radius: 60px;
            font-weight: 600;
            font-size: 1rem;
            color: #eaf3f7;
            border-bottom: 4px solid #10222e;
            transition: 0.1s ease;
            cursor: pointer;
            box-shadow: 0 4px 6px rgba(0,0,0,0.3);
            flex: 1 1 auto;
            min-width: 120px;
            letter-spacing: 0.5px;
        }
        .btn-primary {
            background: #2d6580;
            border-bottom-color: #164153;
        }
        .btn-primary:hover {
            background: #3a7b9b;
            transform: scale(0.97);
        }
        .btn-success {
            background: #2d7a5a;
            border-bottom-color: #17503a;
        }
        .btn-danger {
            background: #8f3f4a;
            border-bottom-color: #5c232b;
        }
        .btn:active {
            transform: scale(0.94);
        }
        .btn:disabled {
            opacity: 0.5;
            filter: grayscale(0.4);
            transform: none;
            cursor: not-allowed;
        }
        .log-book {
            background: #0d1c27;
            border-radius: 30px;
            padding: 16px 20px;
            margin-top: 20px;
            border-left: 6px solid #aac3d1;
            min-height: 90px;
            box-shadow: inset 0 4px 12px rgba(0,0,0,0.6);
        }
        .log-message {
            font-size: 1.05rem;
            line-height: 1.5;
            color: #d6e6f0;
            font-weight: 400;
        }
        .log-message strong {
            color: #f7de8b;
            font-weight: 600;
        }
        .footer-info {
            display: flex;
            justify-content: space-between;
            margin-top: 14px;
            font-size: 0.8rem;
            opacity: 0.7;
            border-top: 1px solid #315066;
            padding-top: 12px;
        }
        .reset-link {
            color: #b4d0e0;
            cursor: pointer;
            text-decoration: underline dotted;
        }
        .reset-link:hover {
            color: #f7de8b;
        }
        .highlight {
            color: #fadf7e;
        }
        @media (max-width: 560px) {
            h1 { font-size: 1.8rem; flex-wrap: wrap; }
            .game-container { padding: 16px; }
        }
    </style>
</head>
<body>

<div class="game-container" id="appDetektif">
    <h1>
        🕵️‍♂️ DETEKTIF
        <small>Lukisan Hilang</small>
    </h1>
    <div class="case-header">
        <span class="case-title">📜 Kasus: <span id="caseName">Misteri 'Monalisa Malam'</span></span>
        <span class="case-status" id="statusDisplay">🔍 penyelidikan</span>
    </div>

    <!-- Petunjuk / Clue Panel -->
    <div class="clue-panel">
        <div style="display: flex; gap: 8px; align-items: center; margin-bottom: 12px;">
            <span style="background: #2d4f64; padding: 4px 18px; border-radius: 40px;">📌 PETUNJUK</span>
            <span style="font-size:0.9rem; opacity:0.8;">Klik saksi / tersangka untuk interogasi</span>
        </div>
        <div class="clue-grid" id="clueContainer">
            <!-- akan diisi oleh JS -->
        </div>
    </div>

    <!-- Interogasi Tersangka -->
    <div class="interrogation-area">
        <div style="display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 8px;">
            <span style="font-weight: 600;">🧐 DAFTAR TERDUGA</span>
            <span style="font-size:0.8rem; background: #1f3345; padding: 2px 14px; border-radius: 30px;">pilih lalu interogasi</span>
        </div>
        <div class="suspect-list" id="suspectList">
            <!-- suspect cards -->
        </div>
        <div class="action-area">
            <button class="btn btn-primary" id="interrogateBtn">🔎 Interogasi</button>
            <button class="btn btn-success" id="accuseBtn">⚖️ Tangkap Pelaku</button>
            <button class="btn" id="investigateBtn">🔦 Cari Petunjuk Baru</button>
        </div>
    </div>

    <!-- Log / Catatan Detektif -->
    <div class="log-book">
        <div style="display: flex; gap: 12px; align-items: center; margin-bottom: 6px;">
            <span style="background: #1c3547; padding: 2px 18px; border-radius: 30px;">📋 CATATAN</span>
        </div>
        <div class="log-message" id="logMessage">
            🕵️ Selamat datang, Detektif. Cari petunjuk, interogasi tersangka, dan tangkap pelaku.
        </div>
    </div>

    <div class="footer-info">
        <span>🔎 petunjuk ditemukan: <span id="clueCounter">0</span>/5</span>
        <span class="reset-link" id="resetGameBtn">↺ mulai ulang kasus</span>
    </div>
</div>

<script>
    (function() {
        // ----- Data Kasus -----
        const suspects = [
            { id: 's1', name: 'Renata', role: 'Kurator Museum', clue: 'Renata tahu kode alarm, tetapi malam itu ia sedang di pesta.' },
            { id: 's2', name: 'Bram', role: 'Penjaga Malam', clue: 'Bram melihat bayangan di taman, tetapi mengaku tidak mendengar bunyi.' },
            { id: 's3', name: 'Luna', role: 'Pemilik Galeri', clue: 'Luna baru saja membeli asuransi lukisan mahal. Ia tampak gugup.' },
            { id: 's4', name: 'Dimitri', role: 'Kolektor Seni', clue: 'Dimitri sering menawar lukisan itu, tapi motifnya kuat: ia butuh dana.' },
        ];

        // Petunjuk awal (tersembunyi, akan muncul bertahap)
        const cluePool = [
            { text: '🔑 Kunci ruang penyimpanan hilang sejak dua hari lalu.', revealed: false },
            { text: '🖼️ Lukisan palsu ditemukan di bengkel sebelah.', revealed: false },
            { text: '📞 Ada panggilan aneh dari galeri pada pukul 02:00.', revealed: false },
            { text: '🧤 Sidik jari di bingkai milik Dimitri.', revealed: false },
            { text: '💸 Rekening Luna menerima transfer besar seminggu lalu.', revealed: false },
        ];

        // State game
        let state = {
            cluesFound: 0,               // jumlah petunjuk yg terungkap
            cluesRevealed: [false, false, false, false, false],
            selectedSuspectId: null,      // id tersangka yg dipilih
            caseSolved: false,
            turnCount: 0,
            log: ['🕵️ Kasus dimulai. Kumpulkan petunjuk!'],
        };

        // Elemen DOM
        const clueContainer = document.getElementById('clueContainer');
        const suspectListEl = document.getElementById('suspectList');
        const logMessageEl = document.getElementById('logMessage');
        const clueCounterEl = document.getElementById('clueCounter');
        const statusDisplay = document.getElementById('statusDisplay');
        const resetBtn = document.getElementById('resetGameBtn');

        // Buttons
        const interrogateBtn = document.getElementById('interrogateBtn');
        const accuseBtn = document.getElementById('accuseBtn');
        const investigateBtn = document.getElementById('investigateBtn');

        // Helper: update UI clues
        function renderClues() {
            let html = '';
            let count = 0;
            cluePool.forEach((clue, idx) => {
                const revealed = state.cluesRevealed[idx];
                if (revealed) {
                    count++;
                    html += `<div class="clue-item new-clue"><span>🔎</span> ${clue.text}</div>`;
                } else {
                    html += `<div class="clue-item" style="opacity:0.4; border-left-color:#3a5a6e;"><span>❓</span> petunjuk tersembunyi</div>`;
                }
            });
            clueContainer.innerHTML = html;
            state.cluesFound = count;
            clueCounterEl.textContent = count;

            // Update status jika semua petunjuk ditemukan
            if (count === cluePool.length && !state.caseSolved) {
                statusDisplay.innerHTML = '💡 semua petunjuk ditemukan!';
            } else if (state.caseSolved) {
                statusDisplay.innerHTML = '✅ KASUS TERSELESAIKAN';
            } else {
                statusDisplay.innerHTML = `🔍 penyelidikan (${count}/${cluePool.length})`;
            }
        }

        // Render suspect cards
        function renderSuspects() {
            let html = '';
            suspects.forEach(s => {
                const selected = state.selectedSuspectId === s.id ? 'selected' : '';
                html += `<div class="suspect-card ${selected}" data-id="${s.id}">${s.name} <span style="font-weight:300; opacity:0.6; display:block; font-size:0.75rem;">${s.role}</span></div>`;
            });
            suspectListEl.innerHTML = html;

            // Event listener untuk memilih tersangka
            document.querySelectorAll('.suspect-card').forEach(card => {
                card.addEventListener('click', function(e) {
                    if (state.caseSolved) {
                        addLog('Kasus sudah selesai, tidak bisa interogasi lagi.');
                        return;
                    }
                    const id = this.dataset.id;
                    state.selectedSuspectId = id;
                    renderSuspects();
                    addLog(`Memilih ${suspects.find(s => s.id === id).name} sebagai fokus.`);
                });
            });
        }

        // Tambah log
        function addLog(msg) {
            state.log.push(msg);
            if (state.log.length > 30) state.log.shift();
            logMessageEl.innerHTML = msg;
        }

        // ----- Investigasi: menemukan petunjuk baru -----
        function investigate() {
            if (state.caseSolved) {
                addLog('Kasus telah dipecahkan. Mulai ulang untuk penyelidikan baru.');
                return;
            }

            // Cari petunjuk yang belum ditemukan
            const unrevealedIndices = [];
            cluePool.forEach((c, idx) => {
                if (!state.cluesRevealed[idx]) unrevealedIndices.push(idx);
            });

            if (unrevealedIndices.length === 0) {
                addLog('Semua petunjuk sudah terungkap. Saatnya menangkap pelaku!');
                return;
            }

            // Acak salah satu petunjuk yang belum ditemukan
            const randomIdx = unrevealedIndices[Math.floor(Math.random() * unrevealedIndices.length)];
            state.cluesRevealed[randomIdx] = true;

            const clueText = cluePool[randomIdx].text;
            addLog(`🔍 Petunjuk baru ditemukan: "${clueText}"`);
            renderClues();

            // Cek jika semua petunjuk sudah ditemukan
            if (state.cluesFound === cluePool.length) {
                addLog('💡 Semua petunjuk terkumpul! Analisis tersangka untuk menemukan pelaku.');
            }
        }

        // Interogasi tersangka yang dipilih
        function interrogate() {
            if (state.caseSolved) {
                addLog('Kasus sudah ditutup. Tidak ada interogasi lebih lanjut.');
                return;
            }

            const selectedId = state.selectedSuspectId;
            if (!selectedId) {
                addLog('Pilih tersangka terlebih dahulu!');
                return;
            }

            const suspect = suspects.find(s => s.id === selectedId);
            if (!suspect) return;

            // Interogasi memberikan petunjuk tambahan (tergantung jumlah petunjuk)
            const clueCount = state.cluesFound;
            let message = `🧐 Interogasi ${suspect.name} (${suspect.role}): `;

            // Berikan informasi tambahan berdasarkan petunjuk yang sudah ditemukan
            if (clueCount >= 4) {
                message += `"${suspect.name} mengakui bahwa ia melihat Dimitri di sekitar galeri malam itu." (Petunjuk kuat)`;
                // Bisa membuka clue tambahan? kita beri clue baru kalau belum semua
                if (state.cluesFound < cluePool.length) {
                    // reveal satu clue random
                    const unrevealed = [];
                    cluePool.forEach((c, idx) => { if (!state.cluesRevealed[idx]) unrevealed.push(idx); });
                    if (unrevealed.length > 0) {
                        const randIdx = unrevealed[Math.floor(Math.random() * unrevealed.length)];
                        state.cluesRevealed[randIdx] = true;
                        renderClues();
                        message += ` (Petunjuk tambahan terungkap!)`;
                    }
                }
            } else if (clueCount >= 2) {
                message += `"${suspect.name} memberikan alibi, tapi terlihat ragu-ragu."`;
            } else {
                message += `"${suspect.name} menjawab dengan hati-hati, tidak banyak informasi."`;
            }

            addLog(message);
            // sedikit peluang menambah clue jika belum semua
            if (state.cluesFound < cluePool.length && Math.random() < 0.4) {
                const unrevealed = [];
                cluePool.forEach((c, idx) => { if (!state.cluesRevealed[idx]) unrevealed.push(idx); });
                if (unrevealed.length > 0) {
                    const randIdx = unrevealed[Math.floor(Math.random() * unrevealed.length)];
                    state.cluesRevealed[randIdx] = true;
                    renderClues();
                    addLog(`🔎 Interogasi mengungkap petunjuk: "${cluePool[randIdx].text}"`);
                }
            }
            renderClues();
        }

        // ----- Tangkap pelaku (menang jika clue lengkap & memilih pelaku benar) -----
        function accuse() {
            if (state.caseSolved) {
                addLog('Kasus sudah selesai. Tidak perlu menangkap lagi.');
                return;
            }

            const selectedId = state.selectedSuspectId;
            if (!selectedId) {
                addLog('Pilih tersangka yang akan ditangkap!');
                return;
            }

            const suspect = suspects.find(s => s.id === selectedId);

            // Pelaku sebenarnya: Dimitri (id s4) berdasarkan petunjuk: sidik jari, transfer, motif
            // Tapi harus mengumpulkan minimal 4 petunjuk untuk bukti kuat
            if (state.cluesFound < 4) {
                addLog(`⚠️ Bukti belum cukup (${state.cluesFound}/5 petunjuk). Kumpulkan lebih banyak petunjuk!`);
                return;
            }

            // Pelaku benar: Dimitri (s4)
            if (selectedId === 's4') {
                state.caseSolved = true;
                statusDisplay.innerHTML = '✅ KASUS TERPECAHKAN!';
                addLog(`🎉 Tepat! ${suspect.name} adalah pelaku pencurian lukisan. Motif: butuh uang, dan sidik jarinya ditemukan. KASUS SELESAI!`);
                renderClues();
                renderSuspects();
                // disable buttons? tidak perlu, tapi logic sudah cegah aksi lebih lanjut
            } else {
                // Salah tangkap
                addLog(`❌ Salah! ${suspect.name} bukan pelaku. Petunjuk mengarah ke yang lain. Coba analisis lagi.`);
                // hukuman: hilangkan 1 petunjuk? (optional) biar seru
                if (state.cluesFound > 0) {
                    // hilangkan satu petunjuk yang sudah ditemukan (acak)
                    const revealedIndices = [];
                    cluePool.forEach((c, idx) => { if (state.cluesRevealed[idx]) revealedIndices.push(idx); });
                    if (revealedIndices.length > 0) {
                        const randIdx = revealedIndices[Math.floor(Math.random() * revealedIndices.length)];
                        state.cluesRevealed[randIdx] = false;
                        addLog(`😤 Akibat salah tuduh, satu petunjuk hilang!`);
                        renderClues();
                    }
                }
            }
        }

        // Reset game
        function resetGame() {
            state.cluesFound = 0;
            state.cluesRevealed = [false, false, false, false, false];
            state.selectedSuspectId = null;
            state.caseSolved = false;
            state.turnCount = 0;
            state.log = ['🕵️ Kasus dimulai ulang. Cari petunjuk!'];
            // reset log
            logMessageEl.innerHTML = '🕵️ Kasus dimulai ulang. Kumpulkan petunjuk dan temukan pelaku.';
            renderClues();
            renderSuspects();
            statusDisplay.innerHTML = '🔍 penyelidikan baru';
            addLog('🔄 Semua petunjuk dan tersangka direset. Selamat menyelidiki!');
        }

        // Setup event listeners
        function init() {
            renderSuspects();
            renderClues();
            addLog('🕵️ Silakan pilih tersangka, lalu interogasi. Gunakan "Cari Petunjuk Baru" untuk mengungkap fakta.');

            // Events
            investigateBtn.addEventListener('click', investigate);
            interrogateBtn.addEventListener('click', interrogate);
            accuseBtn.addEventListener('click', accuse);
            resetBtn.addEventListener('click', resetGame);

            // Click pada suspect card sudah dihandle di renderSuspects
        }

        init();
    })();
</script>
</body>
</html>

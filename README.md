```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Своя Игра — Вечеринка</title>
    <style>
        /* ===== RESET & GLOBAL ===== */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        body {
            font-family: 'Segoe UI', Roboto, system-ui, sans-serif;
            background: #0b0e14;
            color: #f0f4fa;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 16px;
            margin: 0;
        }
        #app {
            width: 100%;
            max-width: 1400px;
            background: #141a24;
            border-radius: 40px;
            padding: 24px 28px 32px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.7);
            position: relative;
            transition: opacity 0.2s;
        }
        .hidden {
            display: none !important;
        }
        button {
            cursor: pointer;
            font-family: inherit;
            font-size: 1rem;
            border: none;
            outline: none;
            background: #2a3342;
            color: #f0f4fa;
            padding: 8px 18px;
            border-radius: 30px;
            transition: background 0.15s, transform 0.1s;
        }
        button:hover {
            background: #3e4a5e;
            transform: scale(0.97);
        }
        button:active {
            transform: scale(0.93);
        }
        input,
        select,
        textarea {
            background: #1e2633;
            border: 1px solid #2f3a4b;
            color: #f0f4fa;
            border-radius: 12px;
            padding: 10px 14px;
            font-size: 1rem;
            font-family: inherit;
            width: 100%;
            transition: border 0.2s;
        }
        input:focus,
        select:focus,
        textarea:focus {
            border-color: #f7c948;
            outline: none;
        }
        textarea {
            resize: vertical;
            min-height: 60px;
        }
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #1e2633;
        }
        ::-webkit-scrollbar-thumb {
            background: #3e4a5e;
            border-radius: 10px;
        }

        /* ===== HEADER ===== */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 12px;
        }
        .header h1 {
            font-weight: 700;
            font-size: 2rem;
            letter-spacing: 1px;
            background: linear-gradient(135deg, #f7c948, #f0a030);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        .header-actions {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }
        .header-actions button {
            background: #2a3342;
            padding: 8px 20px;
            font-weight: 600;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .header-actions .danger {
            background: #5f2e3a;
        }
        .header-actions .danger:hover {
            background: #7f3e4e;
        }

        /* ===== SCOREBOARD ===== */
        .scoreboard {
            display: flex;
            justify-content: space-around;
            gap: 16px;
            margin-bottom: 28px;
            flex-wrap: wrap;
            background: #10161f;
            border-radius: 60px;
            padding: 12px 20px;
            border: 1px solid #2a3342;
        }
        .team {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 1.3rem;
            font-weight: 600;
            flex-wrap: wrap;
            justify-content: center;
        }
        .team input {
            width: 110px;
            background: transparent;
            border: none;
            border-bottom: 2px solid #2f3a4b;
            border-radius: 0;
            padding: 4px 0;
            font-weight: 700;
            font-size: 1.2rem;
            color: #f0f4fa;
            text-align: center;
        }
        .team input:focus {
            border-bottom-color: #f7c948;
        }
        .team .score {
            min-width: 60px;
            text-align: center;
            background: #1e2633;
            padding: 0 14px;
            border-radius: 40px;
            font-size: 1.6rem;
            font-weight: 700;
            color: #f7c948;
        }
        .team .btn-group {
            display: flex;
            gap: 4px;
        }
        .team .btn-group button {
            padding: 2px 12px;
            font-size: 1.2rem;
            background: #2a3342;
            border-radius: 30px;
            line-height: 1.4;
        }
        .team .btn-group button:hover {
            background: #3e4a5e;
        }

        /* ===== GRID ===== */
        .grid-wrapper {
            overflow-x: auto;
            padding-bottom: 8px;
        }
        .grid {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 10px;
            min-width: 600px;
        }
        .grid .category-header {
            background: #1a2330;
            padding: 12px 6px;
            text-align: center;
            font-weight: 700;
            font-size: 1.1rem;
            border-radius: 20px;
            word-break: break-word;
            border: 2px solid transparent;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 6px;
            flex-wrap: wrap;
            min-height: 70px;
            position: relative;
        }
        .grid .category-header input {
            background: transparent;
            border: none;
            border-bottom: 2px solid #2f3a4b;
            border-radius: 0;
            padding: 4px 2px;
            font-weight: 700;
            font-size: 1rem;
            text-align: center;
            color: #f0f4fa;
            width: 100%;
            max-width: 120px;
        }
        .grid .category-header input:focus {
            border-bottom-color: #f7c948;
        }

        .cell {
            background: #1a2330;
            border-radius: 20px;
            padding: 16px 6px;
            text-align: center;
            font-size: 1.8rem;
            font-weight: 700;
            color: #bcc9db;
            cursor: pointer;
            transition: background 0.15s, transform 0.1s, opacity 0.2s;
            border: 3px solid transparent;
            min-height: 80px;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            word-break: break-word;
        }
        .cell:hover:not(.played) {
            background: #26313f;
            transform: scale(1.02);
            border-color: #f7c94840;
        }
        .cell .edit-icon {
            position: absolute;
            top: 4px;
            right: 8px;
            font-size: 0.9rem;
            opacity: 0;
            transition: opacity 0.2s;
            pointer-events: none;
            color: #f7c948;
        }
        .cell:hover .edit-icon {
            opacity: 0.8;
            pointer-events: auto;
        }
        .cell .edit-icon:hover {
            opacity: 1;
        }
        .cell.played {
            opacity: 0.35;
            cursor: default;
            background: #111821;
            border-color: #2a3342;
            color: #5a6a7e;
        }
        .cell.played .edit-icon {
            display: none;
        }

        /* ===== MODAL / FULLSCREEN QUESTION ===== */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background: rgba(8, 12, 18, 0.92);
            backdrop-filter: blur(6px);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: 20px;
            animation: fadeIn 0.25s ease;
        }
        .modal {
            background: #1a2330;
            border-radius: 48px;
            max-width: 1000px;
            width: 100%;
            max-height: 95vh;
            padding: 32px 36px;
            overflow-y: auto;
            box-shadow: 0 30px 60px rgba(0, 0, 0, 0.8);
            border: 1px solid #2f3a4b;
            position: relative;
        }
        .modal.fullscreen {
            max-width: 1200px;
        }
        .modal-close {
            position: absolute;
            top: 16px;
            right: 20px;
            background: none;
            font-size: 2rem;
            color: #8a9bb0;
            padding: 0 8px;
            border-radius: 30px;
        }
        .modal-close:hover {
            background: #2a3342;
            color: #fff;
        }

        /* editor */
        .editor-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px 30px;
            margin-top: 12px;
        }
        .editor-grid .full-width {
            grid-column: 1 / -1;
        }
        .editor-grid label {
            font-weight: 600;
            font-size: 0.9rem;
            color: #b0c0d4;
            display: block;
            margin-bottom: 4px;
        }
        .editor-grid .field-group {
            margin-bottom: 10px;
        }
        .progress-grid {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 6px;
            margin: 12px 0 6px;
        }
        .progress-grid .pcell {
            background: #1e2633;
            border-radius: 8px;
            padding: 8px 0;
            text-align: center;
            font-size: 1.2rem;
            font-weight: 700;
            border: 2px solid transparent;
            transition: border 0.15s;
            cursor: pointer;
        }
        .progress-grid .pcell.filled {
            color: #4caf50;
        }
        .progress-grid .pcell.empty {
            color: #cf6679;
        }
        .progress-grid .pcell.current {
            border-color: #f7c948;
        }

        /* question view */
        .q-view {
            text-align: center;
        }
        .q-view .q-meta {
            font-size: 1.4rem;
            color: #b0c0d4;
            margin-bottom: 6px;
        }
        .q-view .q-text {
            font-size: 2.8rem;
            font-weight: 700;
            margin: 20px 0 28px;
            line-height: 1.3;
        }
        .q-view .options-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 16px;
            margin: 20px 0 30px;
        }
        .q-view .options-grid .opt {
            background: #1e2633;
            padding: 18px 10px;
            border-radius: 30px;
            font-size: 1.4rem;
            font-weight: 500;
            border: 2px solid #2f3a4b;
        }
        .q-view .answer-box {
            background: #0f1620;
            border-radius: 30px;
            padding: 24px;
            margin: 20px 0;
            animation: fadeIn 0.4s ease;
        }
        .q-view .answer-box .correct-answer {
            font-size: 2.2rem;
            font-weight: 700;
            color: #4caf50;
        }
        .q-view .answer-box .media-container {
            margin-top: 16px;
        }
        .q-view .answer-box .media-container img,
        .q-view .answer-box .media-container iframe {
            max-width: 100%;
            border-radius: 20px;
            max-height: 300px;
        }
        .q-view .action-row {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 16px;
            margin-top: 24px;
        }
        .q-view .action-row button {
            padding: 12px 28px;
            font-weight: 700;
            font-size: 1.1rem;
            background: #2a3342;
        }
        .q-view .action-row .primary {
            background: #f7c948;
            color: #0b0e14;
        }
        .q-view .action-row .primary:hover {
            background: #ffd95e;
        }
        .q-view .timer-ring {
            width: 80px;
            height: 80px;
            margin: 0 auto 16px;
            position: relative;
        }
        .q-view .timer-ring svg {
            transform: rotate(-90deg);
            width: 80px;
            height: 80px;
        }
        .q-view .timer-ring .bg {
            fill: none;
            stroke: #2a3342;
            stroke-width: 6;
        }
        .q-view .timer-ring .progress {
            fill: none;
            stroke: #4caf50;
            stroke-width: 6;
            stroke-linecap: round;
            transition: stroke-dashoffset 0.3s, stroke 0.3s;
        }
        .q-view .timer-ring .timer-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 1.8rem;
            font-weight: 700;
        }

        /* winner */
        .winner {
            text-align: center;
            padding: 20px 0;
        }
        .winner h2 {
            font-size: 3.5rem;
            margin-bottom: 8px;
            background: linear-gradient(135deg, #f7c948, #f0a030);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        .winner .score-big {
            font-size: 4rem;
            font-weight: 700;
            color: #f7c948;
        }
        .winner .ranking {
            margin-top: 24px;
            font-size: 1.4rem;
        }
        .winner .ranking li {
            list-style: none;
            padding: 6px 0;
            border-bottom: 1px solid #2a3342;
        }

        /* responsive */
        @media (max-width: 800px) {
            #app {
                padding: 16px;
            }
            .editor-grid {
                grid-template-columns: 1fr;
            }
            .q-view .q-text {
                font-size: 2rem;
            }
            .q-view .options-grid {
                grid-template-columns: 1fr;
            }
            .grid .category-header {
                font-size: 0.9rem;
                min-height: 56px;
            }
            .cell {
                font-size: 1.2rem;
                min-height: 60px;
                padding: 10px 4px;
            }
            .header h1 {
                font-size: 1.5rem;
            }
            .team {
                font-size: 1rem;
            }
            .team input {
                width: 80px;
                font-size: 1rem;
            }
            .modal {
                padding: 20px 18px;
            }
        }
        @media (max-width: 500px) {
            .grid {
                gap: 6px;
                min-width: 400px;
            }
            .cell {
                font-size: 1rem;
                min-height: 50px;
            }
        }

        /* animations */
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: scale(0.97);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }
        .fade-in {
            animation: fadeIn 0.3s ease;
        }

        /* misc */
        .flex-row {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            align-items: center;
        }
        .mt-8 {
            margin-top: 8px;
        }
        .mb-8 {
            margin-bottom: 8px;
        }
        .text-muted {
            color: #8a9bb0;
        }
        .text-center {
            text-align: center;
        }
        .w-full {
            width: 100%;
        }
    </style>
</head>
<body>
    <div id="app">
        <!-- HEADER -->
        <div class="header">
            <h1>🎯 СВОЯ ИГРА</h1>
            <div class="header-actions">
                <button id="resetBtn" class="danger">⟳ Сбросить игру</button>
                <button id="exportBtn">⬇ Экспорт</button>
                <button id="importBtn">⬆ Импорт</button>
                <input type="file" id="importFileInput" accept=".json" style="display:none">
            </div>
        </div>

        <!-- SCOREBOARD -->
        <div class="scoreboard" id="scoreboard"></div>

        <!-- GRID -->
        <div class="grid-wrapper">
            <div class="grid" id="gridContainer"></div>
        </div>

        <!-- MODAL CONTAINER -->
        <div id="modalContainer"></div>
    </div>
    <script>
        // =====================================================================
        // DATA
        // =====================================================================
        const DEFAULT_CATEGORIES = ['История', 'География', 'Наука', 'Кино', 'Спорт'];
        const DEFAULT_VALUES = [100, 200, 300, 400, 500];

        function createDefaultState() {
            const grid = [];
            for (let c = 0; c < 5; c++) {
                for (let r = 0; r < 5; r++) {
                    grid.push({
                        category: DEFAULT_CATEGORIES[c],
                        value: DEFAULT_VALUES[r],
                        question: `Вопрос ${DEFAULT_CATEGORIES[c]} ${DEFAULT_VALUES[r]}`,
                        options: ['Вариант А', 'Вариант Б', 'Вариант В', 'Вариант Г'],
                        correct: 'Вариант А',
                        image: '',
                        video: '',
                        played: false
                    });
                }
            }
            return {
                categories: [...DEFAULT_CATEGORIES],
                grid: grid,
                teams: [
                    { name: 'Команда 1', score: 0 },
                    { name: 'Команда 2', score: 0 },
                    { name: 'Команда 3', score: 0 }
                ],
                currentCellIndex: -1 // -1 means none
            };
        }

        // =====================================================================
        // STATE MANAGEMENT
        // =====================================================================
        let state = loadState();

        function loadState() {
            try {
                const saved = localStorage.getItem('svoya_igra_state');
                if (saved) {
                    const parsed = JSON.parse(saved);
                    // ensure grid length 25
                    if (parsed.grid && parsed.grid.length === 25) return parsed;
                }
            } catch (e) { /* ignore */ }
            return createDefaultState();
        }

        function saveState() {
            localStorage.setItem('svoya_igra_state', JSON.stringify(state));
        }

        // =====================================================================
        // HELPERS
        // =====================================================================
        function getCellIndex(catIdx, valIdx) {
            return catIdx * 5 + valIdx;
        }

        function getCell(catIdx, valIdx) {
            return state.grid[getCellIndex(catIdx, valIdx)];
        }

        function getAllPlayed() {
            return state.grid.every(c => c.played === true);
        }

        // =====================================================================
        // RENDER
        // =====================================================================
        function renderScoreboard() {
            const sb = document.getElementById('scoreboard');
            sb.innerHTML = state.teams.map((t, idx) => `
                <div class="team">
                    <input type="text" value="${escapeHtml(t.name)}" data-team-index="${idx}" class="team-name-input" />
                    <span class="score">${t.score}</span>
                    <div class="btn-group">
                        <button data-team="${idx}" data-delta="${state.grid.find(c => !c.played) ? (state.grid.find(c => !c.played).value || 0) : 0}" class="team-add">+</button>
                        <button data-team="${idx}" data-delta="${state.grid.find(c => !c.played) ? (state.grid.find(c => !c.played).value || 0) : 0}" class="team-sub">−</button>
                    </div>
                </div>
            `).join('');

            // event listeners for team name changes
            sb.querySelectorAll('.team-name-input').forEach(inp => {
                inp.addEventListener('change', function() {
                    const idx = parseInt(this.dataset.teamIndex);
                    state.teams[idx].name = this.value.trim() || `Команда ${idx+1}`;
                    saveState();
                });
            });

            // score buttons
            sb.querySelectorAll('.team-add').forEach(btn => {
                btn.addEventListener('click', function() {
                    const teamIdx = parseInt(this.dataset.team);
                    const delta = parseInt(this.dataset.delta) || 0;
                    if (delta > 0) {
                        state.teams[teamIdx].score += delta;
                        saveState();
                        renderAll();
                    }
                });
            });
            sb.querySelectorAll('.team-sub').forEach(btn => {
                btn.addEventListener('click', function() {
                    const teamIdx = parseInt(this.dataset.team);
                    const delta = parseInt(this.dataset.delta) || 0;
                    if (delta > 0) {
                        state.teams[teamIdx].score = Math.max(0, state.teams[teamIdx].score - delta);
                        saveState();
                        renderAll();
                    }
                });
            });
        }

        function renderGrid() {
            const container = document.getElementById('gridContainer');
            // categories header
            let html = '';
            for (let c = 0; c < 5; c++) {
                const catName = state.categories[c] || `Категория ${c+1}`;
                html += `<div class="category-header">
                    <input type="text" value="${escapeHtml(catName)}" data-cat-index="${c}" class="cat-name-input" />
                </div>`;
            }

            for (let r = 0; r < 5; r++) {
                for (let c = 0; c < 5; c++) {
                    const idx = getCellIndex(c, r);
                    const cell = state.grid[idx];
                    const val = cell.value || (r + 1) * 100;
                    const played = cell.played || false;
                    const hasContent = cell.question && cell.question.trim() !== '';
                    html += `<div class="cell ${played ? 'played' : ''}" data-index="${idx}">
                        ${hasContent ? val : '❓'}
                        <span class="edit-icon" data-index="${idx}">✏️</span>
                    </div>`;
                }
            }
            container.innerHTML = html;

            // category name inputs
            container.querySelectorAll('.cat-name-input').forEach(inp => {
                inp.addEventListener('change', function() {
                    const idx = parseInt(this.dataset.catIndex);
                    const val = this.value.trim() || `Категория ${idx+1}`;
                    state.categories[idx] = val;
                    // update grid category names
                    for (let r = 0; r < 5; r++) {
                        const gi = getCellIndex(idx, r);
                        state.grid[gi].category = val;
                    }
                    saveState();
                    renderAll();
                });
            });

            // cell click -> open question
            container.querySelectorAll('.cell:not(.played)').forEach(el => {
                el.addEventListener('click', function(e) {
                    if (e.target.classList.contains('edit-icon')) return;
                    const idx = parseInt(this.dataset.index);
                    openQuestionView(idx);
                });
            });

            // edit icon -> open editor
            container.querySelectorAll('.edit-icon').forEach(el => {
                el.addEventListener('click', function(e) {
                    e.stopPropagation();
                    const idx = parseInt(this.dataset.index);
                    openEditor(idx);
                });
            });

            // right-click -> editor
            container.querySelectorAll('.cell').forEach(el => {
                el.addEventListener('contextmenu', function(e) {
                    e.preventDefault();
                    const idx = parseInt(this.dataset.index);
                    openEditor(idx);
                });
            });
        }

        function renderAll() {
            renderScoreboard();
            renderGrid();
        }

        // =====================================================================
        // EDITOR MODAL
        // =====================================================================
        function openEditor(cellIndex) {
            if (cellIndex < 0 || cellIndex >= 25) return;
            const cell = state.grid[cellIndex];
            state.currentCellIndex = cellIndex;
            saveState();

            const catIdx = Math.floor(cellIndex / 5);
            const valIdx = cellIndex % 5;

            const modal = document.createElement('div');
            modal.className = 'modal-overlay';
            modal.id = 'editorModal';
            modal.innerHTML = `
                <div class="modal" style="max-width:900px;">
                    <button class="modal-close" data-close="editor">✕</button>
                    <h2 style="margin-bottom:6px;">✏️ Редактор вопроса</h2>
                    <div class="text-muted" style="margin-bottom:12px;">Категория: ${state.categories[catIdx]} | Стоимость: ${cell.value}</div>

                    <div class="editor-grid">
                        <div class="field-group">
                            <label>Категория</label>
                            <select id="editCategory"></select>
                        </div>
                        <div class="field-group">
                            <label>Стоимость</label>
                            <select id="editValue"></select>
                        </div>
                        <div class="field-group full-width">
                            <label>Вопрос</label>
                            <textarea id="editQuestion" rows="2">${escapeHtml(cell.question || '')}</textarea>
                        </div>
                        <div class="field-group">
                            <label>Вариант A</label>
                            <input id="editOpt0" value="${escapeHtml(cell.options[0] || '')}" />
                        </div>
                        <div class="field-group">
                            <label>Вариант B</label>
                            <input id="editOpt1" value="${escapeHtml(cell.options[1] || '')}" />
                        </div>
                        <div class="field-group">
                            <label>Вариант C</label>
                            <input id="editOpt2" value="${escapeHtml(cell.options[2] || '')}" />
                        </div>
                        <div class="field-group">
                            <label>Вариант D</label>
                            <input id="editOpt3" value="${escapeHtml(cell.options[3] || '')}" />
                        </div>
                        <div class="field-group">
                            <label>Правильный ответ</label>
                            <input id="editCorrect" value="${escapeHtml(cell.correct || '')}" />
                        </div>
                        <div class="field-group">
                            <label>Изображение (URL)</label>
                            <input id="editImage" value="${escapeHtml(cell.image || '')}" placeholder="https://..." />
                        </div>
                        <div class="field-group">
                            <label>YouTube (URL или ID)</label>
                            <input id="editVideo" value="${escapeHtml(cell.video || '')}" placeholder="https://youtu.be/... или ID" />
                        </div>
                    </div>

                    <div style="margin-top:16px;">
                        <label style="font-weight:600;">Прогресс заполнения (кликни для перехода)</label>
                        <div class="progress-grid" id="progressGrid"></div>
                    </div>

                    <div style="display:flex; gap:12px; margin-top:20px; flex-wrap:wrap;">
                        <button id="editorSaveBtn" class="primary" style="background:#f7c948;color:#0b0e14;font-weight:700;">💾 Сохранить</button>
                        <button id="editorCloseBtn">Закрыть</button>
                    </div>
                </div>
            `;

            document.getElementById('modalContainer').appendChild(modal);

            // populate selects
            const catSelect = modal.querySelector('#editCategory');
            const valSelect = modal.querySelector('#editValue');
            state.categories.forEach((cat, i) => {
                const opt = document.createElement('option');
                opt.value = i;
                opt.textContent = cat;
                if (i === catIdx) opt.selected = true;
                catSelect.appendChild(opt);
            });
            [100, 200, 300, 400, 500].forEach((v, i) => {
                const opt = document.createElement('option');
                opt.value = i;
                opt.textContent = v;
                if (i === valIdx) opt.selected = true;
                valSelect.appendChild(opt);
            });

            // progress grid
            function renderProgress() {
                const pg = modal.querySelector('#progressGrid');
                pg.innerHTML = '';
                for (let i = 0; i < 25; i++) {
                    const c = state.grid[i];
                    const isFilled = c.question && c.question.trim() !== '';
                    const div = document.createElement('div');
                    div.className = `pcell ${isFilled ? 'filled' : 'empty'} ${i === cellIndex ? 'current' : ''}`;
                    div.textContent = isFilled ? '✓' : '✗';
                    div.dataset.idx = i;
                    div.addEventListener('click', function() {
                        const idx = parseInt(this.dataset.idx);
                        // save current before switching
                        saveEditorData(modal, cellIndex);
                        closeModal('editor');
                        openEditor(idx);
                    });
                    pg.appendChild(div);
                }
            }
            renderProgress();

            // close handlers
            modal.querySelectorAll('[data-close]').forEach(el => {
                el.addEventListener('click', () => closeModal('editor'));
            });
            modal.querySelector('#editorCloseBtn').addEventListener('click', () => closeModal('editor'));
            modal.querySelector('#editorSaveBtn').addEventListener('click', function() {
                saveEditorData(modal, cellIndex);
                closeModal('editor');
            });

            // Escape key
            modal.addEventListener('keydown', (e) => {
                if (e.key === 'Escape') closeModal('editor');
            });
            modal.focus();
        }

        function saveEditorData(modal, idx) {
            const cell = state.grid[idx];
            const catIdx = parseInt(modal.querySelector('#editCategory').value);
            const valIdx = parseInt(modal.querySelector('#editValue').value);
            const newIdx = getCellIndex(catIdx, valIdx);

            // if moving to different cell, swap data
            if (newIdx !== idx) {
                const target = state.grid[newIdx];
                // swap everything except 'played'
                const temp = {
                    question: target.question,
                    options: target.options,
                    correct: target.correct,
                    image: target.image,
                    video: target.video,
                    category: target.category,
                    value: target.value,
                    played: target.played
                };
                target.question = cell.question;
                target.options = cell.options;
                target.correct = cell.correct;
                target.image = cell.image;
                target.video = cell.video;
                target.category = cell.category;
                target.value = cell.value;
                target.played = cell.played;

                cell.question = temp.question;
                cell.options = temp.options;
                cell.correct = temp.correct;
                cell.image = temp.image;
                cell.video = temp.video;
                cell.category = temp.category;
                cell.value = temp.value;
                cell.played = temp.played;

                // update current index
                state.currentCellIndex = newIdx;
            } else {
                // just update
                cell.question = modal.querySelector('#editQuestion').value;
                cell.options = [
                    modal.querySelector('#editOpt0').value,
                    modal.querySelector('#editOpt1').value,
                    modal.querySelector('#editOpt2').value,
                    modal.querySelector('#editOpt3').value
                ];
                cell.correct = modal.querySelector('#editCorrect').value;
                cell.image = modal.querySelector('#editImage').value;
                cell.video = modal.querySelector('#editVideo').value;
                // category & value already set from selects
                cell.category = state.categories[catIdx];
                cell.value = [100, 200, 300, 400, 500][valIdx];
            }

            saveState();
            renderAll();
        }

        // =====================================================================
        // QUESTION VIEW (fullscreen)
        // =====================================================================
        let timerInterval = null;
        let timerValue = 60;
        let timerActive = false;
        let answerRevealed = false;

        function openQuestionView(idx) {
            const cell = state.grid[idx];
            if (cell.played) return;

            // close any open modal first
            closeModal('all');

            const modal = document.createElement('div');
            modal.className = 'modal-overlay';
            modal.id = 'questionModal';
            modal.innerHTML = `
                <div class="modal fullscreen q-view">
                    <button class="modal-close" data-close="question">✕</button>

                    <div class="q-meta">${escapeHtml(cell.category)} · ${cell.value}</div>

                    <div class="timer-ring">
                        <svg viewBox="0 0 80 80">
                            <circle class="bg" cx="40" cy="40" r="34" />
                            <circle class="progress" id="timerCircle" cx="40" cy="40" r="34"
                                stroke-dasharray="${2 * Math.PI * 34}"
                                stroke-dashoffset="0" />
                        </svg>
                        <div class="timer-text" id="timerText">60</div>
                    </div>

                    <div class="q-text" id="qText">${escapeHtml(cell.question || 'Вопрос не задан')}</div>

                    <div class="options-grid" id="optionsGrid">
                        ${cell.options.map(o => `<div class="opt">${escapeHtml(o || '')}</div>`).join('')}
                    </div>

                    <div id="answerContainer" class="hidden">
                        <div class="answer-box fade-in">
                            <div class="correct-answer" id="correctAnswer">✅ ${escapeHtml(cell.correct || '')}</div>
                            <div class="media-container" id="mediaContainer"></div>
                        </div>
                    </div>

                    <div class="action-row">
                        <button id="revealBtn" class="primary">📢 Показать ответ</button>
                        <button id="backToGridBtn">⬅ Назад к полю</button>
                    </div>
                </div>
            `;

            document.getElementById('modalContainer').appendChild(modal);

            // start timer
            timerValue = 60;
            answerRevealed = false;
            timerActive = true;
            updateTimerDisplay(modal);

            if (timerInterval) clearInterval(timerInterval);
            timerInterval = setInterval(() => {
                if (!timerActive) return;
                timerValue--;
                updateTimerDisplay(modal);
                if (timerValue <= 0) {
                    timerActive = false;
                    clearInterval(timerInterval);
                    // auto reveal?
                }
            }, 1000);

            // reveal button
            modal.querySelector('#revealBtn').addEventListener('click', function() {
                revealAnswer(modal, idx);
            });

            // back button
            modal.querySelector('#backToGridBtn').addEventListener('click', function() {
                closeModal('question');
            });

            modal.querySelectorAll('[data-close]').forEach(el => {
                el.addEventListener('click', () => closeModal('question'));
            });

            modal.addEventListener('keydown', (e) => {
                if (e.key === 'Escape') closeModal('question');
            });
            modal.focus();
        }

        function updateTimerDisplay(modal) {
            const circle = modal.querySelector('#timerCircle');
            const text = modal.querySelector('#timerText');
            if (!circle) return;
            const radius = 34;
            const circumference = 2 * Math.PI * radius;
            const offset = circumference * (1 - timerValue / 60);
            circle.style.strokeDashoffset = offset;
            text.textContent = Math.max(0, timerValue);

            // color change last 10 sec
            if (timerValue <= 10) {
                circle.style.stroke = '#cf6679';
            } else {
                circle.style.stroke = '#4caf50';
            }
        }

        function revealAnswer(modal, idx) {
            if (answerRevealed) return;
            answerRevealed = true;
            timerActive = false;
            if (timerInterval) clearInterval(timerInterval);

            const cell = state.grid[idx];
            // mark as played
            cell.played = true;
            saveState();

            // hide timer & options
            modal.querySelector('.timer-ring').style.display = 'none';
            modal.querySelector('#optionsGrid').style.display = 'none';
            modal.querySelector('#revealBtn').style.display = 'none';

            // show answer
            const container = modal.querySelector('#answerContainer');
            container.classList.remove('hidden');

            // correct answer text
            modal.querySelector('#correctAnswer').textContent = `✅ ${cell.correct || 'Нет правильного ответа'}`;

            // media
            const mediaContainer = modal.querySelector('#mediaContainer');
            mediaContainer.innerHTML = '';
            if (cell.image && cell.image.trim() !== '') {
                const img = document.createElement('img');
                img.src = cell.image.trim();
                img.alt = 'Изображение';
                img.style.maxWidth = '100%';
                img.style.maxHeight = '300px';
                img.style.borderRadius = '16px';
                mediaContainer.appendChild(img);
            }
            if (cell.video && cell.video.trim() !== '') {
                let videoId = cell.video.trim();
                // extract ID if full URL
                const match = videoId.match(/(?:youtu\.be\/|youtube\.com\/(?:watch\?v=|embed\/|v\/))([^&?]+)/);
                if (match) videoId = match[1];
                if (videoId.length === 11) {
                    const iframe = document.createElement('iframe');
                    iframe.src = `https://www.youtube.com/embed/${videoId}`;
                    iframe.allow = 'accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture';
                    iframe.allowFullscreen = true;
                    iframe.style.width = '100%';
                    iframe.style.maxWidth = '560px';
                    iframe.style.height = '315px';
                    iframe.style.border = 'none';
                    iframe.style.borderRadius = '16px';
                    mediaContainer.appendChild(iframe);
                }
            }

            // update score buttons delta
            renderScoreboard();

            // change back button text or add close
            const backBtn = modal.querySelector('#backToGridBtn');
            backBtn.textContent = '⬅ Назад к полю';

            // check if all played
            if (getAllPlayed()) {
                setTimeout(() => {
                    showWinner();
                }, 600);
            }

            // re-render grid to mark played
            renderGrid();
        }

        // =====================================================================
        // WINNER
        // =====================================================================
        function showWinner() {
            closeModal('all');
            const sorted = [...state.teams].sort((a, b) => b.score - a.score);
            const topScore = sorted[0].score;
            const winners = sorted.filter(t => t.score === topScore);

            const modal = document.createElement('div');
            modal.className = 'modal-overlay';
            modal.id = 'winnerModal';
            modal.innerHTML = `
                <div class="modal winner" style="max-width:700px;">
                    <button class="modal-close" data-close="winner">✕</button>
                    <h2>🏆 Победитель${winners.length > 1 ? 'ы' : ''}</h2>
                    <div style="font-size:3rem;margin:12px 0;">${winners.map(w => escapeHtml(w.name)).join(' & ')}</div>
                    <div class="score-big">${topScore}</div>
                    <div class="ranking">
                        <h3 style="margin-bottom:8px;">Рейтинг</h3>
                        <ul>
                            ${sorted.map((t,i) => `<li>${i+1}. ${escapeHtml(t.name)} — ${t.score}</li>`).join('')}
                        </ul>
                    </div>
                    <button id="winnerCloseBtn" style="margin-top:20px;padding:12px 40px;background:#f7c948;color:#0b0e14;font-weight:700;">Отлично!</button>
                </div>
            `;
            document.getElementById('modalContainer').appendChild(modal);

            modal.querySelector('#winnerCloseBtn').addEventListener('click', () => closeModal('winner'));
            modal.querySelectorAll('[data-close]').forEach(el => {
                el.addEventListener('click', () => closeModal('winner'));
            });
            modal.addEventListener('keydown', (e) => {
                if (e.key === 'Escape') closeModal('winner');
            });
        }

        // =====================================================================
        // MODAL HELPERS
        // =====================================================================
        function closeModal(id) {
            if (id === 'all') {
                document.getElementById('modalContainer').innerHTML = '';
                if (timerInterval) clearInterval(timerInterval);
                timerActive = false;
                return;
            }
            const overlay = document.getElementById(id + 'Modal');
            if (overlay) overlay.remove();
            if (id === 'question' && timerInterval) {
                clearInterval(timerInterval);
                timerActive = false;
            }
            // if all modals closed, ensure timer cleared
            if (document.getElementById('modalContainer').children.length === 0) {
                if (timerInterval) clearInterval(timerInterval);
                timerActive = false;
            }
        }

        // =====================================================================
        // EXPORT / IMPORT
        // =====================================================================
        function exportData() {
            const data = JSON.stringify(state, null, 2);
            // offer download
            const blob = new Blob([data], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'svoya_igra_backup.json';
            a.click();
            URL.revokeObjectURL(url);
        }

        function importData(file) {
            const reader = new FileReader();
            reader.onload = (e) => {
                try {
                    const data = JSON.parse(e.target.result);
                    if (data.grid && data.grid.length === 25 && data.categories && data.teams) {
                        state = data;
                        saveState();
                        renderAll();
                        alert('Импорт успешно выполнен!');
                    } else {
                        alert('Неверный формат файла.');
                    }
                } catch (err) {
                    alert('Ошибка при чтении файла: ' + err.message);
                }
            };
            reader.readAsText(file);
        }

        // =====================================================================
        // RESET
        // =====================================================================
        function resetGame() {
            if (!confirm('Сбросить игру? Вопросы останутся, но счёт и прогресс обнулятся.')) return;
            // reset played flag but keep questions
            state.grid.forEach(c => c.played = false);
            state.teams.forEach(t => t.score = 0);
            state.currentCellIndex = -1;
            saveState();
            renderAll();
            closeModal('all');
        }

        // =====================================================================
        // UTILITY
        // =====================================================================
        function escapeHtml(str) {
            if (!str) return '';
            const div = document.createElement('div');
            div.textContent = str;
            return div.innerHTML;
        }

        // =====================================================================
        // INIT EVENTS
        // =====================================================================
        document.addEventListener('DOMContentLoaded', function() {
            renderAll();

            document.getElementById('resetBtn').addEventListener('click', resetGame);

            document.getElementById('exportBtn').addEventListener('click', exportData);

            document.getElementById('importBtn').addEventListener('click', function() {
                document.getElementById('importFileInput').click();
            });
            document.getElementById('importFileInput').addEventListener('change', function(e) {
                if (this.files.length > 0) {
                    importData(this.files[0]);
                    this.value = '';
                }
            });

            // close all modals on escape globally
            document.addEventListener('keydown', function(e) {
                if (e.key === 'Escape') {
                    const modals = document.querySelectorAll('.modal-overlay');
                    if (modals.length > 0) {
                        // close the topmost
                        const last = modals[modals.length - 1];
                        const id = last.id.replace('Modal', '');
                        closeModal(id);
                    }
                }
            });
        });

        // =====================================================================
        // Auto-save: save on any change via renderAll already saves
        // =====================================================================
        // ensure renderAll saves
        const origRenderAll = renderAll;
        renderAll = function() {
            origRenderAll();
            // saveState already called inside each action
        };
        // patch saveState to be called more often
        const origSave = saveState;
        saveState = function() {
            origSave();
            // also update current cell index if any
        };

        console.log('🎯 Своя Игра загружена!');
    </script>
</body>
</html>
```

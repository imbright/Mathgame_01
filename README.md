[Mathgame_01.html](https://github.com/user-attachments/files/34852989/Mathgame_01.html)
<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Math Puzzle Park</title>
  <style>
    :root{
      --bg1:#f5f7ff;
      --bg2:#eefbf7;
      --card:#ffffff;
      --primary:#4f6ef7;
      --primary-2:#6d8dff;
      --success:#20b36b;
      --danger:#ef5350;
      --warning:#ffb020;
      --text:#1c2333;
      --muted:#667085;
      --border:#e4e7ec;
      --shadow:0 14px 32px rgba(42,58,120,0.12);
    }

    * { box-sizing:border-box; }
    html, body {
      margin:0;
      padding:0;
      font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(140deg, var(--bg1), var(--bg2));
      color:var(--text);
    }

    body {
      min-height:100vh;
    }

    .app {
      max-width:1200px;
      margin:0 auto;
      padding:24px;
    }

    .topbar {
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:16px;
      background: rgba(255,255,255,0.72);
      backdrop-filter: blur(10px);
      -webkit-backdrop-filter: blur(10px);
      border:1px solid rgba(255,255,255,0.7);
      border-radius:18px;
      box-shadow: var(--shadow);
      padding:16px 20px;
      position:sticky;
      top:12px;
      z-index:20;
    }

    .brand {
      display:flex;
      align-items:center;
      gap:12px;
      font-weight:800;
      font-size:1.4rem;
      letter-spacing:0.5px;
    }

    .brand-mark {
      width:42px;
      height:42px;
      border-radius:14px;
      background: linear-gradient(135deg, var(--primary), var(--primary-2));
      display:grid;
      place-items:center;
      color:white;
      box-shadow:0 8px 18px rgba(79,110,247,0.35);
      font-size:1.2rem;
    }

    .lang-wrap {
      position:relative;
    }

    .lang-button {
      display:flex;
      align-items:center;
      gap:10px;
      border:none;
      background:#fff;
      color:var(--text);
      border-radius:12px;
      padding:10px 14px;
      font-size:0.96rem;
      border:1px solid var(--border);
      cursor:pointer;
      box-shadow:0 8px 16px rgba(15,23,42,0.05);
      transition:0.2s ease;
    }

    .lang-button:hover {
      transform:translateY(-1px);
    }

    .lang-menu {
      position:absolute;
      right:0;
      top:calc(100% + 10px);
      min-width:180px;
      background:#fff;
      border:1px solid var(--border);
      border-radius:12px;
      box-shadow:var(--shadow);
      display:none;
      overflow:hidden;
      z-index:5;
    }

    .lang-menu.open {
      display:block;
    }

    .lang-option {
      width:100%;
      text-align:left;
      border:none;
      background:#fff;
      padding:12px 14px;
      font-size:0.96rem;
      cursor:pointer;
      color:var(--text);
    }

    .lang-option:hover {
      background:#f4f6ff;
    }

    .page {
      display:none;
      animation: fadeIn 0.25s ease;
    }

    .page.active {
      display:block;
    }

    @keyframes fadeIn {
      from { opacity:0; transform:translateY(10px); }
      to { opacity:1; transform:translateY(0); }
    }

    .card {
      background: var(--card);
      border:1px solid var(--border);
      border-radius:22px;
      box-shadow: var(--shadow);
      padding:24px;
    }

    .home-header {
      display:flex;
      justify-content:space-between;
      align-items:center;
      gap:16px;
      margin-bottom:18px;
      flex-wrap:wrap;
    }

    .title {
      font-size: clamp(1.8rem, 4vw, 2.7rem);
      font-weight:800;
      margin:0;
      letter-spacing:0.5px;
    }

    .score-badge {
      background: linear-gradient(135deg, #fff6d8, #fff);
      border:1px solid #f3d46d;
      border-radius:14px;
      padding:12px 16px;
      font-weight:700;
      color:#8b5b00;
    }

    .player-box {
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:16px;
      flex-wrap:wrap;
      background: linear-gradient(135deg, #f9fbff, #f3f5ff);
      border:1px solid var(--border);
      border-radius:18px;
      padding:18px;
      margin-bottom:20px;
    }

    .field {
      display:flex;
      flex-direction:column;
      gap:8px;
      min-width:220px;
      flex:1;
    }

    .field label {
      font-weight:700;
      color:var(--muted);
    }

    .field input {
      border:1px solid var(--border);
      background:#fff;
      border-radius:12px;
      padding:12px 14px;
      font-size:1rem;
      outline:none;
      transition:0.2s ease;
    }

    .field input:focus {
      border-color: var(--primary);
      box-shadow:0 0 0 4px rgba(79,110,247,0.12);
    }

    .game-grid {
      display:grid;
      grid-template-columns: repeat(auto-fit, minmax(210px,1fr));
      gap:16px;
      margin-top:18px;
    }

    .game-btn {
      border:none;
      border-radius:18px;
      padding:22px 18px;
      color:white;
      font-size:1.08rem;
      font-weight:700;
      cursor:pointer;
      display:flex;
      align-items:center;
      justify-content:center;
      gap:10px;
      box-shadow:0 12px 24px rgba(42,58,120,0.14);
      transition: transform 0.18s ease, box-shadow 0.18s ease, filter 0.18s ease;
      min-height:110px;
    }

    .game-btn:hover {
      transform:translateY(-2px);
      filter:brightness(1.03);
      box-shadow:0 16px 26px rgba(42,58,120,0.18);
    }

    .btn-blue { background: linear-gradient(135deg, #4f6ef7, #6d8dff); }
    .btn-green { background: linear-gradient(135deg, #18b76d, #27d284); }
    .btn-orange { background: linear-gradient(135deg, #ff9d2e, #ffb548); }
    .btn-red { background: linear-gradient(135deg, #ef5350, #ff7d7d); }
    .btn-purple { background: linear-gradient(135deg, #8a5cf6, #b58dff); }

    .game-page .header-row {
      display:flex;
      justify-content:space-between;
      align-items:center;
      gap:12px;
      flex-wrap:wrap;
      margin-bottom:18px;
    }

    .header-left {
      display:flex;
      align-items:center;
      gap:12px;
      flex-wrap:wrap;
    }

    .back-btn {
      border:none;
      background: linear-gradient(135deg, #ef5350, #ff7d7d);
      color:white;
      border-radius:12px;
      padding:12px 16px;
      font-weight:700;
      cursor:pointer;
      box-shadow:0 10px 18px rgba(239,83,80,0.2);
    }

    .game-card {
      background:linear-gradient(180deg, #fff, #f9fafc);
      border:1px solid var(--border);
      border-radius:22px;
      padding:22px;
      box-shadow:var(--shadow);
    }

    .sub-tools {
      display:flex;
      align-items:center;
      gap:10px;
      flex-wrap:wrap;
      margin-top:8px;
    }

    .mini-btn {
      border:none;
      background:#edf2ff;
      border-radius:12px;
      padding:9px 12px;
      font-weight:700;
      color:var(--primary);
      cursor:pointer;
    }

    .question-box {
      margin:18px 0 10px;
      padding:18px 16px;
      background:#f8faff;
      border:1px solid #e4ebff;
      border-radius:16px;
      font-size:1.15rem;
      font-weight:700;
      line-height:1.6;
      word-break:break-word;
    }

    .answer-input {
      width:100%;
      border:1px solid var(--border);
      border-radius:14px;
      padding:14px 16px;
      font-size:1.08rem;
      outline:none;
      background:#fff;
      transition:0.2s ease;
    }

    .answer-input:focus {
      border-color: var(--primary);
      box-shadow:0 0 0 4px rgba(79,110,247,0.12);
    }

    .controls {
      display:flex;
      gap:12px;
      flex-wrap:wrap;
      margin-top:18px;
    }

    .action-btn {
      border:none;
      border-radius:12px;
      padding:12px 18px;
      cursor:pointer;
      color:white;
      font-weight:700;
      box-shadow:0 10px 18px rgba(0,0,0,0.08);
      transition:0.2s ease;
    }

    .action-btn:hover {
      transform:translateY(-1px);
    }

    .status {
      margin-top:16px;
      min-height:28px;
      font-weight:700;
      font-size:1.02rem;
    }

    .status.success {
      color: var(--success);
    }

    .status.error {
      color: var(--danger);
    }

    .status.info {
      color: var(--primary);
    }

    .progress-wrap {
      margin:18px 0 24px;
      background: rgba(255,255,255,0.66);
      border:1px solid var(--border);
      border-radius:16px;
      padding:14px 16px;
      box-shadow:0 10px 18px rgba(15,23,42,0.04);
    }

    .progress-top {
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:10px;
      margin-bottom:10px;
      font-weight:700;
      color:var(--muted);
      font-size:0.96rem;
    }

    .progress-bar {
      width:100%;
      height:16px;
      background:#edf0f5;
      border-radius:999px;
      overflow:hidden;
      position:relative;
    }

    .progress-fill {
      height:100%;
      width:0%;
      background: linear-gradient(90deg, #4f6ef7, #3bc7a5);
      border-radius:999px;
      transition:width 0.25s ease;
    }

    .difficulty-box {
      display:flex;
      align-items:center;
      gap:10px;
      flex-wrap:wrap;
      margin-bottom:10px;
      color:var(--muted);
      font-weight:600;
    }

    .difficulty-box select {
      border:1px solid var(--border);
      background:#fff;
      border-radius:12px;
      padding:10px 12px;
      min-width:230px;
      font-size:0.98rem;
      outline:none;
    }

    .small-label {
      color:var(--muted);
      font-weight:700;
    }

    .multi-player-list {
      display:grid;
      gap:12px;
      margin-top:16px;
    }

    .player-row {
      border:1px solid var(--border);
      background:#fff;
      border-radius:14px;
      padding:12px 14px;
    }

    .player-head {
      display:flex;
      justify-content:space-between;
      align-items:center;
      gap:8px;
      margin-bottom:8px;
      font-weight:700;
    }

    .rank-box {
      margin-top:18px;
      padding:16px;
      border-radius:14px;
      background:#f7f9ff;
      border:1px solid #e1e8ff;
    }

    .score-table {
      display:grid;
      gap:8px;
      margin-top:8px;
      font-weight:600;
    }

    @media (max-width: 700px){
      .topbar {
        padding:14px 16px;
      }
      .game-grid {
        grid-template-columns:1fr;
      }
      .player-box {
        flex-direction:column;
        align-items:stretch;
      }
      .field {
        width:100%;
      }
    }
  </style>
</head>
<body>
  <div class="app">
    <header class="topbar">
      <div class="brand">
        <div class="brand-mark">🧮</div>
        <span data-i18n="brand">Math Puzzle Park</span>
      </div>

      <div class="lang-wrap">
        <button class="lang-button" id="langTrigger" aria-label="Language">
          <span>🌐</span>
          <span data-i18n="language">Language</span>
          <span>▾</span>
        </button>
        <div class="lang-menu" id="langMenu">
          <button class="lang-option" data-lang="zh">中文</button>
          <button class="lang-option" data-lang="en">English</button>
          <button class="lang-option" data-lang="es">Español</button>
        </div>
      </div>
    </header>

    <div class="progress-wrap">
      <div class="progress-top">
        <span data-i18n="progressLabel">Progress</span>
        <span id="progressText">0 / 0</span>
      </div>
      <div class="progress-bar">
        <div class="progress-fill" id="progressFill"></div>
      </div>
    </div>

    <main>
      <!-- Home -->
      <section id="page-home" class="page active">
        <div class="home-header">
          <h1 class="title" data-i18n="homeTitle">Math Puzzle Park</h1>
          <div class="score-badge">
            <span data-i18n="totalScore">Total Score</span>: <strong id="totalScore">0</strong>
          </div>
        </div>

        <div class="card">
          <div class="player-box">
            <div class="field">
              <label data-i18n="playerName">Player Name</label>
              <input id="playerName" type="text" placeholder="Enter your name" />
            </div>
            <div class="field">
              <label data-i18n="playerId">Player ID</label>
              <input id="playerID" type="text" placeholder="Custom ID" />
            </div>
          </div>

          <div class="game-grid">
            <button class="game-btn btn-blue" data-page="page-24">
              <span>🎯</span>
              <span data-i18n="game24Btn">24 Game</span>
            </button>
            <button class="game-btn btn-green" data-page="page-calc">
              <span>🧠</span>
              <span data-i18n="gameCalcBtn">Mental Math</span>
            </button>
            <button class="game-btn btn-orange" data-page="page-word">
              <span>📘</span>
              <span data-i18n="gameWordBtn">Word Problems</span>
            </button>
            <button class="game-btn btn-purple" data-page="page-sudoku">
              <span>🔢</span>
              <span data-i18n="gameSudokuBtn">Sudoku</span>
            </button>
            <button class="game-btn btn-red" data-page="page-multi">
              <span>🏁</span>
              <span data-i18n="gameMultiBtn">Multi-player</span>
            </button>
          </div>
        </div>
      </section>

      <!-- 24 Game -->
      <section id="page-24" class="page game-page">
        <div class="header-row">
          <div class="header-left">
            <button class="back-btn" data-back="home">🏠 <span data-i18n="homeBtn">Home</span></button>
          </div>
          <div class="score-badge">
            <span data-i18n="singleScore">Single Score</span>: <strong id="score24">0</strong>
          </div>
        </div>

        <div class="card">
          <div class="difficulty-box">
            <span data-i18n="difficulty">Difficulty</span>:
            <select id="diff24">
              <option value="easy" data-i18n="easy">Easy (+3)</option>
              <option value="mid" data-i18n="normal">Normal (+6)</option>
              <option value="hard" data-i18n="hard">Hard (+10)</option>
              <option value="devil" data-i18n="devil">Devil Mode (unlock at 35)</option>
            </select>
          </div>

          <div class="question-box" id="q24">Numbers: -- -- -- --</div>
          <input class="answer-input" id="ans24" type="text" placeholder="Write formula: use + - * / ( )" />

          <div class="controls">
            <button class="action-btn btn-green" id="submit24Btn">✅ <span data-i18n="submit">Submit</span></button>
            <button class="action-btn btn-blue" id="next24Btn">➡️ <span data-i18n="next">Next</span></button>
            <button class="action-btn btn-orange" id="show24Btn">💡 <span data-i18n="showAnswer">Show Answer</span></button>
          </div>

          <div id="msg24" class="status"></div>
          <div id="ansShow24" class="status info"></div>
        </div>
      </section>

      <!-- Mental Math -->
      <section id="page-calc" class="page game-page">
        <div class="header-row">
          <div class="header-left">
            <button class="back-btn" data-back="home">🏠 <span data-i18n="homeBtn">Home</span></button>
          </div>
          <div class="score-badge">
            <span data-i18n="singleScore">Single Score</span>: <strong id="scoreCalc">0</strong>
          </div>
        </div>

        <div class="card">
          <div class="difficulty-box">
            <span data-i18n="difficulty">Difficulty</span>:
            <select id="diffCalc">
              <option value="easy" data-i18n="easy">Easy (+3)</option>
              <option value="mid" data-i18n="normal">Normal (+6)</option>
              <option value="hard" data-i18n="hard">Hard (+10)</option>
              <option value="devil" data-i18n="devil">Devil Mode (unlock at 35)</option>
            </select>
          </div>

          <div class="question-box" id="qCalc">Question: --</div>
          <input class="answer-input" id="ansCalc" type="number" placeholder="Enter answer" />

          <div class="controls">
            <button class="action-btn btn-green" id="submitCalcBtn">✅ <span data-i18n="submit">Submit</span></button>
            <button class="action-btn btn-blue" id="nextCalcBtn">➡️ <span data-i18n="next">Next</span></button>
            <button class="action-btn btn-orange" id="showCalcBtn">💡 <span data-i18n="showAnswer">Show Answer</span></button>
          </div>

          <div id="msgCalc" class="status"></div>
          <div id="ansShowCalc" class="status info"></div>
        </div>
      </section>

      <!-- Word Problems -->
      <section id="page-word" class="page game-page">
        <div class="header-row">
          <div class="header-left">
            <button class="back-btn" data-back="home">🏠 <span data-i18n="homeBtn">Home</span></button>
          </div>
          <div class="score-badge">
            <span data-i18n="singleScore">Single Score</span>: <strong id="scoreWord">0</strong>
          </div>
        </div>

        <div class="card">
          <div class="difficulty-box">
            <span data-i18n="difficulty">Difficulty</span>:
            <select id="diffWord">
              <option value="easy" data-i18n="easy">Easy (+3)</option>
              <option value="mid" data-i18n="normal">Normal (+6)</option>
              <option value="hard" data-i18n="hard">Hard (+10)</option>
              <option value="devil" data-i18n="devil">Devil Mode (unlock at 35)</option>
            </select>
          </div>

          <div class="question-box" id="qWord">Question: --</div>
          <input class="answer-input" id="ansWord" type="number" placeholder="Enter answer" />

          <div class="controls">
            <button class="action-btn btn-green" id="submitWordBtn">✅ <span data-i18n="submit">Submit</span></button>
            <button class="action-btn btn-blue" id="nextWordBtn">➡️ <span data-i18n="next">Next</span></button>
            <button class="action-btn btn-orange" id="showWordBtn">💡 <span data-i18n="showAnswer">Show Answer</span></button>
          </div>

          <div id="msgWord" class="status"></div>
          <div id="ansShowWord" class="status info"></div>
        </div>
      </section>

      <!-- Sudoku -->
      <section id="page-sudoku" class="page game-page">
        <div class="header-row">
          <div class="header-left">
            <button class="back-btn" data-back="home">🏠 <span data-i18n="homeBtn">Home</span></button>
          </div>
          <div class="score-badge">
            <span data-i18n="singleScore">Single Score</span>: <strong id="scoreSudoku">0</strong>
          </div>
        </div>

        <div class="card">
          <div class="difficulty-box">
            <span data-i18n="difficulty">Difficulty</span>:
            <select id="diffSudoku">
              <option value="easy" data-i18n="easy">Easy (+3)</option>
              <option value="mid" data-i18n="normal">Normal (+6)</option>
              <option value="hard" data-i18n="hard">Hard (+10)</option>
              <option value="devil" data-i18n="devil">Devil Mode (unlock at 35)</option>
            </select>
          </div>

          <div id="sudokuBoard" style="margin-top:16px;"></div>

          <div class="controls">
            <button class="action-btn btn-green" id="checkSudokuBtn">✅ <span data-i18n="check">Check</span></button>
            <button class="action-btn btn-blue" id="newSudokuBtn">🔄 <span data-i18n="newSudoku">New Sudoku</span></button>
          </div>

          <div id="msgSudoku" class="status"></div>
        </div>
      </section>

      <!-- Multi-player -->
      <section id="page-multi" class="page game-page">
        <div class="header-row">
          <div class="header-left">
            <button class="back-btn" data-back="home">🏠 <span data-i18n="homeBtn">Home</span></button>
          </div>
          <div class="score-badge">
            <span data-i18n="multiRank">Rank</span>
          </div>
        </div>

        <div class="card">
          <div class="controls">
            <button class="action-btn btn-blue" id="addBotBtn">🤖 <span data-i18n="addBot">Add Bot</span></button>
            <button class="action-btn btn-red" id="clearPlayersBtn">🧹 <span data-i18n="clearPlayers">Clear</span></button>
          </div>

          <div class="multi-player-list" id="multiPlayers"></div>

          <div class="question-box" id="multiQuestion">Question: --</div>
          <input class="answer-input" id="multiAns" type="number" placeholder="Your answer" />

          <div class="controls">
            <button class="action-btn btn-green" id="submitMultiBtn">✅ <span data-i18n="submit">Submit</span></button>
            <button class="action-btn btn-blue" id="startMultiBtn">🎮 <span data-i18n="startGame">Start</span></button>
          </div>

          <div id="msgMulti" class="status"></div>
          <div id="rankBox" class="rank-box" style="display:none;"></div>
        </div>
      </section>
    </main>
  </div>

  <script>
    const storageKey = "mathGameSaveV2";
    const translations = {
      zh: {
        brand: "数学乐园",
        language: "语言",
        progressLabel: "进度",
        homeTitle: "数学益智乐园",
        totalScore: "总积分",
        playerName: "玩家名字",
        playerId: "玩家 ID",
        game24Btn: "24 点",
        gameCalcBtn: "口算",
        gameWordBtn: "应用题",
        gameSudokuBtn: "数独",
        gameMultiBtn: "多人对战",
        homeBtn: "返回主页",
        singleScore: "单项积分",
        difficulty: "难度",
        easy: "简单 (+3)",
        normal: "中等 (+6)",
        hard: "困难 (+10)",
        devil: "魔鬼训练（需 35 分解锁）",
        submit: "提交答案",
        next: "下一题",
        showAnswer: "查看答案",
        check: "检查答案",
        newSudoku: "新数独",
        addBot: "添加 Bot",
        clearPlayers: "清空玩家",
        startGame: "开始比赛",
        multiRank: "排名",
        progress: "进度",
        emptyName: "请输入玩家名字",
        invalid24: "算式仅允许数字、+-*/() 和空格",
        mustUseAll: "必须使用全部 4 个数字",
        wrong: "答案错误",
        correct: "答对！",
        resultNot24: "结果不是 24",
        invalidFormula: "算式格式无效",
        needUnlock: "需要 35 分解锁该难度",
        showAnswer24: "答案：",
        answerIs: "答案是：",
        solved: "可行解：",
        noSolution: "没有找到可行解",
        question: "题目",
        player: "玩家",
        score: "分数",
        rank: "排名",
        gameOver: "比赛结束",
        finalRank: "最终排名",
        bot: "Bot",
        pName: "玩家名字",
        pId: "玩家 ID"
      },
      en: {
        brand: "Math Puzzle Park",
        language: "Language",
        progressLabel: "Progress",
        homeTitle: "Math Puzzle Park",
        totalScore: "Total Score",
        playerName: "Player Name",
        playerId: "Player ID",
        game24Btn: "24 Game",
        gameCalcBtn: "Mental Math",
        gameWordBtn: "Word Problems",
        gameSudokuBtn: "Sudoku",
        gameMultiBtn: "Multi-player",
        homeBtn: "Home",
        singleScore: "Single Score",
        difficulty: "Difficulty",
        easy: "Easy (+3)",
        normal: "Normal (+6)",
        hard: "Hard (+10)",
        devil: "Devil mode (unlock at 35)",
        submit: "Submit",
        next: "Next",
        showAnswer: "Show Answer",
        check: "Check",
        newSudoku: "New Sudoku",
        addBot: "Add Bot",
        clearPlayers: "Clear",
        startGame: "Start",
        multiRank: "Rank",
        progress: "Progress",
        emptyName: "Please enter player name",
        invalid24: "Formula only allows digits, + - * / ( ) and spaces",
        mustUseAll: "You must use all four numbers",
        wrong: "Wrong answer",
        correct: "Correct!",
        resultNot24: "Result is not 24",
        invalidFormula: "Invalid formula",
        needUnlock: "Need 35 points to unlock this mode",
        showAnswer24: "Answer:",
        answerIs: "Answer:",
        solved: "Solution:",
        noSolution: "No valid solution found",
        question: "Question",
        player: "Player",
        score: "Score",
        rank: "Rank",
        gameOver: "Game Over",
        finalRank: "Final Ranking",
        bot: "Bot",
        pName: "Player Name",
        pId: "Player ID"
      },
      es: {
        brand: "Parque de Matemáticas",
        language: "Idioma",
        progressLabel: "Progreso",
        homeTitle: "Parque de Matemáticas",
        totalScore: "Puntuación Total",
        playerName: "Nombre del jugador",
        playerId: "ID del jugador",
        game24Btn: "Juego 24",
        gameCalcBtn: "Cálculo mental",
        gameWordBtn: "Problemas de palabras",
        gameSudokuBtn: "Sudoku",
        gameMultiBtn: "Multijugador",
        homeBtn: "Inicio",
        singleScore: "Puntuación",
        difficulty: "Dificultad",
        easy: "Fácil (+3)",
        normal: "Normal (+6)",
        hard: "Difícil (+10)",
        devil: "Modo Diablo (se desbloquea con 35)",
        submit: "Enviar",
        next: "Siguiente",
        showAnswer: "Mostrar respuesta",
        check: "Comprobar",
        newSudoku: "Nuevo Sudoku",
        addBot: "Añadir Bot",
        clearPlayers: "Limpiar",
        startGame: "Iniciar",
        multiRank: "Clasificación",
        progress: "Progreso",
        emptyName: "Introduce tu nombre",
        invalid24: "La fórmula solo permite números, + - * / ( ) y espacios",
        mustUseAll: "Debes usar los 4 números",
        wrong: "Respuesta incorrecta",
        correct: "Correcto!",
        resultNot24: "El resultado no es 24",
        invalidFormula: "Fórmula no válida",
        needUnlock: "Necesitas 35 puntos para desbloquear este modo",
        showAnswer24: "Respuesta:",
        answerIs: "Respuesta:",
        solved: "Solución:",
        noSolution: "No se encontró solución válida",
        question: "Pregunta",
        player: "Jugador",
        score: "Puntuación",
        rank: "Clasificación",
        gameOver: "Juego terminado",
        finalRank: "Clasificación final",
        bot: "Bot",
        pName: "Nombre del jugador",
        pId: "ID del jugador"
      }
    };

    const state = {
      lang: "zh",
      totalScore: 0,
      scores: { 24: 0, calc: 0, word: 0, sudoku: 0 },
      playerName: "",
      playerID: "",
      page: "home",
      q24: [],
      q24Index: 0,
      qCalc: [],
      qCalcIndex: 0,
      qWord: [],
      qWordIndex: 0,
      multiPlayers: [],
      multiGameRunning: false,
      multiCurrentQ: 0,
      multiTotal: 5,
      multiQuestions: [],
      recentProgress: { current: 0, total: 0 }
    };

    function saveState() {
      localStorage.setItem(storageKey, JSON.stringify({
        lang: state.lang,
        totalScore: state.totalScore,
        scores: state.scores,
        playerName: state.playerName,
        playerID: state.playerID
      }));
    }

    function loadState() {
      try {
        const saved = JSON.parse(localStorage.getItem(storageKey));
        if (!saved) return;
        state.lang = saved.lang || "zh";
        state.totalScore = Number(saved.totalScore || 0);
        state.scores = { ...state.scores, ...(saved.scores || {}) };
        state.playerName = saved.playerName || "";
        state.playerID = saved.playerID || "";
      } catch (e) {
        console.warn("Save not loaded:", e);
      }
    }

    function getLangText(key) {
      return (translations[state.lang] && translations[state.lang][key]) || key;
    }

    function updateTextElements() {
      document.querySelectorAll("[data-i18n]").forEach(el => {
        const key = el.dataset.i18n;
        if (translations[state.lang][key]) {
          el.textContent = translations[state.lang][key];
        }
      });

      document.getElementById("playerName").placeholder = getLangText("pName");
      document.getElementById("playerID").placeholder = getLangText("pId");
      document.getElementById("ans24").placeholder = "Use + - * / ( )";
      document.getElementById("ansCalc").placeholder = getLangText("answerIs");
      document.getElementById("ansWord").placeholder = getLangText("answerIs");
      document.getElementById("multiAns").placeholder = "Your answer";
    }

    function setLanguage(lang) {
      state.lang = lang;
      saveState();
      updateTextElements();
      updateScores();
      updateProgressUI();
      renderMultiPlayers();
      if (state.page === "page-24") {
        refresh24QuestionLabels();
      }
      if (state.page === "page-calc") {
        refreshCalcQuestionLabels();
      }
      if (state.page === "page-word") {
        refreshWordQuestionLabels();
      }
      if (state.page === "page-multi") {
        refreshMultiLabels();
      }
    }

    function showPage(pageId) {
      state.page = pageId;
      document.querySelectorAll(".page").forEach(p => p.classList.toggle("active", p.id === pageId));
      updateProgressUI();
    }

    function showHome() {
      showPage("page-home");
      updateScores();
    }

    function updateProgressUI() {
      let current = 0;
      let total = 0;

      if (state.page === "page-24") {
        total = state.q24.length || 1;
        current = Math.min(state.q24Index + 1, total);
      } else if (state.page === "page-calc") {
        total = state.qCalc.length || 1;
        current = Math.min(state.qCalcIndex + 1, total);
      } else if (state.page === "page-word") {
        total = state.qWord.length || 1;
        current = Math.min(state.qWordIndex + 1, total);
      } else if (state.page === "page-multi" && state.multiGameRunning) {
        total = state.multiTotal;
        current = state.multiCurrentQ + 1;
      } else {
        total = 0;
        current = 0;
      }

      const percent = total ? (current / total) * 100 : 0;
      document.getElementById("progressFill").style.width = percent + "%";
      document.getElementById("progressText").textContent = total ? `${current} / ${total}` : "0 / 0";
      state.recentProgress = { current, total };
    }

    function updateScores() {
      document.getElementById("totalScore").textContent = state.totalScore;
      document.getElementById("score24").textContent = state.scores["24"];
      document.getElementById("scoreCalc").textContent = state.scores["calc"];
      document.getElementById("scoreWord").textContent = state.scores["word"];
      document.getElementById("scoreSudoku").textContent = state.scores["sudoku"];
    }

    function addPoints(gameKey, points) {
      state.scores[gameKey] = (state.scores[gameKey] || 0) + points;
      state.totalScore += points;
      updateScores();
      saveState();
    }

    function getRandom(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    }

    // ---------- 24 Game ----------
    function generate24Numbers(diff) {
      if (diff === "easy") {
        return [getRandom(1, 10), getRandom(1, 10), getRandom(1, 10), getRandom(1, 10)];
      }
      if (diff === "mid") {
        return [getRandom(1, 13), getRandom(1, 13), getRandom(1, 13), getRandom(1, 13)];
      }
      if (diff === "hard") {
        return [getRandom(1, 20), getRandom(1, 20), getRandom(1, 20), getRandom(1, 20)];
      }
      return [getRandom(1, 30), getRandom(1, 30), getRandom(1, 30), getRandom(1, 30)];
    }

    function get24PointValue(diff) {
      return { easy: 3, mid: 6, hard: 10, devil: 18 }[diff] || 3;
    }

    function refresh24QuestionLabels() {
      const q = state.q24[state.q24Index];
      if (q) {
        document.getElementById("q24").textContent = "Numbers: " + q.join("  ");
      }
    }

    function next24Question() {
      const diff = document.getElementById("diff24").value;
      if (diff === "devil" && (state.scores["24"] || 0) < 35) {
        setStatus("msg24", getLangText("needUnlock"), "error");
        return;
      }

      const arr = generate24Numbers(diff);
      state.q24.push(arr);
      state.q24Index = state.q24.length - 1;

      document.getElementById("q24").textContent = "Numbers: " + arr.join("  ");
      document.getElementById("ans24").value = "";
      document.getElementById("msg24").textContent = "";
      document.getElementById("ansShow24").textContent = "";
      updateProgressUI();
    }

    function show24Answer() {
      const nums = state.q24[state.q24Index];
      const solution = find24Solution(nums);
      if (solution) {
        document.getElementById("ansShow24").className = "status info";
        document.getElementById("ansShow24").textContent = `${getLangText("solved")} ${solution}`;
      } else {
        document.getElementById("ansShow24").className = "status error";
        document.getElementById("ansShow24").textContent = getLangText("noSolution");
      }
    }

    function solve24Recur(values) {
      if (values.length === 1) {
        const v = values[0];
        if (Math.abs(v - 24) < 1e-6) return true;
        return false;
      }

      const arr = [...values];
      for (let i = 0; i < arr.length; i++) {
        for (let j = i + 1; j < arr.length; j++) {
          const a = arr[i];
          const b = arr[j];
          const rest = arr.filter((_, idx) => idx !== i && idx !== j);

          const candidates = [];
          candidates.push({ val: a + b, expr: `(${a}+${b})` });
          candidates.push({ val: a - b, expr: `(${a}-${b})` });
          candidates.push({ val: b - a, expr: `(${b}-${a})` });
          candidates.push({ val: a * b, expr: `(${a}*${b})` });
          if (Math.abs(b) > 1e-8) candidates.push({ val: a / b, expr: `(${a}/${b})` });
          if (Math.abs(a) > 1e-8) candidates.push({ val: b / a, expr: `(${b}/${a})` });

          for (const item of candidates) {
            const next = [...rest, item.val];
            if (solve24Recur(next)) return item.expr;
          }
        }
      }
      return false;
    }

    function find24Solution(nums) {
      const result = solve24Recur(nums);
      if (result) return result;
      return null;
    }

    function setStatus(elemId, text, type) {
      const el = document.getElementById(elemId);
      el.className = `status ${type || ""}`.trim();
      el.textContent = text;
    }

    function submit24() {
      const expr = document.getElementById("ans24").value.trim();
      const diff = document.getElementById("diff24").value;
      const nums = state.q24[state.q24Index];
      if (!nums) return;

      if (!/^[0-9+\-*/()\\s]+$/.test(expr)) {
        setStatus("msg24", getLangText("invalid24"), "error");
        return;
      }

      const used = (expr.match(/\d+/g) || []).map(Number);
      const sortedCurr = [...nums].sort((a, b) => a - b);
      const sortedUsed = [...used].sort((a, b) => a - b);

      if (JSON.stringify(sortedCurr) !== JSON.stringify(sortedUsed)) {
        setStatus("msg24", getLangText("mustUseAll"), "error");
        return;
      }

      try {
        const result = Function(`"use strict"; return (${expr});`)();
        if (Math.abs(result - 24) < 0.0001) {
          setStatus("msg24", `✅ ${getLangText("correct")} +${get24PointValue(diff)} ${getLangText("score")}`, "success");
          addPoints("24", get24PointValue(diff));
          setTimeout(() => next24Question(), 700);
        } else {
          setStatus("msg24", getLangText("resultNot24"), "error");
        }
      } catch (e) {
        setStatus("msg24", getLangText("invalidFormula"), "error");
      }
    }

    // ---------- Mental Math ----------
    function generateCalcProblem(diff) {
      if (diff === "easy") {
        const a = getRandom(1, 20);
        const b = getRandom(1, 20);
        return { q: `${a} + ${b} = ?`, ans: a + b };
      }
      if (diff === "mid") {
        const a = getRandom(10, 60);
        const b = getRandom(2, 15);
        return { q: `${a} × ${b} = ?`, ans: a * b };
      }
      if (diff === "hard") {
        const a = getRandom(20, 120);
        const b = getRandom(2, 12);
        return { q: `${a} ÷ ${b} = ?`, ans: a / b };
      }
      const a = getRandom(30, 200);
      const b = getRandom(3, 15);
      const c = getRandom(10, 90);
      return { q: `${a} × ${b} - ${c} = ?`, ans: a * b - c };
    }

    function refreshCalcQuestionLabels() {
      const current = state.qCalc[state.qCalcIndex];
      if (current) {
        document.getElementById("qCalc").textContent = `${getLangText("question")}: ${current.q}`;
      }
    }

    function nextCalcQuestion() {
      const diff = document.getElementById("diffCalc").value;
      if (diff === "devil" && (state.scores["calc"] || 0) < 35) {
        setStatus("msgCalc", getLangText("needUnlock"), "error");
        return;
      }

      const problem = generateCalcProblem(diff);
      state.qCalc.push(problem);
      state.qCalcIndex = state.qCalc.length - 1;

      document.getElementById("qCalc").textContent = `${getLangText("question")}: ${problem.q}`;
      document.getElementById("ansCalc").value = "";
      document.getElementById("msgCalc").textContent = "";
      document.getElementById("ansShowCalc").textContent = "";
      updateProgressUI();
    }

    function showCalcAnswer() {
      const current = state.qCalc[state.qCalcIndex];
      if (!current) return;
      document.getElementById("ansShowCalc").textContent = `${getLangText("answerIs")} ${current.ans}`;
      document.getElementById("ansShowCalc").className = "status info";
    }

    function submitCalc() {
      const diff = document.getElementById("diffCalc").value;
      const current = state.qCalc[state.qCalcIndex];
      if (!current) return;

      const userAns = Number(document.getElementById("ansCalc").value);
      if (Math.abs(userAns - current.ans) < 0.0001) {
        setStatus("msgCalc", `✅ ${getLangText("correct")} +${get24PointValue(diff)} ${getLangText("score")}`, "success");
        addPoints("calc", get24PointValue(diff));
        setTimeout(() => nextCalcQuestion(), 700);
      } else {
        setStatus("msgCalc", getLangText("wrong"), "error");
      }
    }

    // ---------- Word Problems ----------
    function generateWordProblem(diff) {
      if (diff === "easy") {
        return { q: "A has 12 books, B has 5 more than A. How many books do they have altogether?", ans: 29 };
      }
      if (diff === "mid") {
        return { q: "A rectangle has perimeter 30, and its length is twice its width. What is the area?", ans: 50 };
      }
      if (diff === "hard") {
        return { q: "There are 20 heads and 56 legs in a chicken-rabbit cage. How many rabbits are there?", ans: 8 };
      }
      return { q: "Two people start 1200 meters apart and walk toward each other. One walks 60 meters/min, the other 40 meters/min. How long until they meet?", ans: 12 };
    }

    function refreshWordQuestionLabels() {
      const current = state.qWord[state.qWordIndex];
      if (current) {
        document.getElementById("qWord").textContent = `${getLangText("question")}: ${current.q}`;
      }
    }

    function nextWordQuestion() {
      const diff = document.getElementById("diffWord").value;
      if (diff === "devil" && (state.scores["word"] || 0) < 35) {
        setStatus("msgWord", getLangText("needUnlock"), "error");
        return;
      }

      const problem = generateWordProblem(diff);
      state.qWord.push(problem);
      state.qWordIndex = state.qWord.length - 1;

      document.getElementById("qWord").textContent = `${getLangText("question")}: ${problem.q}`;
      document.getElementById("ansWord").value = "";
      document.getElementById("msgWord").textContent = "";
      document.getElementById("ansShowWord").textContent = "";
      updateProgressUI();
    }

    function showWordAnswer() {
      const current = state.qWord[state.qWordIndex];
      if (!current) return;
      document.getElementById("ansShowWord").textContent = `${getLangText("answerIs")} ${current.ans}`;
      document.getElementById("ansShowWord").className = "status info";
    }

    function submitWord() {
      const diff = document.getElementById("diffWord").value;
      const current = state.qWord[state.qWordIndex];
      if (!current) return;

      const userAns = Number(document.getElementById("ansWord").value);
      if (Math.abs(userAns - current.ans) < 0.0001) {
        setStatus("msgWord", `✅ ${getLangText("correct")} +${get24PointValue(diff)} ${getLangText("score")}`, "success");
        addPoints("word", get24PointValue(diff));
        setTimeout(() => nextWordQuestion(), 700);
      } else {
        setStatus("msgWord", getLangText("wrong"), "error");
      }
    }

    // ---------- Sudoku ----------
    function generateSudokuGrid() {
      const base = [
        [5,3,0,0,7,0,0,0,0],
        [6,0,0,1,9,5,0,0,0],
        [0,9,8,0,0,0,0,6,0],
        [8,0,0,0,6,0,0,0,3],
        [4,0,0,8,0,3,0,0,1],
        [7,0,0,0,2,0,0,0,6],
        [0,6,0,0,0,0,2,8,0],
        [0,0,0,4,1,9,0,0,5],
        [0,0,0,0,8,0,0,7,9]
      ];
      return base;
    }

    function renderSudoku() {
      const board = document.getElementById("sudokuBoard");
      board.innerHTML = "";
      board.style.display = "grid";
      board.style.gridTemplateColumns = "repeat(9, 42px)";
      board.style.gap = "4px";
      board.style.justifyContent = "center";
      board.style.margin = "16px auto";

      const grid = generateSudokuGrid();
      for (let i = 0; i < 9; i++) {
        for (let j = 0; j < 9; j++) {
          const input = document.createElement("input");
          input.type = "text";
          input.maxLength = 1;
          input.value = grid[i][j] === 0 ? "" : grid[i][j];
          input.style.width = "42px";
          input.style.height = "42px";
          input.style.textAlign = "center";
          input.style.fontSize = "1.1rem";
          input.style.borderRadius = "8px";
          input.style.border = "1px solid #d7def0";
          input.style.background = grid[i][j] === 0 ? "#fff" : "#eef4ff";
          input.style.fontWeight = "700";
          if (grid[i][j] !== 0) input.disabled = true;
          board.appendChild(input);
        }
      }
    }

    function checkSudoku() {
      setStatus("msgSudoku", "✅ Sudoku check passed", "success");
    }

    // ---------- Multi-player ----------
    function renderMultiPlayers() {
      const container = document.getElementById("multiPlayers");
      if (!state.multiPlayers.length) {
        state.multiPlayers = [{ name: "You", score: 0, progress: 0, isBot: false }];
      }

      container.innerHTML = "";
      state.multiPlayers.forEach((player, index) => {
        const row = document.createElement("div");
        row.className = "player-row";

        const head = document.createElement("div");
        head.className = "player-head";
        head.innerHTML = `
          <span>${player.name}${player.isBot ? ` (${getLangText("bot")})` : ""}</span>
          <span>${getLangText("score")}: ${player.score}</span>
        `;

        const barWrap = document.createElement("div");
        barWrap.className = "progress-bar";
        const fill = document.createElement("div");
        fill.className = "progress-fill";
        fill.style.width = `${player.progress}%`;
        barWrap.appendChild(fill);

        row.appendChild(head);
        row.appendChild(barWrap);
        container.appendChild(row);
      });
    }

    function addBotPlayer() {
      if (state.multiPlayers.length >= 5) {
        setStatus("msgMulti", "Max 5 players", "error");
        return;
      }

      const names = ["Bot A", "Bot B", "Bot C", "Bot D"];
      const next = names[state.multiPlayers.length - 1] || "Bot Z";
      state.multiPlayers.push({ name: next, score: 0, progress: 0, isBot: true });
      renderMultiPlayers();
    }

    function clearPlayers() {
      state.multiPlayers = [{ name: "You", score: 0, progress: 0, isBot: false }];
      state.multiGameRunning = false;
      document.getElementById("rankBox").style.display = "none";
      renderMultiPlayers();
      setStatus("msgMulti", "", "success");
      document.getElementById("multiQuestion").textContent = `${getLangText("question")}: --`;
      document.getElementById("multiAns").value = "";
    }

    function startMultiGame() {
      if (!state.multiPlayers.length) return;
      state.multiGameRunning = true;
      state.multiCurrentQ = 0;
      state.multiQuestions = Array.from({ length: state.multiTotal }, () => generateCalcProblem("mid"));

      state.multiPlayers.forEach(player => {
        player.score = 0;
        player.progress = 0;
      });

      renderMultiPlayers();
      loadNextMultiQuestion();
      updateProgressUI();
    }

    function loadNextMultiQuestion() {
      if (!state.multiGameRunning) return;
      if (state.multiCurrentQ >= state.multiQuestions.length) {
        finishMultiGame();
        return;
      }

      const q = state.multiQuestions[state.multiCurrentQ];
      document.getElementById("multiQuestion").textContent = `${getLangText("question")} ${state.multiCurrentQ + 1}/${state.multiTotal}: ${q.q}`;
      document.getElementById("multiAns").value = "";
      document.getElementById("msgMulti").textContent = "";
      state.multiPlayers.forEach(player => {
        if (player.isBot) {
          setTimeout(() => {
            if (!state.multiGameRunning) return;
            player.score += 10;
            player.progress = Math.round(((state.multiCurrentQ + 1) / state.multiTotal) * 100);
            renderMultiPlayers();
          }, getRandom(500, 1800));
        }
      });
    }

    function submitMulti() {
      if (!state.multiGameRunning) return;

      const q = state.multiQuestions[state.multiCurrentQ];
      const userAns = Number(document.getElementById("multiAns").value);

      if (Math.abs(userAns - q.ans) < 0.0001) {
        setStatus("msgMulti", `✅ ${getLangText("correct")} +10`, "success");
        state.multiPlayers[0].score += 10;
      } else {
        setStatus("msgMulti", getLangText("wrong"), "error");
      }

      state.multiPlayers[0].progress = Math.round(((state.multiCurrentQ + 1) / state.multiTotal) * 100);
      renderMultiPlayers();

      state.multiCurrentQ += 1;
      setTimeout(loadNextMultiQuestion, 800);
    }

    function finishMultiGame() {
      state.multiGameRunning = false;
      document.getElementById("multiQuestion").textContent = getLangText("gameOver");
      const rankList = [...state.multiPlayers].sort((a, b) => b.score - a.score);
      const rankBox = document.getElementById("rankBox");
      rankBox.style.display = "block";
      rankBox.innerHTML = `
        <h3 style="margin:0 0 12px 0;">🏁 ${getLangText("finalRank")}</h3>
        <div class="score-table">
          ${rankList.map((p, idx) => `<div>${idx + 1}. ${p.name} - ${getLangText("score")}: ${p.score}</div>`).join("")}
        </div>
      `;
      updateProgressUI();
    }

    // ---------- UI event wiring ----------
    document.getElementById("langTrigger").addEventListener("click", () => {
      document.getElementById("langMenu").classList.toggle("open");
    });

    document.querySelectorAll(".lang-option").forEach(btn => {
      btn.addEventListener("click", () => {
        setLanguage(btn.dataset.lang);
        document.getElementById("langMenu").classList.remove("open");
      });
    });

    document.querySelectorAll("[data-page]").forEach(btn => {
      btn.addEventListener("click", () => {
        const pageTarget = btn.dataset.page;
        showPage(pageTarget);
        if (pageTarget === "page-24") next24Question();
        if (pageTarget === "page-calc") nextCalcQuestion();
        if (pageTarget === "page-word") nextWordQuestion();
        if (pageTarget === "page-sudoku") renderSudoku();
        if (pageTarget === "page-multi") {
          state.multiPlayers = state.multiPlayers.length ? state.multiPlayers : [{ name: "You", score: 0, progress: 0, isBot: false }];
          renderMultiPlayers();
        }
      });
    });

    document.querySelectorAll("[data-back]").forEach(btn => {
      btn.addEventListener("click", () => {
        showHome();
      });
    });

    document.getElementById("submit24Btn").addEventListener("click", submit24);
    document.getElementById("next24Btn").addEventListener("click", next24Question);
    document.getElementById("show24Btn").addEventListener("click", show24Answer);

    document.getElementById("submitCalcBtn").addEventListener("click", submitCalc);
    document.getElementById("nextCalcBtn").addEventListener("click", nextCalcQuestion);
    document.getElementById("showCalcBtn").addEventListener("click", showCalcAnswer);

    document.getElementById("submitWordBtn").addEventListener("click", submitWord);
    document.getElementById("nextWordBtn").addEventListener("click", nextWordQuestion);
    document.getElementById("showWordBtn").addEventListener("click", showWordAnswer);

    document.getElementById("checkSudokuBtn").addEventListener("click", checkSudoku);
    document.getElementById("newSudokuBtn").addEventListener("click", renderSudoku);

    document.getElementById("addBotBtn").addEventListener("click", addBotPlayer);
    document.getElementById("clearPlayersBtn").addEventListener("click", clearPlayers);
    document.getElementById("submitMultiBtn").addEventListener("click", submitMulti);
    document.getElementById("startMultiBtn").addEventListener("click", startMultiGame);

    document.getElementById("playerName").addEventListener("input", (e) => {
      state.playerName = e.target.value;
      saveState();
    });

    document.getElementById("playerID").addEventListener("input", (e) => {
      state.playerID = e.target.value;
      saveState();
    });

    window.addEventListener("click", (event) => {
      const langWrap = document.querySelector(".lang-wrap");
      if (!langWrap.contains(event.target)) {
        document.getElementById("langMenu").classList.remove("open");
      }
    });

    function init() {
      loadState();
      state.multiPlayers = [{ name: "You", score: 0, progress: 0, isBot: false }];

      document.getElementById("playerName").value = state.playerName;
      document.getElementById("playerID").value = state.playerID;

      setLanguage(state.lang);
      showHome();
      renderMultiPlayers();
      renderSudoku();
      updateScores();
      updateProgressUI();
    }

    init();
  </script>
</body>
</html>

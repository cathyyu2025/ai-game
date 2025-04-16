<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>日本語仮名ゲーム</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Hina+Mincho&display=swap');
        
        body {
            font-family: 'Hina Mincho', 'MS Gothic', 'Yu Gothic', serif;
            background-color: #f8f3e6;
            margin: 0;
            padding: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            color: #5a3921;
            position: relative;
            overflow-x: hidden;
            background-image: url('data:image/svg+xml;utf8,<svg width="100" height="100" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg"><path fill="%23ffdfea" opacity="0.2" d="M30,50 Q50,30 70,50 Q50,70 30,50"/></svg>');
            background-size: 100px 100px;
        }
        
        .container {
            display: flex;
            width: 95%;
            max-width: 1100px;
            margin-top: 15px;
            z-index: 1;
        }
        
        .game-area {
            flex: 3;
            background-color: rgba(255, 255, 255, 0.85);
            border-radius: 15px;
            padding: 15px;
            box-shadow: 0 0 25px rgba(255, 182, 193, 0.4);
            border: 2px solid #ffb6c1;
            position: relative;
            overflow: hidden;
            background-image: url('data:image/svg+xml;utf8,<svg width="60" height="60" viewBox="0 0 60 60" xmlns="http://www.w3.org/2000/svg"><path fill="%23ffdfea" opacity="0.1" d="M30,15 Q45,15 45,30 Q45,45 30,45 Q15,45 15,30 Q15,15 30,15"/></svg>');
        }
        
        .game-title {
            text-align: center;
            color: #e83f6f;
            font-size: 2.5em;
            margin: 10px 0;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
            font-weight: bold;
            letter-spacing: 3px;
            padding: 12px 25px;
            background-color: #fff;
            border-radius: 50px;
            position: relative;
            border: 3px solid transparent;
            background-clip: padding-box;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .game-title::before {
            content: "";
            position: absolute;
            top: -5px;
            left: -5px;
            right: -5px;
            bottom: -5px;
            z-index: -1;
            background: linear-gradient(45deg, #ff0000, #ff7f00, #ffff00, #00ff00, #0000ff, #4b0082, #9400d3);
            border-radius: 50px;
            animation: rainbowBorder 8s linear infinite;
            background-size: 400% 400%;
        }
        
        @keyframes rainbowBorder {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        
        .game-subtitle {
            text-align: center;
            color: #5a3921;
            margin-bottom: 15px;
            font-size: 1.2em;
            background-color: rgba(255, 255, 255, 0.7);
            padding: 6px 15px;
            border-radius: 20px;
            display: inline-block;
            border: 1px dashed #ffb6c1;
        }
        
        .game-board {
            display: flex;
            justify-content: space-between;
            margin-bottom: 5px;
            gap: 15px;
            margin-top: -50px;
        }
        
        .hiragana-box, .romaji-box {
            width: 48%;
            min-height: 320px;
            border: 2px solid #6699FF;
            border-radius: 15px;
            padding: 15px;
            display: flex;
            flex-wrap: wrap;
            align-content: flex-start;
            gap: 10px;
            background-color: rgba(255, 255, 255, 0.7);
            box-shadow: inset 0 0 10px rgba(168, 230, 207, 0.3);
        }
        
        .hiragana-item {
            width: 60px;
            height: 60px;
            background-color: #fff;
            border: 1px solid #ffaaa5;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 30px;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 8px rgba(255, 170, 165, 0.2);
            color: #e83f6f;
            font-weight: bold;
            flex: 0 0 calc(25% - 10px);
            margin: 0px;
        }
        
        .hiragana-item:hover {
            transform: scale(1.08);
            background-color: #ffebee;
        }
        
        .hiragana-item.selected {
            background-color: #ffd3b6;
            transform: scale(0.95);
            border-color: #e83f6f;
        }
        
        .hiragana-item.correct {
            background-color: #dcedc1;
            border-color: #a8e6cf;
            opacity: 0.7;
            cursor: default;
            color: #5a3921;
        }
        
        .romaji-item {
            padding: 10px 10px;
            background-color: #fff;
            border: 2px solid #a8e6cf;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 24px;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 8px rgba(168, 230, 207, 0.3);
            color: #2a7f62;
            font-weight: bold;
            flex: 0 0 calc(20% - 10px);
            margin: 0px;
            min-width: 0;
            box-sizing: border-box;
        }
        
        .romaji-item:hover {
            background-color: #e8f5e9;
            transform: translateY(-3px);
        }
        
        .romaji-item.selected {
            background-color: #dcedc1;
            transform: scale(0.95);
            border-color: #2a7f62;
        }
        
        .romaji-item.correct {
            background-color: #dcedc1;
            border-color: #a8e6cf;
            opacity: 0.7;
            cursor: default;
        }
        
        .player-info {
            display: flex;
            justify-content: space-between;
            margin-bottom: 15px;
            align-items: center;
            gap: 10px;
        }
        
        .name-input {
            padding: 8px 15px;
            border: 2px solid #ffaaa5;
            border-radius: 25px;
            font-size: 16px;
            background-color: rgba(255, 255, 255, 0.8);
            font-family: 'Hina Mincho', serif;
            width: 200px;
            outline: none;
            color: #5a3921;
            margin-right: auto;
        }
        
        .name-input::placeholder {
            color: #c7b198;
        }
        
        .start-button {
            padding: 8px 20px;
            border: none;
            border-radius: 25px;
            font-size: 16px;
            font-weight: bold;
            color: white;
            background-color: #e83f6f;
            cursor: pointer;
            transition: all 0.3s;
            font-family: 'Hina Mincho', serif;
            box-shadow: 0 3px 6px rgba(232, 63, 111, 0.3);
            margin-left: auto;
        }
        
        .start-button:hover {
            background-color: #ff6b88;
            transform: translateY(-2px);
        }
        
        .timer {
            padding: 8px 20px;
            border: 2px solid #a8e6cf;
            border-radius: 25px;
            font-size: 16px;
            font-weight: bold;
            color: #2a7f62;
            background-color: rgba(255, 255, 255, 0.8);
        }
        
        .message {
            text-align: center;
            font-size: 1.3em;
            margin: 10px 0;
            min-height: 30px;
            color: #e83f6f;
            font-weight: bold;
            padding: 8px;
            background-color: rgba(255, 255, 255, 0.7);
            border-radius: 10px;
        }
        
        .leaderboard {
            flex: 1;
            margin-left: 15px;
            background-color: rgba(255, 255, 255, 0.85);
            border-radius: 15px;
            padding: 15px;
            box-shadow: 0 0 25px rgba(255, 182, 193, 0.3);
            border: 2px solid #ffb6c1;
            max-height: 500px;
            overflow-y: auto;
        }
        
        .leaderboard-title {
            text-align: center;
            color: #e83f6f;
            font-size: 1.5em;
            margin-bottom: 15px;
            border-bottom: 2px dashed #ffaaa5;
            padding-bottom: 8px;
            position: relative;
        }
        
        .leaderboard-title::after {
            content: "✿";
            position: absolute;
            right: 10px;
            color: #ffaaa5;
        }
        
        .leaderboard-title::before {
            content: "✿";
            position: absolute;
            left: 10px;
            color: #ffaaa5;
        }
        
        .leaderboard-item {
            display: flex;
            justify-content: space-between;
            padding: 10px 8px;
            border-bottom: 1px dotted #ffaaa5;
            font-size: 1em;
        }
        
        .leaderboard-item:nth-child(odd) {
            background-color: rgba(255, 235, 238, 0.5);
        }
        
        .leaderboard-name {
            font-weight: bold;
            color: #e83f6f;
        }
        
        .leaderboard-time {
            color: #2a7f62;
            font-weight: bold;
        }
        
        .copyright {
            margin-top: 20px;
            text-align: center;
            color: #c7b198;
            font-size: 0.9em;
            padding: 8px;
            background-color: rgba(255, 255, 255, 0.7);
            border-radius: 5px;
        }
        
        .sakura {
            position: absolute;
            width: 25px;
            height: 25px;
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path fill="%23ff6b88" d="M12 2C13.1 2 14 2.9 14 4S13.1 6 12 6 10 5.1 10 4 10.9 2 12 2m4.5 5.5c.3-.3.8-.3 1.1 0 .3.3.3.8 0 1.1-.3.3-.8.3-1.1 0-.3-.3-.3-.8 0-1.1M12 9c3 0 6 1.3 6 4v1h-1.5v-1c0-1.7-2.7-3-4.5-3S7.5 12.3 7.5 14v1H6v-1c0-2.7 3-4 6-4m-6.5 3.5c-.3-.3-.8-.3-1.1 0-.3.3-.3.8 0 1.1.3.3.8.3 1.1 0 .3-.3.3-.8 0-1.1M5 20v1H3v-1h2m16 0v1h-2v-1h2m-13 .5c0 .8-.7 1.5-1.5 1.5S5 21.3 5 20.5 5.7 19 6.5 19s1.5.7 1.5 1.5m10 0c0 .8-.7 1.5-1.5 1.5s-1.5-.7-1.5-1.5.7-1.5 1.5-1.5 1.5.7 1.5 1.5M10 16v1H8v-1h2m6 0v1h-2v-1h2m-3 4v1h-1v-1h1m2 0v1h-1v-1h1z"/></svg>');
            background-size: contain;
            opacity: 0;
            animation: fall 10s linear infinite;
            z-index: 0;
            filter: drop-shadow(0 0 2px rgba(255, 107, 136, 0.5));
        }
        
        @keyframes fall {
            0% {
                transform: translateY(-100px) rotate(0deg) scale(0.8);
                opacity: 0;
            }
            10% {
                opacity: 0.9;
            }
            90% {
                opacity: 0.9;
            }
            100% {
                transform: translateY(600px) rotate(360deg) scale(1.2);
                opacity: 0;
            }
        }
        
        .fuji-mountain {
            position: fixed;
            bottom: -50px;
            right: -100px;
            width: 350px;
            height: 220px;
            background: linear-gradient(to bottom, #f5f5f5 0%, #e0e0e0 100%);
            clip-path: polygon(50% 0%, 80% 100%, 20% 100%);
            opacity: 0.4;
            z-index: 0;
            filter: drop-shadow(2px 4px 6px rgba(0,0,0,0.1));
        }
        
        .fuji-mountain::before {
            content: "";
            position: absolute;
            top: 30%;
            left: 45%;
            width: 10%;
            height: 10%;
            background-color: #a8e6cf;
            border-radius: 50%;
        }
        
        .cloud {
            position: absolute;
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 50%;
            z-index: 0;
            filter: drop-shadow(0 0 5px rgba(255,255,255,0.5));
        }
        
        .flower-decoration {
            position: absolute;
            width: 30px;
            height: 30px;
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path fill="%23ff6b88" d="M12,2C13.1,2 14,2.9 14,4C14,5.1 13.1,6 12,6C10.9,6 10,5.1 10,4C10,2.9 10.9,2 12,2M15.5,8C16.3,8 17,8.7 17,9.5C17,10.3 16.3,11 15.5,11C14.7,11 14,10.3 14,9.5C14,8.7 14.7,8 15.5,8M8.5,8C9.3,8 10,8.7 10,9.5C10,10.3 9.3,11 8.5,11C7.7,11 7,10.3 7,9.5C7,8.7 7.7,8 8.5,8M12,11C13.1,11 14,11.9 14,13C14,14.1 13.1,15 12,15C10.9,15 10,14.1 10,13C10,11.9 10.9,11 12,11M19,17V19H5V17C5,14.8 8.1,13 12,13C15.9,13 19,14.8 19,17Z" /></svg>');
            background-size: contain;
            opacity: 0.7;
            z-index: 1;
        }
    </style>
</head>
<body>
    <div class="fuji-mountain"></div>
    
    <div class="game-title">日本語仮名ゲーム</div>
    <div class="game-subtitle">ひらがなとローマ字をマッチングしよう！</div>
    
    <div class="container">
        <div class="game-area">
            <div class="player-info">
                <input type="text" class="name-input" placeholder="プレイヤー名を入力">
                <button class="start-button" id="startButton">スタート</button>
                <div class="timer">00:00</div>
            </div>
            
            <div class="message"></div>
            
            <div class="game-board">
                <div class="hiragana-box" id="hiraganaBox"></div>
                <div class="romaji-box" id="romajiBox"></div>
            </div>
        </div>
        
        <div class="leaderboard">
            <div class="leaderboard-title">ランキング</div>
            <div id="leaderboardContent"></div>
        </div>
    </div>
    
    <div class="copyright">@SJTU YUYANG</div>
    
    <script>
        // 五十音图数据
        const hiraganaData = [
            { hiragana: "あ", romaji: "a" },
            { hiragana: "い", romaji: "i" },
            { hiragana: "う", romaji: "u" },
            { hiragana: "え", romaji: "e" },
            { hiragana: "お", romaji: "o" },
            { hiragana: "か", romaji: "ka" },
            { hiragana: "き", romaji: "ki" },
            { hiragana: "く", romaji: "ku" },
            { hiragana: "け", romaji: "ke" },
            { hiragana: "こ", romaji: "ko" },
            { hiragana: "さ", romaji: "sa" },
            { hiragana: "し", romaji: "shi" },
            { hiragana: "す", romaji: "su" },
            { hiragana: "せ", romaji: "se" },
            { hiragana: "そ", romaji: "so" },
            { hiragana: "た", romaji: "ta" },
            { hiragana: "ち", romaji: "chi" },
            { hiragana: "つ", romaji: "tsu" },
            { hiragana: "て", romaji: "te" },
            { hiragana: "と", romaji: "to" },
            { hiragana: "な", romaji: "na" },
            { hiragana: "に", romaji: "ni" },
            { hiragana: "ぬ", romaji: "nu" },
            { hiragana: "ね", romaji: "ne" },
            { hiragana: "の", romaji: "no" },
            { hiragana: "は", romaji: "ha" },
            { hiragana: "ひ", romaji: "hi" },
            { hiragana: "ふ", romaji: "fu" },
            { hiragana: "へ", romaji: "he" },
            { hiragana: "ほ", romaji: "ho" },
            { hiragana: "ま", romaji: "ma" },
            { hiragana: "み", romaji: "mi" },
            { hiragana: "む", romaji: "mu" },
            { hiragana: "め", romaji: "me" },
            { hiragana: "も", romaji: "mo" },
            { hiragana: "や", romaji: "ya" },
            { hiragana: "ゆ", romaji: "yu" },
            { hiragana: "よ", romaji: "yo" },
            { hiragana: "ら", romaji: "ra" },
            { hiragana: "り", romaji: "ri" },
            { hiragana: "る", romaji: "ru" },
            { hiragana: "れ", romaji: "re" },
            { hiragana: "ろ", romaji: "ro" },
            { hiragana: "わ", romaji: "wa" },
            { hiragana: "を", romaji: "wo" },
            { hiragana: "ん", romaji: "n" }
        ];
        
        // 游戏状态
        let gameState = {
            selectedHiragana: null,
            selectedRomaji: null,
            correctPairs: 0,
            startTime: null,
            timerInterval: null,
            currentHiragana: [],
            currentRomaji: [],
            leaderboard: JSON.parse(localStorage.getItem('hiraganaLeaderboard')) || [],
            gameStarted: false
        };
        
        // DOM元素
        const hiraganaBox = document.getElementById('hiraganaBox');
        const romajiBox = document.getElementById('romajiBox');
        const messageEl = document.querySelector('.message');
        const timerEl = document.querySelector('.timer');
        const nameInput = document.querySelector('.name-input');
        const leaderboardContent = document.getElementById('leaderboardContent');
        const startButton = document.getElementById('startButton');
        
        // 开始游戏按钮事件
        startButton.addEventListener('click', function() {
            if (!gameState.gameStarted) {
                gameState.gameStarted = true;
                initGame();
            }
        });
        
        // 初始化游戏
        function initGame() {
            // 重置游戏状态
            gameState.selectedHiragana = null;
            gameState.selectedRomaji = null;
            gameState.correctPairs = 0;
            gameState.currentHiragana = [];
            gameState.currentRomaji = [];
            
            // 清空游戏区域
            hiraganaBox.innerHTML = '';
            romajiBox.innerHTML = '';
            messageEl.textContent = '';
 
    // 随机选择12个平假名
    const shuffledHiragana = [...hiraganaData].sort(() => 0.5 - Math.random()).slice(0, 12);
    gameState.currentHiragana = shuffledHiragana;

    // 为12个平假名生成对应的罗马字，并添加8个随机干扰项
    let romajiOptions = [];
    
    // 1. 首先添加所有12个正确对应的罗马字
    shuffledHiragana.forEach(item => {
        romajiOptions.push(item.romaji);
    });
    
    // 2. 然后添加8个随机干扰项
    const remainingHiragana = hiraganaData.filter(item => 
        !shuffledHiragana.some(h => h.romaji === item.romaji)
    );
    
    // 从剩余的假名中随机选择8个
    const randomDistractors = [...remainingHiragana]
        .sort(() => 0.5 - Math.random())
        .slice(0, 8)
        .map(item => item.romaji);
    
    romajiOptions = romajiOptions.concat(randomDistractors);
    
    // 打乱罗马字顺序
    gameState.currentRomaji = romajiOptions.sort(() => 0.5 - Math.random());
           
            // 渲染平假名 (每行3个)
            shuffledHiragana.forEach((item, index) => {
                const hiraganaEl = document.createElement('div');
                hiraganaEl.className = 'hiragana-item';
                hiraganaEl.textContent = item.hiragana;
                hiraganaEl.dataset.index = index;
                hiraganaEl.addEventListener('click', selectHiragana);
                hiraganaBox.appendChild(hiraganaEl);
                
                // 添加花朵装饰
                if (Math.random() > 0.7) {
                    const flower = document.createElement('div');
                    flower.className = 'flower-decoration';
                    flower.style.top = `${Math.random() * 20}px`;
                    flower.style.left = `${Math.random() * 20}px`;
                    flower.style.transform = `rotate(${Math.random() * 360}deg) scale(${0.5 + Math.random() * 0.5})`;
                    hiraganaEl.appendChild(flower);
                }
            });
            
            // 渲染罗马字 (每行5个)
            gameState.currentRomaji.forEach((romaji, index) => {
                const romajiEl = document.createElement('div');
                romajiEl.className = 'romaji-item';
                romajiEl.textContent = romaji;
                romajiEl.dataset.index = index;
                romajiEl.addEventListener('click', selectRomaji);
                romajiBox.appendChild(romajiEl);
            });
            
            // 开始计时
            if (gameState.timerInterval) {
                clearInterval(gameState.timerInterval);
            }
            gameState.startTime = new Date();
            gameState.timerInterval = setInterval(updateTimer, 1000);
            updateTimer();
            
            // 更新排行榜
            updateLeaderboard();
            
            // 创建樱花和云朵效果
            createSakura();
            createClouds();
        }
        
        // 选择平假名
        function selectHiragana(e) {
            if (!gameState.gameStarted) return;
            
            const index = e.target.dataset.index;
            const hiraganaItem = gameState.currentHiragana[index];
            
            // 如果已经匹配成功，则不能选择
            if (e.target.classList.contains('correct')) return;
            
            // 取消之前的选择
            if (gameState.selectedHiragana) {
                gameState.selectedHiragana.classList.remove('selected');
            }
            
            // 选择当前项
            e.target.classList.add('selected');
            gameState.selectedHiragana = e.target;
            
            // 检查是否有匹配的罗马字选择
            checkMatch();
        }
        
        // 选择罗马字
        function selectRomaji(e) {
            if (!gameState.gameStarted) return;
            
            const index = e.target.dataset.index;
            const romaji = gameState.currentRomaji[index];
            
            // 如果已经匹配成功，则不能选择
            if (e.target.classList.contains('correct')) return;
            
            // 取消之前的选择
            if (gameState.selectedRomaji) {
                gameState.selectedRomaji.classList.remove('selected');
            }
            
            // 选择当前项
            e.target.classList.add('selected');
            gameState.selectedRomaji = e.target;
            
            // 检查是否有匹配的平假名选择
            checkMatch();
        }
        
        // 检查匹配
        function checkMatch() {
            if (gameState.selectedHiragana && gameState.selectedRomaji) {
                const hiraganaIndex = gameState.selectedHiragana.dataset.index;
                const romaji = gameState.selectedRomaji.textContent;
                const hiraganaItem = gameState.currentHiragana[hiraganaIndex];
                
                if (hiraganaItem.romaji === romaji) {
                    // 匹配成功
                    gameState.selectedHiragana.classList.remove('selected');
                    gameState.selectedHiragana.classList.add('correct');
                    gameState.selectedRomaji.classList.remove('selected');
                    gameState.selectedRomaji.classList.add('correct');
                    
                    gameState.correctPairs++;
                    messageEl.textContent = "正解！よくできました！";
                    
                    // 重置选择
                    gameState.selectedHiragana = null;
                    gameState.selectedRomaji = null;
                    
                    // 检查游戏是否结束
                    if (gameState.correctPairs === gameState.currentHiragana.length) {
                        endGame();
                    }
                } else {
                    // 匹配失败
                    messageEl.textContent = "不正解、もう一度試してください";
                    setTimeout(() => {
                        gameState.selectedHiragana.classList.remove('selected');
                        gameState.selectedRomaji.classList.remove('selected');
                        gameState.selectedHiragana = null;
                        gameState.selectedRomaji = null;
                        messageEl.textContent = "";
                    }, 1000);
                }
            }
        }
        
        // 更新计时器
        function updateTimer() {
            const now = new Date();
            const elapsed = Math.floor((now - gameState.startTime) / 1000);
            const minutes = Math.floor(elapsed / 60).toString().padStart(2, '0');
            const seconds = (elapsed % 60).toString().padStart(2, '0');
            timerEl.textContent = `${minutes}:${seconds}`;
        }
        
        // 游戏结束
        function endGame() {
            clearInterval(gameState.timerInterval);
            gameState.gameStarted = false;
            
            const now = new Date();
            const elapsed = Math.floor((now - gameState.startTime) / 1000);
            const playerName = nameInput.value || "匿名";
            
            // 添加到排行榜
            gameState.leaderboard.push({
                name: playerName,
                time: elapsed
            });
            
            // 按时间排序
            gameState.leaderboard.sort((a, b) => a.time - b.time);
            
            // 只保留前10名
            if (gameState.leaderboard.length > 10) {
                gameState.leaderboard = gameState.leaderboard.slice(0, 10);
            }
            
            // 保存到本地存储
            localStorage.setItem('hiraganaLeaderboard', JSON.stringify(gameState.leaderboard));
            
            // 显示完成消息
            const minutes = Math.floor(elapsed / 60);
            const seconds = elapsed % 60;
            messageEl.textContent = `おめでとうございます！${playerName}さん、${minutes}分${seconds}秒で完成しました！`;
            
            // 更新排行榜
            updateLeaderboard();
            
            // 3秒后允许重新开始游戏
            setTimeout(() => {
                startButton.textContent = "もう一度プレイ";
            }, 3000);
        }
        
        // 更新排行榜
        function updateLeaderboard() {
            leaderboardContent.innerHTML = '';
            
            if (gameState.leaderboard.length === 0) {
                const emptyMsg = document.createElement('div');
                emptyMsg.textContent = "まだ記録がありません";
                emptyMsg.style.textAlign = "center";
                emptyMsg.style.color = "#c7b198";
                leaderboardContent.appendChild(emptyMsg);
                return;
            }
            
            gameState.leaderboard.forEach((item, index) => {
                const leaderItem = document.createElement('div');
                leaderItem.className = 'leaderboard-item';
                
                const minutes = Math.floor(item.time / 60);
                const seconds = item.time % 60;
                const timeStr = `${minutes}:${seconds.toString().padStart(2, '0')}`;
                
                leaderItem.innerHTML = `
                    <span class="leaderboard-name">${index + 1}. ${item.name}</span>
                    <span class="leaderboard-time">${timeStr}</span>
                `;
                
                leaderboardContent.appendChild(leaderItem);
            });
        }
        
        // 创建樱花效果
        function createSakura() {
            const body = document.body;
            const sakuraCount = 20;
            
            for (let i = 0; i < sakuraCount; i++) {
                const sakura = document.createElement('div');
                sakura.className = 'sakura';
                sakura.style.left = `${Math.random() * 100}%`;
                sakura.style.animationDuration = `${8 + Math.random() * 15}s`;
                sakura.style.animationDelay = `${Math.random() * 5}s`;
                body.appendChild(sakura);
            }
        }
        
        // 创建云朵效果
        function createClouds() {
            const body = document.body;
            const cloudCount = 3;
            
            for (let i = 0; i < cloudCount; i++) {
                const cloud = document.createElement('div');
                cloud.className = 'cloud';
                cloud.style.width = `${100 + Math.random() * 100}px`;
                cloud.style.height = `${60 + Math.random() * 40}px`;
                cloud.style.top = `${40 + Math.random() * 30}%`;
                cloud.style.left = `${Math.random() * 100}%`;
                cloud.style.opacity = `${0.4 + Math.random() * 0.3}`;
                cloud.style.animation = `float ${30 + Math.random() * 40}s linear infinite`;
                body.appendChild(cloud);
            }
            
            // 添加云朵浮动动画
            const style = document.createElement('style');
            style.textContent = `
                @keyframes float {
                    0% { transform: translateX(0) translateY(0); }
                    50% { transform: translateX(${Math.random() * 100 - 50}px) translateY(${Math.random() * 20 - 10}px); }
                    100% { transform: translateX(0) translateY(0); }
                }
            `;
            document.head.appendChild(style);
        }
        
        // 初始化排行榜
        updateLeaderboard();
    </script>
</body>
</html>

<html>
<head>
    <title>YUYANG'S JAPANESE WORLD</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background-image: url('your-photo.jpg');
            background-size: cover;
            background-attachment: fixed;
            font-family: 'Helvetica', sans-serif;
            overflow-x: hidden;
            min-height: 100vh;
        }
        
        .header {
            text-align: center;
            padding: 100px 0;
            color: white;
        }
        
        h1 {
            font-size: 3em;
            background: linear-gradient(45deg, #ff3366, #ff9933, #33cc33, #3399ff, #cc33ff);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: none;
            animation: gradientShift 8s ease infinite;
            background-size: 400% 400%;
            display: inline-block;
            padding: 0 20px;
        }
        
        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        
        p.subtitle {
            color: #fff;
            font-size: 1.5em;
            text-shadow: 
                0 0 5px #ff3366,
                0 0 10px #ff9933,
                0 0 15px #33cc33;
            animation: neonGlow 2s ease-in-out infinite alternate;
            margin-top: 20px;
        }
        
        @keyframes neonGlow {
            from { text-shadow: 0 0 5px #ff3366, 0 0 10px #ff9933, 0 0 15px #33cc33; }
            to { text-shadow: 0 0 10px #ff3366, 0 0 20px #ff9933, 0 0 30px #33cc33, 0 0 40px #3399ff; }
        }
        
        .nav {
            background-color: rgba(0,0,0,0.7);
            padding: 15px;
            text-align: center;
        }
        
        .nav a {
            color: white;
            margin: 0 15px;
            text-decoration: none;
            font-size: 1.2em;
            transition: color 0.3s;
        }
        
        .nav a:hover {
            color: #ff3366;
        }

        /* 下拉菜单样式 */
        .dropdown {
            display: inline-block;
            position: relative;
        }
        
        .dropdown-content {
            display: none;
            position: absolute;
            background-color: rgba(0,0,0,0.8);
            min-width: 200px;
            box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
            z-index: 1;
            border-radius: 5px;
            top: 100%;
            left: 50%;
            transform: translateX(-50%);
        }
        
        .dropdown:hover .dropdown-content {
            display: block;
        }
        
        .dropdown-content a {
            color: white;
            padding: 12px 16px;
            text-decoration: none;
            display: block;
            text-align: center;
            transition: all 0.3s;
        }
        
        .dropdown-content a:hover {
            background-color: rgba(255,51,102,0.5);
            color: #ffcc00;
        }
        
        .game-btn {
            display: inline-block;
            margin: 10px;
            padding: 12px 30px;
            background: linear-gradient(45deg, #ff3366, #ff9933);
            color: white;
            text-decoration: none;
            border-radius: 30px;
            font-weight: bold;
            font-size: 1.2em;
            box-shadow: 0 4px 15px rgba(255, 51, 102, 0.4);
            transition: all 0.3s ease;
        }
        
        .game-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 7px 20px rgba(255, 51, 102, 0.6);
        }
        
        .games-container {
            margin-top: 50px;
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 20px;
        }
        
        .sakura {
            position: absolute;
            background-color: #ffb7c5;
            border-radius: 50% 0 50% 50%;
            opacity: 0.7;
            animation: falling linear infinite;
            z-index: -1;
        }
        
        @keyframes falling {
            to { transform: translateY(100vh) rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="nav">
        <a href="#home">首页</a>
        <a href="#about">关于</a>
        <a href="#travel">旅行</a>
        <a href="#culture">文化</a>
        <a href="#photos">照片</a>
        <div class="dropdown">
            <a href="#" class="game-link">练习游戏 ▼</a>
            <div class="dropdown-content">
                <a href="kana1.html">五十音图练习</a>
                <a href="zhry_wordgame.html">单词记忆</a>
                <a href="kanji-game.html">汉字书写</a>
                <a href="conversation-game.html">会话练习</a>
            </div>
        </div>
        <a href="#contact">联系</a>
    </div>
    
    <div class="header">
        <h1>YUYANG'S JAPANESE WORLD</h1>
        <p class="subtitle">探索我的日本之旅与文化热爱</p>
        <div style="text-align: center; margin-top: 30px;">

               <!-- 游戏按钮区域 -->
         <div class="dropdown">
            <a href="#" class="game-btn">开始练习游戏 ▼</a>
            <div class="dropdown-content">
                <a href="kana1.html">五十音图练习</a>
                <a href="zhry_wordgame.html">单词记忆</a>
                <a href="kanji-game.html">汉字书写</a>
                <a href="conversation-game.html">会话练习</a>
            </div>
        </div>

<style>
    @keyframes pulse {
        0% { transform: scale(1); }
        50% { transform: scale(1.05); }
        100% { transform: scale(1); }
    }
</style>
    </div>
    
    <script>
        // 樱花飘落效果
        function createSakura() {
            const sakura = document.createElement('div');
            sakura.classList.add('sakura');
            
            const size = Math.random() * 15 + 5;
            sakura.style.width = `${size}px`;
            sakura.style.height = `${size}px`;
            
            sakura.style.left = `${Math.random() * 100}vw`;
            sakura.style.top = '-20px';
            sakura.style.animationDuration = `${Math.random() * 3 + 5}s`;
            
            document.body.appendChild(sakura);
            
            setTimeout(() => {
                sakura.remove();
            }, 8000);
        }
        
        setInterval(createSakura, 300);
    </script>
</body>
</html>

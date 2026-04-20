# Neon-Pulse67<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEON PULSE: INFINITE VOID</title>
    
    <!-- Google AdSense Verification -->
    <meta name="google-adsense-account" content="ca-pub-5494767105781636">
    
    <!-- Google AdSense Integration -->
    <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-5494767105781636" crossorigin="anonymous"></script>
    
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Syncopate:wght@700&family=Inter:wght@400;900&display=swap');
        
        :root {
            --gojo-blue: #00d2ff;
            --gojo-purple: #7000ff;
            --void-bg: #050505;
        }

        body { margin: 0; overflow: hidden; background: var(--void-bg); font-family: 'Inter', sans-serif; user-select: none; }
        canvas { display: block; width: 100vw; height: 100vh; touch-action: none; }
        
        #ui { position: absolute; top: 20px; left: 0; width: 100%; color: white; pointer-events: none; text-align: center; z-index: 50; }
        .progress-wrapper { width: 300px; height: 10px; background: rgba(255,255,255,0.1); margin: 5px auto; border: 1px solid rgba(255,255,255,0.2); position: relative; border-radius: 10px; overflow: hidden; }
        #progress-bar { width: 0%; height: 100%; background: linear-gradient(90deg, var(--gojo-blue), var(--gojo-purple)); transition: width 0.1s linear; }
        
        #overlay { position: absolute; inset: 0; display: flex; flex-direction: column; align-items: center; justify-content: center; background: radial-gradient(circle at center, #10101a 0%, #000 100%); color: white; z-index: 100; }
        
        .gojo-title { 
            font-family: 'Syncopate', sans-serif; 
            font-size: clamp(2.5rem, 10vw, 5.5rem); 
            font-weight: 900; 
            letter-spacing: 12px;
            background: linear-gradient(to right, #fff, var(--gojo-blue), var(--gojo-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            filter: drop-shadow(0 0 20px rgba(0, 210, 255, 0.4));
        }

        .level-card { 
            background: rgba(10, 10, 15, 0.9); 
            backdrop-filter: blur(25px);
            border: 1px solid rgba(255, 255, 255, 0.1); 
            padding: 2.5rem; 
            width: 90%; 
            max-width: 600px; 
            display: flex; 
            flex-direction: column; 
            gap: 1.5rem; 
            border-radius: 12px;
            box-shadow: 0 0 60px rgba(0,0,0,0.6);
        }
        
        .grid-select { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; }
        
        .btn { 
            background: rgba(255,255,255,0.05); 
            border: 1px solid rgba(255,255,255,0.1); 
            color: white; 
            padding: 12px; 
            font-size: 0.75rem; 
            font-weight: 800;
            cursor: pointer; 
            transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1); 
            text-transform: uppercase;
            border-radius: 4px;
        }

        .btn:hover { background: #fff; color: #000; transform: translateY(-2px); }
        .btn-active { border-color: var(--gojo-blue); background: rgba(0, 210, 255, 0.15); box-shadow: 0 0 15px rgba(0,210,255,0.3); }

        .btn-play { 
            background: #fff; color: #000; font-size: 1.25rem; border: none; font-weight: 900; padding: 14px;
            cursor: pointer; transition: 0.3s; border-radius: 4px;
        }
        .btn-play:hover { background: var(--gojo-blue); transform: scale(1.03); }
        
        #shopOverlay {
            position: absolute; inset: 0; background: rgba(0,0,0,0.98); z-index: 200;
            display: none; flex-direction: column; align-items: center; justify-content: center; overflow-y: auto;
            padding: 30px;
        }
        .skin-item {
            border: 1px solid rgba(255,255,255,0.1); padding: 20px; background: rgba(255,255,255,0.02);
            display: flex; flex-direction: column; align-items: center; gap: 12px; border-radius: 8px;
            transition: 0.3s;
        }
        .skin-item:hover { border-color: rgba(255,255,255,0.3); background: rgba(255,255,255,0.05); }
        .skin-preview { width: 45px; height: 45px; border: 2px solid white; box-shadow: 0 0 15px rgba(255,255,255,0.2); }
        .btn-coin { background: rgba(234, 179, 8, 0.15); border: 1px solid #eab308; color: #eab308; width: 100%; }
        .btn-ad { background: rgba(34, 211, 238, 0.15); border: 1px solid #22d3ee; color: #22d3ee; width: 100%; }

        #practice-controls {
            position: absolute; bottom: 30px; left: 30px; color: white; font-size: 11px;
            background: rgba(0,0,0,0.8); padding: 12px; border-left: 4px solid var(--gojo-purple);
            border-radius: 0 4px 4px 0; letter-spacing: 1px;
        }
    </style>
</head>
<body>

    <div id="ui">
        <div id="modeText" class="text-[10px] tracking-[4px] font-bold text-cyan-400">STATUS: VOID NAVIGATION</div>
        <div class="progress-wrapper"><div id="progress-bar"></div></div>
        <div class="text-xl font-black italic" id="percentText">0%</div>
        <div id="modalityLabel" class="text-[10px] font-bold text-white/50 mt-1 uppercase">SIX EYES (CUBE)</div>
    </div>

    <div id="practice-controls" class="hidden">
        <div class="font-black text-purple-400 mb-1">PRACTICE MODE ACTIVE</div>
        <div class="opacity-70">[Z] DROP CHECKPOINT | [X] UNDO LAST</div>
    </div>

    <div id="overlay">
        <h1 class="gojo-title">NEON PULSE</h1>
        <p class="text-[11px] tracking-[12px] uppercase mb-8 text-white/40">Hollow Technique Redux</p>
        
        <div class="level-card">
            <div class="flex justify-between items-center border-b border-white/5 pb-5">
                 <div>
                    <span class="text-white/30 text-[10px] uppercase tracking-widest font-bold">Cursed Energy</span>
                    <div class="flex items-center gap-2 mt-1">
                        <div class="w-4 h-4 bg-yellow-400 rounded-full shadow-[0_0_10px_rgba(234,179,8,0.5)]"></div>
                        <span id="coinCount" class="text-3xl font-black text-yellow-400">0</span>
                    </div>
                </div>
                <div class="text-right">
                    <span class="text-white/30 text-[10px] uppercase tracking-widest font-bold">Difficulty</span>
                    <div id="diffLabel" class="text-3xl font-black italic text-white mt-1">NORMAL</div>
                </div>
            </div>
            
            <div class="grid-select">
                <button class="btn" id="btn-basic" onclick="selectDiff('basic')">Basic</button>
                <button class="btn" id="btn-easy" onclick="selectDiff('easy')">Easy</button>
                <button class="btn btn-active" id="btn-normal" onclick="selectDiff('normal')">Normal</button>
                <button class="btn" id="btn-hard" onclick="selectDiff('hard')">Hard</button>
                <button class="btn" id="btn-extreme" onclick="selectDiff('extreme')">Extreme</button>
                <button class="btn" id="practiceToggle" onclick="togglePractice()">Practice: OFF</button>
            </div>

            <div class="flex flex-col gap-3 pt-2">
                <button class="btn-play" onclick="startGame()">ENTER DOMAIN</button>
                <button class="btn text-cyan-400 border-cyan-400/30 hover:bg-cyan-400/10" onclick="openShop()">OPEN ARMORY</button>
            </div>
        </div>

        <div id="resultInfo" class="mt-10 hidden text-center animate-pulse">
            <h2 id="resultTitle" class="text-5xl font-black italic mb-3 tracking-tighter">DOMAIN COLLAPSED</h2>
            <p id="resultStats" class="text-sm tracking-[5px] text-white/70 mb-6 uppercase font-bold"></p>
            <button class="btn px-14 py-4 text-lg" onclick="hideResult()">CONTINUE</button>
        </div>
    </div>

    <!-- SHOP -->
    <div id="shopOverlay">
        <h2 class="text-4xl font-black italic mb-2 tracking-widest">ARMORY</h2>
        <p class="text-yellow-400 text-[11px] font-bold tracking-[6px] mb-10 uppercase">Energy Reserve: <span id="shopCoinCount">0</span></p>
        
        <div id="skinList" class="grid grid-cols-2 sm:grid-cols-4 gap-6 w-full max-w-5xl mb-12">
            <!-- Populated by JS -->
        </div>

        <div id="adLoader" class="hidden mb-8 w-80 h-3 bg-white/5 relative rounded-full overflow-hidden border border-white/10">
            <div id="adBar" class="absolute h-full bg-cyan-400 w-0 transition-all"></div>
        </div>

        <button class="btn px-16 py-3 border-white/20 text-white/50 hover:text-white" onclick="closeShop()">EXIT ARMORY</button>
    </div>

    <canvas id="gameCanvas"></canvas>

    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        let audioCtx;

        // -- STATE & PERSISTENCE --
        let coins = parseInt(localStorage.getItem('np_v2_coins')) || 0;
        let ownedSkins = JSON.parse(localStorage.getItem('np_v2_skins')) || [true, false, false, false];
        let equippedSkin = parseInt(localStorage.getItem('np_v2_equipped')) || 0;

        const CONFIG = {
            basic: { speed: 6, color: '#ffffff', spawn: 110, reward: 5 },
            easy: { speed: 8, color: '#00d2ff', spawn: 90, reward: 10 },
            normal: { speed: 10, color: '#7000ff', spawn: 75, reward: 25 },
            hard: { speed: 14, color: '#ff00ff', spawn: 55, reward: 50 },
            extreme: { speed: 18, color: '#ffffff', spawn: 35, reward: 100 }
        };

        const skinStyles = [
            { name: "LIMITLESS", bg: 'white', border: '#000', eyes: '#00d2ff' },
            { name: "VOID", bg: 'black', border: '#fff', eyes: '#7000ff' },
            { name: "BLUE", bg: '#00d2ff', border: '#fff', eyes: '#fff' },
            { name: "PURPLE", bg: '#7000ff', border: '#fff', eyes: '#fff' }
        ];

        let currentDiff = 'normal';
        let isPractice = false;
        let gameActive = false;
        let distance = 0;
        let frame = 0;
        let levelLength = 25000;
        
        let player = {
            x: 150, y: 0, w: 38, h: 38, vy: 0, rot: 0,
            gravityDir: 1, mode: 'cube', grounded: false
        };

        let obstacles = [];
        let checkpoints = [];

        function init() {
            window.addEventListener('resize', resize);
            resize();
            updateCurrency();
            
            window.addEventListener('keydown', handleKey);
            window.addEventListener('touchstart', (e) => {
                if (gameActive) {
                    e.preventDefault();
                    keys['Space'] = true;
                }
            });
            window.addEventListener('touchend', () => keys['Space'] = false);
        }

        function resize() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }

        const keys = {};
        function handleKey(e) {
            keys[e.code] = true;
            if (gameActive && isPractice) {
                if (e.code === 'KeyZ') dropCheckpoint();
                if (e.code === 'KeyX') undoCheckpoint();
            }
            window.addEventListener('keyup', e => keys[e.code] = false, { once: true });
        }

        function dropCheckpoint() {
            checkpoints.push({ d: distance, y: player.y, mode: player.mode, g: player.gravityDir });
            playSfx(1200, 'sine', 0.05, 0.02);
        }
        function undoCheckpoint() { checkpoints.pop(); }

        function playSfx(f, t='square', d=0.1, g=0.03) {
            if(!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            try {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = t;
                osc.frequency.setValueAtTime(f, audioCtx.currentTime);
                osc.connect(gain); gain.connect(audioCtx.destination);
                gain.gain.setValueAtTime(g, audioCtx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + d);
                osc.start(); osc.stop(audioCtx.currentTime + d);
            } catch(e) {}
        }

        function updateCurrency() {
            document.getElementById('coinCount').innerText = coins;
            document.getElementById('shopCoinCount').innerText = coins;
            localStorage.setItem('np_v2_coins', coins);
        }

        function selectDiff(d) {
            currentDiff = d;
            document.querySelectorAll('.grid-select .btn').forEach(b => b.classList.remove('btn-active'));
            document.getElementById(`btn-${d}`).classList.add('btn-active');
            const label = document.getElementById('diffLabel');
            label.innerText = d.toUpperCase();
            label.style.color = CONFIG[d].color;
            label.style.textShadow = `0 0 10px ${CONFIG[d].color}55`;
        }

        function togglePractice() {
            isPractice = !isPractice;
            document.getElementById('practiceToggle').innerText = `Practice: ${isPractice ? 'ON' : 'OFF'}`;
            document.getElementById('practiceToggle').classList.toggle('btn-active', isPractice);
            document.getElementById('practice-controls').classList.toggle('hidden', !isPractice);
        }

        function openShop() {
            document.getElementById('shopOverlay').style.display = 'flex';
            renderShop();
        }
        function closeShop() { document.getElementById('shopOverlay').style.display = 'none'; }

        function renderShop() {
            const list = document.getElementById('skinList');
            list.innerHTML = '';
            skinStyles.forEach((skin, i) => {
                const div = document.createElement('div');
                div.className = 'skin-item';
                
                let actionHtml = '';
                if (ownedSkins[i]) {
                    actionHtml = `<button class="btn w-full ${equippedSkin === i ? 'btn-active' : ''}" onclick="equip(${i})">
                        ${equippedSkin === i ? 'EQUIPPED' : 'EQUIP'}
                    </button>`;
                } else {
                    actionHtml = `
                        <button class="btn btn-coin text-[10px]" onclick="buySkin(${i}, 500)">500 ENERGY</button>
                        <button class="btn btn-ad text-[10px]" onclick="watchAd(${i})">REWARD AD</button>
                    `;
                }

                div.innerHTML = `
                    <div class="skin-preview" style="background:${skin.bg}; border-color:${skin.border}"></div>
                    <span class="text-[10px] font-black tracking-widest">${skin.name}</span>
                    <div class="flex flex-col gap-2 w-full mt-2">${actionHtml}</div>
                `;
                list.appendChild(div);
            });
        }

        function buySkin(i, price) {
            if (coins >= price) {
                coins -= price;
                ownedSkins[i] = true;
                localStorage.setItem('np_v2_skins', JSON.stringify(ownedSkins));
                updateCurrency();
                renderShop();
                playSfx(800, 'sine', 0.2, 0.05);
            }
        }

        function watchAd(i) {
            const loader = document.getElementById('adLoader');
            const bar = document.getElementById('adBar');
            loader.classList.remove('hidden');
            let p = 0;
            const int = setInterval(() => {
                p += 1.5;
                bar.style.width = p + '%';
                if (p >= 100) {
                    clearInterval(int);
                    loader.classList.add('hidden');
                    ownedSkins[i] = true;
                    localStorage.setItem('np_v2_skins', JSON.stringify(ownedSkins));
                    renderShop();
                    playSfx(1000, 'sine', 0.5, 0.05);
                }
            }, 30);
        }

        function equip(i) {
            equippedSkin = i;
            localStorage.setItem('np_v2_equipped', i);
            renderShop();
        }

        class Obstacle {
            constructor(type, x, y) {
                this.type = type; this.x = x; this.y = y; this.w = 40; this.h = 40;
            }
            draw() {
                ctx.fillStyle = '#fff';
                ctx.shadowBlur = 10;
                ctx.shadowColor = '#fff';
                if (this.type === 'spike') {
                    ctx.beginPath(); ctx.moveTo(this.x, this.y + this.h);
                    ctx.lineTo(this.x + this.w/2, this.y); ctx.lineTo(this.x + this.w, this.y + this.h);
                    ctx.fill();
                } else {
                    ctx.save(); ctx.translate(this.x+20, this.y+20); ctx.rotate(frame*0.1);
                    ctx.fillRect(-20, -2, 40, 4); ctx.fillRect(-2, -20, 4, 40); ctx.restore();
                }
                ctx.shadowBlur = 0;
            }
        }

        function gameOver() {
            if (!gameActive) return;
            playSfx(100, 'sawtooth', 0.3, 0.1);
            if (isPractice && checkpoints.length > 0) {
                const cp = checkpoints[checkpoints.length-1];
                distance = cp.d; player.y = cp.y; player.mode = cp.mode; player.gravityDir = cp.g;
                obstacles = [];
                return;
            }
            gameActive = false;
            document.getElementById('overlay').style.display = 'flex';
            document.getElementById('resultInfo').classList.remove('hidden');
            document.getElementById('resultTitle').innerText = "DOMAIN COLLAPSED";
            document.getElementById('resultTitle').className = "text-5xl font-black italic mb-3 tracking-tighter text-red-500";
            document.getElementById('resultStats').innerText = `STABILITY AT: ${Math.floor((distance/levelLength)*100)}%`;
        }

        function win() {
            gameActive = false;
            document.getElementById('overlay').style.display = 'flex';
            document.getElementById('resultInfo').classList.remove('hidden');
            document.getElementById('resultTitle').innerText = "LIMITLESS ACHIEVED";
            document.getElementById('resultTitle').className = "text-5xl font-black italic mb-3 tracking-tighter text-cyan-400";
            if (!isPractice) {
                const reward = CONFIG[currentDiff].reward;
                coins += reward;
                updateCurrency();
                document.getElementById('resultStats').innerText = `CORE RESTORED: +${reward} ENERGY`;
            } else {
                document.getElementById('resultStats').innerText = "PRACTICE SIMULATION ENDED";
            }
        }

        function hideResult() { document.getElementById('resultInfo').classList.add('hidden'); }

        function loop() {
            if (!gameActive) return;
            
            ctx.fillStyle = '#050508';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            const ground = canvas.height - 150;
            const ceil = 100;
            
            ctx.fillStyle = 'rgba(20, 20, 30, 1)';
            ctx.fillRect(0, ground, canvas.width, 150);
            ctx.fillRect(0, 0, canvas.width, ceil);
            ctx.strokeStyle = 'rgba(255,255,255,0.05)';
            ctx.strokeRect(0, ground, canvas.width, 1);
            ctx.strokeRect(0, ceil, canvas.width, 1);

            player.vy += 0.85 * player.gravityDir;
            
            if (keys['Space'] && player.grounded) { 
                player.vy = -14.5 * player.gravityDir; 
                player.grounded = false; 
                playSfx(400, 'triangle', 0.05, 0.02);
            }

            player.y += player.vy;
            if (player.y > ground - player.h) { player.y = ground - player.h; player.vy = 0; player.grounded = true; }
            else if (player.y < ceil) { player.y = ceil; player.vy = 0; player.grounded = true; }
            else player.grounded = false;

            if (!player.grounded) player.rot += 6.5 * player.gravityDir;
            else player.rot = Math.round(player.rot/90)*90;

            ctx.save();
            ctx.translate(player.x + player.w/2, player.y + player.h/2);
            ctx.rotate(player.rot * Math.PI/180);
            const s = skinStyles[equippedSkin];
            ctx.fillStyle = s.bg; 
            ctx.shadowBlur = 15;
            ctx.shadowColor = s.bg;
            ctx.fillRect(-player.w/2, -player.h/2, player.w, player.h);
            ctx.strokeStyle = s.border; ctx.lineWidth = 2; 
            ctx.strokeRect(-player.w/2, -player.h/2, player.w, player.h);
            ctx.fillStyle = s.eyes; 
            ctx.fillRect(-12, -12, 7, 7); ctx.fillRect(5, -12, 7, 7);
            ctx.restore();

            if (frame % CONFIG[currentDiff].spawn === 0) {
                obstacles.push(new Obstacle('spike', canvas.width, ground - 40));
            }

            obstacles.forEach((o, i) => {
                o.x -= CONFIG[currentDiff].speed;
                o.draw();
                if (player.x < o.x + o.w - 8 && player.x + player.w > o.x + 8 && 
                    player.y < o.y + o.h - 8 && player.y + player.h > o.y + 8) {
                    gameOver();
                }
                if (o.x < -100) obstacles.splice(i, 1);
            });

            distance += CONFIG[currentDiff].speed;
            const pct = Math.min(100, (distance/levelLength)*100);
            document.getElementById('progress-bar').style.width = pct + '%';
            document.getElementById('percentText').innerText = Math.floor(pct) + '%';
            if (pct >= 100) win();

            frame++;
            requestAnimationFrame(loop);
        }

        function startGame() {
            if (!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            if (audioCtx.state === 'suspended') audioCtx.resume();
            
            distance = 0; frame = 0; obstacles = []; checkpoints = [];
            player.y = canvas.height/2; player.vy = 0; player.gravityDir = 1;
            gameActive = true;
            document.getElementById('overlay').style.display = 'none';
            loop();
        }

        init();
    </script>
</body>
</html>

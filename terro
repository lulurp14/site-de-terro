<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Acesso Restrito</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #000;
            font-family: 'Courier New', monospace;
            overflow: hidden;
            height: 100vh;
            cursor: none;
        }

        .screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            color: #00ff00;
            text-align: center;
            padding: 20px;
            opacity: 0;
            transition: opacity 1s ease-in-out;
            z-index: 100;
        }

        #audio-permission {
            opacity: 1;
            z-index: 1000;
            background: #000;
        }

        #loading {
            background: #000;
        }

        #main-horror {
            background: #000;
        }

        #warning {
            background: #000;
            color: #ff0000;
        }

        .start-button {
            background: #ff0000;
            color: white;
            border: none;
            padding: 20px 40px;
            font-size: 1.5rem;
            font-weight: bold;
            margin-top: 30px;
            cursor: pointer;
            border-radius: 10px;
            text-transform: uppercase;
            animation: pulse 2s infinite;
        }

        .start-button:hover {
            background: #cc0000;
            transform: scale(1.1);
        }

        .jumpscare {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #000;
            z-index: 9999;
            display: none;
            justify-content: center;
            align-items: center;
        }

        .jumpscare-img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            animation: shake 0.1s infinite;
        }

        .glitch {
            font-size: 3rem;
            font-weight: bold;
            text-transform: uppercase;
            position: relative;
            text-shadow: 0.05em 0 0 #00fffc, -0.03em -0.04em 0 #fc00ff,
                         0.025em 0.04em 0 #fffc00;
            animation: glitch 725ms infinite;
        }

        .scan-line {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 2px;
            background: #00ff00;
            box-shadow: 0 0 10px #00ff00;
            animation: scan 2s linear infinite;
            opacity: 0.3;
        }

        .terminal-text {
            font-size: 1.2rem;
            line-height: 1.4;
            max-width: 800px;
            margin: 20px 0;
        }

        .blink {
            animation: blink 1s infinite;
        }

        .horror-image {
            max-width: 90%;
            max-height: 70vh;
            border: 2px solid #ff0000;
            box-shadow: 0 0 30px #ff0000;
            filter: hue-rotate(90deg) contrast(1.5) brightness(0.8);
            margin: 20px 0;
            opacity: 0;
            transform: scale(0.8);
            transition: all 3s ease-in-out;
        }

        .revealed {
            opacity: 1 !important;
            transform: scale(1) !important;
        }

        .blood-drip {
            position: absolute;
            top: -50px;
            width: 2px;
            height: 0;
            background: linear-gradient(to bottom, transparent, #ff0000);
            animation: drip 3s ease-in-out forwards;
        }

        .face-appear {
            position: fixed;
            width: 400px;
            height: 400px;
            opacity: 0;
            z-index: 5000;
            pointer-events: none;
            animation: faceFloat 2s ease-in-out forwards;
            border-radius: 10px;
            box-shadow: 0 0 50px #ff0000;
        }

        .whisper-text {
            position: fixed;
            color: #ff0000;
            font-size: 2rem;
            font-weight: bold;
            opacity: 0;
            z-index: 4000;
            text-shadow: 0 0 20px #ff0000, 0 0 30px #ff0000;
            animation: whisper 3s ease-in-out forwards;
            font-family: 'Arial Black', sans-serif;
            text-transform: uppercase;
        }

        .noise {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: transparent;
            opacity: 0.1;
            pointer-events: none;
            z-index: 1001;
        }

        .noise::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.65' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)'/%3E%3C/svg%3E");
            animation: noise 0.1s infinite;
        }

        .blood-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle, transparent 50%, rgba(255,0,0,0.3) 100%);
            pointer-events: none;
            z-index: 3000;
            opacity: 0;
            transition: opacity 2s;
        }

        .audio-controls {
            position: fixed;
            bottom: 20px;
            right: 20px;
            z-index: 10000;
            color: #00ff00;
            font-size: 14px;
            background: rgba(0,0,0,0.8);
            padding: 10px;
            border-radius: 5px;
        }

        .hidden {
            display: none;
        }

        /* Animações */
        @keyframes glitch {
            0% {
                text-shadow: 0.05em 0 0 #00fffc, -0.03em -0.04em 0 #fc00ff,
                             0.025em 0.04em 0 #fffc00;
            }
            15% {
                text-shadow: 0.05em 0 0 #00fffc, -0.03em -0.04em 0 #fc00ff,
                             0.025em 0.04em 0 #fffc00;
            }
            16% {
                text-shadow: -0.05em -0.025em 0 #00fffc, 0.025em 0.035em 0 #fc00ff,
                             -0.05em -0.05em 0 #fffc00;
            }
            49% {
                text-shadow: -0.05em -0.025em 0 #00fffc, 0.025em 0.035em 0 #fc00ff,
                             -0.05em -0.05em 0 #fffc00;
            }
            50% {
                text-shadow: 0.05em 0.035em 0 #00fffc, 0.03em 0 0 #fc00ff,
                             0 -0.04em 0 #fffc00;
            }
            99% {
                text-shadow: 0.05em 0.035em 0 #00fffc, 0.03em 0 0 #fc00ff,
                             0 -0.04em 0 #fffc00;
            }
            100% {
                text-shadow: -0.05em 0 0 #00fffc, -0.025em -0.04em 0 #fc00ff,
                             -0.04em -0.025em 0 #fffc00;
            }
        }

        @keyframes scan {
            0% {
                top: 0%;
            }
            100% {
                top: 100%;
            }
        }

        @keyframes blink {
            0%, 100% {
                opacity: 1;
            }
            50% {
                opacity: 0;
            }
        }

        @keyframes drip {
            0% {
                height: 0;
                opacity: 1;
            }
            90% {
                height: 100px;
                opacity: 1;
            }
            100% {
                height: 100px;
                opacity: 0;
            }
        }

        @keyframes shake {
            0% { transform: translate(1px, 1px) rotate(0deg) scale(1.1); }
            10% { transform: translate(-1px, -2px) rotate(-1deg) scale(1.1); }
            20% { transform: translate(-3px, 0px) rotate(1deg) scale(1.1); }
            30% { transform: translate(3px, 2px) rotate(0deg) scale(1.1); }
            40% { transform: translate(1px, -1px) rotate(1deg) scale(1.1); }
            50% { transform: translate(-1px, 2px) rotate(-1deg) scale(1.1); }
            60% { transform: translate(-3px, 1px) rotate(0deg) scale(1.1); }
            70% { transform: translate(3px, 1px) rotate(-1deg) scale(1.1); }
            80% { transform: translate(-1px, -1px) rotate(1deg) scale(1.1); }
            90% { transform: translate(1px, 2px) rotate(0deg) scale(1.1); }
            100% { transform: translate(1px, -2px) rotate(-1deg) scale(1.1); }
        }

        @keyframes faceFloat {
            0% {
                opacity: 0;
                transform: scale(0.1) rotate(0deg);
            }
            20% {
                opacity: 1;
                transform: scale(1.3) rotate(5deg);
            }
            40% {
                opacity: 1;
                transform: scale(1.2) rotate(-5deg);
            }
            60% {
                opacity: 1;
                transform: scale(1.25) rotate(3deg);
            }
            80% {
                opacity: 0.8;
                transform: scale(1.2) rotate(-2deg);
            }
            100% {
                opacity: 0;
                transform: scale(0.5) rotate(0deg);
            }
        }

        @keyframes whisper {
            0% {
                opacity: 0;
                transform: translateY(20px) scale(0.8);
            }
            30% {
                opacity: 1;
                transform: translateY(0) scale(1.1);
            }
            70% {
                opacity: 1;
                transform: translateY(0) scale(1.1);
            }
            100% {
                opacity: 0;
                transform: translateY(-20px) scale(0.8);
            }
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }

        @keyframes noise {
            0%, 100% { transform: translate(0,0) }
            10% { transform: translate(-2%,-2%) }
            20% { transform: translate(-2%,2%) }
            30% { transform: translate(2%,2%) }
            40% { transform: translate(2%,-2%) }
            50% { transform: translate(-2%,-2%) }
            60% { transform: translate(-2%,2%) }
            70% { transform: translate(2%,2%) }
            80% { transform: translate(2%,-2%) }
            90% { transform: translate(-2%,-2%) }
        }

        .heartbeat {
            animation: heartbeat 0.8s infinite;
        }

        @keyframes heartbeat {
            0% { transform: scale(1); }
            25% { transform: scale(1.1); }
            50% { transform: scale(1); }
            75% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body>
    <div class="noise"></div>
    <div class="blood-overlay" id="bloodOverlay"></div>
    
    <!-- Elementos de Áudio -->
    <audio id="backgroundSound" loop preload="auto">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-horror-ambience-469.mp3" type="audio/mpeg">
    </audio>

    <audio id="scream1" preload="auto">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-woman-scream-94.mp3" type="audio/mpeg">
    </audio>

    <audio id="scream2" preload="auto">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-horror-scream-483.mp3" type="audio/mpeg">
    </audio>

    <audio id="scream3" preload="auto">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-man-scream-121.mp3" type="audio/mpeg">
    </audio>

    <audio id="whisperSound" preload="auto">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-creepy-whisper-440.mp3" type="audio/mpeg">
    </audio>

    <audio id="heartbeatSound" preload="auto">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-fast-heartbeat-440.mp3" type="audio/mpeg">
    </audio>

    <audio id="jumpscareSound" preload="auto">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-horror-sting-492.mp3" type="audio/mpeg">
    </audio>

    <audio id="staticSound" preload="auto">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-tv-static-3026.mp3" type="audio/mpeg">
    </audio>

    <audio id="doorSound" preload="auto">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-creaky-door-2761.mp3" type="audio/mpeg">
    </audio>

    <!-- Jumpscares -->
    <div class="jumpscare" id="jumpscare1">
        <img src="https://th.bing.com/th/id/R.47e6d7b0d82a1b897a2d42685fe772f2?rik=mjszm9Maie%252bDIg&riu=http%3a%2f%2f4.bp.blogspot.com%2f-8q1_YesBe58%2fT2zM25zt3DI%2fAAAAAAAAAXY%2fFVkqLKJV_q8%2fs1600%2fThe-Grudge-horror-movies-77532_1024_768.jpg" 
             class="jumpscare-img" 
             alt="JUMPS CARE - A GRUDGE">
    </div>

    <div class="jumpscare" id="jumpscare2">
        <img src="https://i.ytimg.com/vi/Irx5fcLu76s/maxresdefault.jpg" 
             class="jumpscare-img" 
             alt="JUMPS CARE 2 - ROSTO ASSUSTADOR">
    </div>

    <div class="jumpscare" id="jumpscare3">
        <img src="https://pm1.narvii.com/6896/509d33c215af25b3e154f3ab763637a223552eadr1-1024-576v2_hq.jpg" 
             class="jumpscare-img" 
             alt="JUMPS CARE 3 - CRIATURA TERRÍVEL">
    </div>

    <!-- Tela de Permissão de Áudio -->
    <div class="screen" id="audio-permission">
        <div class="scan-line"></div>
        <div class="glitch">AVISO DE SEGURANÇA</div>
        <div class="terminal-text">
            <p>⚠️ ESTE SITE CONTÉM CONTEÚDO EXTREMAMENTE ASSUSTADOR ⚠️</p>
            <p>SONS ALTOS, IMAGENS PERTURBADORAS E SUSTOS REPENTINOS</p>
            <p>NÃO RECOMENDADO PARA CARDÍACOS OU PESSOAS SENSÍVEIS</p>
            <p style="color: #ff0000; margin-top: 20px;">CLIQUE NO BOTÃO ABAIXO PARA INICIAR A EXPERIÊNCIA</p>
        </div>
        <button class="start-button" id="startButton">INICIAR EXPERIÊNCIA</button>
    </div>

    <!-- Tela de Loading -->
    <div class="screen" id="loading">
        <div class="scan-line"></div>
        <div class="glitch">SISTEMA INICIANDO</div>
        <div class="terminal-text">
            <p>CARREGANDO MÓDULOS DE SEGURANÇA...</p>
            <p>INICIALIZANDO PROTOCOLOS OCULTOS...</p>
            <p>ACESSANDO DADOS RESTRITOS<span class="blink">_</span></p>
        </div>
    </div>

    <!-- Tela Principal do Horror -->
    <div class="screen" id="main-horror">
        <div class="scan-line"></div>
        <div class="glitch">ACESSO CONCEDIDO</div>
        <div class="terminal-text">
            <p>VOCÊ ENCONTROU O QUE PROCURAVA?</p>
            <p>ALGUMAS COISAS NÃO DEVEM SER VISTAS<span class="blink">_</span></p>
        </div>
        <img src="https://th.bing.com/th/id/R.47e6d7b0d82a1b897a2d42685fe772f2?rik=mjszm9Maie%252bDIg&riu=http%3a%2f%2f4.bp.blogspot.com%2f-8q1_YesBe58%2fT2zM25zt3DI%2fAAAAAAAAAXY%2fFVkqLKJV_q8%2fs1600%2fThe-Grudge-horror-movies-77532_1024_768.jpg" 
             alt="Criatura Horrível" 
             class="horror-image"
             id="horrorImg">
    </div>

    <!-- Tela de Aviso Final -->
    <div class="screen" id="warning">
        <div class="glitch" style="color: #ff0000; font-size: 4rem;">AVISO</div>
        <div class="terminal-text" style="color: #ff0000; font-size: 2rem;">
            <p>NÃO ENTRE EM QUALQUER SITE</p>
            <p>DESCONFIE<span class="blink">_</span></p>
        </div>
    </div>

    <div class="audio-controls" id="audioControls">
        🔊 Sons Ativados
    </div>

    <script>
        // Elementos de áudio
        const backgroundSound = document.getElementById('backgroundSound');
        const scream1 = document.getElementById('scream1');
        const scream2 = document.getElementById('scream2');
        const scream3 = document.getElementById('scream3');
        const whisperSound = document.getElementById('whisperSound');
        const heartbeatSound = document.getElementById('heartbeatSound');
        const jumpscareSound = document.getElementById('jumpscareSound');
        const staticSound = document.getElementById('staticSound');
        const doorSound = document.getElementById('doorSound');

        // Configuração de volume
        backgroundSound.volume = 0.4;
        scream1.volume = 0.8;
        scream2.volume = 0.8;
        scream3.volume = 0.8;
        whisperSound.volume = 0.6;
        heartbeatSound.volume = 0.7;
        jumpscareSound.volume = 1.0;
        staticSound.volume = 0.5;
        doorSound.volume = 0.6;

        // Imagens específicas para jumpscares
        const horrorImages = [
            'https://th.bing.com/th/id/R.47e6d7b0d82a1b897a2d42685fe772f2?rik=mjszm9Maie%252bDIg&riu=http%3a%2f%2f4.bp.blogspot.com%2f-8q1_YesBe58%2fT2zM25zt3DI%2fAAAAAAAAAXY%2fFVkqLKJV_q8%2fs1600%2fThe-Grudge-horror-movies-77532_1024_768.jpg',
            'https://i.ytimg.com/vi/Irx5fcLu76s/maxresdefault.jpg',
            'https://pm1.narvii.com/6896/509d33c215af25b3e154f3ab763637a223552eadr1-1024-576v2_hq.jpg'
        ];

        // Textos assustadores para whispers
        const whisperTexts = [
            "ELA TE OBSERVA",
            "SAIA AGORA",
            "NÃO ESTÁ SOZINHO",
            "ELA VEM AÍ",
            "CORRA",
            "TE ENCONTREI",
            "NÃO OLHE PARA TRÁS",
            "ESTÁ ATRÁS DE VOCÊ",
            "NÃO É SEGURO",
            "FECHE OS OLHOS"
        ];

        // Variável para controlar se os sons estão ativos
        let audioEnabled = false;

        // Sons de gritos aleatórios
        function playRandomScream() {
            if (!audioEnabled) return;
            
            const screams = [scream1, scream2, scream3];
            const randomScream = screams[Math.floor(Math.random() * screams.length)];
            randomScream.currentTime = 0;
            randomScream.play().catch(e => console.log('Erro ao tocar scream:', e));
        }

        // Função para jumpscare com som
        function triggerJumpscare(jumpscareId, duration = 800) {
            const jumpscare = document.getElementById(jumpscareId);
            jumpscare.style.display = 'flex';
            
            // Toca som do jumpscare
            if (audioEnabled) {
                jumpscareSound.currentTime = 0;
                jumpscareSound.play().catch(e => console.log('Erro ao tocar jumpscare sound:', e));
                
                // Toca grito aleatório
                playRandomScream();
                
                heartbeatSound.currentTime = 0;
                heartbeatSound.play().catch(e => console.log('Erro ao tocar heartbeat:', e));
            }
            
            // Efeito de heartbeat no body
            document.body.classList.add('heartbeat');
            
            // Ativa overlay de sangue
            document.getElementById('bloodOverlay').style.opacity = '0.7';
            
            setTimeout(() => {
                jumpscare.style.display = 'none';
                document.body.classList.remove('heartbeat');
                document.getElementById('bloodOverlay').style.opacity = '0';
                if (audioEnabled) {
                    heartbeatSound.pause();
                }
            }, duration);
        }

        // Função para aparecer rostos rapidamente
        function flashFace() {
            const face = document.createElement('img');
            face.className = 'face-appear';
            face.src = horrorImages[Math.floor(Math.random() * horrorImages.length)];
            document.body.appendChild(face);
            
            // Som de estático
            if (audioEnabled) {
                staticSound.currentTime = 0;
                staticSound.play().catch(e => console.log('Erro ao tocar static:', e));
            }
            
            setTimeout(() => {
                face.remove();
            }, 2000);
        }

        // Função para texto sussurrado
        function showWhisper() {
            const whisper = document.createElement('div');
            whisper.className = 'whisper-text';
            whisper.textContent = whisperTexts[Math.floor(Math.random() * whisperTexts.length)];
            whisper.style.left = Math.random() * 70 + 15 + '%';
            whisper.style.top = Math.random() * 70 + 15 + '%';
            document.body.appendChild(whisper);
            
            // Som de sussurro
            if (audioEnabled) {
                whisperSound.currentTime = 0;
                whisperSound.play().catch(e => console.log('Erro ao tocar whisper:', e));
            }
            
            setTimeout(() => {
                whisper.remove();
            }, 3000);
        }

        // Função para tocar som de porta rangendo
        function playDoorSound() {
            if (!audioEnabled) return;
            
            doorSound.currentTime = 0;
            doorSound.play().catch(e => console.log('Erro ao tocar door sound:', e));
        }

        // Iniciar som de fundo
        function startBackgroundSound() {
            if (!audioEnabled) return;
            
            backgroundSound.play().catch(e => {
                console.log('Erro ao iniciar som de fundo:', e);
            });
        }

        // Iniciar a experiência de terror
        function startHorrorExperience() {
            audioEnabled = true;
            document.getElementById('audio-permission').style.opacity = '0';
            
            // Inicia todos os sons
            startBackgroundSound();
            
            setTimeout(() => {
                document.getElementById('audio-permission').style.display = 'none';
                document.getElementById('loading').style.opacity = '1';
                
                // Sequência PRINCIPAL COM MUITOS JUMPSCARES E SONS
                setTimeout(() => {
                    document.getElementById('loading').style.opacity = '0';
                    
                    // Primeiro jumpscare SURPRESA (A Grudge)
                    setTimeout(() => {
                        triggerJumpscare('jumpscare1', 800);
                        
                        setTimeout(() => {
                            document.getElementById('main-horror').style.opacity = '1';
                            
                            // Revela a imagem gradualmente
                            setTimeout(() => {
                                document.getElementById('horrorImg').classList.add('revealed');
                                
                                // Jumpscare durante a revelação (Rosto Assustador)
                                setTimeout(() => {
                                    triggerJumpscare('jumpscare2', 600);
                                }, 1500);

                                // Rosto aparece rapidamente
                                setTimeout(() => {
                                    flashFace();
                                }, 3000);

                                // Whisper assustador
                                setTimeout(() => {
                                    showWhisper();
                                }, 4500);

                                // Som de porta
                                setTimeout(() => {
                                    playDoorSound();
                                }, 5000);

                                // Jumpscare triplo sequencial
                                setTimeout(() => {
                                    triggerJumpscare('jumpscare3', 400);
                                    setTimeout(() => {
                                        triggerJumpscare('jumpscare1', 400);
                                        setTimeout(() => {
                                            triggerJumpscare('jumpscare2', 400);
                                        }, 500);
                                    }, 500);
                                }, 6000);

                                // Pingos de sangue intensos
                                for(let i = 0; i < 25; i++) {
                                    setTimeout(() => {
                                        const drip = document.createElement('div');
                                        drip.className = 'blood-drip';
                                        drip.style.left = Math.random() * 100 + 'vw';
                                        drip.style.animationDelay = Math.random() * 2 + 's';
                                        drip.style.width = (1 + Math.random() * 3) + 'px';
                                        document.body.appendChild(drip);
                                        
                                        setTimeout(() => {
                                            drip.remove();
                                        }, 5000);
                                    }, i * 200);
                                }

                                // JUMPSCARES ALEATÓRIOS CONSTANTES
                                const randomJumpscares = [
                                    () => triggerJumpscare('jumpscare1', 500),
                                    () => triggerJumpscare('jumpscare2', 500),
                                    () => triggerJumpscare('jumpscare3', 500),
                                    () => flashFace(),
                                    () => showWhisper(),
                                    () => playDoorSound(),
                                    () => playRandomScream()
                                ];

                                // Sequência de sustos intensos
                                for(let i = 0; i < 15; i++) {
                                    setTimeout(() => {
                                        const randomEffect = randomJumpscares[Math.floor(Math.random() * randomJumpscares.length)];
                                        randomEffect();
                                        
                                        // Às vezes ativa dois efeitos juntos
                                        if (Math.random() > 0.7) {
                                            setTimeout(() => {
                                                const secondEffect = randomJumpscares[Math.floor(Math.random() * randomJumpscares.length)];
                                                secondEffect();
                                            }, 300);
                                        }
                                    }, 8000 + (i * 1000));
                                }

                                // Mostra o aviso final
                                setTimeout(() => {
                                    // Sequência final de jumpscares
                                    triggerJumpscare('jumpscare1', 600);
                                    setTimeout(() => {
                                        triggerJumpscare('jumpscare2', 500);
                                        setTimeout(() => {
                                            triggerJumpscare('jumpscare3', 700);
                                            
                                            setTimeout(() => {
                                                document.getElementById('main-horror').style.opacity = '0';
                                                
                                                setTimeout(() => {
                                                    document.getElementById('warning').style.opacity = '1';
                                                    
                                                    // Jumpscare DURANTE o aviso
                                                    setTimeout(() => {
                                                        triggerJumpscare('jumpscare1', 400);
                                                    }, 1500);

                                                    // ÚLTIMOS JUMPSCARES FINAIS
                                                    setTimeout(() => {
                                                        triggerJumpscare('jumpscare2', 300);
                                                        setTimeout(() => {
                                                            triggerJumpscare('jumpscare3', 500);
                                                            
                                                            // Fica tudo preto
                                                            setTimeout(() => {
                                                                document.body.style.background = '#000';
                                                                document.getElementById('warning').style.opacity = '0';
                                                                
                                                                // JUMPSCARE FINAL EXTREMO
                                                                setTimeout(() => {
                                                                    triggerJumpscare('jumpscare1', 1000);
                                                                    setTimeout(() => {
                                                                        triggerJumpscare('jumpscare2', 800);
                                                                        setTimeout(() => {
                                                                            triggerJumpscare('jumpscare3', 600);
                                                                            
                                                                            // Para todos os sons e recarrega
                                                                            setTimeout(() => {
                                                                                backgroundSound.pause();
                                                                                location.reload();
                                                                            }, 1000);
                                                                            
                                                                        }, 400);
                                                                    }, 400);
                                                                }, 500);
                                                                
                                                            }, 2000);
                                                            
                                                        }, 400);
                                                    }, 1000);
                                                    
                                                }, 1000);
                                                
                                            }, 1000);
                                            
                                        }, 600);
                                    }, 500);
                                    
                                }, 25000);
                                
                            }, 1000);
                            
                        }, 800);
                        
                    }, 500);
                    
                }, 2000);
                
            }, 1000);
        }

        // Event listener para o botão de início
        document.getElementById('startButton').addEventListener('click', startHorrorExperience);

        // Efeitos de cursor personalizado
        document.addEventListener('mousemove', (e) => {
            if (!document.getElementById('cursor')) {
                const cursor = document.createElement('div');
                cursor.id = 'cursor';
                cursor.style.position = 'fixed';
                cursor.style.width = '25px';
                cursor.style.height = '25px';
                cursor.style.background = '#ff0000';
                cursor.style.borderRadius = '50%';
                cursor.style.pointerEvents = 'none';
                cursor.style.zIndex = '10000';
                cursor.style.mixBlendMode = 'difference';
                cursor.style.boxShadow = '0 0 20px #ff0000';
                document.body.appendChild(cursor);
            }
            
            const cursor = document.getElementById('cursor');
            cursor.style.left = (e.clientX - 12.5) + 'px';
            cursor.style.top = (e.clientY - 12.5) + 'px';
        });

        // Efeito de sombra e cor nas imagens
        setInterval(() => {
            const img = document.getElementById('horrorImg');
            const hue = Math.random() * 360;
            const brightness = 0.5 + Math.random() * 0.3;
            img.style.filter = `hue-rotate(${hue}deg) contrast(1.8) brightness(${brightness})`;
        }, 600);

        // Jumpscare aleatório ao mover o mouse (após início)
        let mouseMoves = 0;
        document.addEventListener('mousemove', () => {
            if (!audioEnabled) return;
            
            mouseMoves++;
            if (mouseMoves > 30 && Math.random() > 0.95) {
                const randomJumpscare = 'jumpscare' + (Math.floor(Math.random() * 3) + 1);
                triggerJumpscare(randomJumpscare, 400);
                mouseMoves = 0;
            }
        });

        // Jumpscare ao clicar (após início)
        document.addEventListener('click', () => {
            if (!audioEnabled) return;
            
            if (Math.random() > 0.7) {
                const randomJumpscare = 'jumpscare' + (Math.floor(Math.random() * 3) + 1);
                triggerJumpscare(randomJumpscare, 500);
            }
        });
    </script>
</body>
</html>

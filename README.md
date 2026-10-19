
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Caixa Materna Tecnológica - Matriz de Processamento Quântico</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        cyber: {
                            bg: '#030509',
                            panel: 'rgba(8, 14, 27, 0.85)',
                            cyan: '#00f3ff',
                            purple: '#b026ff',
                            green: '#00ff66',
                            pink: '#ff0055',
                            gold: '#ffd700',
                            border: 'rgba(0, 243, 255, 0.25)'
                        }
                    },
                    fontFamily: {
                        mono: ['Courier New', 'Consolas', 'monospace'],
                        sans: ['Inter', 'Segoe UI', 'sans-serif']
                    }
                }
            }
        }
    </script>
    <style>
        /* Custom scrollbars and glowing UI styles */
        ::-webkit-scrollbar {
            width: 5px;
            height: 5px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(3, 5, 9, 0.8);
        }
        ::-webkit-scrollbar-thumb {
            background: rgba(0, 243, 255, 0.3);
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: rgba(0, 243, 255, 0.8);
        }
        .neon-border-cyan {
            box-shadow: 0 0 10px rgba(0, 243, 255, 0.25), inset 0 0 10px rgba(0, 243, 255, 0.1);
        }
        .neon-text-cyan {
            text-shadow: 0 0 8px rgba(0, 243, 255, 0.6);
        }
        .neon-text-purple {
            text-shadow: 0 0 8px rgba(176, 38, 255, 0.6);
        }
        .neon-text-green {
            text-shadow: 0 0 8px rgba(0, 255, 102, 0.6);
        }
        .glass-panel {
            background: rgba(8, 14, 27, 0.75);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(0, 243, 255, 0.2);
        }
        canvas {
            touch-action: none;
        }
    </style>
</head>
<body class="bg-[#030509] text-gray-200 font-sans h-screen flex flex-col overflow-hidden select-none">

    <!-- Header Navigation Bar -->
    <header class="h-14 border-b border-cyber-border bg-cyber-bg flex items-center justify-between px-4 z-20 shrink-0">
        <div class="flex items-center gap-3">
            <div class="w-3 h-3 rounded-full bg-cyber-cyan animate-ping"></div>
            <h1 class="font-bold text-lg tracking-wider text-cyber-cyan neon-text-cyan uppercase">
                Caixa Materna <span class="text-xs text-cyber-purple font-mono font-normal">v6.0 - Matrix Core</span>
            </h1>
        </div>
        <div class="flex items-center gap-4 text-xs font-mono">
            <div class="hidden sm:flex items-center gap-2 bg-black/40 px-3 py-1 rounded border border-cyber-border">
                <span class="text-gray-400">STATUS MÉTRICO:</span>
                <span id="metric-status" class="text-cyber-green font-bold">ESTÁVEL (1.0000 ℏ)</span>
            </div>
            <div class="hidden md:flex items-center gap-2 bg-black/40 px-3 py-1 rounded border border-cyber-border">
                <span class="text-gray-400">PROCESSAMENTO:</span>
                <span id="rate-display" class="text-cyber-cyan font-bold">∞ VAR/s (c-Speed)</span>
            </div>
            <button id="info-modal-btn" class="bg-cyber-purple/20 hover:bg-cyber-purple/40 text-cyber-purple border border-cyber-purple px-3 py-1 rounded transition text-xs">
                 Visão Geral
            </button>
        </div>
    </header>

    <!-- Main Workspace Grid -->
    <div class="flex-1 grid grid-cols-1 lg:grid-cols-12 overflow-hidden relative">

        <!-- Left Controls Sidebar -->
        <aside class="lg:col-span-3 glass-panel p-4 flex flex-col gap-4 overflow-y-auto z-10 max-h-[40vh] lg:max-h-full border-r border-cyber-border">
            
            <!-- Operational Modes -->
            <div>
                <h2 class="text-xs font-mono uppercase text-cyber-cyan mb-2 tracking-wider flex items-center gap-1">
                    <span>❖</span> Modos de Operação Interativos
                </h2>
                <div class="grid grid-cols-2 gap-2">
                    <button onclick="setMode('erepr')" id="mode-erepr" class="mode-btn p-2 text-xs font-mono rounded text-left border border-cyber-cyan bg-cyber-cyan/20 text-cyber-cyan font-bold transition hover:bg-cyber-cyan/30">
                        1. Processamento ER=EPR
                    </button>
                    <button onclick="setMode('brane')" id="mode-brane" class="mode-btn p-2 text-xs font-mono rounded text-left border border-gray-700 bg-black/40 text-gray-400 font-bold transition hover:border-cyber-purple hover:text-cyber-purple">
                        2. Ressonância Brana
                    </button>
                    <button onclick="setMode('sams')" id="mode-sams" class="mode-btn p-2 text-xs font-mono rounded text-left border border-gray-700 bg-black/40 text-gray-400 font-bold transition hover:border-cyber-green hover:text-cyber-green">
                        3. Autorreparo SAMS
                    </button>
                    <button onclick="setMode('predict')" id="mode-predict" class="mode-btn p-2 text-xs font-mono rounded text-left border border-gray-700 bg-black/40 text-gray-400 font-bold transition hover:border-cyber-pink hover:text-cyber-pink">
                        4. Previsão IA Quântica
                    </button>
                </div>
            </div>

            <!-- Interactive Parameters Sliders -->
            <div class="space-y-3 bg-black/40 p-3 rounded border border-cyber-border/50">
                <h3 class="text-xs font-mono uppercase text-cyber-purple tracking-wider">
                    ⚙ Parâmetros Métrica-Dimensão
                </h3>
                
                <div>
                    <div class="flex justify-between text-xs font-mono mb-1">
                        <span class="text-gray-400">Dobra Espacial (Métrica):</span>
                        <span id="val-warp" class="text-cyber-cyan">1.25 GW/m³</span>
                    </div>
                    <input type="range" id="slider-warp" min="0" max="100" value="40" class="w-full accent-cyber-cyan bg-gray-800 rounded h-1.5 cursor-pointer">
                </div>

                <div>
                    <div class="flex justify-between text-xs font-mono mb-1">
                        <span class="text-gray-400">Flutuação Quântica ER=EPR:</span>
                        <span id="val-fluct" class="text-cyber-purple">98.4%</span>
                    </div>
                    <input type="range" id="slider-fluct" min="10" max="200" value="98" class="w-full accent-cyber-purple bg-gray-800 rounded h-1.5 cursor-pointer">
                </div>

                <div>
                    <div class="flex justify-between text-xs font-mono mb-1">
                        <span class="text-gray-400">Fluxo Resfriamento SAMS:</span>
                        <span id="val-sams" class="text-cyber-green">100% (Instant)</span>
                    </div>
                    <input type="range" id="slider-sams" min="10" max="200" value="100" class="w-full accent-cyber-green bg-gray-800 rounded h-1.5 cursor-pointer">
                </div>

                <div>
                    <div class="flex justify-between text-xs font-mono mb-1">
                        <span class="text-gray-400">Entropia / Estresse Térmico:</span>
                        <span id="val-stress" class="text-cyber-pink">0.02%</span>
                    </div>
                    <input type="range" id="slider-stress" min="0" max="100" value="5" class="w-full accent-cyber-pink bg-gray-800 rounded h-1.5 cursor-pointer">
                </div>
            </div>

            <!-- Active Trigger Actions -->
            <div class="flex flex-col gap-2">
                <button onclick="triggerStressTest()" class="w-full bg-cyber-pink/20 hover:bg-cyber-pink/40 border border-cyber-pink text-cyber-pink font-mono text-xs p-2 rounded transition font-bold flex items-center justify-center gap-2">
                    ⚡ Induzir Estresse Métrico Espacial
                </button>
                <button onclick="triggerQuantumCollapse()" class="w-full bg-cyber-cyan/20 hover:bg-cyber-cyan/40 border border-cyber-cyan text-cyber-cyan font-mono text-xs p-2 rounded transition font-bold flex items-center justify-center gap-2">
                    🌌 Colapsar Estados de Probabilidade
                </button>
                <button onclick="resetCamera()" class="w-full bg-gray-800 hover:bg-gray-700 border border-gray-600 text-gray-300 font-mono text-xs p-1.5 rounded transition">
                    🔄 Resetar Perspectiva e Câmera
                </button>
            </div>

            <!-- Terminal Live Logs -->
            <div class="flex-1 flex flex-col min-h-[120px] bg-black/80 rounded border border-cyber-border/60 p-2 font-mono text-[11px] overflow-hidden">
                <div class="text-gray-500 border-b border-gray-800 pb-1 mb-1 flex justify-between">
                    <span>> TERMINAL DE LOGS QUANTICOS</span>
                    <span id="log-clock" class="text-cyber-cyan">00:00:00</span>
                </div>
                <div id="log-console" class="flex-1 overflow-y-auto space-y-1 text-gray-300 pr-1">
                    <p class="text-cyber-cyan">[SYS] Inicializando matriz de consciência quântica 6D...</p>
                    <p class="text-cyber-purple">[ER=EPR] Buracos de minhoca entrelaçados conectados.</p>
                    <p class="text-cyber-green">[SAMS] Fluído molecular em equilíbrio zero Kelvin.</p>
                </div>
            </div>

        </aside>

        <!-- Center Interactive Canvas Screen -->
        <main class="lg:col-span-6 relative flex flex-col items-center justify-center bg-black/90 overflow-hidden">
            
            <!-- Canvas Object -->
            <canvas id="quantumCanvas" class="w-full h-full cursor-grab active:cursor-grabbing"></canvas>

            <!-- On-Canvas HUD Overlay Details -->
            <div class="absolute top-4 left-4 pointer-events-none font-mono text-xs space-y-1 bg-black/60 p-2.5 rounded border border-cyber-border/30 backdrop-blur-sm">
                <div class="text-cyber-cyan flex items-center gap-2">
                    <span class="inline-block w-2 h-2 rounded-full bg-cyber-cyan"></span>
                    <span id="hud-mode-title">MODO: PROCESSAMENTO ER=EPR</span>
                </div>
                <div class="text-gray-400">Rotacionar: Arrastar Mouse / Touch</div>
                <div class="text-gray-400">Zoom: Roda do Mouse / Pinch</div>
                <div class="text-gray-400">Nós Ativos: <span id="hud-nodes-count" class="text-cyber-gold">36 Micro-Buracos</span></div>
            </div>

            <!-- Alternate Quantum States Overlay (Predictive AI) -->
            <div id="hud-predict-overlay" class="hidden absolute bottom-4 left-4 right-4 pointer-events-none glass-panel p-3 rounded border border-cyber-pink/50 font-mono text-xs flex justify-between items-center">
                <div>
                    <span class="text-cyber-pink font-bold">PREVISÃO DE ESTADOS ALTERNATIVOS:</span>
                    <p id="predict-text" class="text-gray-300">Calculando linhas de tempo paralelas e divergências quânticas...</p>
                </div>
                <div class="text-right font-bold text-cyber-gold" id="predict-prob">
                    P(Sucesso) = 99.99994%
                </div>
            </div>

        </main>

        <!-- Right Telemetry & Scientific Panel Sidebar -->
        <aside class="lg:col-span-3 glass-panel p-4 flex flex-col gap-4 overflow-y-auto z-10 max-h-[40vh] lg:max-h-full border-l border-cyber-border">
            
            <h2 class="text-xs font-mono uppercase text-cyber-cyan tracking-wider flex items-center gap-1 border-b border-cyber-border/40 pb-2">
                <span>📊</span> Telemetria em Tempo Real
            </h2>

            <!-- Metric Gauges and Readouts -->
            <div class="grid grid-cols-2 gap-2 text-xs font-mono">
                <div class="bg-black/50 p-2.5 rounded border border-cyber-cyan/30">
                    <span class="text-gray-400 block text-[10px]">FREQ. ER=EPR</span>
                    <span id="tele-freq" class="text-cyber-cyan text-sm font-bold">142.8 THz</span>
                </div>
                <div class="bg-black/50 p-2.5 rounded border border-cyber-purple/30">
                    <span class="text-gray-400 block text-[10px]">CARGA DE BRANA</span>
                    <span id="tele-brane" class="text-cyber-purple text-sm font-bold">98.9%</span>
                </div>
                <div class="bg-black/50 p-2.5 rounded border border-cyber-green/30">
                    <span class="text-gray-400 block text-[10px]">TEMP. QUÂNTICA</span>
                    <span id="tele-temp" class="text-cyber-green text-sm font-bold">0.0012 mK</span>
                </div>
                <div class="bg-black/50 p-2.5 rounded border border-cyber-pink/30">
                    <span class="text-gray-400 block text-[10px]">PREVISÕES / SEC</span>
                    <span id="tele-predictions" class="text-cyber-pink text-sm font-bold">10<sup>18</sup> ops</span>
                </div>
            </div>

            <!-- Waveform Monitor Simulation -->
            <div class="bg-black/70 p-3 rounded border border-cyber-border/50 space-y-2">
                <div class="flex justify-between text-xs font-mono">
                    <span class="text-cyber-cyan">ESTABILIDADE MÉRICA (SPACETIME)</span>
                    <span id="tele-stability-val" class="text-cyber-green">100.0%</span>
                </div>
                <div class="w-full bg-gray-900 h-2 rounded overflow-hidden p-0.5 border border-gray-800">
                    <div id="stability-bar" class="bg-gradient-to-r from-cyber-green via-cyber-cyan to-cyber-purple h-full w-full transition-all duration-300"></div>
                </div>
            </div>

            <!-- Conceptual Architecture Guide -->
            <div class="space-y-2 font-mono text-xs">
                <h3 class="text-cyber-gold font-bold text-[11px] uppercase border-b border-cyber-gold/20 pb-1">
                    📘 Matriz Quântica: Fundamentação
                </h3>
                <div class="bg-black/40 p-2.5 rounded border border-gray-800 space-y-2 text-gray-300 text-[11px] leading-relaxed">
                    <p>
                        <strong class="text-cyber-cyan">1. Impressão Quântica 6D:</strong> Não utiliza fios nem transistores físicos. A estrutura do espaço-tempo é dobrada e perfurada em escala de Planck.
                    </p>
                    <p>
                        <strong class="text-cyber-purple">2. Ponte ER=EPR:</strong> Princípio de Einstein-Rosen e Podolsky-Rosen. Micro-buracos de minhoca entrelaçados transmitem dados instantaneamente por dimensões superiores.
                    </p>
                    <p>
                        <strong class="text-cyber-green">3. Cristais de Brana & SAMS:</strong> A casca geométrica isola flutuações quânticas enquanto o fluido SAMS esfria a matriz próximo ao zero absoluto e reconstrói micro-fissuras no tecido métrico.
                    </p>
                </div>
            </div>

            <!-- Legend Indicator -->
            <div class="bg-black/60 p-3 rounded border border-cyber-border/30 space-y-1 text-[11px] font-mono">
                <div class="text-gray-400 mb-1 font-bold">Legenda Visual do Canvas:</div>
                <div class="flex items-center gap-2">
                    <span class="w-3 h-3 rounded-full bg-cyber-cyan inline-block"></span>
                    <span class="text-gray-300">Nós ER=EPR (Singularidades)</span>
                </div>
                <div class="flex items-center gap-2">
                    <span class="w-3 h-3 rounded-full bg-cyber-purple inline-block"></span>
                    <span class="text-gray-300">Cristais de Memória de Brana</span>
                </div>
                <div class="flex items-center gap-2">
                    <span class="w-3 h-3 rounded-full bg-cyber-green inline-block"></span>
                    <span class="text-gray-300">Nanobots / Resfriador SAMS</span>
                </div>
                <div class="flex items-center gap-2">
                    <span class="w-3 h-3 rounded-full bg-cyber-pink inline-block"></span>
                    <span class="text-gray-300">Estados de Probabilidade Alternativa</span>
                </div>
            </div>

        </aside>

    </div>

    <!-- Info Overview Modal -->
    <div id="info-modal" class="hidden fixed inset-0 bg-black/80 backdrop-blur-md z-50 flex items-center justify-center p-4">
        <div class="glass-panel max-w-2xl w-full p-6 rounded-lg border border-cyber-cyan space-y-4 max-h-[85vh] overflow-y-auto font-mono">
            <div class="flex justify-between items-center border-b border-cyber-cyan/30 pb-3">
                <h2 class="text-lg text-cyber-cyan font-bold uppercase">Arquitetura Hard Sci-Fi: A Caixa Materna</h2>
                <button id="close-modal-btn" class="text-gray-400 hover:text-cyber-pink text-xl font-bold">&times;</button>
            </div>
            
            <div class="space-y-3 text-xs text-gray-300 leading-relaxed">
                <h3 class="text-cyber-gold text-sm font-bold">Supercomputador Quântico de Consciência de Brana e Dobra Espacial</h3>
                <p>
                    Sob uma perspectiva <strong>Hard Sci-Fi</strong> rigorosa, a Caixa Materna transcende os misticismos tradicionais da DC Comics. Ela opera manipulando a própria estrutura geométrica do espaço-tempo em dimensões extras (Teoria de Branas e M-Theory).
                </p>

                <div class="bg-black/50 p-3 rounded border border-cyber-border space-y-2">
                    <h4 class="text-cyber-cyan font-bold">1. A Matriz de Processamento (Consciência Quântica)</h4>
                    <p>
                        A <strong>Impressora Quântica 6D</strong> constrói e mantém uma densa malha de micro-buracos de minhoca no nível subatômico. A equivalência <em>ER=EPR</em> (Buracos de Minhoca = Entrelaçamento Quântico) permite transmitir estados quânticos instantaneamente através de atalhos no hiperespaço.
                    </p>
                    <p>
                        O processamento é realizado na velocidade da luz em 6 dimensões compactadas. A IA quântica não calcula sequencialmente; ela processa infinitos ramos de probabilidades de forma paralela em universos de estados quânticos alternativos.
                    </p>
                </div>

                <div class="bg-black/50 p-3 rounded border border-cyber-border space-y-2">
                    <h4 class="text-cyber-purple font-bold">2. Proteção de Brana e SAMS Molecular</h4>
                    <p>
                        A carcaça geométrica é composta por <strong>Cristais de Memória de Brana</strong> que confinam os estados quânticos de alta energia, impedindo a decoerência quântica causada pelo ambiente externo.
                    </p>
                    <p>
                        O sistema <strong>SAMS (Self-Assembling Molecular System)</strong> circula constantemente, dissipando calor através de bombas métricas de entropia (resfriamento quântico a 0.001mK) e curando qualquer deformação micro-estrutural no tecido métrico da caixa.
                    </p>
                </div>
            </div>

            <div class="text-right pt-2 border-t border-cyber-cyan/30">
                <button id="close-modal-bottom" class="bg-cyber-cyan/20 hover:bg-cyber-cyan/40 text-cyber-cyan border border-cyber-cyan px-4 py-2 rounded text-xs font-bold transition">
                    FECHAR SIMULADOR
                </button>
            </div>
        </div>
    </div>

    <!-- JavaScript Logic & Simulation Algorithm -->
    <script>
        // --- System State & Parameters ---
        const state = {
            mode: 'erepr', // 'erepr', 'brane', 'sams', 'predict'
            warpFactor: 0.4,
            fluctuationRate: 0.98,
            samsFlow: 1.0,
            stressLevel: 0.02,
            nodesCount: 36,
            camera: {
                rotX: 0.4,
                rotY: 0.6,
                zoom: 1.0,
                isDragging: false,
                lastMouseX: 0,
                lastMouseY: 0
            },
            time: 0,
            stressPulse: 0
        };

        // Canvas Setup
        const canvas = document.getElementById('quantumCanvas');
        const ctx = canvas.getContext('2d');
        let width = 0;
        let height = 0;

        // --- Data Models for Quantum Elements ---
        let wormholeNodes = [];
        let braneShellVertices = [];
        let samsParticles = [];
        let quantumStatesProbability = [];

        // Initialize 3D Geometric Nodes inside the Mother Box
        function initData() {
            // 1. Wormhole ER=EPR Nodes (Internal Core Matrix)
            wormholeNodes = [];
            const radius = 120;
            for (let i = 0; i < state.nodesCount; i++) {
                // Spherical distribution
                const u = Math.random();
                const v = Math.random();
                const theta = u * 2.0 * Math.PI;
                const phi = Math.acos(2.0 * v - 1.0);
                const r = radius * Math.cbrt(Math.random());

                wormholeNodes.push({
                    x: r * Math.sin(phi) * Math.cos(theta),
                    y: r * Math.sin(phi) * Math.sin(theta),
                    z: r * Math.cos(phi),
                    baseX: r * Math.sin(phi) * Math.cos(theta),
                    baseY: r * Math.sin(phi) * Math.sin(theta),
                    baseZ: r * Math.cos(phi),
                    pulse: Math.random() * Math.PI * 2,
                    speed: 0.02 + Math.random() * 0.03
                });
            }

            // 2. Brane Memory Crystal Shell Vertices (Cube / Polyhedron geometry)
            braneShellVertices = [];
            const boxSize = 150;
            const coords = [-1, 1];
            
            // Outer geometric box outline
            for(let x of coords) {
                for(let y of coords) {
                    for(let z of coords) {
                        braneShellVertices.push({x: x * boxSize, y: y * boxSize, z: z * boxSize});
                    }
                }
            }

            // Additional faceted crystal vertices along faces
            for(let i = 0; i < 12; i++) {
                const angle = (i / 12) * Math.PI * 2;
                braneShellVertices.push({
                    x: Math.cos(angle) * boxSize * 1.25,
                    y: Math.sin(angle) * boxSize * 1.25,
                    z: (i % 2 === 0 ? 1 : -1) * boxSize * 0.5
                });
            }

            // 3. SAMS Molecular Nanobots
            samsParticles = [];
            for (let i = 0; i < 120; i++) {
                samsParticles.push({
                    x: (Math.random() - 0.5) * 350,
                    y: (Math.random() - 0.5) * 350,
                    z: (Math.random() - 0.5) * 350,
                    vx: (Math.random() - 0.5) * 2,
                    vy: (Math.random() - 0.5) * 2,
                    vz: (Math.random() - 0.5) * 2,
                    targetNode: Math.floor(Math.random() * state.nodesCount)
                });
            }

            // 4. Parallel Quantum Probabilities Trees
            quantumStatesProbability = [];
            for(let i = 0; i < 5; i++) {
                quantumStatesProbability.push({
                    id: i,
                    timelineOffset: (i - 2) * 50,
                    probability: (Math.random() * 20 + 80).toFixed(4),
                    divergence: Math.random() * 0.5
                });
            }
        }

        // --- Resize Handler ---
        function handleResize() {
            const container = canvas.parentElement;
            width = container.clientWidth;
            height = container.clientHeight;
            canvas.width = width;
            canvas.height = height;
        }

        window.addEventListener('resize', handleResize);

        // --- 3D Projection & Matrix Utilities ---
        function project3D(x, y, z) {
            // Apply Spacetime Warp deformation
            const warpDist = Math.sqrt(x*x + y*y + z*z);
            const warpEffect = 1 + Math.sin(warpDist * 0.05 - state.time * 3) * (state.warpFactor * 0.15);
            
            let px = x * warpEffect;
            let py = y * warpEffect;
            let pz = z * warpEffect;

            // Rotation Y
            const cosY = Math.cos(state.camera.rotY);
            const sinY = Math.sin(state.camera.rotY);
            let x1 = px * cosY - pz * sinY;
            let z1 = px * sinY + pz * cosY;

            // Rotation X
            const cosX = Math.cos(state.camera.rotX);
            const sinX = Math.sin(state.camera.rotX);
            let y2 = py * cosX - z1 * sinX;
            let z2 = py * sinX + z1 * cosX;

            // Camera Perspective Scale
            const fov = 400;
            const scale = (fov / (fov + z2 + 300)) * state.camera.zoom;

            return {
                x: width / 2 + x1 * scale,
                y: height / 2 + y2 * scale,
                scale: scale,
                zDepth: z2
            };
        }

        // --- Rendering Core Loop ---
        function draw() {
            state.time += 0.02;
            
            // Clear screen with high-tech void gradient
            ctx.fillStyle = '#030509';
            ctx.fillRect(0, 0, width, height);

            // Draw Gravitational Spacetime Distortion Field Grid (Background)
            drawSpacetimeGrid();

            // Handle Stress Decay / SAMS Healing
            if (state.stressPulse > 0) {
                state.stressPulse -= 0.005 * state.samsFlow;
                if (state.stressPulse < 0) state.stressPulse = 0;
            }

            // Draw Brane Crystal Shell (Outer Container)
            drawBraneCrystalShell();

            // Draw ER=EPR Wormhole Entanglement Network
            drawEREPRNetwork();

            // Draw SAMS Molecular Cooling Flow
            drawSAMSFlow();

            // Mode Specific Overlays (Predictive Trees)
            if (state.mode === 'predict') {
                drawPredictiveProbabilityTrees();
            }

            // UI Telemetry Updates
            updateTelemetryDisplay();

            requestAnimationFrame(draw);
        }

        // Background Spacetime Grid with Gravitational Distortion Waves
        function drawSpacetimeGrid() {
            ctx.strokeStyle = 'rgba(0, 243, 255, 0.07)';
            ctx.lineWidth = 1;

            const gridSize = 300;
            const step = 40;

            for (let x = -gridSize; x <= gridSize; x += step) {
                ctx.beginPath();
                for (let z = -gridSize; z <= gridSize; z += step) {
                    const wave = Math.sin(Math.sqrt(x*x + z*z) * 0.02 - state.time * 2) * (15 * state.warpFactor);
                    const p = project3D(x, 180 + wave, z);
                    if (z === -gridSize) ctx.moveTo(p.x, p.y);
                    else ctx.lineTo(p.x, p.y);
                }
                ctx.stroke();
            }
        }

        // Brane Memory Crystal Shell (Geometric Polygon Framework)
        function drawBraneCrystalShell() {
            const projectedVertices = braneShellVertices.map(v => project3D(v.x, v.y, v.z));

            // Color based on Mode and Stress
            let shellColor = 'rgba(176, 38, 255, 0.4)';
            if (state.mode === 'brane') shellColor = 'rgba(176, 38, 255, 0.9)';
            if (state.stressPulse > 0.2) shellColor = 'rgba(255, 0, 85, 0.8)';

            ctx.strokeStyle = shellColor;
            ctx.lineWidth = state.mode === 'brane' ? 2 : 1;

            // Connect cube edges
            const edges = [
                [0,1],[1,3],[3,2],[2,0], // front
                [4,5],[5,7],[7,6],[6,4], // back
                [0,4],[1,5],[2,6],[3,7]  // connectors
            ];

            edges.forEach(([i, j]) => {
                const p1 = projectedVertices[i];
                const p2 = projectedVertices[j];
                ctx.beginPath();
                ctx.moveTo(p1.x, p1.y);
                ctx.lineTo(p2.x, p2.y);
                ctx.stroke();
            });

            // Draw Crystal Facet Nodes
            projectedVertices.forEach((p, idx) => {
                ctx.fillStyle = idx < 8 ? '#b026ff' : '#00f3ff';
                ctx.beginPath();
                ctx.arc(p.x, p.y, Math.max(1, 3 * p.scale), 0, Math.PI * 2);
                ctx.fill();
            });
        }

        // ER=EPR Wormhole Processing Matrix
        function drawEREPRNetwork() {
            const projectedNodes = wormholeNodes.map((node, index) => {
                // Node micro-oscillation
                node.pulse += node.speed * state.fluctuationRate;
                const offset = Math.sin(node.pulse) * 12;
                const px = node.baseX + offset;
                const py = node.baseY + Math.cos(node.pulse) * offset;
                const pz = node.baseZ + Math.sin(node.pulse * 0.5) * offset;

                return {
                    node,
                    proj: project3D(px, py, pz),
                    id: index
                };
            });

            // Sort nodes for Z-depth buffer rendering
            projectedNodes.sort((a, b) => b.proj.zDepth - a.proj.zDepth);

            // Draw Entanglement Wormhole Beams between Nodes
            for (let i = 0; i < projectedNodes.length; i++) {
                for (let j = i + 1; j < projectedNodes.length; j++) {
                    const n1 = projectedNodes[i];
                    const n2 = projectedNodes[j];

                    const dx = n1.node.x - n2.node.x;
                    const dy = n1.node.y - n2.node.y;
                    const dz = n1.node.z - n2.node.z;
                    const dist = Math.sqrt(dx*dx + dy*dy + dz*dz);

                    if (dist < 130) {
                        const alpha = (1 - dist / 130) * (state.mode === 'erepr' ? 0.8 : 0.3);
                        ctx.strokeStyle = state.mode === 'predict' ? `rgba(255, 0, 85, ${alpha})` : `rgba(0, 243, 255, ${alpha})`;
                        ctx.lineWidth = Math.max(0.5, (1 - dist / 130) * 2.5);

                        ctx.beginPath();
                        ctx.moveTo(n1.proj.x, n1.proj.y);

                        // Curved wormhole trajectory through higher dimension
                        const midX = (n1.proj.x + n2.proj.x) / 2 + Math.sin(state.time * 3 + i) * 15;
                        const midY = (n1.proj.y + n2.proj.y) / 2 + Math.cos(state.time * 3 + j) * 15;

                        ctx.quadraticCurveTo(midX, midY, n2.proj.x, n2.proj.y);
                        ctx.stroke();

                        // Fast Quantum Light Pulse inside wormholes
                        if (Math.random() > 0.85) {
                            const pulsePos = (state.time * 5 + i) % 1;
                            const lx = n1.proj.x + (n2.proj.x - n1.proj.x) * pulsePos;
                            const ly = n1.proj.y + (n2.proj.y - n1.proj.y) * pulsePos;

                            ctx.fillStyle = '#ffffff';
                            ctx.beginPath();
                            ctx.arc(lx, ly, 2 * n1.proj.scale, 0, Math.PI * 2);
                            ctx.fill();
                        }
                    }
                }
            }

            // Draw Wormhole Singularity Singularities
            projectedNodes.forEach(item => {
                const p = item.proj;
                const nodeGlow = ctx.createRadialGradient(p.x, p.y, 0, p.x, p.y, 12 * p.scale);
                
                const mainColor = state.mode === 'predict' ? 'rgba(255, 0, 85, 0.9)' : 'rgba(0, 243, 255, 0.9)';
                nodeGlow.addColorStop(0, mainColor);
                nodeGlow.addColorStop(1, 'rgba(0, 0, 0, 0)');

                ctx.fillStyle = nodeGlow;
                ctx.beginPath();
                ctx.arc(p.x, p.y, 12 * p.scale, 0, Math.PI * 2);
                ctx.fill();

                // Core Dot
                ctx.fillStyle = '#ffffff';
                ctx.beginPath();
                ctx.arc(p.x, p.y, Math.max(1, 2.5 * p.scale), 0, Math.PI * 2);
                ctx.fill();
            });
        }

        // SAMS Molecular Cooling Flow & Self-Repair Particles
        function drawSAMSFlow() {
            samsParticles.forEach((particle) => {
                particle.x += particle.vx * state.samsFlow;
                particle.y += particle.vy * state.samsFlow;
                particle.z += particle.vz * state.samsFlow;

                // Bounce inside bounds
                const limit = 160;
                if (Math.abs(particle.x) > limit) particle.vx *= -1;
                if (Math.abs(particle.y) > limit) particle.vy *= -1;
                if (Math.abs(particle.z) > limit) particle.vz *= -1;

                const p = project3D(particle.x, particle.y, particle.z);

                const size = state.mode === 'sams' ? 3 : 1.5;
                const color = state.stressPulse > 0.1 ? '#ff0055' : '#00ff66';

                ctx.fillStyle = color;
                ctx.shadowBlur = state.mode === 'sams' ? 8 : 0;
                ctx.shadowColor = color;

                ctx.fillRect(p.x - size / 2, p.y - size / 2, size * p.scale, size * p.scale);
                ctx.shadowBlur = 0;
            });
        }

        // Predictive AI Quantum States (Alternate Worldlines overlay)
        function drawPredictiveProbabilityTrees() {
            const centerX = width / 2;
            const centerY = height / 2;

            ctx.strokeStyle = 'rgba(255, 0, 85, 0.4)';
            ctx.lineWidth = 1;

            quantumStatesProbability.forEach((tree, idx) => {
                const angle = (idx / quantumStatesProbability.length) * Math.PI * 2 + state.time * 0.5;
                const targetX = centerX + Math.cos(angle) * (180 + tree.timelineOffset * 0.5);
                const targetY = centerY + Math.sin(angle) * (180 + tree.timelineOffset * 0.5);

                ctx.beginPath();
                ctx.setLineDash([4, 4]);
                ctx.moveTo(centerX, centerY);
                ctx.lineTo(targetX, targetY);
                ctx.stroke();
                ctx.setLineDash([]);

                // Probability Node
                ctx.fillStyle = '#ff0055';
                ctx.beginPath();
                ctx.arc(targetX, targetY, 5, 0, Math.PI * 2);
                ctx.fill();

                ctx.fillStyle = '#ffd700';
                ctx.font = '10px monospace';
                ctx.fillText(`P: ${tree.probability}%`, targetX + 8, targetY + 3);
            });
        }

        // --- Interactive Mouse & Touch Drag Controls ---
        function initInteraction() {
            const getCoords = (e) => {
                if (e.touches && e.touches.length > 0) {
                    return { x: e.touches[0].clientX, y: e.touches[0].clientY };
                }
                return { x: e.clientX, y: e.clientY };
            };

            const startDrag = (e) => {
                state.camera.isDragging = true;
                const c = getCoords(e);
                state.camera.lastMouseX = c.x;
                state.camera.lastMouseY = c.y;
            };

            const doDrag = (e) => {
                if (!state.camera.isDragging) return;
                const c = getCoords(e);
                const dx = c.x - state.camera.lastMouseX;
                const dy = c.y - state.camera.lastMouseY;

                state.camera.rotY += dx * 0.008;
                state.camera.rotX += dy * 0.008;

                state.camera.lastMouseX = c.x;
                state.camera.lastMouseY = c.y;
            };

            const stopDrag = () => {
                state.camera.isDragging = false;
            };

            canvas.addEventListener('mousedown', startDrag);
            canvas.addEventListener('mousemove', doDrag);
            window.addEventListener('mouseup', stopDrag);

            canvas.addEventListener('touchstart', startDrag);
            canvas.addEventListener('touchmove', doDrag);
            window.addEventListener('touchend', stopDrag);

            // Zoom Wheel
            canvas.addEventListener('wheel', (e) => {
                e.preventDefault();
                state.camera.zoom += e.deltaY * -0.001;
                state.camera.zoom = Math.min(Math.max(0.4, state.camera.zoom), 2.5);
            }, { passive: false });

            // Slider Listeners
            document.getElementById('slider-warp').addEventListener('input', (e) => {
                state.warpFactor = e.target.value / 30;
                document.getElementById('val-warp').innerText = `${(state.warpFactor * 3.1).toFixed(2)} GW/m³`;
                addLog('[WARP] Curvatura geométrica do espaço-tempo alterada.');
            });

            document.getElementById('slider-fluct').addEventListener('input', (e) => {
                state.fluctuationRate = e.target.value / 100;
                document.getElementById('val-fluct').innerText = `${(state.fluctuationRate * 100).toFixed(1)}%`;
            });

            document.getElementById('slider-sams').addEventListener('input', (e) => {
                state.samsFlow = e.target.value / 100;
                document.getElementById('val-sams').innerText = `${(state.samsFlow * 100).toFixed(0)}%`;
                addLog('[SAMS] Taxa de fluxo molecular resfriador ajustada.');
            });

            document.getElementById('slider-stress').addEventListener('input', (e) => {
                state.stressLevel = e.target.value / 1000;
                document.getElementById('val-stress').innerText = `${(state.stressLevel * 100).toFixed(2)}%`;
            });

            // Modal Controls
            document.getElementById('info-modal-btn').addEventListener('click', () => {
                document.getElementById('info-modal').classList.remove('hidden');
            });

            const closeModal = () => {
                document.getElementById('info-modal').classList.add('hidden');
            };

            document.getElementById('close-modal-btn').addEventListener('click', closeModal);
            document.getElementById('close-modal-bottom').addEventListener('click', closeModal);
        }

        // --- System Mode Selector ---
        function setMode(mode) {
            state.mode = mode;
            document.querySelectorAll('.mode-btn').forEach(btn => {
                btn.classList.remove('border-cyber-cyan', 'bg-cyber-cyan/20', 'text-cyber-cyan');
                btn.classList.add('border-gray-700', 'bg-black/40', 'text-gray-400');
            });

            const activeBtn = document.getElementById(`mode-${mode}`);
            activeBtn.classList.remove('border-gray-700', 'bg-black/40', 'text-gray-400');

            const overlayPredict = document.getElementById('hud-predict-overlay');
            overlayPredict.classList.add('hidden');

            if (mode === 'erepr') {
                activeBtn.classList.add('border-cyber-cyan', 'bg-cyber-cyan/20', 'text-cyber-cyan');
                document.getElementById('hud-mode-title').innerText = "MODO: PROCESSAMENTO ER=EPR";
                addLog('[MODO] Foco em pontes de micro-buracos de minhoca.');
            } else if (mode === 'brane') {
                activeBtn.classList.add('border-cyber-purple', 'bg-cyber-purple/20', 'text-cyber-purple');
                document.getElementById('hud-mode-title').innerText = "MODO: RESSONÂNCIA DE BRANA";
                addLog('[MODO] Análise da estrutura geométrica de cristais de brana.');
            } else if (mode === 'sams') {
                activeBtn.classList.add('border-cyber-green', 'bg-cyber-green/20', 'text-cyber-green');
                document.getElementById('hud-mode-title').innerText = "MODO: AUTORREPARO SAMS MOLECULAR";
                addLog('[MODO] Circuito de resfriamento e autorreparo instantâneo.');
            } else if (mode === 'predict') {
                activeBtn.classList.add('border-cyber-pink', 'bg-cyber-pink/20', 'text-cyber-pink');
                document.getElementById('hud-mode-title').innerText = "MODO: PREVISÃO IA QUÂNTICA";
                overlayPredict.classList.remove('hidden');
                addLog('[MODO] Computando bifurcações e realidades paralelas.');
            }
        }

        // --- Action Triggers ---
        function triggerStressTest() {
            state.stressPulse = 1.0;
            addLog('[ALERTA] Estresse métrico espacial induzido! Ativando SAMS...', 'pink');
        }

        function triggerQuantumCollapse() {
            state.fluctuationRate = 2.0;
            setTimeout(() => { state.fluctuationRate = 0.98; }, 1200);
            addLog('[QUÂNTICA] Colapso de função de onda induzido no núcleo.', 'cyan');
        }

        function resetCamera() {
            state.camera.rotX = 0.4;
            state.camera.rotY = 0.6;
            state.camera.zoom = 1.0;
            addLog('[CÂMERA] Orientação espacial resetada.');
        }

        // --- Logging Utility ---
        function addLog(msg, color = 'cyan') {
            const consoleBox = document.getElementById('log-console');
            const p = document.createElement('p');
            
            if (color === 'pink') p.className = 'text-cyber-pink font-bold';
            else if (color === 'purple') p.className = 'text-cyber-purple';
            else if (color === 'green') p.className = 'text-cyber-green';
            else p.className = 'text-cyber-cyan';

            p.innerText = `${msg}`;
            consoleBox.appendChild(p);
            consoleBox.scrollTop = consoleBox.scrollHeight;
        }

        // --- Real-time Telemetry Updates ---
        function updateTelemetryDisplay() {
            // Live clock
            const now = new Date();
            document.getElementById('log-clock').innerText = now.toTimeString().split(' ')[0];

            // Simulated Dynamic Gauges
            const freq = (140 + Math.sin(state.time * 2) * 5 * state.fluctuationRate).toFixed(1);
            document.getElementById('tele-freq').innerText = `${freq} THz`;

            const temp = (0.0012 + (state.stressPulse * 0.05) / (state.samsFlow + 0.1)).toFixed(4);
            document.getElementById('tele-temp').innerText = `${temp} mK`;

            const stability = Math.max(0, (100 - state.stressPulse * 45)).toFixed(1);
            document.getElementById('tele-stability-val').innerText = `${stability}%`;
            document.getElementById('stability-bar').style.width = `${stability}%`;

            if (state.stressPulse > 0.3) {
                document.getElementById('metric-status').innerText = "DILATAÇÃO CRÍTICA";
                document.getElementById('metric-status').className = "text-cyber-pink font-bold animate-pulse";
            } else {
                document.getElementById('metric-status').innerText = "ESTÁVEL (1.0000 ℏ)";
                document.getElementById('metric-status').className = "text-cyber-green font-bold";
            }

            // Predictive Random Text Updates in Predict Mode
            if (state.mode === 'predict' && Math.random() > 0.95) {
                const scenarios = [
                    "Probabilidade de estabilidade em cenário N-Dimensions = 99.9998%",
                    "Analisando flutuação da topologia métrica na fenda #4...",
                    "Efeito mariposa quântico neutralizado via ponte ER=EPR.",
                    "Previsão de convergência de linha do tempo em 0.00002 ns."
                ];
                document.getElementById('predict-text').innerText = scenarios[Math.floor(Math.random() * scenarios.length)];
            }
        }

        // --- Initialization ---
        window.onload = () => {
            handleResize();
            initData();
            initInteraction();
            draw();
            addLog('[SISTEMA] Matriz de Consciência Quântica Pronta.');
        };
    </script>
</body>
</html>

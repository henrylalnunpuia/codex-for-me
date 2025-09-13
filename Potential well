<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Finite Potential Well - 3Blue1Brown Style</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Computer+Modern+Serif&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Computer Modern Serif', 'Times New Roman', serif;
            background: linear-gradient(135deg, #1e1e2e 0%, #0a0a0f 100%);
            color: #ffffff;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            width: 100%;
        }
        
        h1 {
            text-align: center;
            font-size: 2.5em;
            margin-bottom: 10px;
            background: linear-gradient(90deg, #56CCF2, #2F80ED, #56CCF2);
            background-size: 200% auto;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: shine 3s linear infinite;
        }
        
        @keyframes shine {
            to { background-position: 200% center; }
        }
        
        .subtitle {
            text-align: center;
            color: #8888aa;
            margin-bottom: 30px;
            font-size: 1.1em;
        }
        
        .main-canvas {
            background: #0a0a0f;
            border-radius: 15px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.5);
            margin-bottom: 30px;
            position: relative;
            overflow: hidden;
        }
        
        canvas {
            display: block;
            width: 100%;
            cursor: crosshair;
        }
        
        .controls {
            background: rgba(30, 30, 46, 0.8);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 20px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.3);
        }
        
        .control-group {
            margin-bottom: 20px;
        }
        
        .control-group label {
            display: block;
            margin-bottom: 8px;
            color: #56CCF2;
            font-size: 1.1em;
            font-weight: 500;
        }
        
        .slider-container {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        input[type="range"] {
            flex: 1;
            height: 6px;
            background: #2a2a3e;
            border-radius: 3px;
            outline: none;
            -webkit-appearance: none;
        }
        
        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 20px;
            height: 20px;
            background: #56CCF2;
            border-radius: 50%;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 0 10px rgba(86, 204, 242, 0.5);
        }
        
        input[type="range"]::-webkit-slider-thumb:hover {
            transform: scale(1.2);
            box-shadow: 0 0 20px rgba(86, 204, 242, 0.8);
        }
        
        .value-display {
            min-width: 60px;
            text-align: right;
            color: #ffffff;
            font-size: 1.1em;
            font-weight: bold;
        }
        
        .button-group {
            display: flex;
            gap: 15px;
            margin-top: 25px;
        }
        
        button {
            flex: 1;
            padding: 12px 24px;
            background: linear-gradient(135deg, #56CCF2, #2F80ED);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1.1em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(86, 204, 242, 0.3);
        }
        
        button:hover:not(:disabled) {
            transform: translateY(-2px);
            box-shadow: 0 6px 25px rgba(86, 204, 242, 0.5);
        }
        
        button:active:not(:disabled) {
            transform: translateY(0);
        }
        
        button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
        
        .info-panel {
            background: rgba(30, 30, 46, 0.6);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 20px;
            color: #cccccc;
            line-height: 1.8;
        }
        
        .equation {
            background: rgba(0, 0, 0, 0.3);
            padding: 15px;
            border-radius: 8px;
            margin: 15px 0;
            text-align: center;
            font-size: 1.2em;
            color: #56CCF2;
            border: 1px solid rgba(86, 204, 242, 0.3);
        }
        
        .legend {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-top: 15px;
            flex-wrap: wrap;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .legend-color {
            width: 20px;
            height: 3px;
            border-radius: 2px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Finite Potential Well</h1>
        <p class="subtitle">Interactive Quantum Mechanics Visualization</p>
        
        <div class="main-canvas">
            <canvas id="canvas"></canvas>
        </div>
        
        <div class="controls">
            <div class="control-group">
                <label>Well Depth (V₀)</label>
                <div class="slider-container">
                    <input type="range" id="wellDepth" min="5" max="50" value="20" step="1">
                    <span class="value-display" id="wellDepthValue">20 eV</span>
                </div>
            </div>
            
            <div class="control-group">
                <label>Well Width (2a)</label>
                <div class="slider-container">
                    <input type="range" id="wellWidth" min="1" max="5" value="2" step="0.1">
                    <span class="value-display" id="wellWidthValue">2.0 nm</span>
                </div>
            </div>
            
            <div class="control-group">
                <label>Energy Level (n)</label>
                <div class="slider-container">
                    <input type="range" id="energyLevel" min="1" max="5" value="1" step="1">
                    <span class="value-display" id="energyLevelValue">n = 1</span>
                </div>
            </div>
            
            <div class="control-group">
                <label>Animation Speed</label>
                <div class="slider-container">
                    <input type="range" id="animSpeed" min="0" max="2" value="1" step="0.1">
                    <span class="value-display" id="animSpeedValue">1.0x</span>
                </div>
            </div>
            
            <div class="button-group">
                <button id="playPause">Pause</button>
                <button id="showProbability">Show Probability</button>
                <button id="reset">Reset</button>
            </div>
            
            <div class="legend">
                <div class="legend-item">
                    <div class="legend-color" style="background: #56CCF2;"></div>
                    <span>Wavefunction ψ(x)</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color" style="background: #FF6B6B;"></div>
                    <span>Probability |ψ(x)|²</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color" style="background: #4ECDC4;"></div>
                    <span>Energy Level</span>
                </div>
            </div>
        </div>
        
        <div class="info-panel">
            <h3 style="color: #56CCF2; margin-bottom: 15px;">Understanding the Finite Potential Well</h3>
            <p>
                The finite potential well is a fundamental quantum mechanical system where a particle is confined by a potential that has finite height. Unlike the infinite well, the wavefunction can penetrate into the classically forbidden regions.
            </p>
            
            <div class="equation">
                -ℏ²/2m · d²ψ/dx² + V(x)ψ = Eψ
            </div>
            
            <p>
                <strong>Key Features:</strong><br>
                • The wavefunction decays exponentially outside the well<br>
                • Only discrete energy levels exist for bound states (E < V₀)<br>
                • Higher energy states have greater penetration depth<br>
                • The number of bound states depends on well depth and width
            </p>
            
            <p style="margin-top: 15px;">
                <strong>Interactive Features:</strong><br>
                • Click and drag on the visualization to explore different regions<br>
                • Adjust parameters to see how they affect the wavefunction<br>
                • Observe the continuity of ψ and dψ/dx at boundaries
            </p>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        
        // Set canvas size
        function resizeCanvas() {
            canvas.width = canvas.offsetWidth * window.devicePixelRatio;
            canvas.height = 500 * window.devicePixelRatio;
            ctx.scale(window.devicePixelRatio, window.devicePixelRatio);
            canvas.style.height = '500px';
        }
        resizeCanvas();
        window.addEventListener('resize', resizeCanvas);
        
        // Animation variables
        let animationId;
        let time = 0;
        let isPlaying = true;
        let showProbability = false;
        let mouseX = 0;
        let mouseY = 0;
        let isMouseOver = false;
        
        // Physics parameters
        let V0 = 20; // Well depth in eV
        let wellWidth = 2; // nm
        let n = 1; // Energy level
        let animSpeed = 1;
        
        // Colors
        const colors = {
            background: '#0a0a0f',
            grid: 'rgba(255, 255, 255, 0.05)',
            axes: 'rgba(255, 255, 255, 0.2)',
            well: 'rgba(86, 204, 242, 0.2)',
            wellBorder: '#56CCF2',
            wavefunction: '#56CCF2',
            probability: '#FF6B6B',
            energy: '#4ECDC4',
            text: '#ffffff'
        };
        
        // Calculate energy levels and wavefunctions
        function calculateWavefunction(x, n, t) {
            const a = wellWidth / 2;
            const k = n * Math.PI / (2 * a);
            const E = (n * n * Math.PI * Math.PI) / (8 * a * a) * 5; // Simplified energy
            
            if (E >= V0) return 0; // No bound state
            
            const alpha = Math.sqrt(2 * (V0 - E));
            const phase = E * t * animSpeed;
            
            let psi;
            if (Math.abs(x) <= a) {
                // Inside the well
                if (n % 2 === 1) {
                    psi = Math.cos(k * x);
                } else {
                    psi = Math.sin(k * x);
                }
            } else {
                // Outside the well
                const decay = Math.exp(-alpha * (Math.abs(x) - a));
                if (x > a) {
                    psi = Math.cos(k * a) * decay;
                } else {
                    psi = (n % 2 === 1 ? 1 : -1) * Math.cos(k * a) * decay;
                }
            }
            
            // Add time evolution
            const real = psi * Math.cos(phase);
            const imag = psi * Math.sin(phase);
            
            return showProbability ? psi * psi : real;
        }
        
        // Draw the visualization
        function draw() {
            const width = canvas.width / window.devicePixelRatio;
            const height = canvas.height / window.devicePixelRatio;
            
            // Clear canvas
            ctx.fillStyle = colors.background;
            ctx.fillRect(0, 0, width, height);
            
            // Draw grid
            ctx.strokeStyle = colors.grid;
            ctx.lineWidth = 1;
            for (let i = 0; i <= 10; i++) {
                const x = (width / 10) * i;
                const y = (height / 10) * i;
                ctx.beginPath();
                ctx.moveTo(x, 0);
                ctx.lineTo(x, height);
                ctx.stroke();
                ctx.beginPath();
                ctx.moveTo(0, y);
                ctx.lineTo(width, y);
                ctx.stroke();
            }
            
            // Draw axes
            ctx.strokeStyle = colors.axes;
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.moveTo(0, height / 2);
            ctx.lineTo(width, height / 2);
            ctx.stroke();
            ctx.beginPath();
            ctx.moveTo(width / 2, 0);
            ctx.lineTo(width / 2, height);
            ctx.stroke();
            
            // Draw potential well
            const wellPixelWidth = wellWidth * width / 10;
            const wellLeft = (width - wellPixelWidth) / 2;
            const wellRight = (width + wellPixelWidth) / 2;
            const wellBottom = height / 2 + V0 * 3;
            
            // Well fill
            ctx.fillStyle = colors.well;
            ctx.fillRect(wellLeft, height / 2, wellPixelWidth, wellBottom - height / 2);
            
            // Well borders
            ctx.strokeStyle = colors.wellBorder;
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.moveTo(0, wellBottom);
            ctx.lineTo(wellLeft, wellBottom);
            ctx.lineTo(wellLeft, height / 2);
            ctx.lineTo(wellRight, height / 2);
            ctx.lineTo(wellRight, wellBottom);
            ctx.lineTo(width, wellBottom);
            ctx.stroke();
            
            // Draw energy level
            const E = (n * n * Math.PI * Math.PI) / (8 * wellWidth * wellWidth) * 5;
            if (E < V0) {
                const energyY = height / 2 + E * 3;
                ctx.strokeStyle = colors.energy;
                ctx.lineWidth = 2;
                ctx.setLineDash([5, 5]);
                ctx.beginPath();
                ctx.moveTo(0, energyY);
                ctx.lineTo(width, energyY);
                ctx.stroke();
                ctx.setLineDash([]);
                
                // Energy label
                ctx.fillStyle = colors.energy;
                ctx.font = '14px Computer Modern Serif';
                ctx.fillText(`E${n} = ${E.toFixed(1)} eV`, 10, energyY - 5);
            }
            
            // Draw wavefunction
            ctx.strokeStyle = showProbability ? colors.probability : colors.wavefunction;
            ctx.lineWidth = 3;
            ctx.beginPath();
            
            for (let px = 0; px <= width; px++) {
                const x = (px - width / 2) / (width / 10);
                const psi = calculateWavefunction(x, n, time);
                const y = height / 2 - psi * 100;
                
                if (px === 0) {
                    ctx.moveTo(px, y);
                } else {
                    ctx.lineTo(px, y);
                }
            }
            ctx.stroke();
            
            // Draw mouse indicator
            if (isMouseOver) {
                const x = (mouseX - width / 2) / (width / 10);
                const psi = calculateWavefunction(x, n, time);
                const y = height / 2 - psi * 100;
                
                ctx.fillStyle = colors.wavefunction;
                ctx.beginPath();
                ctx.arc(mouseX, y, 5, 0, Math.PI * 2);
                ctx.fill();
                
                // Show value
                ctx.fillStyle = colors.text;
                ctx.font = '12px Computer Modern Serif';
                const label = showProbability ? `|ψ|² = ${(psi).toFixed(3)}` : `ψ = ${psi.toFixed(3)}`;
                ctx.fillText(label, mouseX + 10, y - 10);
                ctx.fillText(`x = ${x.toFixed(2)} nm`, mouseX + 10, y + 20);
            }
            
            // Labels
            ctx.fillStyle = colors.text;
            ctx.font = '16px Computer Modern Serif';
            ctx.fillText('Position (nm)', width - 100, height / 2 - 10);
            ctx.save();
            ctx.translate(15, height / 2);
            ctx.rotate(-Math.PI / 2);
            ctx.fillText('Wavefunction', 0, 0);
            ctx.restore();
        }
        
        // Animation loop
        function animate() {
            if (isPlaying) {
                time += 0.05;
            }
            draw();
            animationId = requestAnimationFrame(animate);
        }
        
        // Event listeners
        document.getElementById('wellDepth').addEventListener('input', (e) => {
            V0 = parseFloat(e.target.value);
            document.getElementById('wellDepthValue').textContent = `${V0} eV`;
        });
        
        document.getElementById('wellWidth').addEventListener('input', (e) => {
            wellWidth = parseFloat(e.target.value);
            document.getElementById('wellWidthValue').textContent = `${wellWidth.toFixed(1)} nm`;
        });
        
        document.getElementById('energyLevel').addEventListener('input', (e) => {
            n = parseInt(e.target.value);
            document.getElementById('energyLevelValue').textContent = `n = ${n}`;
        });
        
        document.getElementById('animSpeed').addEventListener('input', (e) => {
            animSpeed = parseFloat(e.target.value);
            document.getElementById('animSpeedValue').textContent = `${animSpeed.toFixed(1)}x`;
        });
        
        document.getElementById('playPause').addEventListener('click', (e) => {
            isPlaying = !isPlaying;
            e.target.textContent = isPlaying ? 'Pause' : 'Play';
        });
        
        document.getElementById('showProbability').addEventListener('click', (e) => {
            showProbability = !showProbability;
            e.target.textContent = showProbability ? 'Show Wavefunction' : 'Show Probability';
        });
        
        document.getElementById('reset').addEventListener('click', () => {
            V0 = 20;
            wellWidth = 2;
            n = 1;
            animSpeed = 1;
            time = 0;
            document.getElementById('wellDepth').value = 20;
            document.getElementById('wellDepthValue').textContent = '20 eV';
            document.getElementById('wellWidth').value = 2;
            document.getElementById('wellWidthValue').textContent = '2.0 nm';
            document.getElementById('energyLevel').value = 1;
            document.getElementById('energyLevelValue').textContent = 'n = 1';
            document.getElementById('animSpeed').value = 1;
            document.getElementById('animSpeedValue').textContent = '1.0x';
        });
        
        canvas.addEventListener('mousemove', (e) => {
            const rect = canvas.getBoundingClientRect();
            mouseX = e.clientX - rect.left;
            mouseY = e.clientY - rect.top;
            isMouseOver = true;
        });
        
        canvas.addEventListener('mouseleave', () => {
            isMouseOver = false;
        });
        
        // Start animation
        animate();
    </script>
</body>
</html>

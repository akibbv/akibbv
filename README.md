<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Akib | Computer Science Student</title>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Fira+Code:wght@400;500&display=swap" rel="stylesheet">
    <!-- FontAwesome for Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --bg-color: #0f172a;
            --card-bg: rgba(30, 41, 59, 0.85); /* Semi-transparent cards */
            --text-primary: #f8fafc;
            --text-secondary: #94a3b8;
            --accent: #38bdf8;
            --accent-glow: rgba(56, 189, 248, 0.15);
            --border: #334155;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--bg-color);
            color: var(--text-primary);
            line-height: 1.6;
            overflow-x: hidden;
            position: relative;
        }

        /* --- Animated Background Canvas --- */
        canvas#bg-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1; /* Pushes canvas behind all content */
            opacity: 0.6; /* Subdued so it's not distracting */
        }

        /* --- Content Styling --- */
        .container {
            max-width: 900px;
            margin: 0 auto;
            padding: 2rem 1.5rem;
            position: relative;
            z-index: 1; /* Ensures content sits on top of canvas */
        }

        header {
            padding: 4rem 0 2rem;
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }

        .badge {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            background-color: var(--card-bg);
            color: var(--accent);
            padding: 0.4rem 0.8rem;
            border-radius: 50px;
            font-size: 0.85rem;
            font-weight: 500;
            width: fit-content;
            border: 1px solid var(--border);
            font-family: 'Fira Code', monospace;
        }

        h1 {
            font-size: 3rem;
            font-weight: 700;
            letter-spacing: -0.025em;
        }

        h1 span {
            color: var(--accent);
        }

        /* --- Title Transition Styling --- */
        .title-transition-container {
            font-size: 1.2rem;
            color: var(--text-secondary);
            height: 2rem;
            display: flex;
            align-items: center;
            overflow: hidden;
        }

        .typing-text {
            border-right: 2px solid var(--accent);
            white-space: nowrap;
            animation: blink 0.75s step-end infinite;
        }

        @keyframes blink {
            from, to { border-color: transparent }
            50% { border-color: var(--accent); }
        }

        .socials {
            display: flex;
            gap: 1rem;
            margin-top: 0.5rem;
        }

        .social-btn {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            background-color: var(--card-bg);
            color: var(--text-primary);
            padding: 0.6rem 1.2rem;
            border-radius: 8px;
            text-decoration: none;
            font-size: 0.9rem;
            font-weight: 500;
            border: 1px solid var(--border);
            transition: all 0.2s ease;
        }

        .social-btn:hover {
            border-color: var(--accent);
            background-color: var(--accent-glow);
            color: var(--accent);
        }

        section {
            margin: 3rem 0;
        }

        h2 {
            font-size: 1.5rem;
            margin-bottom: 1.5rem;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        h2 i {
            color: var(--accent);
            font-size: 1.2rem;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 1.25rem;
        }

        .card {
            background-color: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 1.5rem;
            transition: transform 0.2s ease, border-color 0.2s ease;
            backdrop-filter: blur(4px); /* Applies slight blur effect behind cards */
        }

        .card:hover {
            transform: translateY(-3px);
            border-color: var(--accent);
        }

        .card h3 {
            font-size: 1.1rem;
            margin-bottom: 0.75rem;
            color: var(--text-primary);
        }

        .card p {
            color: var(--text-secondary);
            font-size: 0.95rem;
        }

        .tech-list {
            display: flex;
            flex-wrap: wrap;
            gap: 0.5rem;
            margin-top: 0.5rem;
        }

        .tech-tag {
            background-color: rgba(15, 23, 42, 0.6);
            color: var(--text-secondary);
            padding: 0.3rem 0.6rem;
            border-radius: 6px;
            font-size: 0.8rem;
            font-family: 'Fira Code', monospace;
            border: 1px solid var(--border);
        }

        footer {
            text-align: center;
            padding: 3rem 0 2rem;
            color: var(--text-secondary);
            font-size: 0.85rem;
            border-top: 1px solid var(--border);
            margin-top: 4rem;
        }

        @media (max-width: 600px) {
            h1 {
                font-size: 2.25rem;
            }
            .container {
                padding: 1rem;
            }
        }
    </style>
</head>
<body>

    <!-- The Live Background -->
    <canvas id="bg-canvas"></canvas>

    <div class="container">
        <header>
            <div class="badge">
                <i class="fa-solid fa-terminal"></i> CS Student @ BRACU
            </div>
            <h1>Hi, I'm <span>Akib</span></h1>
            
            <!-- Dynamic Typing Title Transition -->
            <div class="title-transition-container">
                <span class="typing-text" id="typing-output"></span>
            </div>
            
            <div class="socials">
                <a href="https://github.com/akibbv" target="_blank" class="social-btn">
                    <i class="fa-brands fa-github"></i> GitHub (@akibbv)
                </a>
            </div>
        </header>

        <section>
            <h2><i class="fa-solid fa-user-astronaut"></i> About Me</h2>
            <div class="card">
                <p>I'm an undergraduate Computer Science student focusing heavily on core engineering principles, efficient algorithmic design, and low-level data structure implementations from scratch. Always eager to turn logical problems into optimized solutions.</p>
            </div>
        </section>

        <section>
            <h2><i class="fa-solid fa-laptop-code"></i> Projects & Current Focus</h2>
            <div class="card">
                <h3>University Course Projects</h3>
                <p>Currently deep-diving into rigorous university course projects, implementing advanced data structures, graph traversal algorithms, and hardware-software logic from scratch. Every project is an exercise in clean code and optimized performance without relying on built-in shortcuts.</p>
            </div>
        </section>

        <section>
            <h2><i class="fa-solid fa-layer-group"></i> Tech Stack & Tools</h2>
            <div class="grid">
                <div class="card">
                    <h3>Languages</h3>
                    <div class="tech-list">
                        <span class="tech-tag">Java</span>
                        <span class="tech-tag">C</span>
                        <span class="tech-tag">C++</span>
                    </div>
                </div>
                <div class="card">
                    <h3>Core Concepts</h3>
                    <div class="tech-list">
                        <span class="tech-tag">Data Structures</span>
                        <span class="tech-tag">Algorithms</span>
                        <span class="tech-tag">Graph Theory</span>
                        <span class="tech-tag">Digital Logic</span>
                    </div>
                </div>
                <div class="card">
                    <h3>Workflow & Tools</h3>
                    <div class="tech-list">
                        <span class="tech-tag">Git & GitHub</span>
                        <span class="tech-tag">AI Assistants</span>
                        <span class="tech-tag">CLI</span>
                    </div>
                </div>
            </div>
        </section>

        <section>
            <h2><i class="fa-solid fa-dice"></i> Beyond the Code</h2>
            <div class="card">
                <h3>What I Enjoy</h3>
                <p>When I'm not debugging algorithms or working through course modules, you'll find me sharpening my problem-solving skills with competitive programming puzzles, reverse-engineering how underlying systems work, or discovering neat ways to structure logic cleanly.</p>
            </div>
        </section>

        <footer>
            <p>&copy; 2026 Akib. Built with clean code & coffee.</p>
        </footer>
    </div>

    <!-- JavaScript for Binary Rain Animation & Typing Transition -->
    <script>
        // --- Binary Rain Animation ---
        const canvas = document.getElementById('bg-canvas');
        const ctx = canvas.getContext('2d');

        let width, height, columns;
        let drops = [];
        const chars = "01";

        function init() {
            width = canvas.width = window.innerWidth;
            height = canvas.height = window.innerHeight;
            const fontSize = 16;
            columns = width / fontSize;

            drops = [];
            for (let x = 0; x < columns; x++) {
                drops[x] = 1;
            }
        }

        function draw() {
            ctx.fillStyle = 'rgba(15, 23, 42, 0.05)'; 
            ctx.fillRect(0, 0, width, height);

            ctx.fillStyle = '#38bdf8'; 
            ctx.font = '16px "Fira Code", monospace';

            for (let i = 0; i < drops.length; i++) {
                const text = chars.charAt(Math.floor(Math.random() * chars.length));
                ctx.fillText(text, i * 16, drops[i] * 16);

                if (drops[i] * 16 > height && Math.random() > 0.975) {
                    drops[i] = 0;
                }
                drops[i]++;
            }
        }

        init();
        window.addEventListener('resize', init);
        setInterval(draw, 35);

        // --- Title Typing Transition Effect ---
        const words = [
            "Computer Science Student passionate about algorithms.",
            "Building robust data structures from scratch.",
            "Turning complex system logic into optimized code."
        ];
        
        let wordIndex = 0;
        let charIndex = 0;
        let isDeleting = false;
        const typingOutput = document.getElementById('typing-output');

        function typeEffect() {
            const currentWord = words[wordIndex];
            
            if (isDeleting) {
                typingOutput.textContent = currentWord.substring(0, charIndex - 1);
                charIndex--;
            } else {
                typingOutput.textContent = currentWord.substring(0, charIndex + 1);
                charIndex++;
            }

            let typeSpeed = isDeleting ? 40 : 80;

            if (!isDeleting && charIndex === currentWord.length) {
                typeSpeed = 2000; // Pause at end of word
                isDeleting = true;
            } else if (isDeleting && charIndex === 0) {
                isDeleting = false;
                wordIndex = (wordIndex + 1) % words.length;
                typeSpeed = 500; // Pause before next word
            }

            setTimeout(typeEffect, typeSpeed);
        }

        document.addEventListener("DOMContentLoaded", () => {
            setTimeout(typeEffect, 500);
        });
    </script>

</body>
</html>

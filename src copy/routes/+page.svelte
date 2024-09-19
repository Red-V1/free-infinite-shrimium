<script>
    import { onMount } from "svelte";

    let rotation = 0;

    onMount(() => {
        document.title = "Shrimium";
        const observer = new IntersectionObserver(
            (entries) => {
                entries.forEach((entry) => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add("animate");
                    }
                });
            },
            { threshold: 0.1 },
        );

        document
            .querySelectorAll(".feature-item, .stream-item, .roadmap-item")
            .forEach((item) => {
                observer.observe(item);
            });

        createParticles();
        animateParticles();
        rotateShrimo();
        updateCountdown();
    });

    function createParticles() {
        const heroBackground = document.querySelector(".hero-background");
        for (let i = 0; i < 50; i++) {
            const particle = document.createElement("div");
            particle.classList.add("particle");
            particle.style.setProperty("--size", `${Math.random() * 5 + 2}px`);
            particle.style.left = `${Math.random() * 100}%`;
            particle.style.top = `${Math.random() * 100}%`;
            heroBackground.appendChild(particle);
        }
    }

    function animateParticles() {
        const particles = document.querySelectorAll(".particle");
        particles.forEach((particle) => {
            const speed = Math.random() * 2 + 1;
            const angle = Math.random() * 360;
            const radius = Math.random() * 100 + 50;
            let x = 0;
            let y = 0;

            function animate() {
                x += speed / 60;
                y = Math.sin(x) * radius;

                particle.style.transform = `translate(${y}px, ${x}px)`;

                if (x > window.innerHeight + 100) {
                    x = -100;
                    y = 0;
                }

                requestAnimationFrame(animate);
            }

            animate();
        });
    }

    function rotateShrimo() {
        setInterval(() => {
            rotation += 1;
        }, 50);
    }

    function updateCountdown() {
        let timeLeft = 3600; // 1 hour in seconds

        const countdownInterval = setInterval(() => {
            const minutes = Math.floor(timeLeft / 60);
            const seconds = timeLeft % 60;
            const countdownElement = document.querySelector(
                ".stream-item:nth-child(2) p",
            );
            if (countdownElement) {
                countdownElement.textContent = `Starting in ${minutes}:${seconds.toString().padStart(2, "0")}`;
            }

            if (timeLeft <= 0) {
                clearInterval(countdownInterval);
                if (countdownElement) {
                    countdownElement.textContent = "Live Now!";
                }
            }

            timeLeft--;
        }, 1000);
    }
</script>

<main>
    <header>
        <nav>
            <div class="logo">
                <img
                    src="https://static-cdn.jtvnw.net/channel-points-icons/896020889/4504bc6b-5dde-4545-aff1-79b61e8ae2aa/icon-2.png"
                    alt="Shrimo Logo"
                    class="shrimo-avatar"
                    style="transform: rotate({rotation}deg)"
                />
                Shrimium
            </div>
            <ul>
                <li><a href="#hero">Home</a></li>
                <li><a href="#features">Features</a></li>
                <li><a href="#streams">Streams</a></li>
                <li><a href="#roadmap">Roadmap</a></li>
            </ul>
        </nav>
    </header>

    <section id="hero">
        <div class="hero-content">
            <h1>Shrimium</h1>
            <p class="tagline">The Streamer's Crypto Revolution</p>
            <div class="cta-container">
                <button class="cta-button">Join the Stream</button>
                <button class="secondary-button">Learn More</button>
            </div>
        </div>
        <div class="hero-background">
            <div class="stream-particles"></div>
        </div>
    </section>

    <section id="features">
        <h2>Streaming Features</h2>
        <div class="feature-grid">
            <div class="feature-item">
                <div class="feature-icon">🎮</div>
                <h3>Stream-Powered Mining</h3>
                <p>Earn Shrimium while you watch streams!</p>
            </div>
            <div class="feature-item">
                <div class="feature-icon">🏆</div>
                <h3>Streamer Rewards</h3>
                <p>Support your favorite streamers with Shrimium.</p>
            </div>
            <div class="feature-item">
                <div class="feature-icon">🌟</div>
                <h3>Exclusive Content</h3>
                <p>Unlock special streams with your Shrimium tokens.</p>
            </div>
            <div class="feature-item">
                <div class="feature-icon">🎁</div>
                <h3>Gambling</h3>
                <p>Win Shrimium in the digi-casino!</p>
            </div>
        </div>
    </section>

    <section id="streams">
        <h2>Featuring</h2>
        <div class="stream-grid">
            <div class="stream-item">
                <div class="stream-preview"></div>
                <h3>Shrimo's Big Win</h3>
                <p>Shrimo hits the JACKPOT</p>
            </div>
            <div class="stream-item">
                <div class="stream-preview"></div>
                <h3>Shrimium Trading 101</h3>
                <p>Starting in 1 hour</p>
            </div>
            <div class="stream-item">
                <div class="stream-preview"></div>
                <h3>Crypto Market Analysis</h3>
                <p>Shrimo gets in early and EARNS</p>
            </div>
        </div>
    </section>

    <section id="roadmap">
        <h2>Shrimium Roadmap</h2>
        <div class="roadmap-timeline">
            <div class="roadmap-item">
                <div class="roadmap-content">
                    <h3>Q1 2024</h3>
                    <p>Shrimo & Shrimium Launch... FLOOD!</p>
                </div>
            </div>
            <div class="roadmap-item">
                <div class="roadmap-content">
                    <h3>Q2 2024</h3>
                    <p>Streamer Partnership Program</p>
                </div>
            </div>
            <div class="roadmap-item">
                <div class="roadmap-content">
                    <h3>Q3 2025</h3>
                    <p>Shrimium Proprietary Trading Platform</p>
                </div>
            </div>
            <div class="roadmap-item">
                <div class="roadmap-content">
                    <h3>Q4 2025</h3>
                    <p>Streaming Virtual Crypto Convention</p>
                </div>
            </div>
        </div>
    </section>

    <footer>
        <p>
            &copy; 2024 Shrimium. All rights reserved. Powered by Shrimo's
            chat's tears.
        </p>
    </footer>
</main>

<style>
    @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;700&display=swap");

    :global(*) {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    :global(body) {
        font-family: "Poppins", sans-serif;
        background-color: #0a0e17;
        color: #e0e0e0;
        line-height: 1.6;
    }

    header {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        z-index: 1000;
        background-color: rgba(10, 14, 23, 0.8);
        backdrop-filter: blur(10px);
    }

    nav {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 1rem 2rem;
        max-width: 1200px;
        margin: 0 auto;
    }

    .logo {
        font-size: 1.5rem;
        font-weight: bold;
        color: #00ff9d;
        display: flex;
        align-items: center;
    }

    .shrimo-avatar {
        width: 40px;
        height: 40px;
        border-radius: 50%;
        margin-right: 10px;
        border: 2px solid #00ff9d;
        transition: transform 0.3s ease;
    }

    .shrimo-avatar:hover {
        transform: scale(1.1) rotate(360deg) !important;
    }

    nav ul {
        display: flex;
        list-style-type: none;
    }

    nav ul li {
        margin-left: 2rem;
    }

    nav ul li a {
        color: #e0e0e0;
        text-decoration: none;
        transition: color 0.3s ease;
    }

    nav ul li a:hover {
        color: #00ff9d;
    }

    main {
        padding-top: 80px;
    }

    section {
        padding: 4rem 2rem;
        max-width: 1200px;
        margin: 0 auto;
    }

    h1,
    h2,
    h3 {
        line-height: 1.2;
    }

    h1 {
        font-size: 4rem;
        background: linear-gradient(45deg, #00ff9d, #6bff84);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        margin-bottom: 1rem;
    }

    h2 {
        font-size: 2.5rem;
        color: #00ff9d;
        margin-bottom: 2rem;
        text-align: center;
    }

    .tagline {
        font-size: 1.5rem;
        margin-bottom: 2rem;
    }

    #hero {
        height: calc(100vh - 80px);
        display: flex;
        align-items: center;
        justify-content: center;
        position: relative;
        overflow: hidden;
    }

    .hero-content {
        text-align: center;
        z-index: 1;
    }

    .hero-background {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        overflow: hidden;
    }

    .stream-particles {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-image: radial-gradient(#1dd716 2px, transparent 2px),
            radial-gradient(#0ef121 2px, transparent 2px);
        background-size: 50px 50px;
        background-position:
            0 0,
            25px 25px;
        animation: particleFlow 20s linear infinite;
    }

    @keyframes particleFlow {
        0% {
            transform: translateY(0);
        }
        100% {
            transform: translateY(-50px);
        }
    }

    .cta-container {
        display: flex;
        justify-content: center;
        gap: 1rem;
    }

    .cta-button,
    .secondary-button {
        padding: 0.75rem 1.5rem;
        font-size: 1rem;
        font-weight: bold;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        transition: all 0.3s ease;
    }

    .cta-button {
        background-color: #00ff9d;
        color: #0a0e17;
    }

    .secondary-button {
        background-color: transparent;
        color: #00ff9d;
        border: 2px solid #00ff9d;
    }

    .cta-button:hover,
    .secondary-button:hover {
        transform: translateY(-3px);
        box-shadow: 0 10px 20px rgba(0, 255, 157, 0.2);
    }

    .feature-grid,
    .stream-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 2rem;
    }

    .feature-item,
    .stream-item {
        background-color: #1a1f2c;
        border-radius: 15px;
        padding: 1.5rem;
        transition: all 0.3s ease;
        text-align: center;
    }

    .feature-item:hover,
    .stream-item:hover {
        transform: translateY(-5px);
        box-shadow: 0 10px 20px rgba(0, 255, 157, 0.1);
    }

    .feature-icon {
        font-size: 3rem;
        margin-bottom: 1rem;
    }

    .stream-preview {
        width: 100%;
        height: 150px;
        background-color: #00ff9dae;
        border-radius: 10px;
        margin-bottom: 1rem;
        position: relative;
        overflow: hidden;
        transition: transform 0.3s ease;
    }

    .stream-preview::after {
        content: "";
        position: absolute;
        top: 0;
        left: -100%;
        width: 100%;
        height: 100%;
        background: linear-gradient(
            90deg,
            transparent,
            rgba(0, 0, 0, 0.2),
            transparent
        );
        animation: shimmer 2s infinite;
    }

    @keyframes shimmer {
        0% {
            left: -100%;
        }
        100% {
            left: 100%;
        }
    }

    .roadmap-timeline {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        gap: 2rem;
        position: relative;
    }

    .roadmap-timeline::before {
        content: "";
        position: absolute;
        top: 50%;
        left: 0;
        right: 0;
        height: 2px;
        background-color: #00ff9d;
        transform: translateY(-50%);
    }

    .roadmap-item {
        position: relative;
        padding-top: 2rem;
    }

    .roadmap-content {
        background-color: #1a1f2c;
        border-radius: 15px;
        padding: 1rem;
        text-align: center;
    }

    .roadmap-item::before {
        content: "";
        position: absolute;
        width: 20px;
        height: 20px;
        background-color: #00ff9d;
        border-radius: 50%;
        top: 0;
        left: 50%;
        transform: translateX(-50%);
    }

    footer {
        text-align: center;
        padding: 2rem;
        background-color: #1a1f2c;
    }

    @keyframes fadeInUp {
        from {
            opacity: 0;
            transform: translateY(20px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }

    .feature-item,
    .stream-item,
    .roadmap-item {
        animation: fadeInUp 0.6s ease-out forwards;
        opacity: 0;
    }

    .feature-item:nth-child(1),
    .stream-item:nth-child(1),
    .roadmap-item:nth-child(1) {
        animation-delay: 0.1s;
    }
    .feature-item:nth-child(2),
    .stream-item:nth-child(2),
    .roadmap-item:nth-child(2) {
        animation-delay: 0.2s;
    }
    .feature-item:nth-child(3),
    .stream-item:nth-child(3),
    .roadmap-item:nth-child(3) {
        animation-delay: 0.3s;
    }
    .feature-item:nth-child(4),
    .stream-item:nth-child(4),
    .roadmap-item:nth-child(4) {
        animation-delay: 0.4s;
    }

    .particle {
        position: absolute;
        background-color: #00ff9d;
        border-radius: 50%;
        width: var(--size);
        height: var(--size);
        opacity: 0.6;
        pointer-events: none;
    }

    :global(.animate) {
        animation: fadeInUp 0.6s ease-out forwards;
    }
</style>

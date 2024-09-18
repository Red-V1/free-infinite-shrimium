<script>
    import { onMount, tick } from "svelte";
    import { fade, fly, scale } from "svelte/transition";
    import { spring } from "svelte/motion";

    let mounted = false;
    let currentPrice = 42.0;
    let marketCap = 420000000;

    const formatNumber = (num) => {
        return new Intl.NumberFormat("en-US", {
            style: "currency",
            currency: "USD",
            minimumFractionDigits: 2,
            maximumFractionDigits: 2,
        }).format(num);
    };

    const updatePrice = () => {
        currentPrice = currentPrice * (1 + (Math.random() - 0.5) * 0.01);
        marketCap = currentPrice * 10000000;
    };

    onMount(async () => {
        mounted = true;
        await tick();
        setInterval(updatePrice, 5000);
    });

    const highlight = spring(1);
</script>

<main class="container" class:mounted>
    <div class="grid-overlay"></div>

    <nav class="bento-item" in:fly={{ y: -50, duration: 1000 }}>
        <div class="logo">Shrimium</div>
        <ul>
            <li><a href="#about">About</a></li>
            <li><a href="#features">Features</a></li>
            <li><a href="#tokenomics">Tokenomics</a></li>
            <li><a href="#community">Community</a></li>
        </ul>
    </nav>

    <div class="bento-row">
        <div class="bento-item hero" in:scale={{ duration: 1000, start: 0.8 }}>
            <h1>Shrimium</h1>
            <p>Gnome-Powered Cryptocurrency</p>
        </div>
    </div>

    <div class="bento-row">
        <div
            class="bento-item section-title"
            in:fly={{ y: 50, duration: 1000 }}
        >
            <h2>About</h2>
        </div>
    </div>

    <div class="bento-row">
        <div class="bento-item large" in:fly={{ x: -100, duration: 1000 }}>
            <p>
                Shrimium harnesses gnome magic for a sustainable and efficient
                blockchain ecosystem.
            </p>
        </div>
    </div>

    <div class="bento-row">
        <div
            class="bento-item section-title"
            in:fly={{ y: 50, duration: 1000 }}
        >
            <h2>Magical Features</h2>
        </div>
    </div>

    <div class="bento-row">
        <div
            class="bento-item"
            in:fly={{ y: 100, duration: 1000 }}
            on:mouseenter={() => highlight.set(1.1)}
            on:mouseleave={() => highlight.set(1)}
        >
            <h3>Gnome Mining</h3>
            <p>Eco-friendly blockchain validation</p>
        </div>
        <div
            class="bento-item"
            in:fly={{ y: 100, duration: 1000, delay: 200 }}
            on:mouseenter={() => highlight.set(1.1)}
            on:mouseleave={() => highlight.set(1)}
        >
            <h3>Gnome Castles</h3>
            <p>Secure wallet storage</p>
        </div>
    </div>

    <div class="bento-row">
        <div
            class="bento-item"
            in:fly={{ y: 100, duration: 1000 }}
            on:mouseenter={() => highlight.set(1.1)}
            on:mouseleave={() => highlight.set(1)}
        >
            <h3>Wizard Staking</h3>
            <p>Earn magical rewards</p>
        </div>
        <div
            class="bento-item"
            in:fly={{ y: 100, duration: 1000, delay: 200 }}
            on:mouseenter={() => highlight.set(1.1)}
            on:mouseleave={() => highlight.set(1)}
        >
            <h3>Rainbow Bridge</h3>
            <p>Cross-chain gnome network</p>
        </div>
    </div>

    <div class="bento-row">
        <div
            class="bento-item section-title"
            in:fly={{ y: 50, duration: 1000 }}
        >
            <h2>Tokenomics</h2>
        </div>
    </div>

    <div class="bento-row">
        <div
            class="bento-item"
            in:fly={{ x: -100, duration: 1000 }}
            style="transform: scale({$highlight})"
        >
            <h3>Current Price</h3>
            <p class="highlight">{formatNumber(currentPrice)}</p>
        </div>
        <div
            class="bento-item"
            in:fly={{ x: 100, duration: 1000 }}
            style="transform: scale({$highlight})"
        >
            <h3>Market Cap</h3>
            <p class="highlight">{formatNumber(marketCap)}</p>
        </div>
    </div>

    <div class="bento-row">
        <div
            class="bento-item section-title"
            in:fly={{ y: 50, duration: 1000 }}
        >
            <h2>Join Our Gnome Village</h2>
        </div>
    </div>

    <div class="bento-row">
        <div class="bento-item large" in:fade>
            <p>
                Unite with gnomes and crypto enthusiasts in our magical
                community!
            </p>
            <div class="social-links">
                <a
                    href="#"
                    class="social-icon"
                    in:scale={{ duration: 500, delay: 500 }}>Twitter</a
                >
                <a
                    href="#"
                    class="social-icon"
                    in:scale={{ duration: 500, delay: 700 }}>Discord</a
                >
                <a
                    href="#"
                    class="social-icon"
                    in:scale={{ duration: 500, delay: 900 }}>Telegram</a
                >
            </div>
        </div>
    </div>

    <div class="bento-row">
        <div class="bento-item" in:fade>
            <p>© 2024 Shrimium. All rights reserved. Gnomes at work! 🍄</p>
        </div>
    </div>
</main>

<style>
    :global(body) {
        margin: 0;
        padding: 0;
        font-family: "Inter", sans-serif;
        background: #1a1a2e;
        color: #e0e0e0;
        min-height: 100vh;
    }

    .container {
        max-width: 1200px;
        margin: 0 auto;
        padding: 2rem;
        opacity: 0;
        transition: opacity 0.5s ease;
    }

    .container.mounted {
        opacity: 1;
    }

    .grid-overlay {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background-image: linear-gradient(
                to right,
                rgba(255, 255, 255, 0.05) 1px,
                transparent 1px
            ),
            linear-gradient(
                to bottom,
                rgba(255, 255, 255, 0.05) 1px,
                transparent 1px
            );
        background-size: 50px 50px;
        pointer-events: none;
        z-index: -1;
    }

    .bento-item {
        background: rgba(255, 255, 255, 0.05);
        backdrop-filter: blur(10px);
        border-radius: 20px;
        padding: 2rem;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        transition: all 0.3s ease;
        border: 1px solid rgba(255, 255, 255, 0.1);
    }

    .bento-item:hover {
        transform: translateY(-5px);
        box-shadow: 0 6px 12px rgba(255, 105, 180, 0.2);
    }

    .bento-row {
        display: flex;
        justify-content: center;
        gap: 2rem;
        margin-bottom: 2rem;
    }

    .bento-row .bento-item {
        flex: 1;
        min-width: 0;
    }

    .large {
        flex: 2;
    }

    .section-title {
        text-align: center;
    }

    nav {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 2rem;
    }

    nav ul {
        display: flex;
        list-style-type: none;
        padding: 0;
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
        color: #ff69b4;
    }

    .logo {
        font-size: 1.5rem;
        font-weight: bold;
        color: #ff69b4;
    }

    .hero {
        text-align: center;
        padding: 4rem 2rem;
    }

    h1 {
        font-size: 4rem;
        margin-bottom: 1rem;
        color: #ff69b4;
    }

    h2 {
        font-size: 2.5rem;
        margin-bottom: 1rem;
        color: #ff69b4;
    }

    h3 {
        font-size: 1.8rem;
        margin-bottom: 0.5rem;
        color: #ff69b4;
    }

    .highlight {
        color: #ff69b4;
        font-size: 2rem;
        font-weight: bold;
    }

    .social-links {
        display: flex;
        justify-content: center;
        gap: 1rem;
        margin-top: 2rem;
    }

    .social-icon {
        color: #e0e0e0;
        text-decoration: none;
        padding: 0.75rem 1.5rem;
        border: 1px solid #e0e0e0;
        border-radius: 25px;
        transition: all 0.3s ease;
        font-size: 1.1rem;
    }

    .social-icon:hover {
        color: #ff69b4;
        border-color: #ff69b4;
    }

    @media (max-width: 768px) {
        nav {
            flex-direction: column;
        }

        nav ul {
            margin-top: 1rem;
        }

        nav ul li {
            margin: 0 1rem;
        }

        .bento-row {
            flex-direction: column;
        }
    }
</style>

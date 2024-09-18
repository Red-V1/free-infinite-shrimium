<script>
    import { onMount } from "svelte";
    import { fade, fly, scale } from "svelte/transition";

    let visible = false;
    let spinning = false;
    let result = "";
    let jackpot = 1000000;
    let shrimiumBalance = 0;
    let spinCost = 100;
    let slots = ["💎", "🔥", "🌟", "🚀"];
    let slotResults = ["💎", "💎", "💎"];

    onMount(() => {
        visible = true;
        setInterval(() => {
            jackpot += Math.floor(Math.random() * 10000);
        }, 1000);
    });

    function spinWheel() {
        if (shrimiumBalance < spinCost) {
            alert("Not enough Shrimium! Generate more to spin.");
            return;
        }

        shrimiumBalance -= spinCost;
        spinning = true;
        slotResults = slots.map(() => "❓");

        let spinDuration = 3000;
        let spinInterval = setInterval(() => {
            slotResults = slots.map(
                () => slots[Math.floor(Math.random() * slots.length)],
            );
        }, 100);

        setTimeout(() => {
            clearInterval(spinInterval);
            spinning = false;
            slotResults = slots.map(
                () => slots[Math.floor(Math.random() * slots.length)],
            );
            checkWin();
        }, spinDuration);
    }

    function checkWin() {
        if (slotResults.every((slot) => slot === slotResults[0])) {
            if (slotResults[0] === "🚀") {
                result = `MEGA JACKPOT! +${jackpot} Shrimium! 🎉🚀`;
                shrimiumBalance += jackpot;
            } else {
                let winAmount = jackpot / 10;
                result = `WIN! +${winAmount} Shrimium! 🎉`;
                shrimiumBalance += winAmount;
            }
        } else {
            result = "Try again!";
        }
    }

    function generateShrimium() {
        let generatedAmount = Math.floor(Math.random() * 1000) + 100;
        shrimiumBalance += generatedAmount;
        result = `Generated ${generatedAmount} Shrimium!`;
    }
</script>

<svelte:head>
    <link
        href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&display=swap"
        rel="stylesheet"
    />
</svelte:head>

<div class="container">
    {#if visible}
        <header in:fly={{ y: -50, duration: 1000 }} out:fade>
            <h1 class="mega-title">Free Infinite Shrimium</h1>
        </header>

        <section class="balance glassmorphic-card rainbow-border">
            <h2 class="neon-text">Your Shrimium Balance</h2>
            <p class="balance-amount">{shrimiumBalance.toLocaleString()} 🚀</p>
        </section>

        <section class="jackpot glassmorphic-card rainbow-border">
            <h2 class="neon-text">Current Jackpot</h2>
            <p class="jackpot-amount">${jackpot.toLocaleString()}</p>
        </section>

        <section class="game-section glassmorphic-card rainbow-border">
            <h2 class="neon-text">Shrimium Slots</h2>
            <div class="slot-machine">
                {#each slotResults as slot}
                    <div class="slot" class:spinning>{slot}</div>
                {/each}
            </div>
            <button class="cosmic-button" on:click={spinWheel}
                >SPIN NOW! (Cost: {spinCost} 🚀)</button
            >
            <button
                class="cosmic-button generate-button"
                on:click={generateShrimium}>GENERATE SHRIMIUM</button
            >
            {#if result}
                <p class="result mega-rainbow" in:scale>{result}</p>
            {/if}
        </section>

        <section class="testimonials glassmorphic-card rainbow-border">
            <h2 class="neon-text">Shrimium Success Stories</h2>
            <div class="testimonial-grid">
                <div class="testimonial">
                    <div class="avatar money-man"></div>
                    <p class="quote">
                        "Shrimium turned my life into a goldmine!" - J.
                        Moneybags
                    </p>
                </div>
                <div class="testimonial">
                    <div class="avatar cash-lady"></div>
                    <p class="quote">
                        "I'm swimming in wealth thanks to Shrimium!" - C.
                        Richstone
                    </p>
                </div>
                <div class="testimonial">
                    <div class="avatar crypto-bro"></div>
                    <p class="quote">
                        "Shrimium is the future of finance!" - B. Hodler
                    </p>
                </div>
                <div class="testimonial">
                    <div class="avatar lucky-guy"></div>
                    <p class="quote">
                        "I hit the Shrimium jackpot and never looked back!" - L.
                        Starr
                    </p>
                </div>
            </div>
        </section>

        <footer>
            <p class="disclaimer">
                Disclaimer: You <b>NEED</b> to pay us double what you earn .
            </p>
        </footer>
    {/if}
</div>

<style>
    :global(body) {
        margin: 0;
        padding: 0;
        background-color: #000;
        color: #fff;
        font-family: "Orbitron", sans-serif;
        overflow-x: hidden;
    }

    .container {
        background: linear-gradient(45deg, #000000, #1a0033, #330066);
        background-size: 400% 400%;
        animation: gradientBG 15s ease infinite;
        min-height: 100vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 2rem;
    }

    @keyframes gradientBG {
        0% {
            background-position: 0% 50%;
        }
        50% {
            background-position: 100% 50%;
        }
        100% {
            background-position: 0% 50%;
        }
    }

    .mega-title {
        font-size: 4rem;
        text-align: center;
        background: linear-gradient(to right, #ff4e50, #f9d423);
        -webkit-background-clip: text;
        background-clip: text;
        color: transparent;
        animation: title-shine 2s linear infinite;
    }

    @keyframes title-shine {
        0% {
            background-position: 0% center;
        }
        100% {
            background-position: 200% center;
        }
    }

    .neon-text {
        font-size: 2rem;
        color: #fff;
        text-shadow:
            0 0 5px #fff,
            0 0 10px #fff,
            0 0 15px #fff,
            0 0 20px #ff00de,
            0 0 35px #ff00de,
            0 0 40px #ff00de,
            0 0 50px #ff00de,
            0 0 75px #ff00de;
        animation: neon-pulse 1.5s ease-in-out infinite alternate;
    }

    @keyframes neon-pulse {
        from {
            text-shadow:
                0 0 5px #fff,
                0 0 10px #fff,
                0 0 15px #fff,
                0 0 20px #ff00de,
                0 0 35px #ff00de,
                0 0 40px #ff00de,
                0 0 50px #ff00de,
                0 0 75px #ff00de;
        }
        to {
            text-shadow:
                0 0 2.5px #fff,
                0 0 5px #fff,
                0 0 7.5px #fff,
                0 0 10px #ff00de,
                0 0 17.5px #ff00de,
                0 0 20px #ff00de,
                0 0 25px #ff00de,
                0 0 37.5px #ff00de;
        }
    }

    .glassmorphic-card {
        background: rgba(255, 255, 255, 0.1);
        box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
        backdrop-filter: blur(4px);
        border-radius: 10px;
        padding: 2rem;
        margin: 2rem 0;
        text-align: center;
        max-width: 80%;
    }

    .rainbow-border {
        position: relative;
    }

    .rainbow-border::before {
        content: "";
        position: absolute;
        top: -3px;
        left: -3px;
        right: -3px;
        bottom: -3px;
        background: linear-gradient(
            45deg,
            #ff0000,
            #ff7f00,
            #ffff00,
            #00ff00,
            #0000ff,
            #8b00ff
        );
        border-radius: 12px;
        z-index: -1;
        animation: rainbow-border-animate 5s linear infinite;
    }

    @keyframes rainbow-border-animate {
        0% {
            filter: hue-rotate(0deg);
        }
        100% {
            filter: hue-rotate(360deg);
        }
    }

    .balance-amount,
    .jackpot-amount {
        font-size: 3rem;
        font-weight: bold;
        color: gold;
        text-shadow: 0 0 10px gold;
        animation: pulse 1s infinite alternate;
    }

    @keyframes pulse {
        from {
            transform: scale(1);
        }
        to {
            transform: scale(1.05);
        }
    }

    .slot-machine {
        display: flex;
        justify-content: center;
        gap: 1rem;
        margin: 2rem 0;
    }

    .slot {
        font-size: 4rem;
        background: #333;
        padding: 1rem;
        border-radius: 10px;
        box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.5);
    }

    .slot.spinning {
        animation: spin 0.2s linear infinite;
    }

    @keyframes spin {
        0% {
            transform: translateY(0);
        }
        100% {
            transform: translateY(-100%);
        }
    }

    .cosmic-button {
        padding: 1rem 2rem;
        font-size: 1.5rem;
        background: linear-gradient(45deg, #ff00de, #00ff00, #00ffff, #ff00de);
        background-size: 300% 300%;
        color: #000;
        border: none;
        border-radius: 50px;
        cursor: pointer;
        transition: all 0.3s ease;
        animation:
            cosmic-pulse 2s infinite,
            gradient-shift 5s ease infinite;
    }

    @keyframes cosmic-pulse {
        0% {
            transform: scale(1);
        }
        50% {
            transform: scale(1.05);
        }
        100% {
            transform: scale(1);
        }
    }

    @keyframes gradient-shift {
        0% {
            background-position: 0% 50%;
        }
        50% {
            background-position: 100% 50%;
        }
        100% {
            background-position: 0% 50%;
        }
    }

    .generate-button {
        margin-top: 1rem;
        background: linear-gradient(45deg, #00ff00, #00ffff, #00ff00);
    }

    .result {
        font-size: 3rem;
        margin-top: 1rem;
    }

    .mega-rainbow {
        background: linear-gradient(
            to right,
            red,
            orange,
            yellow,
            green,
            blue,
            indigo,
            violet
        );
        -webkit-background-clip: text;
        background-clip: text;
        color: transparent;
        animation: mega-rainbow 5s linear infinite;
    }

    @keyframes mega-rainbow {
        0% {
            filter: hue-rotate(0deg);
        }
        100% {
            filter: hue-rotate(360deg);
        }
    }

    .testimonial-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
        gap: 2rem;
    }

    .testimonial {
        text-align: center;
    }

    .avatar {
        width: 100px;
        height: 100px;
        border-radius: 50%;
        margin: 0 auto 1rem;
        background-size: cover;
        background-position: center;
        animation: avatar-float 3s ease-in-out infinite;
    }

    @keyframes avatar-float {
        0%,
        100% {
            transform: translateY(0);
        }
        50% {
            transform: translateY(-10px);
        }
    }

    .money-man {
        background-image: url("https://media.cnn.com/api/v1/images/stellar/prod/gettyimages-2158244120-20240916111442794.jpg?c=16x9&q=h_833,w_1480,c_fill");
    }
    .cash-lady {
        background-image: url("https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQAXuICwo8dDn5AIgGxd31-x2d-QVwPc4-maA&s");
    }
    .crypto-bro {
        background-image: url("https://static-cdn.jtvnw.net/jtv_user_pictures/a72716b8-7586-4da2-bb8a-034c3e47e758-profile_image-70x70.png");
    }
    .lucky-guy {
        background-image: url("data:image/webp;base64,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");
    }

    .quote {
        font-style: italic;
        font-size: 0.9rem;
        padding: 1rem;
        background: rgba(255, 255, 255, 0.1);
        border-radius: 10px;
    }

    .disclaimer {
        font-size: 0.8rem;
        opacity: 0.7;
        text-align: center;
        margin-top: 2rem;
    }
</style>

<script lang="ts">
    const TARGET_SIZE = 44;
    const STEP = 0.08;
    const COLORS = 5;

    let width = $state(0);
    let height = $state(0);

    const FALLBACK_COLS = 48;
    let measured = $derived(width > 0);

    let cols = $derived(measured ? Math.max(1, Math.round(width / TARGET_SIZE)) : FALLBACK_COLS);
    const rows = 6;
    let total = $derived(cols * rows);
    let duration = $derived((cols + rows) * STEP * COLORS);
</script>


<div class="header" bind:clientWidth={width} style:height="{measured ? rows * (width / cols) : rows * TARGET_SIZE}px">
    <div
        class="squares"
        style:grid-template-columns={measured ? `repeat(${cols}, 1fr)` : `repeat(auto-fill, minmax(${TARGET_SIZE - 4}px, 1fr))`}
        style:--duration="{duration}s"
        aria-hidden="true"
    >
        {#each { length: total }, i}
            <div class="square" style:animation-delay="{((i % cols) + Math.floor(i / cols)) * STEP - duration}s"></div>
        {/each}
    </div>
    <h1 class="main-txt title">LC iTeam</h1>
</div>
<div class="border"></div>
<div class="dir-body">
    <div class="dir-div"><h2 class="main-txt page-dir">About</h2></div>
    <div class="dir-div"><h2 class="main-txt page-dir">Calendar</h2></div>
    <div class="dir-div"><h2 class="main-txt page-dir">Cabinet</h2></div>
    <div class="dir-div"><h2 class="main-txt page-dir">Resources</h2></div>
    <div class="dir-div"><h2 class="main-txt page-dir">Contact</h2></div>

</div>

<div class="body">
    <div class="news">
        <div class="cover"><img class="news-img" src="src/img/ss1.png" alt="outlook screenshot"></div>
        <div class="cover"><img class="news-img" src="src/img/ss2.png" alt="c3ss screenshot"></div>
    </div>
</div>

<h3 class="main-txt">Made by iTeam VP Jeo Lee</h3>

<style lang="css">
    @import url('https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,356..800;1,14..32,356&display=swap');

    :global(html, body) {
        margin: 0;
        padding: 0;
        min-height: 100vh;
        background-color: #1a1a1a;

        position: relative;
    }

    .main-txt {
        font-family: "Inter", sans-serif;
        font-optical-sizing: auto;
        font-style: normal;
    }

    .title {
        margin: 0;
        padding: 0.4em 0.9em;
        background: #fffdf7;
        color: #1a1a1a;

        font-size: clamp(2.25rem, 6vw, 4.5rem);
        font-weight: 800;
        letter-spacing: -0.03em;
        line-height: 1;
        white-space: nowrap;

        border: 3px solid #1a1a1a;
        border-radius: 14px;
        box-shadow: 8px 8px 0 #1a1a1a;
    }

    .border {
        position: absolute;
        background-image: linear-gradient(to bottom, transparent, #1a1a1a);

        width: 100%;
        height: 200px;
        top: 70px;
    }

    .header {
        position: relative;
        overflow: hidden;
        min-height: 220px;


        display: flex;
        justify-content: center;
        align-items: center;

        margin-bottom: 35px;
    }

    .title {
        position: relative;
        z-index: 1;
    }

    .squares {
        position: absolute;
        inset: 0;
        display: grid;
        gap: 4px;
        padding: 4px;
        align-content: start;
        background-color: #1e1e1e;
    }

    .square {
        aspect-ratio: 1;
        border-radius: 6px;
        opacity: 0.85;
        animation: color-cycle var(--duration) linear infinite;
    }

    .dir-body {
        display: flex;

        justify-content: center;

        margin-top: 30px;
    }

    .dir-div {
        width: 150px;
        height: 50px;
        background-color: #f0f0f0;
        
        border-radius: 15px; 

        outline: 4px solid #0076ff; 
        
        outline-offset: 4px; 

        display: flex;
        justify-content: center;
        align-items: center;

        margin-left: 20px;
        margin-right: 20px;
    }

    .body {
        width: 100%;

        display: flex;
        justify-content: center;
        align-items: center;

        margin-top: 45px;
    }

    .news {
        width: 65vw;
        height: 40vh;
        background-color: #f0f0f0;

        border-radius: 50px; 

        outline: 4px solid #0076ff; 

        outline-offset: 4px; 

        display: flex;

        justify-content: center;
        align-items: center;
    }

    .cover {
        width: 40%;
        height: 75%;
        margin: 0px 35px;

        outline: 5px solid #EB5231;

        outline-offset: 4px;

        border-radius: 15px;

        background-color: rgba(255, 0, 0, 0.5);

        
    }

    .news-img {
        width: 100%;
        height: 100%;

        border-radius: 15px;
    }

    @keyframes color-cycle {
        0%, 15%, 100% { background-color: #ffd6a5; }
        20%, 35% { background-color: #fdffb6; }
        40%, 55% { background-color: #caffbf; }
        60%, 75% { background-color: #9bf6ff; }
        80%, 95% { background-color: #bdb2ff; }
    }

    @media (prefers-reduced-motion: reduce) {
        .square {
            animation-play-state: paused;
        }
    }


</style>
<script lang="ts">
    const TARGET_SIZE = 40;
    const STEP = 0.08;
    const COLORS = 5;

    let width = $state(0);
    let height = $state(0);

    let cols = $derived(Math.round(width / TARGET_SIZE));
    const rows = 5;
    let total = $derived(cols * rows);
</script>


<div class="header" bind:clientWidth={width} style:height="{rows * (width / cols)}px">
    <div
        class="squares"
        style:grid-template-columns="repeat({cols}, 1fr)"
        style:--duration="{(cols + rows) * STEP * COLORS}s"
        aria-hidden="true"
    >
        {#each { length: total }, i}
            <div class="square" style:animation-delay="{((i % cols) + Math.floor(i / cols)) * STEP}s"></div>
        {/each}
    </div>
    <h1 class="main-txt title">LC iTeam</h1>
</div>
<div class="border"></div>
<div class="dir-body">
    <h2 class="main-txt page-dir">About</h2>
    <h2 class="main-txt page-dir">Calendar</h2>
    <h2 class="main-txt page-dir">Cabinet</h2>
    <h2 class="main-txt page-dir">Resources</h2>
    <h2 class="main-txt page-dir">Contact</h2>
</div>

<style lang="css">
    @import url('https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,356;1,14..32,356&display=swap');

    html, body {
        margin: 0;
        padding: 0;
        min-height: 100vh;
        background-color: #1e1e1e;
    }

    .main-txt {
        font-family: "Inter", sans-serif;
        font-optical-sizing: auto;
        font-style: normal;
    }

    .title {
        width: 16vw;
        height: 8vh;

        margin: 0;
        padding: 0.1em 0.4em;
        background: #fffdf7;
        color: #1a1a1a;
        font-size: 6vh;

        border: 4px solid rgba(0, 0, 0, 0.5);
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
        box-shadow: 5px 5px 0 rgba(0, 0, 0, 0.5);

        display: flex;
        justify-content: center;
        align-items: center;
    }

    .border {
        border: 2px solid black;
    }

    .header {
        position: relative;
        overflow: hidden;

        margin: 10px 0px;

        display: flex;
        justify-content: center;
        align-items: center;
    }

    .title {
        position: relative;
        z-index: 1;
    }

    .squares {
        position: absolute;
        inset: 0;
        display: grid;
        align-content: start;
    }

    .square {
        aspect-ratio: 1;
        box-shadow: inset 0 0 0 1px white;
        animation: color-cycle var(--duration) linear infinite backwards;

        border: 4px solid rgba(0, 0, 0, 0.5);
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
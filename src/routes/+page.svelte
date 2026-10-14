<script lang="ts">
    const TARGET_SIZE = 44;
    const STEP = 0.08;
    const COLORS = 5;
    const ROWS = 6;

    const links = [
        { href: '/about', label: 'About', desc: 'Who we are and what we do' },
        { href: '/calendar', label: 'Calendar', desc: 'Upcoming meetings and events' },
        { href: '/cabinet', label: 'Cabinet', desc: 'Meet the team behind iTeam' },
        { href: '/resources', label: 'Resources', desc: 'Guides, tools, and docs' },
        { href: '/contact', label: 'Contact', desc: 'Get in touch with us' }
    ];

    let width = $state(0);

    let cols = $derived(Math.max(1, Math.round(width / TARGET_SIZE)));
    let total = $derived(cols * ROWS);
</script>

<header class="hero" bind:clientWidth={width} style:height="{ROWS * (width / cols)}px">
    <div
        class="squares"
        style:grid-template-columns="repeat({cols}, 1fr)"
        style:--duration="{(cols + ROWS) * STEP * COLORS}s"
        aria-hidden="true"
    >
        {#each { length: total }, i}
            <div
                class="square"
                style:animation-delay="{((i % cols) + Math.floor(i / cols)) * STEP}s"
            ></div>
        {/each}
    </div>

    <div class="title-card">
        <h1>LC iTeam</h1>
    </div>
</header>

<main class="content">
    <p class="eyebrow">Explore</p>
    <nav class="nav-grid" aria-label="Main">
        {#each links as link, i}
            <a class="nav-card" href={link.href}>
                <span class="index">{String(i + 1).padStart(2, '0')}</span>
                <span class="label">{link.label}</span>
                <span class="desc">{link.desc}</span>
                <span class="arrow" aria-hidden="true">→</span>
            </a>
        {/each}
    </nav>
</main>

<style>
    /* ---------- Hero ---------- */

    .hero {
        position: relative;
        overflow: hidden;
        min-height: 220px;

        display: flex;
        justify-content: center;
        align-items: center;
    }

    .squares {
        position: absolute;
        inset: 0;
        display: grid;
        gap: 4px;
        padding: 4px;
        align-content: start;

        /* Fade the grid into the page background at the bottom */
        mask-image: linear-gradient(to bottom, black 55%, transparent 100%);
    }

    .square {
        aspect-ratio: 1;
        border-radius: 6px;
        opacity: 0.85;
        animation: color-cycle var(--duration) linear infinite backwards;
    }

    @keyframes color-cycle {
        0%, 15%, 100% { background-color: var(--peach); }
        20%, 35% { background-color: var(--lemon); }
        40%, 55% { background-color: var(--mint); }
        60%, 75% { background-color: var(--sky); }
        80%, 95% { background-color: var(--lavender); }
    }

    .title-card {
        position: relative;
        z-index: 1;

        padding: 0.4em 0.9em;
        background: var(--cream);
        color: var(--ink);
        border: 3px solid var(--ink);
        border-radius: 14px;
        box-shadow: 8px 8px 0 var(--ink);
    }

    .title-card h1 {
        font-size: clamp(2.25rem, 6vw, 4.5rem);
        font-weight: 800;
        letter-spacing: -0.03em;
        line-height: 1;
        white-space: nowrap;
    }

    /* ---------- Nav ---------- */

    .content {
        max-width: var(--max-width);
        margin: 0 auto;
        padding: 3rem 1.5rem 5rem;
    }

    .eyebrow {
        margin-bottom: 1.25rem;
        font-size: 0.8rem;
        font-weight: 600;
        letter-spacing: 0.12em;
        text-transform: uppercase;
        color: var(--text-muted);
    }

    .nav-grid {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
        gap: 1rem;
    }

    .nav-card {
        --accent: var(--peach);

        position: relative;
        display: flex;
        flex-direction: column;
        gap: 0.35rem;
        padding: 1.25rem 1.25rem 1.5rem;

        background: var(--surface);
        border: 1px solid var(--line);
        border-radius: var(--radius);

        transition:
            transform 0.2s ease,
            border-color 0.2s ease,
            background-color 0.2s ease,
            box-shadow 0.2s ease;
    }

    .nav-card:nth-child(2) { --accent: var(--lemon); }
    .nav-card:nth-child(3) { --accent: var(--mint); }
    .nav-card:nth-child(4) { --accent: var(--sky); }
    .nav-card:nth-child(5) { --accent: var(--lavender); }

    .nav-card:hover,
    .nav-card:focus-visible {
        transform: translateY(-3px);
        background: var(--surface-hover);
        border-color: var(--accent);
        box-shadow: 4px 4px 0 var(--accent);
    }

    .nav-card:focus-visible {
        outline: 2px solid var(--accent);
        outline-offset: 3px;
    }

    .index {
        font-size: 0.8rem;
        font-weight: 600;
        font-variant-numeric: tabular-nums;
        color: var(--accent);
    }

    .label {
        font-size: 1.35rem;
        font-weight: 700;
        letter-spacing: -0.01em;
    }

    .desc {
        font-size: 0.9rem;
        line-height: 1.45;
        color: var(--text-muted);
    }

    .arrow {
        position: absolute;
        top: 1.1rem;
        right: 1.25rem;
        color: var(--text-muted);
        transition:
            transform 0.2s ease,
            color 0.2s ease;
    }

    .nav-card:hover .arrow,
    .nav-card:focus-visible .arrow {
        transform: translateX(3px);
        color: var(--accent);
    }

    /* ---------- Motion ---------- */

    @media (prefers-reduced-motion: reduce) {
        .square {
            animation-play-state: paused;
        }

        .nav-card,
        .arrow {
            transition: none;
        }

        .nav-card:hover,
        .nav-card:focus-visible {
            transform: none;
        }
    }
</style>

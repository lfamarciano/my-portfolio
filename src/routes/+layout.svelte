<script>
import { base } from "$app/paths";
import { page } from "$app/stores";
let pages = [
    { url: "/", title: "Home" },
    { url: "/projects", title: "Projects" },
    { url: "/contact", title: "Contact" },
    {url: "https://github.com/lfamarciano", title:"Github"}
];
</script>

<nav>
  {#each pages as p}
    <a
        href={p.url.startsWith("http") ? p.url: `${base}${p.url}`}
        class:current={$page.route.id === p.url}
        target={p.url.startsWith("http") ? "_blank" : undefined}
    >
        {p.title}
    </a>
  {/each}
</nav>

<style>
    nav {
        --border-color: oklch(50% 10% 200 / 40%);
        display: flex;
        padding: 0.1em;
        border-bottom-width: 1px;
        border-bottom-style: solid;
        border-bottom-color: var(--grey);
        text-align: center;
    }

    nav a {
        flex: 1;
        text-decoration: none;
        color: inherit;
        /* text-align: center; */
        padding: 0.5em;
    }

    nav .current {
        font-weight: bold;
        border-bottom-width: 5px;
        border-bottom-style: solid;
        border-bottom-color: var(--grey);
    }

    nav a:hover {
        padding-bottom: -0.1em;
        padding: 0.5em;
        background-color: oklch(from var(--grey) 95% 5% h);
    }
</style>
<slot />

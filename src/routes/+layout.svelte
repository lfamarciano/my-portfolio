<script>
import { base } from "$app/paths";
import { page } from "$app/stores";

let pages = [
    { url: "/", title: "Home" },
    { url: "/projects", title: "Projects" },
    { url: "/contact", title: "Contact" },
    { url: "/resume", title: "Resume" },
    { url: "/meta", title: "Meta"},
    { url: "https://github.com/Mike-Kowalski", title:"Github"}
];

let localStorage = globalThis.localStorage ?? {};
let colorScheme = localStorage.colorScheme ?? "light dark";
let root = globalThis?.document?.documentElement;
$: root?.style.setProperty("color-scheme", colorScheme);
$: localStorage.colorScheme = colorScheme;
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

<label class="color-scheme">
    Theme:
    <select bind:value={ colorScheme }>       >
        <option value="light dark"> Automatic </option>
        <option value="light"> Light </option>
        <option value="dark"> Dark </option>
    </select>
</label>

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

    .color-scheme{
	position:absolute;
	top: 1rem;
	right: 1rem;
	display: inline-flex;
	gap: 5px;
}
</style>

<slot />
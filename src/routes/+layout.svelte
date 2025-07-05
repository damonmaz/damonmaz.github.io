<script lang="ts">
    import '../app.css';
    import { onMount } from 'svelte';

    let navVisible = false;

    onMount(() => {
        setTimeout(() => {
            navVisible = true;
        }, 100); // slight delay for fade-in effect
    });

    let { children } = $props();
</script>

<nav
  class="fixed top-0 left-0 w-full z-50 flex items-center justify-center px-4 py-2 transition-opacity duration-1000 opacity-50"
  style="background: rgba(0,0,0,0.7);"
  class:opacity-100={navVisible}
>
    <a
        href="https://www.linkedin.com/in/damonmazurek/"
        target="_blank"
        rel="noopener noreferrer"
        class="mx-2 px-3 py-1 rounded text-white  hover:bg-black/60 transition-colors duration-200 font-semibold text-sm"
    >
        LinkedIn
    </a>
    <span class="mx-6 text-white font-bold tracking-wide text-lg select-none">Damon Mazurek</span>
    <a
        href="https://github.com/damonmaz"
        target="_blank"
        rel="noopener noreferrer"
        class="mx-2 px-3 py-1 rounded text-white  hover:bg-black/60 transition-colors duration-200 font-semibold text-sm"
    >
        GitHub
    </a>
</nav>

{@render children()}
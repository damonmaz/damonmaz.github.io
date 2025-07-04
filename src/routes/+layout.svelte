<script lang="ts">
    import '../app.css';
    import TitleZoom from '$lib/components/TitleZoom.svelte';
    import NavBar from '$lib/components/NavBar.svelte';
    import Main from '$lib/components/Main.svelte';
    import { onMount } from 'svelte';
    let showNav = false;
    let titleProgress = 0;

	const DURATION: number = 2000; // Duration for the title zoom animation in milliseconds

    onMount(() => {
        const timeout = setTimeout(() => {
            showNav = true;
        }, DURATION);
        return () => clearTimeout(timeout);
    });
</script>

<TitleZoom
  text="Damon Mazurek"
  duration={DURATION}
  on:progress={e => titleProgress = e.detail.progress}
/>

<div class="flex justify-center w-full mt-8 xl:mt-12 pt-30">
    <NavBar {showNav} show={showNav} />
</div>

<Main className="" {titleProgress}>
  <slot />
</Main>
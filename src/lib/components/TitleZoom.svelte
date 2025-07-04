<script>
  import { createEventDispatcher, onMount } from 'svelte';
  export let text = "YOUR TITLE HERE";
  export let duration = 5000; // in milliseconds

  const dispatch = createEventDispatcher();

  let animationFrame;
  let startTime;

  function animateProgress() {
    const now = performance.now();
    const elapsed = Math.min(now - startTime, duration);
    const progress = elapsed / duration;
    dispatch('progress', { progress });
    if (elapsed < duration) {
      animationFrame = requestAnimationFrame(animateProgress);
    } else {
      dispatch('progress', { progress: 1 });
    }
  }

  onMount(() => {
    startTime = performance.now();
    animationFrame = requestAnimationFrame(animateProgress);
    return () => cancelAnimationFrame(animationFrame);
  });
</script>

<style>
  @keyframes zoom-in {
    0% {
      transform: scale(0.5) rotateX(0deg) translateZ(-500px); /* Changed rotateX(20deg) to rotateX(0deg) */
      opacity: 0;
    }
    100% {
      transform: scale(1.5) rotateX(0deg) translateZ(0);
      opacity: 1;
    }
  }

  .zoom-in {
    animation: zoom-in var(--duration) ease-in-out forwards;
  }

  .fade-bg {
    background: grey;
    border-radius: 2rem;
    box-shadow: 0 8px 32px 0 rgba(0,0,0,0.37);
  }

  .titlezoom {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    z-index: 1000;
    display: flex;
    justify-content: center;
    align-items: center;
    padding-top: 1rem;
    padding-bottom: 1rem;
    background: transparent;
    pointer-events: none;
  }

  /* Responsive top/bottom padding */
  @media (min-width: 640px) {
    .titlezoom {
      padding-top: 2rem;
      padding-bottom: 2rem;
    }
  }
  @media (min-width: 1280px) {
    .titlezoom {
      padding-top: 3rem;
      padding-bottom: 3rem;
    }
  }

  .titlezoom > * {
    pointer-events: auto;
  }
</style>

<div class="titlezoom">
  <div
    class="fade-bg zoom-in text-white text-4xl sm:text-6xl font-[Consolas] font-console px-12 py-4"
    style={`--duration: ${duration}ms`}
  >
    {text}
  </div>
</div>
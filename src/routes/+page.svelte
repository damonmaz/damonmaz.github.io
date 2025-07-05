<script>
  import { onMount } from 'svelte';
  let container;

  onMount(async () => {
    const gsap = (await import('gsap')).default;
    const { ScrollTrigger } = await import('gsap/ScrollTrigger');
    const { ScrollSmoother } = await import('gsap/ScrollSmoother');
    gsap.registerPlugin(ScrollTrigger, ScrollSmoother);

    ScrollSmoother.create({
      wrapper: container,
      content: container.querySelector('.smooth-content'),
      smooth: 1.2,
      effects: true
    });

    gsap.utils.toArray('.section').forEach((section) => {
      gsap.fromTo(
        section,
        { autoAlpha: 0, y: 40 },
        {
          autoAlpha: 1,
          y: 0,
          duration: 1,
          ease: 'power1.out',
          scrollTrigger: {
            trigger: section,
            start: 'top 80%',
            toggleActions: 'play none none none',
            once: true
          }
        }
      );
    });

    // Animate the background of .smooth-content with a stricter, saturated palette
    gsap.to(container.querySelector('.smooth-content'), {
      background: [
        // Start: deep red to purple
        "linear-gradient(120deg, #2a0a12 0%, #6b162b 40%, #3a185b 100%)",
        // Middle: purple to blue
        "linear-gradient(120deg, #3a185b 0%, #7c3aed 40%, #2563eb 100%)",
        // End: blue to deep blue
        "linear-gradient(120deg, #1e3a5c 0%, #2563eb 60%, #0e101c 100%)"
      ],
      scrollTrigger: {
        trigger: container.querySelector('.smooth-content'),
        start: "top top",
        end: "bottom bottom",
        scrub: true
      }
    });
  });
</script>

<div
  bind:this={container}
  class="min-h-screen w-full overflow-x-hidden font-sans text-white transition-colors duration-700"
  style="background: linear-gradient(120deg, #0e101c, #232526, #2c5364);"
>
  <div class="smooth-content">
    <section class="section min-h-screen flex flex-col justify-center items-center px-8 opacity-0">
      <h1 class="text-5xl font-bold tracking-wide mb-4">temp 1</h1>
    </section>
    <section class="section min-h-screen flex flex-col justify-center items-center px-8 opacity-0">
      <h2 class="text-4xl font-bold tracking-wide mb-4">temp 2</h2>
    </section>
    <section class="section min-h-screen flex flex-col justify-center items-center px-8 opacity-0">
      <h2 class="text-4xl font-bold tracking-wide mb-4">temp 3</h2>
    </section>
  </div>
</div>
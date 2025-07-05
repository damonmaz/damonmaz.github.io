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
        "linear-gradient(120deg, #d85a80 0%, #d85a80 30%, #d85a80 60%, #d85a80 100%)",
        "linear-gradient(120deg, #2563eb 0%, #2563eb 30%, #233a5e 60%, #2563eb 100%)",
        "linear-gradient(120deg, #662ba1 0%, #8c4acf 30%, #662ba1 60%, #662ba1 100%)"
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
<!--  #32619a -->
<div
  bind:this={container}
  class="min-h-screen w-full overflow-x-hidden font-sans text-white transition-colors duration-700"
  style="background: linear-gradient(120deg, #32619a, #32619a, #32619a);"
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
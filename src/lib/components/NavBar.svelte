<script>
  export let show = true;
</script>

<style>
  .navbar-fade {
    opacity: 0;
    transition: opacity 1000ms ease;
    pointer-events: none;
  }
  .navbar-fade.show {
    opacity: 1;
    pointer-events: auto;
  }
</style>

<nav class="bg-[#18181b] bg-opacity-90 rounded-2xl shadow-lg px-8 py-2 flex gap-6 navbar-fade {show ? 'show' : ''}">
  <button class="text-white font-semibold px-4 py-2 rounded hover:bg-neutral-800 transition">Button 1</button>
  <button class="text-white font-semibold px-4 py-2 rounded hover:bg-neutral-800 transition">Button 2</button>
  <button class="text-white font-semibold px-4 py-2 rounded hover:bg-neutral-800 transition">Button 3</button>
  <button class="text-white font-semibold px-4 py-2 rounded hover:bg-neutral-800 transition">Button 4</button>
</nav>
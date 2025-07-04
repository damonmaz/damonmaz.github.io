<script>
  export let className = "";
  export let titleProgress = 0;
  // Calculate top margin: from 0 (when progress=0) to e.g. 8rem (when progress=1)
  $: topMargin = 0 + (8 * titleProgress); // 0rem to 8rem
</script>

<div
  class={`min-h-screen bg-gray-400 text-white p-4 rounded-2xl m-4 ${className}`}
  style={`margin-top: ${topMargin}rem; transition: margin-top;`}
>
  <slot />
</div>
<script>
  // Animation for collapse.
  import { fade, fly, slide } from "svelte/transition";
  import { quintOut } from "svelte/easing";

  import { spring, tweened } from "svelte/motion";

  // Collapsible.
  export let collapse = false;

  // Title prop.
  export let title;

  export let height = tweened(0, { duration: 300, delay: 0 });

  // An animate property.
  // export let animate;

  export let noAnimate;

  if (noAnimate) {
    height.set(600);
  }

  let collapseFn = function() {
    if (!noAnimate) {
      let h = collapse ? 0 : 600;
      height.set(h);
    } else {
      height.set(600);
    }

    collapse = collapse ? false : true;
  };
</script>

<!-- TODO: how do you do HOC or wrapped components in Svelte? --> -->
<h3 on:click={collapseFn}>
  {#if collapse}
    <i class="las la-arrow-up"></i>
  {:else}
    <i class="las la-arrow-down"></i>
  {/if}
  {title}
</h3>

<style lang="scss">
</style>
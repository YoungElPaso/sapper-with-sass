<script>
  // Animation for collapse.
  import { fade, fly, slide } from "svelte/transition";
  import { quintOut } from "svelte/easing";

  import { spring, tweened } from "svelte/motion";

  // Collapsible.
  export let collapse = false;

  // Title prop.
  export let title;

  let contentHeight;
  let height = tweened();
  // export let height = tweened(contentHeight, { duration: 300, delay: 0 });

  // An animate property.
  // export let animate;

  export let noAnimate;

  if (noAnimate) {
    // TODO: this needs to be the caculated height of the markup being collapsed.
  } else {
    // height.set(contentHeight);
    console.log(contentHeight);
    height.set(0);
    console.log(contentHeight);
  }

  let collapseFn = function() {
    if (!noAnimate) {
      let h = collapse ? 0 : contentHeight;
      height.set(h);
    } else {
      // height.set(contentHeight);
    }

    console.log("contentHeight", contentHeight);
    collapse = collapse ? false : true;
  };
</script>

<!-- TODO: how do you do HOC or wrapped components in Svelte? -->
<h3 on:click={collapseFn}>
  {#if collapse}
    <i class="las la-arrow-up"></i>
  {:else}
    <i class="las la-arrow-down"></i>
  {/if}
  {title}
</h3>
<div class={'open-'+collapse} bind:offsetHeight={contentHeight} style="height: {$height || contentHeight}px; overflow: hidden; padding: 1em">
  <slot></slot>
</div>

<style lang="scss">
  @import "https://maxst.icons8.com/vue-static/landings/line-awesome/line-awesome/1.3.0/css/line-awesome.min.css";
</style>
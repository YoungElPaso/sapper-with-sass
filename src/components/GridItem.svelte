<script>
  export let spanOne;
  export let spanTwo;
  export let spanThree;
  export let spanFour;
</script>

<div class="gr-item" class:spanTwo  >
  <slot />
</div>

<style lang="scss">
  .gr-item {
    border: 1px #eaeaea solid;
    :global(div) {
      // Make height of contents that of grid item.
      height: 100%;
    }
  }
  .spanOne {
    grid-column: auto / span 1;
  }
  .spanTwo {
    grid-column: auto / span 2;
  }
  .spanThree {
    grid-column: auto / span 3;
  }
  .spanFour {
    grid-column: auto / span 4;
  }
</style>

<script>
  // TODO: clean these class variables up.
  export let dark;
  export let light;
</script>


<div class="tp" class:light class:dark>
	<slot></slot>
</div>

<style lang="scss">
  /* Load ThemeProvider Sass component.*/
  @use "../sass/components/ThemeProvider.scss" as TP;
  @use "sass:map";

  .tp.light {
    :global(h1),
    :global(h2) {
      color: TP.$headercolor;
    }

    :global(p),
    :global(div) {
      color: TP.$textcolor;
    }
  }

  .tp.dark {
    background-color: map.get(TP.$dark, bg);
    :global(h2) {
      color: map.get(TP.$dark, headercolor);
    }
    :global(div),
    :global(p),
    :global(section) {
      color: map.get(TP.$dark, textcolor);
    }
    :global(section),
    :global(div) {
      background-color: map.get(TP.$dark, bg);
    }
  }
</style>

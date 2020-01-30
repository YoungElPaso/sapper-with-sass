<script>
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
    :global(h2),
    :global(h3) {
      color: TP.$headercolor;
    }

    :global(p),
    :global(div) {
      color: TP.$textcolor;
    }
  }

  .tp.dark {
    :global(h2) {
      color: map.get(TP.$dark, headercolor);
    }
    :global(div),
    :global(p),
    :global(section) {
      color: map.get(TP.$dark, textcolor);
    }
    :global(section) {
      background-color: map.get(TP.$dark, bg);
    }
  }
</style>

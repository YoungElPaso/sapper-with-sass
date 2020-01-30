<script>
  export let regular;
  export let invert;
</script>

<div class="fp" class:regular class:invert>
	<slot></slot>
</div>

<style lang="scss">
  /* Load FontProvider Sass component.*/
  @use "../sass/components/FontProvider.scss" as FP;

  .fp.regular :global(h1),
  .fp.regular :global(h2) {
    @include FP.headers;
  }
  .fp.regular :global(p) {
    @include FP.regularText;
  }

  .fp.invert :global(h1),
  .fp.invert :global(h2) {
    @include FP.regularText;
  }
  .fp.invert :global(p) {
    @include FP.headers;
  }
</style>

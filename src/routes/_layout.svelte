<script>
  import Container from "../components/Container.svelte";
  import PageFooter from "../components/PageFooter.svelte";
  import PageHeader from "../components/PageHeader.svelte";
  import FontProvider from "../components/FontProvider.svelte";
  import ThemeProvider from "../components/ThemeProvider.svelte";
  import Grid from "../components/Grid.svelte";
  import GridItem from "../components/GridItem.svelte";
</script>

<Container>
  <ThemeProvider light>
    <FontProvider regular>
      <PageHeader>
        <h1>Page Header</h1>
      </PageHeader>
      <main>
        <slot></slot>
      </main>
    </FontProvider>
  </ThemeProvider>
  <ThemeProvider dark>
    <FontProvider invert>
      <PageFooter>
        <h2>Page Footer</h2>
        <p>Footer text</p>
      </PageFooter>
    </FontProvider>
  </ThemeProvider>
</Container>

<style lang="scss">
  /* Load Layout Sass component.*/
  @use "../sass/components/Layout.scss";

  /* Local overrides */
  $debug: false;
  main {
    background-color: $debug;
  }
</style>

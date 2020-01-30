<script>
  // TODO: add live-reload if possible.
  import PageHeader from "../components/PageHeader.svelte";
  import PageFooter from "../components/PageFooter.svelte";
  import FontProvider from "../components/FontProvider.svelte";
  import ThemeProvider from "../components/ThemeProvider.svelte";
  import Grid from "../components/Grid.svelte";
  import GridItem from "../components/GridItem.svelte";
</script>

<svelte:head>
  <title>Dogfood 🐶🍗🍖</title>
</svelte:head>

<p>
  By default the headers on this all use serif fonts, while the body text uses
  sans-serif fonts. But that can be overridden by adding a property called
  'invert' to the FontProvider component.
</p>
<p>
  Similarly, the default palette is darker text on light background, with a red
  color for headers. This too can be changed with a property - using the 'dark'
  palette these values are again inverted (more or less). You can see examples
  of both of these variants in action below.
</p>

<Grid triple>
  <GridItem>
    <ThemeProvider dark>
      <section>
        <h2>A dark section</h2>
        <p>Light color text</p>
      </section>
    </ThemeProvider>
  </GridItem>
  <GridItem>
    <ThemeProvider light>
      <section>
        <h2>A default section</h2>
        <p>Dark color text</p>
      </section>
    </ThemeProvider>
  </GridItem>
  <GridItem>
    <ThemeProvider dark>
      <section>
        <h2>Another dark section</h2>
        <p>Dark color text</p>
      </section>
    </ThemeProvider>
  </GridItem>
</Grid>

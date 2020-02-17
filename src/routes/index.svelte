<script>
  // TODO: add live-reload if possible.
  import PageHeader from "../components/PageHeader.svelte";
  import PageFooter from "../components/PageFooter.svelte";
  import FontProvider from "../components/FontProvider.svelte";
  import ThemeProvider from "../components/ThemeProvider.svelte";
  import Grid from "../components/Grid.svelte";
  import GridItem from "../components/GridItem.svelte";
  import Lists from "../components/Lists.svelte";
  import BoxWithCollapse from "../components/BoxWithCollapse.svelte";

  // Fake list data.
  let fakeList = [
    {
      markup: "Canadian Honey",
      active: true,
      count: 22,
      indexed_value: "canuckistani"
    },
    {
      markup: "NZ Honey",
      active: true,
      count: 10,
      indexed_value: "kiwistan"
    },
    {
      markup: "Greek Honey",
      active: false,
      count: 200,
      indexed_value: "greekish"
    },
    {
      markup: "Spanish Honey",
      active: false,
      count: 10,
      indexed_value: "spaneek"
    }
  ];
</script>

<svelte:head>
  <title>Dogfood 🐶🍗🍖</title>
  <!-- <link rel="stylesheet" href="https://maxst.icons8.com/vue-static/landings/line-awesome/line-awesome/1.3.0/css/line-awesome.min.css"> -->
</svelte:head>

<BoxWithCollapse title="Sample Collapse Box Without Animation" noAnimate> 
  <Lists bulletStyle="none" 
    items= {fakeList} title="Samples" 
  />
</BoxWithCollapse>

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

<ThemeProvider dark>
  <section>
    <h2>Here's a horizontal check list, collapsed shut (default) </h2>
    <Lists horizontal title="Honey" />
  </section>
</ThemeProvider>

<section>
  <h2>Here's a vertical (regular) check list, already open </h2>
  <BoxWithCollapse title="Types" >
    <Lists bulletStyle="none" 
    items= {fakeList} title="Types"  LoadData
  />
</BoxWithCollapse>
</section>

<Grid quad>
  <GridItem>
    <ThemeProvider dark>
      <section>
        <h2>A dark section</h2>
        <p>Light color text</p>
      </section>
    </ThemeProvider>
  </GridItem>
  <GridItem >
    <ThemeProvider light>
      <section>
        <h2>A default section</h2>
        <p>Dark color text</p>
      </section>
    </ThemeProvider>
  </GridItem>
  <GridItem spanTwo>
    <ThemeProvider dark>
      <section>
        <h2>Another dark section</h2>
        <p>Dark color text</p>
      </section>
    </ThemeProvider>
  </GridItem>
</Grid>

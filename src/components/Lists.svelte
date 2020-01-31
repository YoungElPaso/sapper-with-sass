<!-- TODO: add some basic lists markup and styling. -->
<script>
  export let horizontal;
  export let vertical;
  export let ordered;
</script>

<ul class:horizontal>
  <li>Foo</li>
  <li>Bar</li>
  <li>Foobar</li>
</ul>

<style>
  .horizontal {
    padding: 0;
  }
  .horizontal li {
    display: inline-block;
    border: 1px #aaa solid;
    padding: 0.25em 0.5em;
  }
</style>

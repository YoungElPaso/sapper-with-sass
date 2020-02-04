<script>
  // An class to switch to horizontal layout.
  export let horizontal;

  // Ditto for vertical.
  export let vertical;

  // TODO: add code to convert to ordered as option.
  export let ordered;

  // Collapsible.
  export let collapse = false;

  // Default list-style: disc, options [none, disc, alpha?]
  export let bulletStyle = "disc";

  // Title prop.
  export let title;

  // Default items.
  export let items = [
    {
      name: "Canadian Honey",
      active: false,
      count: 22,
      slug: "canuck"
    },
    {
      name: "NZ Honey",
      active: false,
      count: 10,
      slug: "kiwi"
    },
    {
      name: "Greek Honey",
      active: false,
      count: 200,
      slug: "greek"
    },
    {
      name: "Spanish Honey",
      active: false,
      count: 10,
      slug: "spanish"
    }
  ];
</script>

<!-- Not really a generic list ATM but adaptable to be one.
TODO: move this to a new component CheckList
TODO: how do you do HOC or wrapped components in Svelte? -->
<ul class:horizontal class={bulletStyle + ' ' + 'open-'+collapse}>
  <h3 on:click="{()=> collapse= collapse? false:true }">
    {#if collapse}
      <i class="las la-arrow-up"></i>
    {:else}
      <i class="las la-arrow-down"></i>
    {/if}
  {title || 'List Title'}
  </h3>
  {#each items as {name, active, count, slug} }
    <li class:active>
      <input hidden type="checkbox" bind:checked={active} id={slug} />
      <label for={slug}>
      {#if active}
        <i class="las la-check-square"></i>
      {:else}
        <i class="las la-stop"></i>
      {/if}
      {name}
      </label> ({count})
    </li>
  {:else}
    <li>Foo</li>
    <li>Bar</li>
    <li>Foobar</li>
  {/each}
</ul>

<style lang="scss">
  /* Imports basic Lists styling.*/
  @import "../sass/components/Lists.scss";

  /* Imports basic Forms styling. TODO: add this file. */
  /* @import "../sass/components/Forms.scss"; */
</style>

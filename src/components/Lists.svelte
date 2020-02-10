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
  export let shmitems = [
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

  async function getData() {
    // Faking a request.
    // let fakeRequest = new Promise((res, rej) => {
    //   setTimeout(() => res(shmitems), 1500);
    // });
    // Getting data from JSON.
    let response = await fetch("/facetdata.json");
    let data = await response.json();
    // let items = await fakeRequest;
    let items = data.facetjson;
    console.log(data);
    items = Object.values(items);
    console.log(items);
    return items;
  }

  // Sets the getItems property to the async function.
  let getItems = getData();

  // function isActive(status) {
  //   let active = status == 1 ? true : false;
  // }
  // let active;
  // // $: realActive = (active == 1) ? true : false;
  // $: realActive = function(active) {
  //   return active == 1;
  // };
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
  {#await getItems}
    <li>Fetching data...</li>
  {:then items}
    <!-- {#each items as {name, active, count, slug} } -->
    {#each items as {markup, active, count, indexed_value}}
      <li class:active>
        <input type="checkbox" bind:checked={active} id={indexed_value+title.replace(/\s+/g, '')} />
        <label for={indexed_value+title.replace(/\s+/g, '')}>
        {#if active}
          <i class="las la-check-square"></i>
        {:else}
          <i class="las la-stop"></i>
        {/if}
        {markup} {active}
        </label> ({count})
      </li>
    {:else}
      <li>Foo</li>
      <li>Bar</li>
      <li>Foobar</li>
    {/each}
  {:catch error}
    <li>Error!</li>
  {/await}
</ul>

<style lang="scss">
  /* Imports basic Lists styling.*/
  @import "../sass/components/Lists.scss";

  /* Imports basic Forms styling. TODO: add this file. */
  /* @import "../sass/components/Forms.scss"; */
</style>

<script>
  // Animation for collapse.
  import { fade, fly, slide } from "svelte/transition";
  import { quintOut } from "svelte/easing";

  import { spring, tweened } from "svelte/motion";

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
    // console.log(data);
    items = Object.values(items);
    // console.log(items);
    return items;
  }

  // LoadData prop.
  // Controls recursion.
  export let LoadData = false;

  // Defaults to an empty array.
  export let items = [];
  let getItems;
  if (LoadData) {
    // Sets the getItems property to the async function.
    getItems = getData();
  } else {
    getItems = Object.values(items);
  }
  // console.log("items", items);

  // function isActive(status) {
  //   let active = status == 1 ? true : false;
  // }
  // let active;
  // // $: realActive = (active == 1) ? true : false;
  // $: realActive = function(active) {
  //   return active == 1;
  // };

  export let height = tweened(0, { duration: 300, delay: 0 });

  // $: realHeight = height;
  // ? 100 : 0;

  // return active == 1;
  // };
  // An animate property.
  // export let animate;

  export let noAnimate;
  if (noAnimate) {
    height.set(600);
  }

  let collapseFn = function() {
    if (!noAnimate) {
      let h = collapse ? 0 : 600;
      height.set(h);
    } else {
      height.set(600);
    }

    collapse = collapse ? false : true;
  };
</script>

<!-- Not really a generic list ATM but adaptable to be one.
TODO: move this to a new component CheckList
TODO: how do you do HOC or wrapped components in Svelte? -->
{#if title}
  <h3 on:click={collapseFn}>
    {#if collapse}
      <i class="las la-arrow-up"></i>
    {:else}
      <i class="las la-arrow-down"></i>
    {/if}
  {title || 'List Title'}
  </h3>
  {/if}

  <ul class:horizontal class={bulletStyle + ' ' + 'open-'+collapse}
  style="max-height: {$height}px; overflow: hidden;" >
  {#await getItems}
    <li>Fetching data...</li>
  {:then items}
    <!-- {#each items as {name, active, count, slug} } -->
    {#each items as {markup, active, count, indexed_value, item_children}}
    <!-- {#if items} -->
      <li class:active transition:fade="{{delay: 300}}"> 
        <input type="checkbox" hidden bind:checked={active} id={indexed_value+title.replace(/\s+/g, '')} />
        <label for={indexed_value+title.replace(/\s+/g, '')}>
        {#if active}
          <i class="las la-check-square" ></i>
        {:else}
          <i class="las la-stop" ></i>
        {/if}
        {markup}
        </label> ({count})
      {#if item_children}
         <div transition:fade="{{delay: 300}}">
          <!-- TODO: need to rethink approach to transitions. Its a bit janky. Child list pops in and out of existence. -->
            <svelte:self bulletStyle="none" items={item_children} title="" noAnimate  collapse />
          </div>
      {/if}
      </li>
      <!-- {/if} -->
    {/each}
  {:catch error}
    <li>Error!</li>
  {/await}
</ul>

<style lang="scss">
  @import "https://maxst.icons8.com/vue-static/landings/line-awesome/line-awesome/1.3.0/css/line-awesome.min.css";

  /* Imports basic Lists styling.*/
  @import "../sass/components/Lists.scss";

  /* Imports basic Forms styling. TODO: add this file. */
  /* @import "../sass/components/Forms.scss"; */
</style>

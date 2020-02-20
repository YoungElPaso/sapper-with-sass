<script>
  // Animation for transitions.
  import { fade, fly, slide } from "svelte/transition";
  import { quintOut } from "svelte/easing";

  import { spring, tweened } from "svelte/motion";

  import { Component } from "svelte";

  // An class to switch to horizontal layout.
  export let horizontal;

  // Ditto for vertical.
  export let vertical;

  // If set, use an <ol> for ordered list.
  export let ordered;

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

  // Get's data as an async function.
  // Returns a an array of items for the list to render.
  async function getData() {
    // Getting data from JSON.
    let response = await fetch("/facetdata.json");
    let data = await response.json();

    // TODO: there should be a dataMapping function that can handle differently structured data.
    // Get the right key.
    let items = data.facetjson;

    // Get an array of the values of the items.
    items = Object.values(items);
    return items;
  }

  // LoadData prop.
  // Controls recursion. Svelte allows components to nest themselves, but often we don't want to fetch data on nested lists.
  export let LoadData = false;

  // Defaults to an empty array.
  export let items = [];

  // Variable to hold items retrieved from getData.
  let getItems;
  if (LoadData) {
    // Sets the getItems property to the async function.
    getItems = getData();
  } else {
    getItems = Object.values(items);
  }

  // let RenderTag = ordered ? "<ol>" : "<ul>";
  // TODO: trying ClientSide API for dynamic component.
  // const RenderTag = new Component({
  //   target: null
  // });
</script>

<!-- Not really a generic list ATM but adaptable to be one.
TODO: move this to a new component CheckList? - all the form stuff seems to suggest that.
TODO: how do you do HOC or wrapped components in Svelte? -->

<!-- TODO: remove data loading stuff into own component that does that, loading, then passing results to List -->
<!-- TODO: get a sample of Fusion API query/results use as sample for results List.  -->
<!-- TODO: remove a bunch of comments etc, be aggressive about refactoring. -->

<!-- Optional title? -->
<!-- {title} -->

<!-- Logic for ordered list markup <ol> --> 
<!-- {#if ordered} -->
<!-- Cant have this conditional Structure, svelte errors, probably doesnt want unclosed tag -->
  <!-- <ol class:horizontal class={bulletStyle}> -->
<!-- {:else} -->
  <!-- <ul class:horizontal class={bulletStyle}> -->
  <!-- <svelte:component this={'ul'} /> -->
  RenderTag: {@html RenderTag}
  <!-- TODO: check out using 'Use' if that helps  -->
  <!-- TODO: perhaps Each block could work like a switch since there's fallback to each? -->
  <!-- TODO: yeah, Each could be used if restructure array's a bit...I think. -->
<!-- {/if} -->
 

<!-- TODO: Yeah, probably should just have a wrapper element ListShell or something that determines type of list that renders actual list items in ListItems component. -->
<!-- TODO: Could I use the Client Side API to dynamically do this? Probably. -->
  <ul class:horizontal class={bulletStyle}>
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
            <svelte:self bulletStyle="none" items={item_children} title="" noAnimate />
          </div>
      {/if}
      </li>
      <!-- {/if} -->
    {/each}
  {:catch error}
    <li>Error!</li>
  {/await}
<!-- <!-- {#if ordered}
  </ol>
{:else}  --> 
  </ul>
<!-- {/if} -->
<style lang="scss">
  @import "https://maxst.icons8.com/vue-static/landings/line-awesome/line-awesome/1.3.0/css/line-awesome.min.css";

  /* Imports basic Lists styling.*/
  @import "../sass/components/Lists.scss";

  /* Imports basic Forms styling. TODO: add this file. */
  /* @import "../sass/components/Forms.scss"; */
</style>

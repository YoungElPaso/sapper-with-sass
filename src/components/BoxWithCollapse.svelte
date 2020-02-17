<script>
  // Animation for collapse.
  import { fade, fly, slide } from "svelte/transition";
  import { quintOut } from "svelte/easing";

  import { spring, tweened } from "svelte/motion";

  import { beforeUpdate, afterUpdate, onMount, tick } from "svelte";

  // Collapsible.
  export let collapse = false;

  // Title prop.
  export let title;

  // An animate property.
  // export let animate;

  export let noAnimate;

  // A tweened value - that is 'animated'. Duration = 0 if noAnimate prop is set.
  let height = tweened(0, { duration: noAnimate ? 0 : 100, delay: 0 });

  // // This is the right idea...to use an async call to set the styled height only after the actual content height is determined.
  // // BUT! I think Svelte has lifecycle functions that are better at this... in fact, the tutorial addresses almost exactly this type of use case...
  // function getInitHeight() {
  //   return new Promise(resolve => {
  //     resolve(50);
  //   });
  // }

  // reference to the box that contains the contents.
  let box;
  // , slotBox;
  // slotBox = "foobar";
  // let heightSet = false; //
  // This is a good place for it, but the component monuts before the slot I think.
  // onMount(() => {
  //   // Only do this once(?)
  //   // if (box && !heightSet) {
  //   // let actualHeight = box && box.offsetHeight;
  //   // contentHeight = actualHeight;
  //   // console.log("actual height", actualHeight, contentHeight, box);
  //   // heightSet = true;
  //   // } // TODO: this generally works, needs some work. Should probably only run once. Maybe use onMount? But generally good enough at the moment.
  // });

  // afterUpdate(() => {
  //   // So this sort of works too. but I got caught out by the async of the content- the List component itself loads async so its height isn't determined right away.
  //   // Need to use Tick I bet.
  //   console.log("post-update:", box);
  //   contentHeight = box.offsetHeight;
  // });

  // tick(() => {
  //   console.log(box.offsetHeight);
  //   contentHeight = box.offsetHeight;
  // });

  // async function setHeight() {
  //   let result = await getInitHeight();
  //   // console.log("promised result", result);
  //   return result;
  // }

  // setHeight();

  // if (noAnimate) {
  //   // TODO: this needs to be the caculated height of the markup being collapsed.
  // } else {
  //   // height.set(contentHeight);
  //   // console.log(contentHeight);
  //   // height.set(0);
  //   // console.log(contentHeight);
  // }

  let collapseFn = function() {
    // if (!noAnimate) {
    // Assign 0 or box.offsetHeight (height of content of child in slot).
    let h = collapse ? 0 : box.offsetHeight;
    height.set(h);
    // } else {
    //   // Set height, but with no tweening.
    //   height.set(contentHeight);
    //   let h = collapse ? 0 : box.offsetHeight;
    // }

    // console.log("contentHeight", contentHeight);
    collapse = collapse ? false : true;
  };
</script>

<!-- TODO: how do you do HOC or wrapped components in Svelte? -->
<h3 on:click={collapseFn}>
  {#if collapse}
    <i class="las la-arrow-up"></i>
  {:else}
    <i class="las la-arrow-down"></i>
  {/if}
  {title}
</h3>
<!-- bind:offsetHeight={contentHeight} -->
<div class={'collapse-box open-'+collapse}  style="height: {$height || 0}px; overflow: hidden;">
  <div bind:this={box}>
    <slot></slot>
  </div>
</div>

<style lang="scss">
  @import "https://maxst.icons8.com/vue-static/landings/line-awesome/line-awesome/1.3.0/css/line-awesome.min.css";
  .collapse-box div {
    padding-bottom: 1em;
  }
</style>
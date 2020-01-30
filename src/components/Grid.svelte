<div class="gr" class:double class:triple class:quad>
  <slot />
</div>

<style lang="scss">
  .gr,
  .gr.double {
    display: grid;
    grid-template-columns: 1fr 1fr;
  }
  .gr.triple {
    grid-template-columns: 1fr 1fr 1fr;
  }
  .gr.quad {
    grid-template-columns: 1fr 1fr 1fr 1fr;
  }
</style>

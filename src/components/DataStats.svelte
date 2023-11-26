<script>
  import { tweened } from "svelte/motion";

  export let statColor;
  export let value;

  let amount = tweened(0);
  $: amount.set(value);
</script>

<div class="progressbar-container">
  <span class="value-text">{value}</span>

  <div class="progressbar">
    <div class="progressbar-item" style="width: {$amount}%; background-color: var({statColor});">
    </div>
  </div>
</div>

<style>
  .progressbar-container {
    display: flex;
    align-items: center;
  }

  .progressbar-container .value-text {
    flex-basis: auto;
    margin-right: var(--gutter);
  }

  .progressbar {
    flex: 1 0 auto;
    display: inline-flex;
    height: 0.75rem;
    border-radius: 0.5rem;
    outline: 1px solid transparent;
    background-color: var(--color-link-border);
    overflow: hidden;
  }

  .progressbar-item {
    outline: 2px solid transparent;
  }
</style>

<script>
  export let name;
  export let color;
</script>

<span class="pokemon-type" style="background-color: var({color});">
  {name}
</span>

<style>
  .pokemon-type {
    display: block;
    width: 66px;
    font-size: 0.75rem;
    line-height: 1.75;
    letter-spacing: 0.05em;
    color: #fff;
    text-shadow: 1px 1px 2px var(--color-details);
    text-align: center;
    border: 1px solid var(--color-details);
    border-radius: 4px;
    margin: 0.05rem;
    -webkit-user-select: none;
    user-select: none;
    cursor: default;
  }
</style>

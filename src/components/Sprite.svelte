<script>
  export let sprites;
</script>

<figure class="pokemon-sprites">
  {#if sprites.front_default}
    <img alt="Front of the Pokémon" src={sprites.front_default} />
  {/if}
  {#if sprites.back_default}
    <img alt="Back of the Pokémon" src={sprites.back_default} />
  {/if}

  {#if sprites.front_female}
    <img alt="Front of the female Pokémon" src={sprites.front_female} />
  {/if}
  {#if sprites.back_female}
    <img alt="Back of the female Pokémon" src={sprites.back_female} />
  {/if}

  {#if sprites.front_shiny}
    <img
      alt="Front of the Shiny variant of the Pokémon"
      src={sprites.front_shiny}
    />
  {/if}
  {#if sprites.back_shiny}
    <img
      alt="Back of the Shiny variant of the Pokémon"
      src={sprites.back_shiny}
    />
  {/if}

  {#if sprites.front_shiny_female}
    <img
      alt="Front of the Shiny variant of the female Pokémon"
      src={sprites.front_shiny_female}
    />
  {/if}
  {#if sprites.back_shiny_female}
    <img
      alt="Back of the Shiny variant of the female Pokémon"
      src={sprites.back_shiny_female}
    />
  {/if}
</figure>

<style>
  .pokemon-sprites {
    margin: var(--gutter) 0;
    padding: 0;
    text-align: center;
  }
</style>

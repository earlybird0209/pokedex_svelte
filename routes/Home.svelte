<script>
  import ky from "ky";

  import PokeCard from "../src/components/PokeCard.svelte";

  let pokemons = [];
  let offset = 0;
  let perPage = 24;

  $: {
    getPokemon(offset);
  }

  const getPokemon = async () => {
    let requestURL = `https://pokeapi.co/api/v2/pokemon/?offset=${offset}&limit=${perPage}`;
    const data = await ky.get(requestURL).json();

    pokemons = [...pokemons, ...data.results];
  };

  const loadMore = () => {
    offset += perPage;
  };
</script>

<ol class="pokemon-list">
  {#each pokemons as { name, url } (url)}
    <li>
      <PokeCard {name} {url} />
    </li>
  {/each}
</ol>

<button type="submit" id="load-more" on:click={loadMore}>
  Load more Pokémon!
</button>

<style>
  .pokemon-list {
    padding-left: 0;
    margin: 0;
    list-style: none;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: var(--gutter);
    margin-bottom: 2rem;
  }

  @media screen and (max-width: 600px) {
    .pokemon-list {
      grid-template-columns: 1fr 1fr;
    }
  }

  #load-more {
    font: inherit;
    appearance: none;
    margin-bottom: 3rem;
    border-radius: 0;
    display: block;
    width: 100%;
    padding: var(--gutter);
    background: transparent;
    border: none;
    color: var(--color-link);
    border-bottom: 1px solid var(--color-link-border);
    cursor: pointer;
    font-weight: 700;
  }

  #load-more:hover,
  #load-more:active {
    color: var(--color-link-hover);
    border-bottom-color: var(--color-link-border-hover);
  }
</style>

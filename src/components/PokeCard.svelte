<script>
  import { Link } from "svelte-routing";

  export let name;
  export let url;

  const splittedURL = url.split("/");
  const indexLocation = splittedURL.length - 2;

  const index = splittedURL[indexLocation];

  const imgURL = `//raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index}.png`;
</script>

<figure class="pokecard">
  <Link to="/{index}">
    <img
      class="sprite"
      alt="{name.toUpperCase()} sprite"
      src={imgURL}
      role="presentation"
    />
  </Link>

  <figcaption>
    <Link to="/{index}">
      <span class="dex-id">#{index}</span>
      <strong class="pokemon-name">{name.toUpperCase()}</strong>
    </Link>
  </figcaption>
</figure>

<style>
  .pokecard {
    margin: 0;
    text-align: center;
  }

  .pokecard .sprite {
    display: block;
    max-width: 100%;
    margin-left: auto;
    margin-right: auto;
  }
</style>

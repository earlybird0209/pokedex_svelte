<script>
  import { Link } from "svelte-routing";

  import DataStats from "./DataStats.svelte";
  import Sprites from "./Sprite.svelte";
  import Type from "./Type.svelte";

  export let pokemon;
</script>

<header class="pokedetails-header">
  <h2><span class="dex-number">#{pokemon.id}</span> {pokemon.name}</h2>

  <ul class="pokemon-type-list">
    {#each pokemon.types as type (type.name)}
      <li>
        <Type name={type.name} color={type.color} />
      </li>
    {/each}
  </ul>

  <p>{pokemon.description}</p>
</header>

<Sprites sprites={pokemon.sprites} />

<div class="datagroups" style="--color-theme: var({pokemon.detailTheme});">
  <section class="dataset">
    <h3>Profile</h3>
    <dl>
      <dt>Species:</dt>
      <dd>{pokemon.species}</dd>
      <dt>Height:</dt>
      <dd>
        {pokemon.height / 10} m ({Math.round(
          (pokemon.height * 0.328084 + 0.00001) * 100
        ) / 100}
        lb)
      </dd>
      <dt>Weight:</dt>
      <dd>
        {pokemon.weight / 10} kg ({Math.round(
          (pokemon.weight * 0.220462 + 0.00001) * 100
        ) / 100}
        lb)
      </dd>
      <dt>Abilities:</dt>
      <dd>{pokemon.abilities}</dd>
    </dl>
  </section>

  <section class="dataset">
    <h3>Training Stats</h3>
    <dl>
      <dt>EV Yield:</dt>
      <dd>{pokemon.evs}</dd>
      <dt>Capture Rate:</dt>
      <dd>{pokemon.captureRate}</dd>
      <dt>Growth Rate:</dt>
      <dd>{pokemon.growthRate}</dd>
    </dl>
  </section>

  <section class="dataset">
    <h3>Breeding Stats</h3>
    <dl>
      <dt>Gender Ratio:</dt>
      <dd>
        <p>
          Female:<br />
          <DataStats
            value={pokemon.genderRatio.female}
            statColor={pokemon.detailTheme}
          />
        </p>
        <p>
          Male:<br />
          <DataStats
            value={pokemon.genderRatio.male}
            statColor={pokemon.detailTheme}
          />
        </p>
      </dd>
      <dt>Egg Groups:</dt>
      <dd>
        {#each pokemon.eggGroups as egg}{egg}{/each}
      </dd>
    </dl>
  </section>

  <section class="dataset">
    <h3>Base Stats</h3>
    <dl>
      {#each pokemon.stats as stat}
        <dt>{stat.name}:</dt>
        <dd>
          <DataStats value={stat.base_stat} statColor={pokemon.detailTheme} />
        </dd>
      {/each}
    </dl>
  </section>
</div>

<footer>
  {#if pokemon.evolvesFrom}
    <p>
      {pokemon.name} evolves from
      <Link to="/{pokemon.evolvesFrom.url}">
        <span class="dex-number">#{pokemon.evolvesFrom.url}</span>
        <strong>
          {pokemon.evolvesFrom.name}
        </strong>.
      </Link>
    </p>
  {:else}
    <p>{pokemon.name} does not evolve from another Pokémon.</p>
  {/if}
</footer>

<style>
  .pokedetails-header {
    margin-bottom: 3rem;
  }

  .pokedetails-header .dex-number {
    font-weight: 400;
  }

  .pokedetails-header .pokemon-type-list {
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
  }

  .datagroups {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: var(--gutter);
  }

  @media screen and (max-width: 600px) {
    .datagroups {
      grid-template-columns: 1fr;
    }
  }

  dl {
    border: 1px solid var(--color-link-border);
    border-radius: 4px;
    font-size: 0.75rem;
  }

  dl dt {
    font-weight: 700;
    background: var(--color-theme);
    color: #fff;
    text-shadow: 1px 1px 2px var(--color-details);
  }

  dl dt,
  dl dd {
    padding: 0.5rem;
    margin: 0;
  }

  footer {
    text-align: center;
  }
</style>

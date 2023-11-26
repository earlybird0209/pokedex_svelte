<script>
  import ky from "ky";
  import PokeDetail from "../src/components/PokeDetail.svelte";

  export let id;
  export let pokemon;

  let loading;
  let error;

  const TYPE_COLORS = {
    bug: "--type-bug",
    dark: "--type-dark",
    dragon: "--type-dragon",
    electric: "--type-electric",
    fairy: "--type-fairy",
    fighting: "--type-fighting",
    fire: "--type-fire",
    flying: "--type-flying",
    ghost: "--type-ghost",
    grass: "--type-grass",
    ground: "--type-ground",
    ice: "--type-ice",
    normal: "--type-normal",
    poison: "--type-poison",
    psychic: "--type-psychic",
    rock: "--type-rock",
    steel: "--type-steel",
    water: "--type-water",
  };
  const getPokemon = async (id) => {
    const pokeURL = `https://pokeapi.co/api/v2/pokemon/${id}/`;
    const pokeSpeciesURL = `https://pokeapi.co/api/v2/pokemon-species/${id}/`;

    /*
      Flavor text is a huge array, so we will randomize which text will be shown
      for fun!
    */

    const getFlavorText = (flavorTexts) => {
      let pokeDescription = [];

      pokeDescription = flavorTexts
        .filter((flavor) => flavor.language.name === "en")
        .map((item) => item.flavor_text);

      const randomIndex = Math.floor(Math.random() * pokeDescription.length);

      return pokeDescription[randomIndex];
    };

    try {
      loading = true;

      const pokeStats = await ky.get(pokeURL).json();
      const pokeSpecies = await ky.get(pokeSpeciesURL).json();

      const {
        name,
        types,
        sprites,
        stats,
        height,
        weight,
        abilities,
      } = pokeStats;
      const {
        flavor_text_entries,
        capture_rate,
        growth_rate,
        gender_rate,
        egg_groups,
        evolves_from_species,
        genera,
      } = pokeSpecies;

      // Setting detail theme (using the Pokémon type).
      const detailTheme = TYPE_COLORS[types[0].type.name];

      // Description.
      const detailDescription = getFlavorText(flavor_text_entries);

      // Stats
      const detailStats = stats.map((stat) => {
        return {
          name: stat.stat.name.toUpperCase().replace("-", " "),
          base_stat: stat.base_stat,
        };
      });

      // Growth rate
      const growthRate = growth_rate.name.toUpperCase().replace("-", " ");

      // Gender ratio
      const genderRate = gender_rate;
      const genderRatio = {
        female: 12.5 * genderRate,
        male: 12.5 * (8 - genderRate),
      };

      // Eggs
      const eggGroups = egg_groups
        .map((group) => group.name.toUpperCase(group.name, " "))
        .join(", ");

      // Abilities
      const detailAbilities = abilities
        .map((ability) => ability.ability.name.toUpperCase().replace("-", " "))
        .join(", ");

      // EVs
      const evs = stats
        .map(
          (stat) =>
            `${stat.effort} ${stat.stat.name.toUpperCase().replace("-", " ")}`
        )
        .join(", ");

      // Evolution
      let evolvesFrom = undefined;

      if (evolves_from_species) {
        evolvesFrom = {
          name: evolves_from_species.name.toUpperCase(),
          url: evolves_from_species.url.split("/")[
            evolves_from_species.url.split("/").length - 2
          ],
        };
      }

      // Species
      const species = genera.filter((genus) => genus.language.name === "en")[0]
        .genus;

      pokemon = {
        id,
        name: name.toUpperCase(),
        types: types.map((type) => ({
          name: type.type.name.toUpperCase(),
          color: TYPE_COLORS[type.type.name.toLowerCase()],
        })),
        description: detailDescription,
        sprites,
        stats: detailStats,
        height,
        weight,
        captureRate: capture_rate,
        growthRate,
        detailTheme,
        genderRatio,
        eggGroups,
        abilities: detailAbilities,
        evs,
        evolvesFrom,
        species,
      };

      loading = false;
    } catch (e) {
      loading = false;

      const serverMessage = await e.response.text();

      error = serverMessage;
    }

    console.debug(pokemon);
  };

  $: getPokemon(id);
</script>

<article>
  {#if error}
    {error}
  {:else if loading}
    Loading
  {:else}
    <PokeDetail {pokemon} />
  {/if}
</article>

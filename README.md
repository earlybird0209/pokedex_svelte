# @arthrfrts' Pokédex

This is a simple Pokédex made with [Svelte](https://svelte.dev), using data from the [PokéAPI](https://pokeapi.co).

You can see it live at [arthrfrts-pokedex.vercel.app](https://arthrfrts-pokedex.vercel.app).

## Installing

If you want to install this project locally and make changes, follow these three beautifully simple steps:

```bash
$ git clone git@github.com:arthrfrts/pokedex
$ cd pokedex
$ npm i
```

Now you have this repo in your local machine! Let's run [Rollup](https://rollupjs.org) and start making changes

```bash
$ npm run dev
```

Now the Pokédex wil be live on [localhost:5000](http://localhost:5000). Edit a component file in `src`, save it, and your browser will reload the page to show your changes.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

If you're using [Visual Studio Code](https://code.visualstudio.com/), it's recommended to install the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.
## Building and deploying

Svelte is hugely optimized for production. In fact, it makes the hard work while building, so the final product will be light on your visitors.

To build a production-ready version of the project, run:

```bash
$ npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com).

### Deploying

#### With [Vercel](https://vercel.com)

If you never used Vercel before, you need to install it:

```bash
$ npm install -g vercel
```

(You also need to create an account at <vercel.com>).

Then, from within your project folder:

```bash
$ cd public
$ vercel deploy
```

## License

The Pokémon data is property of (c) Nintendo, Ltd., Creatures, Inc and The Pokémon Company.

The data used by this Pokédex comes from PokéAPI, made by [their awesome contributors](https://github.com/PokeAPI/pokeapi#contributing).

This repo is licensed under the MIT License. Copy it, use it and change anything you want. Make it better and tell me about it!

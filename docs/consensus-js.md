# JavaScript

## Language
Whenever writing comments, variable names, etc. you use the **English** language. If projects become open source, a larger community must be able to understand the syntax.

## Style guides
The use of style guides (in combination with automatic linting tools e.g. eslint) is very effective. There are a lot of guides available:

- [Airbnb](https://github.com/airbnb/javascript)
- [Google Style Guide](https://google.github.io/styleguide/jsguide.html)
- [Idiomatic](https://github.com/rwaldron/idiomatic.js/)
- [Standard](https://github.com/standard/standard)

**Style guide to use:** Airbnb
**Linting tool to use:** ESLint

## Bundlers
For bundling larger applications we can use several different tools:

- [Webpack](https://webpack.js.org/)
- [Parcel](https://parceljs.org/)
- [rollup](https://rollupjs.org/guide/en/)
- [Vite](https://vitejs.dev/)

**Bundler to use**: Vite

When creating React applications, instead of using the create-react-app tool (which is webpack under the hood), you should prefer the Vite tool. In [the documentation of Vite](https://vitejs.dev/guide/#scaffolding-your-first-vite-project), you'll find more information on initialising different projects (Vanilla, React, Vue, ...).
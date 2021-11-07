# Pokedex made with SvelteKit
## Setup
Here's some config-steps I did before I started digging into creating the actual pokedex app  

### Create a new SvelteKit project  
```bash
    npm init svelte@next svelte-pokedex  
``` 
+ Which Svelte app template? > Skeleton Project  
+ Use Typescript? > No  
+ Add ESLint for code linting? > Yes  
+ Add Prettier for code formatting? > Yes  
<br>  

### Init node_modules and install dependencies  

```bash
    cd svelte-pokedex ; npm i && npm i -D tailwindcss autoprefixer  
``` 
### Config external dependencies 
First we'll add a postcss config file and add the plugins needed
```bash  
    echo 'module.exports = {plugins: {autoprefixer: {},tailwindcss: {},}}' > postcss.config.cjs
```  
The next thing we need is a tailwindcss config file which we'll initiate with the following command  
```bash  
    echo 'module.exports = {mode: 'jit',purge: ['./src/**/*.svelte']};' > tailwindcss.config.cjs
```   

Create a new svelte component called <strong>__layout.svelte</strong> with the following code;  
```html
<script>  
    import Nav from '../components/nav.svelte';  
</script>  
<div class="p-8 max-w-6xl mx-auto">  
     <Nav/> <!--The Nav component needs to exist in order for this to work-->  
    <slot></slot>  
</div>  
  
<style>  
    @tailwind base;  
    @tailwind components;  
    @tailwind utilities;  
</style>  
```  
That's it 😃 Now everything is setup and you can start to work on your web app  

## Developing

Once you've cloned the repository and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

Before creating a production version of your app, install an [adapter](https://kit.svelte.dev/docs#adapters) for your target environment. Then:

```bash
npm run build
```

> You can preview the built app with `npm run preview`, regardless of whether you installed an adapter. This should _not_ be used to serve your app in production.

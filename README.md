# vite-crash-course

My first project in Vite. Following the official docs.
Created by lilKriT.

# Tutorial

`yarn create vite`

then, follow the instructions.

`index.html` is the entry point.
Vite will find any code references in it, and it will rebase all the URLs.
It can support multiple .html entry points.
Root is referenced as <root>
You can change current root with
`vite serve some/sub/dir`

Run:
`dev` or `vite`, `vite dev`, `vite serve`
`build` or `vite build`
`preview` or `vite preview` (this makes a production build and runs it locally)

# Features

Vite will:

- pre-bundle imports for you `import {something} from "somewhere"`
- HMR - for example, React Fast Refresh
- TS - vite only does transpilation. it doesn't check types. (for that you need build process, like `tsc --noEmit`). check docs for more info.
- JSX - out of the box.
- CSS - will be injected as <style> tag. all the URL will be rebased. (you can turn off inline injection by adding ?inline)
- Sass, Less etc - you don't need any plugins but you need the compilers. (`yarn add -D sass`)
- static assets - urls will be resolved. you can use modifiers like `?url`, `?raw`, `?worker` you can even combine them
- JSON - out of the box
- Glob - `import.meta.glob('./dir/*.js`)
- dynamic import (`const module = await import(./path)`)
- WASM - import with `?init` modifier
- Web Workers (for example `const worker = new Worker(new URL("./worker.js", import.meta.url));`) or add `?worker?` modifier

Build optimizations:

- CSS code splitting
- preload directives
- async chunk loading
  (all by default)

# Plugins

add to devDependencies
include in `plugins` array

Enforcing plugin order:
`enforce: 'pre'`
`enforce: 'post'`

Conditional Application - if you need a plugin only for build or production:
`apply: 'build'` or `apply: 'serve'`

# Dependency pre-bundling

Speeds everything up.
Vite will discover dependencies on it's own.
You can manually include dependencies too.

# Static asset handling

Vite will find the proper URL whenever needed. You can use both relative and absolute paths.
You can use modifiers to import in a specific way
`?url`
`?raw`
`?worker`

Public folder
You put all the stuff that doesn't get referenced (robots.txt for example), has to maintain the same name.
Use absolute path for them.

# Building for production

`vite build`

If you need root url in a dynamically concatenated URL, use `import.meta.env.BASE_URL`

You can customize rollup options with https://rollupjs.org/guide/en/#big-list-of-options

Chunking strategy - works be default, can be customized
Rebuild file changes - can be turned on `vite build --watch`
Multi page apps:
Specify all the entry points

```
rollupOptions: {
  input: {
    main: resolve(__dirname, 'index.html`),
    nested: resolve(__dirname, 'nested/index.html')
  }
}
```

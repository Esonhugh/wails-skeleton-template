# SvelteKit + TypeScript

## About

SvelteKit + Typescript Template for Wails

**Thank you** to [@figuerom16](https://github.com/figuerom16) for the sveltekit guide in the _next_ documentation. It was essential in creating this work.

[![buy me a beer](README.png)](https://www.buymeacoffee.com/haukened)

## Using this template

To use this template, run `wails init` with the following options:

`wails init -n <your_project_name> -t https://github.com/haukened/wails-sveltekit-ts`

or, if you use vscode:

`wails init -n <your_project_name> -t https://github.com/haukened/wails-sveltekit-ts -ide vscode`


## Information about setup

Please see [this wails.io page](https://wails.io/docs/next/guides/sveltekit/) for more detailed information about using SvelteKit with wails.

## Important Notes

1. Server files will cause build failures.  Because wails serves SvelteKit as a static site, using any `+layout.server.ts`, `+page.server.ts`, or `+server.ts` pages will fail to build since all routes are pre-rendered.

1. Anything that causes full page navigation (like `window.location.href = '/<some>/<page>`) or reloads when using wails dev.  What this means is possibly losing the ability to call any runtime, and breaking the app.  Work around this by using the svelte `goto` function from `$app/navigation`. More details [here](https://wails.io/docs/next/guides/sveltekit/#3-important-notes).

1. Server files notwithstanding, `+page.ts`, works well with load() functions in the typical sveltekit way, like this:

`+page.ts`
```
import { Greet } from '$lib/wailsjs/go/main/App';
import type { PageLoad } from './$types';

export const load: PageLoad = async () => {
    let response = await Greet('')
    return {greeting: response}
}
```
`+page.svelte`
```
<script lang="ts">
    import type {PageData} from './$types';
    export let data: PageData;
</script>

{data.greeting}
```

## Live Development

To run in live development mode, run `wails dev` in the project directory. In another terminal, go into the `frontend`
directory and run `npm run dev`. The frontend dev server will run on http://localhost:34115. Connect to this in your
browser and connect to your application.

## Building

To build a redistributable, production mode package, use `wails build`.
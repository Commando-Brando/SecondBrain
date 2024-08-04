TARGET DECK: TechStack::NextJs
## next.config.js

#### Speeds up builders
Use Github actions to check for these errors instead of host build step
```ts
const config = {
    typescript: {
        ignoreBuildErrors: true,
    },
    eslint: {
        ignoreDuringBuilds: true,
    }
};
```


## package.json

Add `--turbo` to next dev command to get turbo pack benefits of dev local server being much faster
`"dev": "next dev --turbo",`
# Absolute Imports Path in CRA

## Configure `jsconfig.json`

Create a `jsconfig.json` file at your root directory.

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "jsx": "react",
    "paths": {
      "@/*": ["src/*"]
    }
  },
  "exclude": ["node_modules"]
}
```

compilerOptions:

- baseUrl - relative to which root dir
- jsx - must provide 'react' to let vscode know it's react project to enable auto-imports behavior.
- paths - alias mapping, must using `craco-alias` if this prop provided
- exclude - just node_modules

## Configure Craco & Craco Alias

If we need alias mapping ability, we should use `@craco/craco` to inject webpack configuration without ejecting the CRA webpack stuff.

Install

```shell
yarn add @craco/craco craco-alias -D
```

Create `craco.config.js` in root directory

```js
const CracoAlias = require('craco-alias')

module.exports = {
  plugins: [
    {
      // See docs in https://www.npmjs.com/package/craco-alias
      plugin: CracoAlias,
      options: {
        source: 'jsconfig'
      }
    }
  ]
}
```

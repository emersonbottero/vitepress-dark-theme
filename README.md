# vitepress-dark-theme

Basic dark theme for vitepress
It starts with the current OS theme and for now it does not save the state.
so refreshes will reset theme to OS default
It add itself as last element in the navLink slot

## Installation

install the module

```bash
npm i vitepress-dark-theme -D
```

## Setup

import the theme and export the theme inside the theme folder

```js
//.vitepress/theme/index.js
import DarkTheme from 'vitepress-dark-theme/index.js'
export default { ...DarkTheme }
```

In case you don't ave any nav bar and didn't set a repo in the configuration at least add an empty array in the nav config settings...

```js
//docs\.vitepress\config.js
...
themeConfig: {
    ...
    nav: [],
    ...
}
```

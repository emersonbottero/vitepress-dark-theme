# vitepress-dark-theme

Basic dark theme for vitepress
It starts with the current OS theme and for now it does not save the state.
so refreshes will reset theme to OS default
It add itself as last element in the navLink slot

# Usage

install the module

```bash
npm i vitepress-dark-theme -D
```

import the theme and export the theme inside the theme folder

```js
//.vitepress/theme/index.js
import DarkTheme from 'vitepress-dark-theme/index.js'
export default { ...DarkTheme }
```

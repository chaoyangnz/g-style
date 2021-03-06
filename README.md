# global-style

This library was strongly inspired by [CXS](https://github.com/cxs-css/cxs), but there are some key differences in how it works.

```js
import { GlobalStyle } from "g-style";
const gStyle = new GlobalStyle();
const className = gStyle.getClassNames({ color: "gold" });
```

## Features

- Small
- Typescript Support
- 100% Unit tested
- Zero dependencies
- High performance
- Deduplicates repeated styles
- Dead-code elimination
- Framework independent
- Media queries
- Pseudoclasses
- Nesting
- No CSS files


## Install

```sh
npm install g-style
```
```sh
yarn add g-style
```

## Usage

Example with React

```js
import React from "react"
import { GlobalStyle } from "g-style";
const gStyle = new GlobalStyle();
const className = gStyle.getClassNames({ color: "gold" });

export const Box = (props) => <div {...props} className={className} />

```

### Pseudo-classes

####This is one of the main differences comparing to CXS, pseudo-classes should have the `&` symbol similar to SCSS/SASS

```js
const className = gStyle.getClassNames({
  color: "gold",
  "&:hover": {
    border: "1px solid #ccc"
  }
})
```

### Media Queries
```js
const className = gStyle.getClassNames({
  fontSize: "32px",
  "@media screen and (min-width: 40em)": {
    fontSize: "48px"
  }
})
```

### Child Selectors

####One more difference comparing to CXS, child selectors don't need to start with a space symbol.

```js
const className = gStyle.getClassNames({
  color: "gold",
  ".link": {
    color: "red"
  }
})
```

### Static/Server-Side Rendering

For Node.js environments, use the `gStyle.getFullCss()` method to return the static CSS string *after* rendering a view.

```js
import React from "react";
import ReactDOMServer from "react-dom/server";
import { GlobalStyle } from "g-style";
import App from "./App";

...
// Create a new instance of gStyle for each render
const gStyle = new GlobalStyle();
...

const html = ReactDOMServer.renderToString(<App />);
const css = gStyle.getFullCss();

const doc = `<!DOCTYPE html>
<style>${css}</style>
${html}
`
```

## API

### `const gStyle = new GlobalStyle()`

Create a new gStyle instance

### `const gStyle = new GlobalStyle("prefix")`

Create a new gStyle instance with custom prefix

### `gStyle.getClassNames(styleObject)`

Accepts one style object a className string.

### `gStyle.getFullCss()`

Returns the rendered CSS string for static and server-side rendering.

[MIT License](LICENSE.md)

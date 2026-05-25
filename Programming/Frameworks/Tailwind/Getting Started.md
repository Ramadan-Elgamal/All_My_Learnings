Tailwind CSS works by scanning all of your HTML files, JavaScript components, and any other templates for class names, generating the corresponding styles and then writing them to a static CSS file.

## Installation & Usage
### Install via CDN
Use the Play CDN to try Tailwind right in the browser without any build step. The Play CDN is designed for development purposes only, and is not intended for production.

Add this Play CDN script tag to the `<head>` of your HTML file, and start using Tailwind’s utility classes to style your content.
```html
<script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
```

### Install via Vite
#### 1 - Install `tailwindcss` and `@tailwindcss/vite` via npm.
```bash
npm install tailwindcss @tailwindcss/vite
```

#### 2 - Add the `@tailwindcss/vite` plugin to your Vite configuration.

```js
import tailwindcss from '@tailwindcss/vite'

//plugins
tailwindcss(),
```

#### 3 -Add an `@import` to your CSS file that imports Tailwind CSS.

```css
@import "tailwindcss";
```


## Links
- Docs: https://tailwindcss.com/docs
- Useful Tools: https://github.com/aniftyco/awesome-tailwindcss
## What to learn
Functions & Directives: https://tailwindcss.com/docs/functions-and-directives
Plugins

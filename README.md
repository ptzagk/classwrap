# Classwrap
[![Travis CI](https://img.shields.io/travis/JorgeBucaran/classwrap/master.svg)](https://travis-ci.org/JorgeBucaran/classwrap)
[![Codecov](https://img.shields.io/codecov/c/github/JorgeBucaran/classwrap/master.svg)](https://codecov.io/gh/JorgeBucaran/classwrap)
[![npm](https://img.shields.io/npm/v/classwrap.svg)](https://www.npmjs.org/package/classwrap)

Classwrap is a 0.3 KB JavaScript utility for conditionally concatenating [class names](https://developer.mozilla.org/en-US/docs/Web/API/Element/className).

[Try it Online](https://codepen.io/JorgeBucaran/pen/GMRjRB)

```js
import cw from "classwrap"

export function ToggleButton({ toggle, isOn }) {
  return (
    <div class="btn" onclick={toggle}>
      <div
        class={cw({
          circle: true,
          off: !isOn,
          on: isOn
        })}
      />
      <span
        class={cw({
          textOff: !isOn
        })}
      >
        {isOn ? "ON" : "OFF"}
      </span>
    </div>
  )
}
```

Classwrap works in all browsers >=IE9. Use it with your favorite JavaScript view library.

[![Classwrap](https://user-images.githubusercontent.com/56996/30416101-cda83bd4-9965-11e7-9db5-230ba3fc83fd.gif)](https://codepen.io/JorgeBucaran/full/GMRjRB/)

## Installation

Install with npm / Yarn.

<pre>
npm i <a href="https://www.npmjs.com/package/classwrap">classwrap</a>
</pre>

Then with a module bundler like [Rollup](https://github.com/rollup/rollup) or [Webpack](https://github.com/webpack/webpack), use as you would anything else.

```js
import cw from "classwrap"
```

Or download the minified library from a [unpkg](https://unpkg.com/classwrap@latest/dist/classwrap.js) or [jsDelivr](https://cdn.jsdelivr.net/npm/classwrap@latest/dist/classwrap.js).

```html
<script src="https://unpkg.com/classwrap"></script>
```

Then find it on `window.classwrap`.

## Usage

Classwrap joins all elements of an array or keys of an object into a string. If the value associated with a given key is falsy, the key will be ignored.

```js
cw([
  "btn",
  {
    "btn-active": true,
    "btn-large": false
  }
]) // => btn btn-active
```

Nested arrays or objects are supported too. Use this feature to assemble classes with a common prefix.

```js
cw([
  "tab",
  {
    tab: {
      "--success": true,
      "--error": false,
      "--pending": false
    }
  }
]) // => tab tab--success
```

## Credits

Classwrap was inspired by [JedWatson/classnames](https://github.com/JedWatson/classnames) with support for nested objects and [improved](/bench/README.md) performance. It differs from classnames in that it does not accept [variable arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments).

```js
cw("foo", "bar", "baz") // => foo
```

To solve this, wrap the arguments inside an array.

```js
cw(["foo", "bar", "baz"]) // => foo bar baz
```

## License

Classwrap is MIT licensed. See [LICENSE](LICENSE.md).

# confetti-es

[
![ISC License](https://img.shields.io/badge/license-ISC-blue.svg)
](LICENSE)

A lightweight ES module for creating spectacular, customizable confetti effects on a canvas.

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

## Demos

- [**Basic Cannon**](https://code4fukui.github.io/confetti-es/demo/BasicCannon.html) - A single, centered burst of confetti.
- [**Fireworks**](https://code4fukui.github.io/confetti-es/demo/Fireworks.html) - Continuous, random bursts from the top of the screen.
- [**School Pride**](https://code4fukui.github.io/confetti-es/demo/SchoolPride.html) - A steady stream of confetti from both sides of the screen.
- [**Level Up**](https://code4fukui.github.io/confetti-es/demo/LevelUp.html) - A celebratory explosion from the bottom corners, followed by star-shaped bursts. (from [chiritsumo](https://github.com/haruyuki-16278/chiritsumo))

## Features

- **Modern JavaScript**: Delivered as a standard ES module with no dependencies.
- **Highly Customizable**: Control particle count, colors, shapes (`square`, `circle`, `star`), spread, velocity, gravity, and more.
- **Flexible Targeting**: Render confetti across the entire viewport or within a specific `<canvas>` element.
- **Accessibility-Ready**: Automatically respects the `prefers-reduced-motion` media query to disable animations for users who need it.

## Usage

Import the `confetti` function directly from the CDN and call it.

```javascript
import { confetti } from "https://code4fukui.github.io/confetti-es/confetti.js";

// A simple burst
confetti();

// Or, get creative with custom options
confetti({
  particleCount: 150,
  spread: 180,
  origin: { y: 0.6 }
});
```

Here is a more advanced example that launches two streams of confetti from the sides of the screen:

```javascript
// Launch from the left
confetti({
  particleCount: 100,
  angle: 60,
  spread: 55,
  origin: { x: 0 }
});

// Launch from the right
confetti({
  particleCount: 100,
  angle: 120,
  spread: 55,
  origin: { x: 1 }
});
```

## API

### `confetti([options])` → `Promise|null`

Triggers a confetti animation. It returns a `Promise` that resolves when the animation is complete, or `null` if Promises are not supported.

The `options` object allows you to customize the effect. All properties are optional.

| Option                  | Type             | Default                               | Description                                                                                             |
| ----------------------- | ---------------- | ------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `particleCount`         | `Integer`        | `50`                                  | The number of confetti particles to launch.                                                             |
| `angle`                 | `Number`         | `90`                                  | The launch angle in degrees. `0` is to the right, `90` is straight up.                                  |
| `spread`                | `Number`         | `45`                                  | How far off the `angle` the confetti can spread, in degrees.                                            |
| `startVelocity`         | `Number`         | `45`                                  | The initial velocity of the confetti particles, in pixels.                                              |
| `decay`                 | `Number`         | `0.9`                                 | How quickly the confetti slows down. `1` means no decay.                                                |
| `gravity`               | `Number`         | `1`                                   | How quickly the particles are pulled down. `0` means no gravity.                                        |
| `drift`                 | `Number`         | `0`                                   | How much the confetti drifts to the side. `0` is straight, negative is left, positive is right.         |
| `ticks`                 | `Number`         | `200`                                 | The number of animation frames for each particle.                                                       |
| `origin`                | `Object`         | `{ x: 0.5, y: 0.5 }`                  | The launch origin, where `x` and `y` are values from `0` to `1` representing percentages of the canvas. |
| `colors`                | `Array<String>`  | `['#26ccff', ...]`                    | An array of HEX color strings to use for the confetti.                                                  |
| `shapes`                | `Array<String>`  | `['square', 'circle']`                | An array of shape names. Available shapes: `'square'`, `'circle'`, `'star'`.                            |
| `scalar`                | `Number`         | `1`                                   | A scale factor for each confetti particle.                                                              |
| `zIndex`                | `Integer`        | `100`                                 | The z-index for the confetti canvas.                                                                    |
| `disableForReducedMotion` | `Boolean`      | `false`                               | If `true`, disables confetti if the user prefers reduced motion.                                        |

### `confetti.create(canvas, [globalOptions])` → `function`

Creates a new `confetti` instance that will render to a specific `<canvas>` element instead of the entire viewport.

```javascript
import { confetti } from "https://code4fukui.github.io/confetti-es/confetti.js";

const myCanvas = document.getElementById('my-canvas');

// Create a custom confetti instance
const myConfetti = confetti.create(myCanvas);

// Use it like the global confetti function
myConfetti({
  particleCount: 200,
  spread: 80
});
```

You can also provide `globalOptions` that will apply to all calls made with this instance.

## License

ISC License
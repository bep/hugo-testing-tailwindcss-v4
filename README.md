

>**Note:** The TailwindCSS v4 alpha 25 is broken and should not be used, see https://github.com/tailwindlabs/tailwindcss/issues/14521. This will be fixed in the next alpha release.

Hugo `v0.128.0` added improved support for the upcoming [TailwindCSS v4](https://tailwindcss.com/blog/tailwindcss-v4-alpha).


This version is still in alpha, and there are still some missing pieces. This repo contains a few variants of how to set up TailwindCSS with Hugo as a test/documentation about what's working and what's not.

Notes below updated 2024-06-25:


## General

TailwindCSS v4 alpha does not yet support custom a Tailwind configuration file. This means that there's currently no way to configure the input to TailwindCSS's build, e.g:

```js
module.exports = {
	content: ['./hugo_stats.json'],
};
```

TailwindCSS scans text files for HTML identifiers starting from the project directory, and is very fast and smart about it. But this is a limitation we expect to be fixed before the final release.

## Variants

### TailwindCSS CLI Simple

Triggers CSS rebuild on changes to CSS or to layout files.

Benefits:

* Simple to set up.
* Works well in simple setups.

Drawbacks:

* Triggers CSS rebuild on changes to layout files that's not related to style.
* Does not work in more complex setups (e.g. HTML identifiers from Hugo Modules).

### TailwindCSS CLI Defer

Only triggers CSS rebuilds when either CSS or the `hugo_stats.json` file changes.

Benefits:

* Faster rebuilds when changing layout files that's not related to style.
* Works in more complex setups (e.g. HTML identifiers from Hugo Modules).

Drawbacks:

* Slightly more complex setup.

### PostCSS CLI Defer

This is same as `TailwindCSS CLI Defer`, but using PostCSS CLI instead of TailwindCSS CLI.

Benefits:

* Can use PostCSS plugins. But note that TailwindCSS v4 comes with autoprefixer and nesting built-in.

Drawbacks:

* Slower builds (about 170ms vs 100ms for the others for this small setup).



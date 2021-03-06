# Leaflet Plugin Authoring Guide

One of the greatest things about Leaflet is its powerful plugin ecosystem.
The [Leaflet plugins page](http://leafletjs.com/plugins.html) lists dozens of awesome plugins, and more are being added every week.

This guide lists a number of best practices for publishing a perfect Leaflet plugin that meets the quality standards of Leaflet itself.

1. [Presentation](#presentation)
	- [Repository](#repository)
	- [Demo](#demo)
	- [Readme](#readme)
	- [License](#license)
2. [Code](#code)
	- [File Structure](#file-structure)
	- [Code Conventions](#code-conventions)
	- [Plugin API](#plugin-api)

## Presentation

### Repository

The best place to put your Leaflet plugin to is a separate [GitHub](http://github.com) repository.
If you create a collection of plugins for different uses,
don't put them in one repo &mdash;
it's usually easier to work with small, self-contained plugins.

### Demo

The most essential thing to do when publishing a plugin is putting up a demo that showcases what the plugin does &mdash;
it's usually the first thing people will look for.

The easiest way to put up a demo is using [GitHub Pages](http://pages.github.com/).
A good [starting point](https://help.github.com/articles/creating-project-pages-manually) is creating a `gh-pages` branch in your repo and adding an `index.html` page to it  &mdash;
after pushing, it'll be published as `http://<user>.github.io/<repo>`.

### Readme

The next thing you need to have is a good descriptive `README.md` in the root of the repo (or a link to a website with a similar content).
At the least, it should contain the following items:

- plugin title
- simple, concise description
- requirements
	- Leaflet version
	- other external dependencies (if present)
	- browser / device compatibility
- links to demos
- instructions for including the plugin
- simple usage code example
- API reference (methods, options, events)

### License

Every good open source repository should have a license specified.
If you don't know what open source license to choose for your code,
[MIT License](http://opensource.org/licenses/MIT) and [BSD 2-Clause License](http://opensource.org/licenses/BSD-2-Clause) are both good choices.
You can either put it in the repo as a `LICENSE` file or just link to the license from the Readme.

## Code

### File Structure

Keep the file structure clean and simple,
don't pile up lots of files in one place  &mdash;
make it easy for a new person to find their way in your repo.

A barebones repo for a simple plugin would like this:

```
my-plugin.js
README.md
```

An example of a file structure for a more sophisticated plugin:

```
/src        JS source files
/dist       minified plugin JS, CSS, images
/spec       test files
/examples   HTML examples of plugin usage
README.md
LICENSE
package.json
```

### Code Conventions

Everyone's tastes are different, but it's important to be consistent with whatever conventions you choose for your plugin.

For a good starting point, check out [Airbnb JavaScript Guide](https://github.com/airbnb/javascript).
Leaflet follows pretty much the same conventions
except for using smart tabs (hard tabs for indentation, spaces for alignment)
and putting space after `function` keyword.

### Plugin API

Never expose global variables with your plugin.
If you have a new class, put it directly in the `L` namespace (`L.MyPlugin`).
If you inherit one of the existing classes, put it as its property (`L.TileLayer.Banana`).
If you want to add new methods to existing Leaflet classes, you can do it like this: `L.Marker.include({myPlugin: …})`.

Function, method and property names should be in `camelCase`.
Class names should be in `CapitalizedCamelCase`.

If you have a lot of arguments in your function, consider accepting an options object instead (putting default values where possible so that users don't need specify all of them):

```js
// bad
marker.myPlugin('bla', 'foo', null, {}, 5, 0);

 // good
marker.myPlugin('bla', {
	optionOne: 'foo', 
	optionThree: 5
});
```

And most importantly, keep it simple. Leaflet is all about *simplicity*.

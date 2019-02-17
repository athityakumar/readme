<p align="center">
  <img src="https://github.com/andreasbm/readme/blob/master/assets/logo-shadow.png" alt="Logo" width="150" height="150" />
</p>
<h1 align="center">@appnest/readme</h1>
<p align="center">
		<a href="https://github.com/badges/shields"><img alt="Custom badge" src="https://img.shields.io/badge/custom-badge-f39f37.svg" height="20"/></a>
<a href="https://npmcharts.com/compare/@appnest/readme?minimal=true"><img alt="Downloads per month" src="https://img.shields.io/npm/dm/@appnest/readme.svg" height="20"/></a>
<a href="https://www.npmjs.com/package/@appnest/readme"><img alt="NPM Version" src="https://img.shields.io/npm/v/@appnest/readme.svg" height="20"/></a>
<a href="https://david-dm.org/andreasbm/readme"><img alt="Dependencies" src="https://img.shields.io/david/andreasbm/readme.svg" height="20"/></a>
<a href="https://github.com/andreasbm/readme/graphs/contributors"><img alt="Contributors" src="https://img.shields.io/github/contributors/andreasbm/readme.svg" height="20"/></a>
	</p>

<p align="center">
  <b>Generate pretty best-practice and easy-to-maintain README files</b></br>
  <sub>Use this readme generator to easily generate pretty readme's like this one! Simply extend your <code>package.json</code> and create a readme blueprint.<sub>
</p>

<br />

<p align="center">
  <img src="https://github.com/andreasbm/readme/blob/master/assets/demo.gif" alt="Demo" width="500" />
</p>
* **Simple:** Extremely simple to use - so simple that it almost feels like magic!
* **Powerful:** Customize almost everything - add your own templates and variables if you like
* **Awesome:** The tool you don't know you need before you have many different repositories that all need maintenance

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/line-colored.png)

## ❯ Table of Contents

* [❯ Installation](#-installation)
* [❯ Create a blueprint](#-create-a-blueprint)
* [❯ Templates](#-templates)
	* [Logo](#logo)
	* [Badges](#badges)
	* [Description](#description)
	* [Bullets](#bullets)
	* [Table of Contents](#table-of-contents)
	* [Contributors](#contributors)
* [❯ Contributors](#-contributors)
	* [License](#license)
* [❯ License](#-license)
* [❯ Load markdown files](#-load-markdown-files)
* [❯ A bit about this readme](#-a-bit-about-this-readme)
* [❯ Custom templates](#-custom-templates)
* [❯ Advanced!](#-advanced)
	* [New template syntax](#new-template-syntax)
	* [Arrays and objects](#arrays-and-objects)
	* [Different colored lines](#different-colored-lines)
* [❯ Future work](#-future-work)
* [❯ Contributors](#-contributors)
* [❯ License](#-license)

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/line-colored.png)

## ❯ Installation

```javascript
npm install @appnest/readme -D
```

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/line-colored.png)

## ❯ Create a blueprint

First you need to create a `blueprint.md` file (name it whatever you like). This blueprint is going to be the blueprint for the `README.md` file we are going to generate later.

Let's start simple. In order to get values from your `package.json` file injected into the readme we use the `{{ .. }}` syntax. Let's say your `package.json` file looks like this:

```json
{
  "name": "@appnest/readme",
  "version": "1.0.7"
}
```

To get the `name` and `version` into your readme you will need to write `{{ name }}` and `{{ version }}` in your `blueprint.md` file like this:

```markdown
Welcome to {{ name }}. This is version {{ version }}!
```

When running `node node_modules/.bin/readme --input=blueprint.md --output=README.md` the file `README.md` will be generated with the following contents:

```markdown
Welcome to @appnest/readme. This is version 1.0.7.
```

Great. Let's continue and see how you can use templates!

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/line-colored.png)

## ❯ Templates

If you have come this far you are probably interested to figure out how to use readme templates. This library comes with a set of pre-defined templates to make your readme awesome, but you can of course create your own. More about that later, let's not get ahead of our self just yet.

The most simple template you can use is the title template. The way to generate a title is by writing `{{ template:title }}` in your blueprint. When you run the `readme` command the template will generate the following:

<h1 align="center">@appnest/readme</h1>

The important thing to note here is that the template automatically reads your `package.json` file and inserts the `name` from the package. That's pretty cool. Let's go through some of the other built-in templates you might want to add.

### Logo

The logo template adds a logo to your readme and looks like this:

<p align="center">
  <img src="https://github.com/andreasbm/readme/blob/master/assets/logo-shadow.png" alt="Logo" width="150" height="150" />
</p>

Use the placeholder `{{ template:logo }}` to stamp it. You will need to add the `readme.logo` field to your `package.json`. The logo field requires an `url` field and the fields `width`, `height` and `alt` are optional. Below is an example on how to add a logo.

```json
{
  "readme": {
    "logo": {
      "url": "https://github.com/andreasbm/readme/blob/master/assets/logo-shadow.png",
      "width": 150
    }
  }
}
```

### Badges

The badges template adds badges to your readme and looks like this:

<p align="center">
		<a href="https://github.com/badges/shields"><img alt="Custom badge" src="https://img.shields.io/badge/custom-badge-f39f37.svg" height="20"/></a>
<a href="https://npmcharts.com/compare/@appnest/readme?minimal=true"><img alt="Downloads per month" src="https://img.shields.io/npm/dm/@appnest/readme.svg" height="20"/></a>
<a href="https://www.npmjs.com/package/@appnest/readme"><img alt="NPM Version" src="https://img.shields.io/npm/v/@appnest/readme.svg" height="20"/></a>
<a href="https://david-dm.org/andreasbm/readme"><img alt="Dependencies" src="https://img.shields.io/david/andreasbm/readme.svg" height="20"/></a>
<a href="https://github.com/andreasbm/readme/graphs/contributors"><img alt="Contributors" src="https://img.shields.io/github/contributors/andreasbm/readme.svg" height="20"/></a>
	</p>


Use the `{{ template:badges }}` placeholder to stamp it. You will need to add the information about how the badges should be generated. For that you can extend the "readme.ids" property in your `package.json` add the `npm` and `github` ids (both are optional). If you want to add your own badges you can use the `readme.badges` field.

```json
{
  "readme": {
    "ids": {
      "github": "andreasbm/readme",
      "npm": "@appnest/readme"
    },
    "badges": [
      {
        "alt": "Custom badge",
        "url": "https://github.com/badges/shields",
        "img": "https://img.shields.io/badge/custom-badge-f39f37.svg"
      }
    ]
  }
}
```

### Description

The description template adds a description to your readme and looks like this:

<p align="center">
  <b>Generate pretty best-practice and easy-to-maintain README files</b></br>
  <sub>Use this readme generator to easily generate pretty readme's like this one! Simply extend your <code>package.json</code> and create a readme blueprint.<sub>
</p>

<br />


Use the `{{ template:description }}` placeholder to stamp it. To use this template you are required to add the field `description` to your `package.json` file. Optionally you can also add the fields `readme.text` and `readme.demo` which will be presented below the description.

```json
{
  "description": "Generate pretty best-practice and easy-to-maintain README files",
  "readme": {
    "text": "Use this readme generator to easily generate pretty readme's like this one! Simply extend your <code>package.json</code> and create a readme blueprint."
  }
}
```

### Bullets

The bullets template adds bullets to your readme and looks like this:

* **Simple:** Extremely simple to use - so simple that it almost feels like magic!
* **Powerful:** Customize almost everything - add your own templates and variables if you like
* **Awesome:** The tool you don't know you need before you have many different repositories that all need maintenance

Use the `{{ template:bullets }}` placeholder to stamp it. To use this template you are required to add the `readme.bullets` array to your `package.json` file. This array has to be an array of strings as shown below.

```json
{
  "description": "Generate pretty README.md files with your new superpowers!",
  "readme": {
    "bullets": [
      "**Simple:** Extremely simple to use - so simple that it almost feels like magic!",
      "**Powerful:** Customize almost everything - add your own templates and variables if you like",
      "**Awesome:** The tool you don't know you need before you have many different repositories that all need maintenance"
    ]
  }
}
```

### Table of Contents

The table of contents template adds a table of contents and looks like this:


![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/line-colored.png)

## ❯ Table of Contents

* [❯ Installation](#-installation)
* [❯ Create a blueprint](#-create-a-blueprint)
* [❯ Templates](#-templates)
	* [Logo](#logo)
	* [Badges](#badges)
	* [Description](#description)
	* [Bullets](#bullets)
	* [Table of Contents](#table-of-contents)
	* [Contributors](#contributors)
* [❯ Contributors](#-contributors)
	* [License](#license)
* [❯ License](#-license)
* [❯ Load markdown files](#-load-markdown-files)
* [❯ A bit about this readme](#-a-bit-about-this-readme)
* [❯ Custom templates](#-custom-templates)
* [❯ Advanced!](#-advanced)
	* [New template syntax](#new-template-syntax)
	* [Arrays and objects](#arrays-and-objects)
	* [Different colored lines](#different-colored-lines)
* [❯ Future work](#-future-work)
* [❯ Contributors](#-contributors)
* [❯ License](#-license)

Use the `{{ template:toc }}` placeholder to stamp it. It has been scientifically proven that this template will save you approximately 392.3 hours during your life-time.

### Contributors

The contributors template adds the list of contributors and looks like this:


![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/line-colored.png)

## ❯ Contributors
	
* <a href="https://twitter.com/andreasmehlsen">Andreas Mehlsen</a> (<a href="mailto:andmehlsen@gmail.com">andmehlsen@gmail.com</a>)

Use the `{{ template:contributors }}` placeholder to stamp it. To use this template your are required to add the `contributors` array to your `package.json` file like this.

```json
{
  "contributors": [
    {
      "name": "Andreas Mehlsen",
      "email": "andmehlsen@gmail.com",
      "url": "https://twitter.com/andreasmehlsen"
    }
  ]
}
```

### License

The license template adds a license section and looks like this:


![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/line-colored.png)

## ❯ License
	
Licensed under [MIT](https://opensource.org/licenses/MIT).

Use the `{{ template:license }}` placeholder to stamp it. To use this template you are required to add the `license` field to your `package.json` file like this.

```json
{
  "license": "MIT"
}
```

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/line-colored.png)

## ❯ Load markdown files

What? You heard right. You can split the contents of your readme into multiple different files to make your life easier. Let's say you have a file called `my-section.md`. To stamp it you'll need to add `{{ load:my-section.md }}`.

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/line-colored.png)

## ❯ A bit about this readme

By now you are probably curious to know how this `README.md` was generated? It was created from the following `blueprint.md` file.

```markdown
{{ template:logo }}
{{ template:title }}
{{ template:badges }}
{{ template:description }}
{{ template:bullets }}
{{ template:toc }}
{{ load:readme/1-installation.md }}
{{ load:readme/2-create-blueprint.md }}
{{ load:readme/3-templates.md }}
{{ load:readme/4-load-markdown.md }}
{{ load:readme/5-this-readme.md }}
{{ load:readme/6-custom-templates.md }}
{{ load:readme/7-advanced.md }}
{{ load:readme/8-future-work.md }}
{{ template:contributors }}
{{ template:license }}
```

It really couldn't be more simple that this.

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/line-colored.png)

## ❯ Custom templates

To create your own templates you'll first need to add the `readme.templates` array to your `package.json` file like this.

```json
{
  "readme": {
    "templates":[
      {
        "name": "install",
        "template": "Run `npm install {{ readme.ids.npm }} to install this library!"
      }
    ]
  }
}
```

Then you can stamp your custom template using the `{{ template:install }}` syntax ('install' here referencing the name of the custom template).

Run `npm install @appnest/readme' to install this library!

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/line-colored.png)

## ❯ Advanced!

Oh! So are you ready to open Pandora's box? Let's do it.

### New template syntax

If you are in the mood you can change the syntax used for matching with the templates. Let's say you want your placeholders to look like this instead `{[ template:title }]` you'll need to add the `readme.placeholder` array with the new syntax being `["{[", "}]"]` like this.


```json
{
  "readme": {
    "placeholder": ["{[", "}]"]
  }
}
```

### Arrays and objects

If you have an array or an object you want to stamp to your readme as a list just use the `{{ ... }}` syntax as usual. If you for example want to stamp the `dependencies` from your `package.json` file you write `{{ dependencies }}` and the dependencies will be stamped in a nice formatted way.

* **colors**: ^1.3.3
* **fs-extra**: ^7.0.1
* **minimist**: ^1.2.0
* **path**: ^0.12.7

### Different colored lines

If you want to change the color of the lines above headers you can change the `readme.line` field in the `package.json`. You can either choose `dark` or `colored` values.

```json
{
  "readme": {
    "line": "dark"
  }
}
```

The following is the dark variant of the line.

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/line-dark.png)

Yeah! Dark mode on your `README.md` is awesome indeed.



![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/line-colored.png)

## ❯ Future work

That's it for now! Lot's of exiting features a going to be added in the future. If you stumble upon an issue or have a feature request you can open a github issue. Also, if you use this generator for one of your projects I would love to hear about it so I can feature it. Have a great day!

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/line-colored.png)

## ❯ Contributors
	
* <a href="https://twitter.com/andreasmehlsen">Andreas Mehlsen</a> (<a href="mailto:andmehlsen@gmail.com">andmehlsen@gmail.com</a>)

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/line-colored.png)

## ❯ License
	
Licensed under [MIT](https://opensource.org/licenses/MIT).
# altheajs-prettier-config

Althea Web Service's [`prettier`](https://prettier.io) configuration.

View this package on NPM: [click here](https://www.npmjs.com/package/altheajs-prettier-config)

## Installation

### npm

```sh
npm install --save-dev altheajs-prettier-config
```

If you don't have it installed already, also install `prettier` as a devDependency.

```sh
npm install --save-dev prettier --save-exact
```

### yarn

```sh
yarn add --dev altheajs-prettier-config prettier
```

## Usage

We export two ESLint configurations for your usage:

1. AWS Default
2. Prettier's Default

### AWS Default Config

The simplest way to install and use the default config is to reference it directly in your `package.json` file as follows:

```js
{
	// ...package.json
	"prettier": "altheajs-prettier-config"
}
```

If you'd like to extend the configurations, create a `.prettierrc.js` file at the root of your project that contains:

```js
module.exports = {
	...require("altheajs-prettier-config"),
	semi: true,
};
```

### Prettier's Default Config

If you prefer to use Prettier's defaults, you can access it via `"altheajs-prettier-config/default"`. Just use it as a reference to what package to extend from or point to, as used in the above two examples.

````

## NPM Scripts Command

You can add in an npm script to your `package.json` which will apply prettier rules across all the file patterns specified. Simply add the following to apply to all files:

```js
	"scripts": {
		// --write will apply the rules
		"lint:prettier": "npx prettier --config ./prettier.config.js **/*.* --write",
		// if you prefer to just check for errors use the --check flag
		"lint:prettiercheck": "npx prettier --config ./prettier.config.js **/*.* --check"
	}
````

## Pre-commit Hook

As another line of defense, if you want Prettier to automatically fix your errors on commit, you can use [`lint-staged`](https://github.com/okonet/lint-staged) with [`husky`](https://github.com/typicode/husky), which manages git hooks.

1. `npm install --save-dev lint-staged husky`
2. Update your `package.json` like this:

```js
{
	"lint-staged": {
		"*.{js,css,json,md}": ["prettier --write", "git add"]
	},
	"husky": {
		"hooks": {
			"pre-commit": "lint-staged"
		}
	}
}
```

If you already have `lint-staged` running [ESLint](https://github.com/eslint/eslint), just add the prettier step on top of it:

```js
{
	"lint-staged": {
		"*.{js,css,json,md}": ["prettier --write", "git add"],
		"*.js": ["eslint --fix", "git add"]
	},
	"husky": {
		"hooks": {
			"pre-commit": "lint-staged"
		}
	}
}
```

## [Editor Integration](https://prettier.io/docs/en/editors.html)

### Visual Studio Code

1. Install Prettier extension: `View → Extensions` then find and install Prettier - Code formatter
2. Reload the editor
3. In your user settings `Code -> Preferences -> Settings` add `editor.formatOnSave: true`

### Sublime Text 3

[https://packagecontrol.io/packages/JsPrettier](https://packagecontrol.io/packages/JsPrettier)

### Atom

[https://atom.io/packages/prettier-atom](https://atom.io/packages/prettier-atom)

## Enforced Rules

Check out all of Prettier's [configuration options](https://prettier.io/docs/en/options.html).

- **Print Width**

  Line wrap at 100 characters.

- **Tab Width**

  2 spaces per indentation-level.

- **Tabs**

  Indent lines with tabs, not spaces.

- **Semicolons**

  Always print semicolons at the ends of statements.

  ```js
  const greeting = "hi";
  ```

- **Quote**

  Use single quotes instead of double quotes.

  ```js
  const quote = "single quotes are better";
  ```

- **Trailing Commas**

  Use trailing commas wherever possible.

  ```js
  const obj = {
  	a: "hi",
  	b: "hey",
  };
  ```

- **Bracket Spacing**

  Print spaces between brackets in object literals.

  ```js
  {
  	foo: bar;
  }
  ```

- **JSX Brackets**

  Put the `>` of a multi-line JSX element at the end of the last line instead of being alone on the next line (does not apply to self closing elements).

  ```jsx
  <button
  	className="prettier-class"
  	id="prettier-id"
  	onClick={this.handleClick}
  >
  	Click Here
  </button>
  ```

- **Arrow Function Parentheses**

  Omit parens when possible.

  ```js
  (x) => x;
  ```

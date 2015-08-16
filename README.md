# Autoprefixer for React Inline Styles
[![Build Status](https://travis-ci.org/rofrischmann/react-style-prefixer.svg)](https://travis-ci.org/rofrischmann/react-style-prefixer)
[![Code Climate](https://codeclimate.com/github/rofrischmann/react-style-prefixer/badges/gpa.svg)](https://codeclimate.com/github/rofrischmann/react-style-prefixer)
[![npm version](https://badge.fury.io/js/inline-style-prefixer.svg)](http://badge.fury.io/js/react-style-prefixer)
![Dependencies](https://david-dm.org/rofrischmann/react-style-prefixer.svg)
> **Warning**: Very early stage supporting only a small set of prefixes by now.
**Usage on your own risk**!

	npm install react-style-prefixer
**react-style-prefixer** adds required **vendor prefixes** to your style object. It only adds prefixes if they're actually required since it evaluates the environments `userAgent`.<br>
> The information is based on [caniuse.com](http://caniuse.com/).

## Usage
```javascript
import Prefixer from 'react-style-prefixer';

let styles = {
	transition: '200ms all linear',
	userSelect: 'none',
	nested : {
		boxSizing: 'border-box',
		appearance: 'none',
		color: 'blue',
		flex: 1
	}
}

Prefixer.process(styles);
```

Assuming you are using .e.g Chrome version 27.0 this would output the following styles object:
```javascript
{
	transition: '200ms all linear',
	WebkitUserSelect: 'none',
	userSelect: 'none',
	nested: {
		boxSizing: 'border-box',
		WebkitAppearance: 'none',
		appearance: 'none',
		color: 'blue',
		WebkitFlex: 1,
		flex: 1
	}
}
```

## Custom userAgent
Sometimes your environment does not provide a proper userAgent string e.g. if you are **rendering on server-side**. Therefore you can use `setUserAgent` and `getUserAgent`.

```javascript
import Prefixer from 'react-style-prefixer';

Prefixer.setUserAgent('Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/44.0.2403.155 Safari/537.36');
Prefixer.getUserAgent() // => Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/44.0.2403.155 Safari/537.36

```
## How it works
While installing it automatically searches the latest **caniuse.com data** for CSS properties and creates a data map sort by browsers. Those maps include pairs of properties and the maximum version that needs a prefix.<br>

Based on browser and browser version it then generates a list of properties that need to be prefixed.
> Conclusion: It only adds prefixes that are really needed!

# License
**react-style-prefixer** is licensed under the [MIT License](LICENSE).<br>
Created with ♥ by [@rofrischmann](http://rofrischmann.de).
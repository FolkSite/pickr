<h1 align="center">
    <img src="logo.png" alt="Logo">
</h1>

<h3 align="center">
    Flat, Simple, Hackable Color-Picker.
</h3>

<p align="center">
  <a href="https://choosealicense.com/licenses/mit/"><img
	  alt="License MIT"
	  src="https://img.shields.io/badge/licence-MIT-3498db.svg"></a>
  <a href="https://webpack.js.org/"><img
     alt="Webpack"
     src="https://img.shields.io/badge/Webpack-4-3498db.svg"></a>
  <img alt="No dependencies"
       src="https://img.shields.io/badge/dependencies-none-27ae60.svg">
  <a href="https://travis-ci.org/Simonwep/pickr"><img
       alt="Build Status"
       src="https://travis-ci.org/Simonwep/pickr.svg?branch=master"></a>
  <a href="https://www.npmjs.com/"><img
     alt="npm package"
     src="https://img.shields.io/badge/npm-6.0.1-e74c3c.svg"></a>
  <img alt="Current version"
       src="https://img.shields.io/badge/version-0.1.0-f1c40f.svg">
</p>

<br>

<h3 align="center">
  <img alt="Demo" src="gh-page/pickr.apng"/>
</h3>

<h3 align="center">
  <a href="https://simonwep.github.io/pickr/">Fully Featured demo</a>
</h3>

<br>

### Features
* Simple usage
* No jQuery
* No dependencies
* Multiple color representations
* Color comparison
* Opacity control
* Supports touch devices
* Nodejs support

### Install

Via npm
```
$ npm install pickr-widget --save
```

Link styles and add scripts
```markdown
<link rel="stylesheet" href="node_modules/pickr/dist/pickr.min.css"/>
<script src="node_modules/pickr/dist/pickr.min.js"></script>
```

Be sure to load the `pickr.min.js` **after** `pickr.min.css`. Moreover the `script` tag doesn't work with the `defer` attribute.

### Usage
```javascript
const pickr = Pickr.create({
    el: '.color-picker'
});
```

### Optional options
```javascript
const pickr = new Pickr({

    // Selector or element which will be replaced with the actual color-picker
    el: '.color-picker',
    
    // Default color
    default: 'fff',

    // Option to keep the color picker always visible. You can still hide / show it via 
    // 'pickr.hide()' and 'pickr.show()'. The save button keeps his functionality, so if 
    // you click it, it will fire the onSave event.
    showAlways: false,

    // Defines the position of the color-picker. Available options are
    // top, left and middle relativ to the picker button.
    position: 'middle',

    // Show or hide specific components.
    // By default only the palette (and the save button) is visible.
    components: {

        preview: true, // Left side color comparison
        opacity: true, // Opacity slider
        hue: true,     // Hue slider

        // Bottom output bar, theoretically you could use 'true' as propery.
        // But this would also hide the save-button.
        output: {
            hex: true,  // hex option  (hexadecimal representation of the rgb value)
            rgba: true, // rgba option (red green blue and alpha)
            hsla: true, // hsla option (hue saturation lightness and alpha)
            hsva: true, // hsva option (hue saturation value and alpha)
            cmyk: true, // cmyk option (cyan mangenta yellow key )
            
            input: true, // input / output element
            clear: true  // Button which provides the ability to select no color
        },
    },


    // User has changed the color
    onChange(hsva, instance) {
        hsva;     // HSVa color object, if cleared null
        instance; // Current Pickr instance
    },

    // User has clicked the save button
    onSave(hsva, instance) {
        // same as onChange
    }
});
```

## The HSVaColor object
As default color representation is hsva (`hue`, `saturation`, `value` and `alpha`) used, but you can also convert it to other formats as listed below.

* hsva.toHSVA() _- Converts the object to a hsva string / array._
* hsva.toHSLA() _- Converts the object to a hsla string / array._
* hsva.toRGBA() _- Converts the object to a rgba string / array._
* hsva.toHEX() _- Converts the object to a hexa-decimal string / array._
* hsva.toCMYK() _- Converts the object to a cymk string / array._
* hsva.clone() _- Clones the color object._

The `toString()` is overriden so you can get a color representaion string.

```javascript
hsva.toRGBA(); // Returns [r, g, b, a]
hsva.toRGBA().toString();     // Returns rgba(r, g, b, a)
```

## Methods
* pickr.setHSVA(h`:Number`,s`:Number`,v`:Number`,a`:Float`) _- Set an color._
* pickr.setColor(string`:String`) _- Parses a string which represents a color_
* pickr.show() _- Shows the color-picker._
* pickr.hide() _- Hides the color-picker._
* pickr.getRoot()`:HTMLElement` _- Returns the root DOM-Element of the color-picker._
* pickr.getColor()`:HSVaColor` _- Returns the current HSVaColor object._

## Static methods
**Pickr**
* Pickr.create(options`:Object`)`:Pickr` _- Creates a new instance._

**Pickr.utils**
* once(element`:HTMLElement`, event`:String`, fn`:Function`[, options `:Object`]) _- Attach an event handle which will be fired only once_
* on(elements`:HTMLElement(s)`, events`:String(s)`, fn`:Function`[, options `:Object`]) _- Attach an event handler function._
* off(elements`:HTMLElement(s)`, event`:String(s)`, fn`:Function`[, options `:Object`]) _- Remove an event handler._
* createElementFromString(html`:String`)`:HTMLElement` _- Creates an new HTML Element out of this string._
* eventPath(evt`:Event`)`:[HTMLElement]` _- A polyfill for the event-path event propery._

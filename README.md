# windows-titlebar-color
Reads the title bar's color from the Windows 7, 8, 8.1 or 10 registry.

Created for usage in [Electron](https://github.com/electron/electron) apps.

[![JavaScript Style Guide](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com/)

## Usage
```javascript
const winColor = require('windows-titlebar-color')

console.log(winColor.titlebarColor)

// could be #4ca0fe. or anything else.
//           ^ this is at least not a completely arbitrary color since it's
//             the default blue window chrome color that ships with Windows 8
```

## Works with...

...Windows 7, Windows 8/8.1 and Windows 10. Generally.


## Does not work with...

...Windows 7 "Basic" style (non-Aero), classic window style (as in Win2k and below), high contrast window style and any other kind of manually tweaked window styles.

If you know how to elegantly provide information for those, feel free to open an issue. I'm generally fine with the lack of those since that's where other software (such as Google Chrome) also draws the line to fall back to their own non-OS-following styles.

Also note that the color determined for Windows 7 in Aero mode may differ from the perceived color of the title bar due to glossy transparency magic.

## API

It's pretty simple. Grab the module and then go for it:

`const winColor = require('windows-titlebar-color')`

### Stuff you can access on the `winColor` object:

#### `winColor.titlebarColor`
Returns the color of the your Windows machines' title bar as a hex string.

#### `winColor.inactiveTitlebarColor`
Returns the color of the title bar on an inactive window.

#### `winColor.isSupported`
Returns a boolean indicating if the running OS is generally supported to read colors from. Does not check for other limitations like those stated above.

#### `winColor.isDetectable`
Returns a boolean indicating if the running OS is supported and if a color is detectable for the title bar. (In other words: additionally checks if Aero is active in case the OS is Windows 7.)

#### `winColor.reload()`
Freshly loads the colors from the Registry. This is also done on initiation so typically you won't ever need to call this.

#### `winColor.raw`
Returns a hash containing the registry values from the `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\DWM` key entries, converted to either boolean or hex color strings. For example my personal Windows 10 hash looks like this:

```javascript
{
  Composition: true,
  ColorizationGlassAttribute: false,
  EnableAeroPeek: true,
  ColorPrevalence: true,
  AccentColor: '#484a4c',
  ColorizationColor: '#4c4a48',
  ColorizationColorBalance: '#000059',
  ColorizationAfterglow: '#4c4a48',
  ColorizationAfterglowBalance: '#00000a',
  ColorizationBlurBalance: true,
  EnableWindowColorization: true
}
  ```

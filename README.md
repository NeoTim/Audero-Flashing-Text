# Audero Flashing Text

[Audero Flashing Text](https://github.com/AurelioDeRosa/Audero-Flashing-Text) is a jQuery plugin that creates the
effect of a flashing, randomly-placed and randomly-sized text inside a given HTML element (typically a `div`).

## Demo

A live demo is available
[here](http://htmlpreview.github.io/?https://github.com/AurelioDeRosa/Audero-Flashing-Text/blob/master/demo/index.html).

## Requirements

Being a jQuery plugin, the only requirement is [jQuery](http://www.jquery.com) starting from version **1.2**.

## Compatibility

It has been tested and works on all the major browsers, including Internet Explorer 6 and later.

Audero Flashing Text follows the [UMD (Universal Module Definition)](https://github.com/umdjs/umd) pattern to work
seamlessly with module systems such as AMD and CommonJS, and the browser.

## Installation

You can install Audero Flashing Text by using [npm](https://www.npmjs.com):

```
npm install audero-flashing-text
```

Alternatively, you can install it via [Bower](http://bower.io):

```
bower install audero-flashing-text
```

Alternatively, you can manually download it.

Remember to include the JavaScript file **after** the [jQuery](http://www.jquery.com) library, ideally before the 
closing `body` tag:

```html
   <script src="path/to/jquery.js"></script>
   <script src="path/to/jquery.auderoFlashingText.js"></script>
</body>
```

### Inclusion with Browserify

To use Audero Flashing Text with Browserify, you have to write:

```js
require('audero-flashing-text')();
```

If you want to specify the global environment and augment a specific version of jQuery, you can pass both to
the plugin:

```js
var jQuery = require('jquery');
require('audero-flashing-text')(window, jQuery);
```

## Usage

Using this plugin is very simple. Just call the `auderoFlashingText()` method on the element you want to apply
the effect.

For example, let that you have the following code:

```html
<div id="box">
   <p>First</p>
   <p>Second</p>
   <p>Third</p>
</div>
```

A basic call to the plugin, that will rotate the text of the three paragraphs is:

```js
$('#box').auderoFlashingText();
```

### Disable the effect

After you initialize the plugin, you have the chance to disable it at any time. To disable the effect, you have to
call the `auderoFlashingText()` method passing the string `disable`, as you can see in the next example:

```js
$('#box').auderoFlashingText('disable');
```

### Enable the effect

Once you disabled the plugin you may want to enable it again. To do this, you have to call the `auderoFlashingText()`
method passing the string `enable` as shown below:

```js
$('#box').auderoFlashingText('enable');
```

### Toggle the effect

In some cases you may want to toggle the effect, for example based on a user action. Let's say that you want to
enable/disable the animation when a user clicks a button. To achieve this goal, you have to call the
`auderoFlashingText()` method passing the string `toggle`.

So, let that you have the following HTML code:

```html
<div id="box">
   <p>First</p>
   <p>Second</p>
   <p>Third</p>
</div>
<button id="toggle-button">Toggle animation</button>
```

You can bind the `click` event on the `<button>` to toggle the animation as shown in the following snippet:

```js
$('#toggle-button').click(function() {
   $('#box').auderoFlashingText('toggle');
});
```

### Destroy the effect

Under some circumstances you may want to stop the animation and clean all the resources. To perform this task, you can
call the `auderoFlashingText()` method passing the string `destroy`. To see it in action, take a look at the following
example:

```js
$('#box').auderoFlashingText('destroy');
```

## Options

Audero Flashing Text has several options you can set during the call to the `auderoFlashingText()` method that
allow you to customize the effect to fit your needs. The options are:

* `strings` (`array`. Default: `null`, but if it isn't specified the text of the children of the elements is used):
A set of strings to show.
* `isEnabled`: `true` (`boolean`. Default: `true`): The state of the animation. If the value is `false`, the animation
will stop keeping its current options
* `fadeIn` (`numeric`. Default: `300`): The time in milliseconds the element appears by fading to opaque.
* `duration` (`numeric`. Default: `500`): The time of milliseconds the element stays visible.
* `fadeOut` (`numeric`. Default: `300`): The time of milliseconds the element disappears by fading to transparent.
* `selection` (`string`. Default: `random`): The order of selection of the strings. The possible values are: `random`,
`ascending`, `descending`.
* `repeat` (`number`. Default: `-1`): The number of times to repeat the animation. -1 means unlimited.
* `pause` (`number`. Default: `0`): The time (milliseconds) between animations. Set to `random` to have a random time.
* `fontMinSize` (`number`. Default: `7`): The minimum font's size of the strings.
* `fontMaxSize` (`number`. Default: `28`): The maximum font's size of the strings.
* `fontUnit` (`string`. Default: `px`): The unit to use for the font's size. The value accepted are all those accepted
by the browsers, for example: `px`, `em`, `rem` and so on.

### Override default values

[Audero Flashing Text](https://github.com/AurelioDeRosa/Audero-Flashing-Text) has been developed following the current
best practices in developing plugins for jQuery. Therefore, it exposes the previously cited options through the
`defaults` object, allowing you to override the properties' default value. This is very useful if you usually use the
same values to run the animation. In fact, changing the default values, you don't need to specify them again when you
initialize the effect.

For example, let that you have the following code:

```js
$('#box-1').auderoFlashingText({
   repeat: 5,
   pause: 500,
   duration: 1000
});

$('#box-2').auderoFlashingText({
   repeat: 5,
   pause: 500,
   duration: 2000
});
```

Overriding the default values you can turn it into the following:

```js
$.fn.auderoFlashingText.defaults.repeat = 5;
$.fn.auderoFlashingText.defaults.pause = 500;
$('#box-1').auderoFlashingText({
   duration: 1000
});
$('#box-2').auderoFlashingText({
   duration: 2000
});
```

## Advanced Examples

### Example 1

This example demonstrates how you can customize the animation passing options to the initialization method. In this
example almost all the properties seen in the previous section are used:

```js
$('#box').auderoFlashingText({
   fadeIn: 500,
   duration: 800,
   fadeOut: 500,
   pause: 500,
   selection: 'descending',
   fontUnit: 'em',
   fontMinSize: 0.5,
   fontMaxSize: 3,
});
```

### Example 2

This second example is slightly more complex then the previous. In fact, it shows you how to select the strings to
show using the `children()` and `map()` methods of jQuery.

Let that you have this code:

```html
<div id="box-2">
   <ul>
      <li>Lorem</li>
      <li>Ipsum</li>
      <li>Dolor</li>
      <li>Sit</li>
      <li>Amet</li>
   </ul>
</div>
```

You can run the script in this way:

```js
$('#box-2').auderoFlashingText({
   strings: $('#box-2 > ul').children('li').map(function() {
      return $(this).text();
   }),
   fadeOut: 1500,
   selection: 'ascending'
});
```

## License

[Audero Flashing Text](https://github.com/AurelioDeRosa/Audero-Flashing-Text) is dual licensed under
[MIT](http://www.opensource.org/licenses/MIT) and [GPL-3.0](http://opensource.org/licenses/GPL-3.0).

## Author

[Aurelio De Rosa](http://www.audero.it) ([@AurelioDeRosa](https://twitter.com/AurelioDeRosa))
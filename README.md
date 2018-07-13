# A CSS MathML fallback

## Acknowledgements
Big thanks to [Fred Wang](https://github.com/fred-wang/mathml.css) for his initial CSS sheats and [MathJax](https://github.com/mathjax/MathJax) for their general existance.

## Theory of Operation
### Fallback Loading
According to [caniuse.org](https://caniuse.com/mathml), only Firefox and Safari support MathML reliably. There exist [browser specific hacks](http://browserhacks.com/#hack-a13653e3599eb6e6c11ba7f1a859193e) to target Safari and Firefox. (Bonus: Chrome #24, the only Chrome to support MathML, is excluded!)

These queries need to be negated, so Firefox and Safari are excluded instead of targeted. I'm not sure weather this works reliably across all browsers, test on your own!

A CSS-file is loaded when MathML is not supported. The according media-query should be:

    not \\0 screen or (-moz-images-in-menus:0)

(a `not` always negates the full media-query.)

Once media-query is cleared, the fallback-css is loaded.

There is a JS-based method of loading fallback-CSS, which looks at the aspect-ration of a fraction. [Fred Wang](https://github.com/fred-wang/mathml.css) uses this method, which should be easy enough to implement, but I wanted a CSS-only solution.

### Styling + Fonts
MathJax has a bunch of beatutiful math-fonts, which i copied in this projects font folder, simply because I had them locally for testing and having a copy with paths I can rely on can't hurt. If you want to simply load a bunch of fonts for your CSS, link the github_fonts.css - file. Beware, this will cause a bunch of additional, unneccessary reqeusts for your users! Ideally, you select the fonts you need for each page specifically.

### Using Github as CDN
This is a slightly murky business and I implore you to use this feature responsibly! Essentially I dump a bunch of requests from visitors on github by linking the CSS and font files as raw files. I trust you to host these files yourself if you have the infrastructure!

## Usage

Write some math in MathML. I found MathJax a very helpful tool, since it immediately renders the formula and rightclicking your formula reveals the option to show corresponding MathML-code with LaTex-code as annotation! (This is used in the fallback as show on hover!)

Then copy the `<math>`-code to your HTML, serve the fallback to those not understanding MathML and beware that even the fallback won't look as pretty as native MathML-support.

### Styling
Most styling should apply to both MathML and CSS. Beware of some specifics, such as applying font `color` to `mfrac > *{border-color}` as well!

### Testing
`index.html` contains a basic implementation and some formulas to test the CSS-fallback. If you use firefox, disable MathML in the about:config and remove the media-selector to test the fallback.

### TBD/problems
* Brackets can't be stretched to be as high as contained elements (e.g. brackets around a fraction). This seems to be a CSS constrain.
* The root is an amalgamation of border and unicode-sign. It will depend on the font used.

## Motivation
Speed. JS takes time to load and I don't like that. So here is a completely CSS-based MathML fallback. I edited Fred Wang's original CSS a bit, mostly regarding roots.

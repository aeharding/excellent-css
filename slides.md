# Excellent CSS

#### Alexander Harding

[github.com/aeharding/excellent-css](https://github.com/aeharding/excellent-css)

---

## "CSS is easy" (?)

![easy](laser.gif)

 * Syntactically easy: selector, property, value
   ```css
   selector [, selector2, ...] [:pseudo-class] {
     property: value;
     [property2: value2;
     ...]
    }
    ```
 * Not a programming language

---

## "CSS is hard" (?)

 * Constantly evolving -- CSS 1, 2, 2.1, 3
 * Support for a HUGE device matrix
   * FF, Safari, Chrome, IE 9/10/11/Edge on Tablets, phones, desktops (WP, iPhone, Windows 10, Mac OS X)
   ```css
   .flex {
      -ms-box-orient: horizontal;
      display: -ms-flexbox;
      display: -webkit-flex;
      display: -moz-flex;
      display: -ms-flex;
      display: flex;
   }
   ```
   <small><small>(It even broke the syntax highlighting.)</small></small>
 * Everything's a global
 * CSS specificity

---

## What you need to start with

![foundation](foundation.gif)


 * normalize.css
 * `* { box-sizing: border-box }`
 * No big library <small><small>*cough* bootstrap *cough*</small></small>

---

## `normalize.css`

 * NOT a reset -- a normaliz-er
 * Preserves useful browser defaults
 * Correct bugs/inconsistencies
 * VERY simple, each rule is justified [[source]](http://nicolasgallagher.com/about-normalize-css/)
 * Always should be your base


 ![a css reset](css-reset-debugging.png)

---

## `box-sizing: border-box`

```css
html {
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: inherit;
}
```

---

![box model](widthbox.png)

---

```html
<div class="modal fade" tabindex="-1" role="dialog" aria-labelledby="gridSystemModalLabel">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        <h4 class="modal-title" id="gridSystemModalLabel">Modal title</h4>
      </div>
      <div class="modal-body">
        <div class="row">
          <div class="col-md-4">.col-md-4</div>
          <div class="col-md-4 col-md-offset-4">.col-md-4 .col-md-offset-4</div>
        </div>
        <div class="row">
          <div class="col-md-3 col-md-offset-3">.col-md-3 .col-md-offset-3</div>
          <div class="col-md-2 col-md-offset-4">.col-md-2 .col-md-offset-4</div>
        </div>
        <div class="row">
          <div class="col-md-6 col-md-offset-3">.col-md-6 .col-md-offset-3</div>
        </div>
        <div class="row">
          <div class="col-sm-9">
            Level 1: .col-sm-9
            <div class="row">
              <div class="col-xs-8 col-sm-6">
                Level 2: .col-xs-8 .col-sm-6
              </div>
              <div class="col-xs-4 col-sm-6">
                Level 2: .col-xs-4 .col-sm-6
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div><!-- /.modal-content -->
  </div><!-- /.modal-dialog -->
</div><!-- /.modal -->
```

---

![myeyes.gif](myeyes.gif)

---

## No big library

Touch CSS? => No Bootstrap

 * Specificity war
 * Upgrading / removal

Reasons you use bootstrap:

 * You can't CSS
 * Somebody told you to

---

## When building

 * EMs, REMs
 * BEM
 * Many files

---

## EMs, REMs
Use instead of `px`

#### EMs
Equal to the computed `font-size` of the element, inherited

#### REMs
Equal to the computed `font-size` of the `:root`


Note: except `border: 1px solid black`

---

## BEM

### Block Element Modifier

[https://css-tricks.com/bem-101/](https://css-tricks.com/bem-101/)

```css
/* Block component */
.button {}

/* Element that depends upon the block */ 
.button__price {}

/* Modifier that changes the style of the block */
.button--orange {} 
.button--big {}
```

```html
<a href="#" class="button button--orange"></a>
```

(Namespace `.am4-button` if needed)

---

## BEM cont'd

 * Block names should correspond to filenames
   ```
   .am4-button--primary {} ==> button.scss
   ```
 * Specificity is no longer a problem!
   * ONLY nest for `:hover`, `:active`, etc.
   * DO NOT nest for the sake of nesting
 * Scoping/conflicts fixed!

---

## Many files

#### Your project 

```
myProject/
  src/
    sass/
      app.scss
      _variables.scss
      _zindex.scss

      otherComponent.scss
      anotherComponent.scss

      core/
        button.scss
        form.scss
```

---

## Many files (cont'd)

#### `app.scss`

```sass
@import 'normalize';
@import 'variables';
@import 'zindex';

html {
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: inherit;
}

@import 'core/button';
@import 'core/form';

@import 'otherComponent';
@import 'anotherComponent';
```

(Remember to setup `includePaths`.)

---

## Bourbon

```sass
// app.scss
@import 'bourbon';
```

```sass
@include keyframes(my-animation) {
  0% {
    @include transform(translate(0, 0));
  }
  100% {
    @include transform(translate(0, -1em));
  }
}
```
=> Vendor prefixing

---

## autoprefixer

[https://github.com/postcss/autoprefixer](https://github.com/postcss/autoprefixer)

"postcss"

```js
// gulpfile.js
.pipe(postcss([ autoprefixer({ browsers: ['last 2 versions'] }) ]))
```
```css
@keyframes my-animation {
  0% {
    transform: translate(0, 0);
  }
  100% {
    transform: translate(0, -1em);
  }
}
```
=> Vendor prefixing

---

(I prefer autoprefixer.)

---

## Neat

A customizable, lightweight (use what you need), semantic grid

```sass
.am4-welcome {
  @include outer-container;
}
.am4-welcome__aside {
  @include span-columns(3);
}
.am4-welcome__content {
  @include span-columns(9);
}
```
```html
<div class="am4-welcome">
  <div class="am4-welcome__aside"></div>
  <main class="am4-welcome__content">
    <!-- Hello, world! -->
  </main>
</main>
```

Set your own breakpoints, gutter size, etc.

---

# Testing

 * Linting
 * Pixel-by-pixel

---

![adventuretime.gif](adventuretime.gif)

---

# Linting

Everyone ~~is~~ <sup>should be</sup> doing it.

[scss-lint](https://github.com/brigade/scss-lint) or [sass-lint](https://github.com/sasstools/sass-lint)

![lint](lint.png)
![lint2](lint2.png)

---

```ruby
rules:
  border-zero:
    - 1
    - convention: '0'
  brace-style:
    - 1
    - allow-single-line: true
  clean-import-paths:
    - 0
    - filename-extension: false
      leading-underscore: false
[...]
```

---

# Pixel perfect tests

![pp.png](pp.png)

---

# PP tests (con't)

 * It's unmaintainable, shitty, and your only option
 * PhantomCSS vs WebdriverCSS

| WebdriverCSS    | PhantomCSS      |
|-----------------|-----------------|
| Slow            | Fast-ish        |
| All devices     | Webkit          |
| Buggy           | Very buggy      |

```js
phantomcss.screenshot("#feedback-form");
```

---

![githubphantomcss.png](githubphantomcss.png)

---

# Animations

Don't use jQuery for animations

 * CSS fallback
 * "We're not in 2008 anymore"
   * Brute forcing the DOM
 * Animating to dynamic heights
 * [CSS3 Animation Events spec](https://www.w3.org/TR/css3-animations/#animation-events)
   * Use [ngAnimate](https://docs.angularjs.org/api/ngAnimate), [React Animation](https://facebook.github.io/react/docs/animation.html), etc.

---

```css
/* The starting CSS styles for the enter animation */
.jht-page--fade-in.ng-enter {
  transition: 0.5s linear all;
  opacity: 0;
}

/* The finishing CSS styles for the enter animation */
.jht-page--fade-in.ng-enter.ng-enter-active {
  opacity: 1;
}
```

---

# k thx

[github.com/aeharding/excellent-css](https://github.com/aeharding/excellent-css)

![htp.gif](htp.gif)
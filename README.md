# Style Guide Workshop

Learn how to create front-end style guides like <https://www.homify.de/assets/styleguide.html> with Sass and the [LivingStyleGuide Extension](https://github.com/hagenburger/livingstyleguide#readme).


## Setup

Open your terminal and follow those steps:


### (1) Check if Ruby is installed:

```
ruby -v
```

(To install Ruby check <https://www.ruby-lang.org/>)


### (2) Install the generator:

```
gem install livingstyleguide
```

### (3) Test if it’s working:

```
livingstyleguide
```

(This should output a quick help)


## Create a new project

```
mkdir my-style-guide
cd my-style-guide
git init .
```


## Create your styles in Sass as usual

You can use Sass or SCSS as you prefer.
For this workshop, the file structure will be extremely simple,
not caring about any codinging/structure conventions.

``` scss
// main.scss
@import "_colors.scss";
@import "_button.scss";
```

``` scss
// _colors.scss
$pink: #C4558C;
```

``` scss
// _button.scss
button {
  background: $pink;
  border: none;
  color: white;
}
```


## Configure the style guide

Create a new file *styleguide.lsg*. You can name it up to your
preferences. _LSG_ stands for living style guide and that’s what we want
to do. All we need to do to start is reference to our Sass file:

``` yaml
# styleguide.lsg
source: main.scss
```


## First compilation

```
livingstyleguide compile styleguide.lsg styleguide.html
open styleguide.html
```

At least on a Mac, the second line (`open`) will open the result in your
default web browser.

By now, it should be empty having just the headline “Living Style Guide”


## Adding an example for a button

Create a Markdown file in the same folder and the same name as your
button definition and set the file suffix to *.md*. So for
*my-style-guide/_button.scss*, the documentation would be *my-style-guide/_button.md*.

    # Button

    This is how buttons look like:

    ```
    <button>Hello World!</button>
    ```

If you recompile the style guide (`livingstyleguide compile styleguide.lsg styleguide.html`)
and refresh your browser, you should see:

* The headline “Button”
* The example of a pink button
* The syntax-highlighted HTML for the example


## Using classes

If you prefer CSS classes over styling HTML tags, we can change the
example:

``` scss
// _button.scss
.button {
  background: $pink;
  border: none;
  color: white;
}
```

    # Button

    This is how buttons look like:

    ```
    <button class="button">Hello World!</button>
    ```

This should look like the example above, just the HTML source should
change. Again, don’t forget to recompile and refresh.


## Building variations

There might be a special button. Let’s call it secondary and have it
gray to not stand out as much as the other one:

``` scss
// _button.scss
.button {
  background: $pink;
  border: none;
  color: white;

  &.secondary {
    background: gray;
    color: black;
  }
}
```

As it’s Markdown, we can just add another code example in the
*_button.md*:

    # Button

    This is how buttons look like:

    ```
    <button class="button">Hello World!</button>
    ```

    Secondary buttons look like this:

    ```
    <button class="button secondary">Cancel</button>
    ```


## Highlighting differences

Both examples are pretty simple—just one line of HTML and few CSS
classes. So it’s easy to notice the difference. For more complex
examples, a little difference might be hard to notice.

Just like in Markdown, some parts can be highlighted. Markdown uses one
`*` for italics, `**` for bold; in the HTML examples, `***` will create
a highlight.

This way, you can show what has been added/modified in comparison to the
previous example.

    # Button

    This is how buttons look like:

    ```
    <button class="***button***">Hello World!</button>
    ```

    Secondary buttons look like this:

    ```
    <button class="button ***secondary***">Cancel</button>
    ```


## Showing colors

Color swatches are generated in a way that is close to adding HTML
examples. Create a new Markdown file for the Sass file where your colors
are defined. So in our example this would be *_colors.md*.

The difference to an HTML example: In the first line of the example
deinition, the filter `@colors` is set:

    # Colors

    ```
    @colors
    $pink
    ```

After recompilation, a huuuuge pink color swatch should appear in your
style guide.

If we ad a second and third color, this will get smaller as color
swatches will use the full width of the style guide:

``` scss
// _colors.scss
$pink: #C4558C;
$purple: #923D6A;
$yellow: #E9D784;
```

    # Colors

    ```
    @colors
    $pink $purple $yellow
    ```


## Arranging colors

Let’s assume those 3 colors are the main colors of the project. There
are also 5 shades of blue.


``` scss
// _colors.scss
$pink: #C4558C;
$purple: #923D6A;
$yellow: #E9D784;

$blue-1: #C8E9E9;
$blue-2: #3B9E9D;
$blue-3: #319796;
$blue-4: #268584;
$blue-5: #1B6262;
```

Putting all in one line might not look very good:

    # Colors

    ```
    @colors
    $pink $purple $yellow $blue-1 $blue-2 $blue-3 $blue-4 $blue-5
    ```

It’s possible to put the colors into two lines:

    # Colors

    ```
    @colors
    $pink $purple $yellow
    $blue-1 $blue-2 $blue-3 $blue-4 $blue-5
    ```

If you like it to be centered, you can leave a color swatch empty by
putting a `-` in the list:

    # Colors

    ```
    @colors
    - $pink $purple $yellow -
    $blue-1 $blue-2 $blue-3 $blue-4 $blue-5
    ```

Finally to make this more readable, you can add more white space:

    # Colors

    ```
    @colors
    -        $pink    $purple  $yellow  -
    $blue-1  $blue-2  $blue-3  $blue-4  $blue-5
    ```

But as the primary colors are more important, they might should look
bigger. The easiest way is to split it up into 2 examples:

    # Colors

    ```
    @colors
    $pink $purple $yellow
    ```

    ```
    @colors
    $blue-1 $blue-2 $blue-3 $blue-4 $blue-5
    ```


## Typography

To show, which fonts are used in your project, create an example in
*_typography.md* like this:

    # Typography

    ```
    @font-example Helvetica Neue
    ```

Recompile and have a look. Doesn’t it show up? Most likely yes. To
integrate a Markdown file into the style guide, be sure:

* To have a matching *.scss* or *.sass* file.
* To have this file imported somewhere during the compilation of your
  main Sass file (*main.scss* in our case)

Follow those steps and recompile again.

No Helvetica? Be sure to match the [CSS specifications for font properties](http://www.w3.org/TR/CSS2/fonts.html#font-shorthand):

    # Typography

    ```
    @font-example normal 20px Helvetica Neue
    ```


## Different font examples

If you like to have another example text—e.g. to show German
umlauts—just add it below the filter command:

    # Typography

    ```
    @font-example Helvetica Neue
    ABCDEFGHIJKLMNOPQRSTUVWXYZÄÖÜ
    abcdefghijklmnopqrstuvwxyzäöüß
    0123456789
    !&/()$=@;:,.
    ```


## Adding a title

``` yaml
# styleguide.lsg
source: main.scss
title: My first style guide
```

This will change the `<title>` of your document.


## Styling the style guide itself

Till now, everything looks quite gray and not much like your own
project. With a little configuration you can change the style that is
automatically generated for your style guide:

``` yaml
# styleguide.lsg
source: main.scss
title: My first style guide
style:
  color: #C4558C
```

This will set the pink color at some places. As this will be put into
Sass code, you can also use your variables like `$pink` which we defined
in *_colors.scss*:

``` yaml
# styleguide.lsg
source: main.scss
title: My first style guide
style:
  color: "$pink"
```

A tip: Yaml does not require quotes, but it’s recommended to use them
here as they might have problems with SassScript.

Try out some more styles (also have a look at the [readme](https://github.com/hagenburger/livingstyleguide#custom-settings)):

``` yaml
# styleguide.lsg
source: main.scss
title: My first style guide
style:
  color: "$pink"
  code-color: "$blue-4"
  code-background-color: "$blue-1"
  color-swatch-border-radius: "10px"
```


## Adding a custom header

The first thing you see when you open a front-end style guide might be a
logo of the website you’re coding for. You can put any HTML in here:

``` yaml
# styleguide.lsg
source: main.scss
title: My first style guide
style:
  color: "$pink"
  code-color: "$blue-4"
  code-background-color: "$blue-1"
  color-swatch-border-radius: "10px"
header: <img src="http://sass-lang.com/assets/img/styleguide/color-1c4aab2b.png">
```

If you want to use multi-line HTML, Yaml is tricky. You need to a a `|`
and indent your content below by 2 spaces:

``` yaml
# styleguide.lsg
source: main.scss
title: My first style guide
style:
  color: "$pink"
  code-color: "$blue-4"
  code-background-color: "$blue-1"
  color-swatch-border-radius: "10px"
header: |
  <div class="my-header">
    <img src="http://sass-lang.com/assets/img/styleguide/white-e44bed0d.png">
  </div>
```

The CSS for styling this header should only appear in the style guide.
We don’t want to have this in our production CSS.

Add additional Sass code like this:

``` yaml
# styleguide.lsg
source: main.scss
title: My first style guide
style:
  color: "$pink"
  code-color: "$blue-4"
  code-background-color: "$blue-1"
  color-swatch-border-radius: "10px"
header: |
  <div class="my-header">
    <img src="http://sass-lang.com/assets/img/styleguide/white-e44bed0d.png">
  </div>
styleguide-scss: |
  .my-header {
    background: $pink;
    padding: 20px;
    text-align: center;
   }
```

If you want to use the intended syntax, use `styleguide-sass:` instead.
The code written here has access to all variables, mixins, placeholders,
… you defined in your project.


## Automation

Running the compile command in the command line every time may not be
fun. There’s a lot of integration available for Rails, Middleman, Gulp,
Broccoli and others. Check the [readme section](https://github.com/hagenburger/livingstyleguide#getting-started) for details.


## Questions? Feedback?

* Follow [@hagenburger](https://twitter.com/hagenburger) on Twitter
* [Open an issue](https://github.com/hagenburger/livingstyleguide-workshop/issues/new)
  if you found a typo, error, or want to suggest an improvement for this
  workshop
* If the issue does not apply to this workshop but to the
  LivingStyleGuide generator itself (bug, question, …), please open [an
  issue over there](https://github.com/hagenburger/livingstyleguide/issues/new).

Feel free to use this workshop and have one at your [local Sass user group](http://una.github.io/sassconf-2014/#/) :)

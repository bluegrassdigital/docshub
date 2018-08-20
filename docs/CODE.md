Regular markdown syntax works for all pages, including code fences.

Some more advanced docshub specific features have their own html-like components with various available options.

These custom docshub "widgets" are documented below.

## Supported languages

You can render anything in a code block, however only a certain subset of languages are supporte for syntax highlighting.

- xml
- html
- bash
- clojure
- coffeescript
- css
- markdown
- bash
- clojure
- coffeescript
- css
- markdown
- dart
- diff
- dockerfile
- ruby
- go
- gradle
- haml
- handlebars
- java
- javascript
- json
- less
- nginx
- objectivec
- powershell
- python
- scala
- scss
- shell
- stylus
- swift
- yaml
- typescript
- vbnet
- dart
- diff
- dockerfile
- ruby
- go
- gradle
- haml
- handlebars
- java
- javascript
- json
- less
- nginx
- objectivec
- powershell
- python
- scala
- scss
- shell
- stylus
- swift
- yaml
- typescript
- vbnet

## Refs

Each widget can have a ref attribute which can be used by other widgets to reference that widget later. This allows you to interlink parts of your code. For example, you can show the html code and render it as an embed without duplicating anything.

### codeblock

At it's most basic:
``` html
<?codeblock lang="javascript">
alert('hello world');
</codeblock?>
```

Why not just use a code fence? Well, for the above example you would just use a code fence. However when you need to dispaly more advanced code, external files and use code for embeds the power of docshub widgets comes to the fore.

#### lang (codeblock attribute)

Any one of the above options. Dochsub will try to auto detect based on content if no lang attribute is provided.

#### prettify (codeblock attribute)

If this attribute is present, content is prettified. Only works for css, scss, less, js, json, javascript, typescript, html

#### external (codeblock attribute)

A url to an external file to reference for the code. Overrides any children passed to the widget.

eg.

``` html
<?codeblock external="config.json" lang="json" prettify></codeblock?>
```

### embed

An embed, by default will simply take the html provided and render it in an iframe.

<?codeembed base="base.html" adjust-height size="320x240">
<p>test</p>
</codeembed?>

``` html
<?codeembed base="base.html" adjust-height size="320x240">
<p>test</p>
</codeembed?>
```

#### base (codeembed attribute)
Base specifies the url of the file to use as the base for the iframe. This is required. At a minimum that file would contain:

<?codeblock external="base.html" lang="html" prettify></codeblock?>

An element with id exampleContent is required as the injection point.

#### use-html (codeembed attribute)
When use-html is provided this specifies the ref of the codeblock to use as the injected html rather than the children of the widget.

#### stylesheets (codeblock attribute)
comma-separated list of external stylesheets to add to the embed.

#### scripts (codeembed attribute)
comma-separated list of external javascript files to add to the embed.

#### script-refs (codeembed attribute)
comma-separated list of javascript codeblock refs to add to the embed.

#### style-refs (codeembed attribute)
comma-separated list of css codeblock refs to add to the embed.

#### seamless (codeembed attribute)
An alternative style embed. Shows no sizing controls and no borders etc.

<?codeembed seamless base="base.html" adjust-height size="320x240">
<p>test</p>
</codeembed?>

#### minimal (codeembed attribute)
Another alternative minimal style that still shows size controls

<?codeembed minimal base="base.html" adjust-height size="320x240">
<p>test</p>
</codeembed?>


#### adjust-height (codeembed attribute)
Will adjust height to fit the content (up to the height defined in the ssize attribute)

#### min-height (codeembed attribute)
Minimum height of iframe. If you're rendering something that expends on interaction (like a menu or accordion) you might need this attribute to set a minimum height.

#### size (codeembed attribute)
Either a predefined size:

- iphone5s (320x568)
- iphone6 (375x667)
- ipad (768x1024)
- desktop (1100x700)

OR a custom size in the format `{width}x{height}` - eg. `400x600`

### tabs
Tabs are a nice clean way of tying your embeds and code display into a single interface.

codeembed and codeblock widgets arledy extend off of a base widget that is a tab. Each widget supports a `title` attribute which shows as the tabs title if rendered inside a tabs widget.

So the simplest implementation of tabs would be:

``` html
<?tabs>
<codeembed
  base="base.html"
  adjust-height
  size="iphone5s"
  use-html="html-eg"
  title="Result"
  script-refs="script-eg"
  minimal
></codeembed>
<codeblock lang="html" ref="html-eg" title="The HTML">
<p id="test">test</p>
</codeblock>
<codeblock lang="javascript" ref="script-eg" title="The JS">
document.querySelector('#test').style.color = 'blue';
</codeblock>
</tabs?>
```

<?tabs>
<codeembed
  base="base.html"
  adjust-height
  size="iphone5s"
  use-html="html-eg"
  title="Result"
  script-refs="script-eg"
  style-refs="style-eg"
  minimal
></codeembed>
<codeblock lang="html" ref="html-eg" title="The HTML">
<p id="test">test</p>
</codeblock>
<codeblock lang="css" ref="style-eg" title="The CSS">
#test {
  color: orange;
}
</codeblock>
<codeblock lang="javascript" ref="script-eg" title="The JS">
document.querySelector('#test').style.color = 'blue';
</codeblock>
</tabs?>

__NB: When rendering multiple widget children in the case of tabs, you only need the ? in the tag name at the beginning of the opening and end of the closing tags.__

## Computed style
 
These days elements are rarely styled with just inline styles. For example, a, inline style can be applied to an error message to make the text red:

{lang="html"}
~~~~~~~~
<div style="color:red;">Error</div>
~~~~~~~~

Styles are now often moved into classes so that they can be consistently applied across different elements and pages. For example, using a class, the element might become:

{lang="html"}
~~~~~~~~
<div class="error_message">Error</div>
~~~~~~~~

To check that the error message text is red, it is not sufficient to just check the style attribute. Instead, you need to check the computed style - ie the actual style applied by the browser. This can be achieved by using the Element#style method and specifying a style property: 

{lang="ruby"}
~~~~~~~~
browser.div.style('color')
#=> "rgba(255, 0, 0, 1)"
~~~~~~~~

Note:
* The shorthand CSS properties (e.g. background, font, etc.) are not supported. The longhand properties should be used instead - eg background-color.
* Depending on the browser, the formatting of the property may vary.
## Text

The :text locator allows elements to be located by their text.

{lang="html"}
~~~~~~~~
<div>This is the text of the element.</div>
~~~~~~~~

The element can located by an exact text match:

{lang="ruby"}
~~~~~~~~
browser.div(:text => 'This is the text of the element.')
~~~~~~~~

As well as by a partial text match:

{lang="ruby"}
~~~~~~~~
browser.div(:text => /text of the element/)
~~~~~~~~

Note that an element's text is considered all text nodes of the element as well as its descendents.

{lang="html"}
~~~~~~~~
<span id="container">This line has <span id="inner">inner</span> text</span>
~~~~~~~~

For this element, the span's text is "This line has inner text". It is not just the element's direct child text nodes - "This line has text".

{lang="ruby"}
~~~~~~~~
browser.span(:text => 'This line has inner text').exists?
#=> true
~~~~~~~~

This is important to remember when locating an element by its text using a regular expression. If locating a span that contains the text "inner", the outer span with id "container" will be returned rather than the inner span.

{lang="ruby"}
~~~~~~~~
browser.span(:text => /inner/).id
#=> "container"
~~~~~~~~
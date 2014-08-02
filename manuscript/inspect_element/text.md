## Text

The _text_ method returns the visible text of an element.

Given the html:

{lang="html"}
~~~~~~~~	
<div>This is the text of the element.</div>
~~~~~~~~

The text of the div element is:

{lang="ruby"}
~~~~~~~~	
browser.div.text
#=> "This is the text of the element."
~~~~~~~~

Note that the text of an element includes:

* The text nodes of the element and
* The text nodes of the element's descendants.

The following span has its own text node, " is a Ruby gem.", as well as a descendant text node, "Watir".

{lang="html"}
~~~~~~~~	
<span><a href="watir.com">Watir</a> is a Ruby gem.</span>
~~~~~~~~

The text of the span is the concatenation of the text nodes:

{lang="ruby"}
~~~~~~~~	
browser.span.text
#=> "Watir is a Ruby gem."
~~~~~~~~

Also note that Watir will only include the text that is visible to the user. In the following div, the first span is visible to the user, while the second span is not.

{lang="html"}
~~~~~~~~	
<div>
  <span>visible text</span>
  <span style="display:none;">hidden text</span>
</div>
~~~~~~~~

Therefore, text of the div will only be the first span:

{lang="ruby"}
~~~~~~~~	
browser.div.text
#=> "visible text"
~~~~~~~~

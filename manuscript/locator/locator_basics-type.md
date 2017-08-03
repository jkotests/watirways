## Element type

When locating an element, Watir needs to be told: 

  * What type of element to find and
  * How many matches to return.

This is achieved by calling the corresponding element type method. 

### Element vs collection

Watir can find and return an: 

  * Element - The first (single) matching element or
  * Element Collection - All matching elements.

There are two element type methods, for each supported element, that correlate to the return type: 

  * Singular - This version returns the element.
  * Plual - This version returns the element collection.

For example, the `div` method, which is singular, will tell Watir to find the first `div` element on the page.

{lang="ruby"}
~~~~~~~~
browser.div
~~~~~~~~

The pluralization of `div` is `divs`, which will return all `div` elements on the page.

{lang="ruby"}
~~~~~~~~
browser.divs
~~~~~~~~

Note that the pluralized version is generally the singular version with a "s" added to the end. However, following English conventions, there will be some element types that have "es" added to the end or have the ending "y" replaced by "ies". 

| Scenario | HTML Element | Singular | Plural | 
|----------|--------------|----------|--------|
| Add 's' | \<span\> | span | spans |
| Add 'es' | \<progress\> | progress | progresses |
| Add 'ies' | \<summary\> | summary | summaries |

### Standard HTML element methods

In general, the singular element type method is the same as the HTML element tag.

For example, the HTML `ul` element:

{lang="html"}
~~~~~~~~
<ul id="my_id">
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
~~~~~~~~

Would be retrieved by Watir's `ul` method.

{lang="ruby"}
~~~~~~~~
browser.ul
~~~~~~~~

The following table lists the methods to locate some common element types. 

| Element Method | Collection Method | HTML Elements Matched |
|----------------|-------------------|-----------------------|
| a | as | \<a\> |
| div | divs | \<div\> |
| h1 | h1s | \<h1\> |
| li | lis | \<li\> |
| span | spans | \<span\> |
| table | tables | \<table\> |

### Convenience methods

Watir defines additional element type methods that: 

  * Are more specific. For example, `\<input type="checkbox"\>` can be located using `browser.checkbox` instead of using `browser.input(type: 'checkbox')`.
  * Makes visually similar elements equivalent. For example, HTML has a variety of buttons - `\<button\>`, `\<input type="button"\>`, etc. They are all equivalent in Watir as each is located with the same `browser.button` method.
  * Provide more readable names through aliases. For example, `\<a\>` elements can be located via `browser.a` or `browser.link`.

The following table lists the common convenience methods. 

| Element Method | Collection Method | HTML Elements Matched |
|----------------|-------------------|-----------------------|
| button | buttons | \<button\> |
| | | \<input type="button"\> |
| | | \<input type="image"\> |
| | | \<input type="reset"\> |
| | | \<input type="submit"\> |
|----------------|-------------------|-----------------------|
| checkbox | checkboxes | \<input type="checkbox"\> |
|----------------|-------------------|-----------------------|
| element | elements | All | 
|----------------|-------------------|-----------------------|
| file_field | file_fields | \<input type="file"\> |
|----------------|-------------------|-----------------------|
| hidden | hiddens | \<input type="hidden"\> |
|----------------|-------------------|-----------------------|
| image | images | \<img\> |
|----------------|-------------------|-----------------------|
| link | links | \<a\> |
|----------------|-------------------|-----------------------|
| radio | radios | \<input type="radio"\> |
|----------------|-------------------|-----------------------|
| select_list | select_lists | \<select\> |
|----------------|-------------------|-----------------------|
| text_field | text_fields | \<input type="password"\> |
| | | \<input type="text"\> |
|----------------|-------------------|-----------------------|

### Custom elements

Some applications use element types that are not in the HTML specifications.

{lang="html"}
~~~~~~~~	
<li class="lastMove">
  <div id="81ae2" class="folder">
    <small onclick="someFunction1()"> </small>
  </div>
</li>
~~~~~~~~

The `small` element type is not defined in the specifications. As a result, Watir does not define a _small_ method - ie you cannot do `browser.small.click`. To locate these elements, you can use the genaric element method with a `:tag_name` locator.

{lang="ruby"}
~~~~~~~~
browser.element(:tag_name => 'small')
~~~~~~~~
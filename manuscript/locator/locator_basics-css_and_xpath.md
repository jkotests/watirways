## CSS

The :css locator allows a css-selector to be used to find an element.

{lang="ruby"}
~~~~~~~~
browser.div(:css => 'div#my_id')
~~~~~~~~

For more details on creating a css-selector, see the [css-selector specifications](http://www.w3.org/TR/css3-selectors/).

## Xpath

The :xpath locator allows an element to be located based on its path.

{lang="ruby"}
~~~~~~~~
browser.div(:xpath => '//div[@id="my_id"]')
~~~~~~~~

For more details on determining an element's xpath, see the [xpath specifications](http://www.w3.org/TR/xpath20/).
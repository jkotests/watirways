## Approach

There are usually many approaches that can be taken to locate an element.

For example, consider finding the user id, "j.smith", in the following html.

~~~~~~~~
<div id="field1">
  <span class="label">User ID:</span>
  <span class="value">j.smith</span>
</div>
~~~~~~~~

The element could be located by its class.

~~~~~~~~
browser.span(:class => 'value').text
#=> "j.smith"
~~~~~~~~

The element could also be located based on its relative location within its parent element.

~~~~~~~~
browser.div(:id => 'field1').span(:index => 1).text
#=> "j.smith"
~~~~~~~~

Another option would be to locate the element based on the text of its sibling span.

~~~~~~~~
browser.span(:text => /User ID/).parent.span(:class => 'value').text
#=> "j.smith"
~~~~~~~~

From these (and other) options, how do you decide which to use?

It is important to consider the factors:

* Robustness
* Readability
* Performance

### Robustness


### Readability 



### Performance






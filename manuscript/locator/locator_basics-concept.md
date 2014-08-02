## Concepts

An element's properties, such as attributes, text, label, etc., can be used to be specific about which element to find.

### Single vs multiple properties

An element can be located using 0 properties, which returns the first element.

{lang="ruby"}
~~~~~~~~
browser.div
~~~~~~~~

To locate an element with specific properties, create a hash of the properties. A hash looks like:

{lang="ruby"}
~~~~~~~~
:property1 => 'value1', :property2 => 'value2'
~~~~~~~~

Where:
 
  * The keys of the hash are the properties to test or the how to match the element.
  * The values of the hash are the expected property values or the what to match.

The hash can be used to match a single property. For example, the following says to find a div element that has the id "my_id".

{lang="ruby"}
~~~~~~~~
browser.div(:id => 'my_id')
~~~~~~~~

The hash can be expanded to include any number of properties. The following locates a div element that has the class "enabled", the text "Navigate" and name attribute containing the word "navigate".

{lang="ruby"}
~~~~~~~~
browser.div(:class => 'enabled', :text => 'Navigate', :name => /navigate/)
~~~~~~~~

### Exact vs partial match

When looking for matching elements, Watir can check if the property is an exact match or a partial match. This is controlled by the value in the locator.

  * A String object will perform an exact match.
  * A Regular Expression (Regexp) object will perform a partial match.

For example, the following locator is using a String (denoted by the quotation marks) for the value of the :id property. This means that it will only match elements whose id attribute is exactly "my_id". It will not match elements whose id is "before_my_id" or "my_id_after".

{lang="ruby"}
~~~~~~~~
browser.div(:id => 'my_id')
~~~~~~~~

If you want to match elements whose id attribute contains "my_id" anywhere (ie a partial match), you can use a Regexp (denoted by the forward slashes). The following locator will match elements that have the id "my_id", as well as "before_my_id" or "my_id_after".

{lang="ruby"}
~~~~~~~~
browser.div(:id => /my_id/)
~~~~~~~~
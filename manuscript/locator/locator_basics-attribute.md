## Attributes

Attributes provide additional infomation (meaning and context) about the element. They appear in the opening tag of an element in the form name="value".

In the following element, there are 3 attributes - id, name and class. They have the values "divs_id", "divs_name" and "divs_class" respectively.

{lang="ruby"}
~~~~~~~~
<div id="divs_id" name="divs_name" class="divs_class">text</div>
~~~~~~~~

Watir can locate an element by its attributes by setting attribute name as the key and the attribute value as the value.

{lang="ruby"}
~~~~~~~~
browser.div(:attribute_name => "attribute_value")
~~~~~~~~

### Standard attributes

The HTML specifications only allow certain attributes to be included on an element. In Watir, any of these attributes can be used to locate the element.

As an example, consider the id attribute used in the following HTML. The uniqueness of this attribute makes it an ideal unambiguous locator.

{lang="html"}
~~~~~~~~
<div id="phone_number">
  <span id="area_code">123</span>
  <span id="exchange">456</span>
  <span id="subscriber">7890</span>
</div>
~~~~~~~~

An element can be located by an exact id match:

{lang="ruby"}
~~~~~~~~
browser.span(:id => "exchange").text
#=> "456"
~~~~~~~~

Or by a partial id match:

{lang="ruby"}
~~~~~~~~
browser.span(:id => /area/).text
#=> "123"
~~~~~~~~

### Class

If something on the page looks different (ex the text size, the background colour, etc), it means that a style has been applied to the element. Often, to reduce maintenance of the page, developers will extract these styles into a style sheet that defines groups of styles. These groups of styles are called classes. An element can use one or more classes by defining the class attribute.

While the class is a standard HTML attribute, there is special handling by Watir. Consider the following HTML:

{lang="html"}
~~~~~~~~
<span class="number">123</span>
<span class="bold number">456</span>
<span class="bold number">7890</span>
~~~~~~~~

The first span element has a single class called "number". The other two spans have two classes - "bold" and "number". Note that in the class attribute value, multiple classes are separated by a space.

When locating an element by its class, watir will try matching each individual class rather than the entire attribute value. For example, locating an element with class "number", will return elements with a class attribute value "number" as well as "multiple number classes".

Locating an element based on an exact class match would look like:

{lang="ruby"}
~~~~~~~~
browser.span(:class => 'number').text
#=> "123"
~~~~~~~~

A regular expression can be used to partially match a class name:

{lang="ruby"}
~~~~~~~~
browser.span(:class => /bo/).text
#=> "456"
~~~~~~~~

### Data attributes

In some cases, the standard HTML attributes do not provide enough information for an application. Custom data attributes allow additional information to be added to the element, while still being valid HTML markup.

For example, a div element that represents a person might use custom data attributes to store the person's height and weight.

{lang="html"}
<<(code/locator/locate_by_data_attribute.htm)

The custom data attributes will have the form "data-customname", where "customname" can be any text.

These custom attributes can be used the same as the standard locators. However, for the attribute name, the dash (-) must be replaced by an underscore (_).

Locate an element based on an exact match of the attribute value:

{lang="ruby"}
<<(code/locator/locate_by_data_attribute_exact.rb)

Locate an element based on a partial match of the attribute value:

{lang="ruby"}
<<(code/locator/locate_by_data_attribute_partial.rb)

### Custom attributes

Some applications will still be using attributes that are not in the HTML specifications (likely due to the application being developed before data attributes were introduced). These attributes are not directly supported by Watir as locators.

For these attributes, you can use a CSS or XPath selector.

{lang="html"}
~~~~~~~~
<div>
    <span customattribute="custom1">Custom Attribute 1</span>
    <span customattribute="custom2">Custom Attribute 2</span>
    <span customattribute="custom3">Custom Attribute 3</span>
</div>
~~~~~~~~

In CSS-locators, the square brackets are used for matching attributes.

To locate a span that has the customattribute attribute, of any value:

{lang="ruby"}
~~~~~~~~
browser.span(:css, 'span[customattribute]').text
#=> "Custom Attribute 1"
~~~~~~~~

To locate the span with a specific customattribute value:

{lang="ruby"}
~~~~~~~~
browser.span(:css, 'span[customattribute="custom2"]').text
#=> "Custom Attribute 2"
~~~~~~~~

XPath is similar to CSS-locators, however the attribute name must be prefixed with an at symbol (@):

{lang="ruby"}
~~~~~~~~
browser.span(:xpath, '//span[@customattribute="custom2"]').text
#=> "Custom Attribute 2"
~~~~~~~~
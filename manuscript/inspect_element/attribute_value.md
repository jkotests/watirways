## Attribute value

Attributes provide additional information or behaviour for an element. They can be found within the element's start tag.

Watir provides 2 ways to get attribute values:

1. Using the method that returns the specific attribute's value.
2. Using the _attribute_value_ method.

### Standard attributes

For attributes that are defined in the HTML specification, there is a corresponding method that returns the attribute value. In most cases, the attribute name and the method name are exactly the same. However, Ruby naming conventions are applied in some situations.

{width="wide"}
| Scenario | Naming Rule | Example Attribute | Corresponding Method |
|----------|-------------|-------------------|----------------------|
| Single word attribute | Match attribute name | id | id |
| Multi-word attribute | Words separated by underscore | maxlength | max_length |
| Boolean attribute | End with question mark | disabled | disabled? |
| Data attribute | Dashes replaced by underscores | data-field | data_field |
| Aria attribute | Dashes replaced by underscores | aria-describedby | aria_describedby |
| Class attribute | Due to Ruby objects already having a _class_ method, which returns the instance's class, the "class" attribute is a special case. | class | class_name |

The following HTML has several attributes:

{lang="html"}
~~~~~~~~
<div data-field="first_name">
  <label id="tp1-label" for="first">First Name:</label>
  <input type="text" id="first" maxlength="50" required="required"
    aria-labelledby="tp1-label" aria-describedby="tp1">
  <div id="tp1" class="tooltip" role="tooltip" hidden="hidden"
    aria-hidden="true">Your first name is a required</div>
</div>
~~~~~~~~

The attribute methods can be used to get the values:

{lang="ruby"}
~~~~~~~~
# Retrieve a single word attribute
browser.text_field.id
#=> "first"

# Retrieve a multi-word attribute
browser.text_field.max_length
#=> 50

# Retrieve a boolean attribute
browser.text_field.required?
#=> true
browser.text_field.disabled?
#=> false

# Retrieve a data attribute
browser.div.data_field
#=> "first_name"

# Retrieve an aria attribute
browser.input.aria_labelledby
#=> "tp1-label"

# Retrieve a class attribute
browser.div(id: 'tp1').class_name
#=> "tooltip"
~~~~~~~~

Note that the object type returned by the method will depend on the attribute:

* Boolean attributes will return a TrueClass or FalseClass object.
* Numeric attributes will return a Fixnum object.
* The rest of the attributes will return a String object.

### Custom attributes

There will be some attributes that do not have an associated method:

* Attributes that are not defined in the HTML specification.
* Standard attribute methods that are not yet implemented in Watir-Classic.

In these cases, the _attribute_value_ method is required.

Given an element with a custom attribute:

{lang="html"}
~~~~~~~~
<div myCustomAttribute="custom" id="div_id">text</div>
~~~~~~~~

The value of the custom attribute can be obtained by passing the name of the attribute to the _attribute_value_ method:

{lang="ruby"}
~~~~~~~~
browser.div.attribute_value('myCustomAttribute')
#=> "custom"
~~~~~~~~

The method can also be useful when dynamically retrieving attribute values. For example, the following collects the attribute values specified in an array.

{lang="ruby"}
~~~~~~~~
attrs = ['id', 'myCustomAttribute']
values = attrs.map { |attr| browser.div.attribute_value(attr) }
#=> ["div_id", "custom"]
~~~~~~~~
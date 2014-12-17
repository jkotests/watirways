## Text Field

### Input

To simulate a user typing into a text field, use the _set_ method:

{lang="ruby"}
~~~~~~~~
browser.text_field.set("first")
p browser.text_field.value
#=> "first"
~~~~~~~~

Note that the _set_ method will overwrite the previous text:

{lang="ruby"}
~~~~~~~~
browser.text_field.set("first")
browser.text_field.set("second")
p browser.text_field.value
#=> "second"
~~~~~~~~

If you want to add additional text, use the _append_ method instead:

{lang="ruby"}
~~~~~~~~
browser.text_field.set("first")
browser.text_field.append("second")
p browser.text_field.value
#=> "firstsecond"
~~~~~~~~

To make the text field blank, use the _clear_ method:

{lang="ruby"}
~~~~~~~~
browser.text_field.clear
p browser.text_field.value
#=> ""
~~~~~~~~

### Inspect

The text that a user sees in a text field is stored in the input's value attribute. Therefore, to get the text of the text field, use the standard attribute methods:

{lang="ruby"}
~~~~~~~~
browser.text_field.set('some text')
p browser.text_field.value
#=> "some text"
~~~~~~~~

### Textarea

While textareas can be located differently than text fields, they are set and inspected using the same methods. What makes textareas special on web pages is that they can have multi-line text. A real user would create multiple lines by pressing the Enter key on the keyboard. With Watir, you can do the exact same keystrokes:

{lang="ruby"}
~~~~~~~~
browser.textarea.set('first line', :return, 'second line')
puts browser.textarea.value
#=> first line
#=> second line
~~~~~~~~

However, it is often more convenient to send a double-quoted String with the line break character ("\n"):

{lang="ruby"}
~~~~~~~~
browser.textarea.set("first line\nsecond line")
puts browser.textarea.value
#=> first line
#=> second line
~~~~~~~~
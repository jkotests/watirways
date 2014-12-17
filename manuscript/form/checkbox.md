## Checkbox

### Input

A checkbox is checked by using the _set_ method:

{lang="ruby"}
~~~~~~~~
browser.checkbox.set
~~~~~~~~

It can be unchecked by using the _clear_ method:

{lang="ruby"}
~~~~~~~~
browser.checkbox.clear
~~~~~~~~

The _set_ method can take a boolean parameter, where true will check the box and false will uncheck the box:

{lang="ruby"}
~~~~~~~~
# Check
browser.checkbox.set(true)

# Uncheck
browser.checkbox.set(false)
~~~~~~~~

This is useful when the checkbox needs to be set based on a condition. For example, an if-else statement:

{lang="ruby"}
~~~~~~~~
if condition_met?
  browser.checkbox.set
else
  browser.checkbox.clear
end
~~~~~~~~

Can be re-written as:

{lang="ruby"}
~~~~~~~~
browser.checkbox.set(condition_met?)
~~~~~~~~

### Inspect

The state of the checkbox, whether it is checked or unchecked, can be determined by the _set?_ method:

{lang="ruby"}
~~~~~~~~
browser.checkbox.set
p browser.checkbox.set?
#=> true

browser.checkbox.clear
p browser.checkbox.set?
#=> false
~~~~~~~~
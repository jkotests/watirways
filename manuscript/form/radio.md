## Radio

### Input

A radio button is selected by using the _set_ method:

{lang="ruby"}
~~~~~~~~
browser.radio.set
~~~~~~~~
    
### Inspect

The _set?_ method is used to determine if a radio button is turned on:

{lang="ruby"}
~~~~~~~~
p browser.radio.set?
#=> false

browser.radio.set

p browser.radio.set?
#=> true
~~~~~~~~
# towrite

needed for version 1.0:

book introduction
* what watir is
 * what watir does
* what watir used for
* watir gem relationship

concept
* structure:
** find browser/element
** perform action - inspect, get elements, interact
* example

browser
* open
Default browser is IE on windows and Firefox on others.
browser = Watir::Browser.new
Specify specific browser
browser = Watir::Browser.new :ff
browser = Watir::Browser.new :chrome
browser = Watir::Browser.new :ie
Note regarding requiring watir:
--> browser selection will determine loaded gem (classic vs webdriver)


* close
browser.close

* goto
* attach
watir-classic only
browser = Watir::Browser.attach()
--> locators include title, url (exact and partial)

Inspecting elements
* text
* present/exists/visible
* computed style

mouse interactions
* click

* waiting

* filling in forms




future:

locating an element
* parent
* working with frames

browser
* forward
* backward
* multiple windows

Inspecting browser
* url
* html?

Inspecting elements
* attribute values 
    some can be accessed by doing .whatever
    class_name
* tag name    
* html
* scroll into view (does not belong here?)
* disabled

mouse/keyboard interactions
* click with modifiers
* drag and drop
* double click
* select text?
* send_keys

 javascript
* fire events
* execute_script
* ie direct dom access

collections
  number of matching elements
  iterating

*steps to the locator
  how many to return
  type of element to find
  unique characteristics of an element (or other related elements)


Browser
	Open
		Browser Type
	Close
	Goto
	Window Size
Element
	html
	text
	style
	visibility
Inputs
	
		
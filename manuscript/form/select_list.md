## Select List

A select list, often called a dropdown, consists of:

* A select element - the overall control
* Option elements - the items that the user picks

The HTML:

{lang="html"}
~~~~~~~~
<select id="language">
  <option value="ar">Arabic</option>
  <option value="en">English</option>
  <option value="hi">Hindi</option>
  <option value="zh">Mandarin</option>
  <option value="es">Spanish</option>
</select>
~~~~~~~~

### Input

The most straight forward way to select an option is to use the text visible to the user:

{lang="ruby"}
~~~~~~~~
# Exact match
browser.select_list.select('English')

# Partial match
browser.select_list.select(/Eng/)
~~~~~~~~

For localized applications, the visible text may change based on the language. For example, a user may see "English" or "Anglais" depending on if they are viewing the page in English or French. In this scenario, it is better to select options based on their `value` attribute, which is language independent.

{lang="ruby"}
~~~~~~~~
browser.select_list.select_value('en')
~~~~~~~~

If you need more control, you can directly locate the option element and call its `select` method.

{lang="ruby"}
~~~~~~~~
# Select option based on multiple attributes
browser.select_list.option(text: 'English', value: 'en').select

# Select first option
browser.select_list.option.select

# Select last option
browser.select_list.options.last.select
~~~~~~~~

### Inspect

To check the currently selected option, you can use the `value` method. For example, let us assume that "English" has been selected.

{lang="ruby"}
~~~~~~~~
browser.select_list.value
#=> "en"
~~~~~~~~

Note that the returned value is the `value` attribute of the selected option. If you want other details of the selected option, for example the user visible text, you can use the `selected_options` method. This will return an `Array` of option elements, where the first and only element is the one of interest. 

{lang="ruby"}
~~~~~~~~
browser.select_list.selected_options.first.text
#=> "English"
~~~~~~~~

### Multi-Select

By default, the `select` element only allows a user to select a single option. An application can allow for multiple selections by adding the `multiple` attribute.

{lang="html"}
~~~~~~~~
<select id="language" multiple>
  <option value="ar">Arabic</option>
  <option value="en">English</option>
  <option value="hi">Hindi</option>
  <option value="zh">Mandarin</option>
  <option value="es">Spanish</option>
</select>
~~~~~~~~

The Watir methods available to multi-select lists are the same as a dropdown list. Selecting multiple options is as simple as calling `select` or `select_value` multiple times.

{lang="ruby"}
~~~~~~~~
browser.select_list.select_value('ar')
browser.select_list.selected_options.map(&:text)
#=> ["Arabic"]

browser.select_list.select('English')
browser.select_list.selected_options.map(&:text)
#=> ["Arabic", "English"]
~~~~~~~~

You will notice that each selection does not clear the previous selections. If you want to unselect the selected options, call the `clear` method.

{lang="ruby"}
~~~~~~~~
browser.select_list.clear
browser.select_list.selected_options.map(&:text)
#=> []
~~~~~~~~

When inspecting the selected options, you should use the `selected_options` approach over the `value` method. The `value` only returns the _first_ selected option, which will be wrong when multiple are selected.

{lang="ruby"}
~~~~~~~~
browser.select_list.select('Arabic')
browser.select_list.select('English')
browser.select_list.selected_options.map(&:value) # good
#=> ["ar", "en"]
browser.select_list.value # bad
#=> "ar"
~~~~~~~~

### Look-alikes

More and more web pages are using controls that look like dropdowns, but are actually a combination of links, text fields, etc. In other words, there is no `select` element in the HTML. These cannot be located and interacted with using the `select_list` method. 

For example, the Dojo Combobox looks like a select list, but creates the following HTML (simplified to fit the book):

{lang="html"}
~~~~~~~~
<div id="widget_stateSelect" role="combobox">
  <div class="dijitArrowButton">
    <input value="? " type="text" tabindex="-1">
  </div>
  <div>
    <input id="stateSelect" value="Alabama">
  </div>
</div>
<div>
  <div>
    <div class="dijitMenuItem">Alabama</div>
    <div class="dijitMenuItem">Alaska</div>
    <div class="dijitMenuItem">American Samoa</div>
  </div>
</div>
~~~~~~~~

In this case, you need to interact with the individual elements that create the control.

{lang="ruby"}
~~~~~~~~
# Expand combo box
combo_box = browser.div(id: 'widget_stateSelect')
combo_box.div(class: 'dijitArrowButton').click
 
# Select an option
dropdown = browser.div(id: 'widget_stateSelect_dropdown')
dropdown.div(class: 'dijitMenuItem', text: 'Alabama').when_present.click
 
# Get the selected option
browser.text_field(id: 'stateSelect').value
#=> "Alabama"
~~~~~~~~

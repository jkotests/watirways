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
select_list.select('English')

# Partial match
select_list.select(/Eng/)
~~~~~~~~

For localized applications, the visible text may change based on the language. For example, a user may see "English" or "Anglais" depending on if they are viewing the page in English or French. In this scenario, it is  better to select options based on their `value` attribute, which is language independent.

{lang="ruby"}
~~~~~~~~
select_list.select_value('en')
~~~~~~~~

If you need more control, you can directly locate the option element and call its `select` method.

{lang="ruby"}
~~~~~~~~
# Select option based on multiple attributes
select_list.option(text: 'English', value: 'en').select

# Select first option
select_list.option.select

# Select last option
select_list.options.last.select
~~~~~~~~

### Inspect

- value (first selected value)
- selected_options
- selected?
- check if has option - `include?`

### Multi-Select

- Can select multiples (using same method)
- Can clear

### Select List Look-Alikes
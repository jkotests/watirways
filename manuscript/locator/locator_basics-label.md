## Label

Elements can also be located by their associated label element's text. Note that this only works in Watir-Webdriver.

In the following html, the input field has an associated label with the text "First Name:".

{lang="html"}
~~~~~~~~
<label for="first_name">First Name:</label>
<input type="text" id="first_name" name="first_name" />
~~~~~~~~

The input field can be located by the exact label text:

{lang="ruby"}
~~~~~~~~
browser.text_field(:label => 'First Name:')
~~~~~~~~

Or by part of the label text:

{lang="ruby"}
~~~~~~~~
browser.text_field(:label => /Name/)
~~~~~~~~
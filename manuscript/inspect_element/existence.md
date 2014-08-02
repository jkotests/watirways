## Existence
 
Watir has three methods to check whether an elements exists on the page:

* exists? – Returns true if the element exists (in the DOM).
* visible? - Returns true if the element is visible to the user.
* present? – Returns true if the element exists and is visible to the user.

These methods are called similar to:

{lang="ruby"}
~~~~~~~~
browser.div.exists?
browser.div.visible?
browser.div.present?
~~~~~~~~

Consider the following page, which has one div tag that is visible (ie displayed to the user) and one that is not.

{lang="html"}
~~~~~~~~
<body>
  <div id="1" style="block:display;">This text is visible</div>
  <div id="2" style="block:none;">This text is not visible</div>
</body>
~~~~~~~~

When each method (exists?, present?, visible?) is run for the different elements (displayed, not displayed, non-existent), the following results are seen:

| Element | .exists? | .visible? | .present? |
|---------|----------|-----------|-----------|
| Displayed (browser.div(:id => '1')) | true | true | true |
| Not Displayed (browser.div(:id => '2')) | true | false | false |
| Non-Existent (browser.div(:id => '3')) | false | exception | false |

Element#exists? checks if the element is in the DOM (or HTML). Element#visible? checks if the element can be seen by the user, but throws an exception if the element is not in the DOM. Element#present? is the same as Element#visible? except that it returns false, instead of an exception, when the element is not in the DOM.
Conclusion

While the three methods are definitely different, I think, at least from my experience, that you should typically be using Element#present?.

One point to keep in mind, especially for those working with legacy watir libraries/tests, is that .exists? can lead to false positives. Imagine you have a form. When the form is submitted, an error message is displayed for fields that fail validation (ex missing a required field). In some applications this will be implemented by simply changing the style of the element containing the error message from display:none to display:block. Now consider writing a test to check that the validation message is displayed. If you use .exists?, the test will have false positives (ie it will always pass since the element is always in the DOM). In this situation, .visible? or present? should have been used.


## Based on its decendants

There are several approaches that can be used to locate an element based on its decendants, which are the elements within the target element.

For example, consider locating the li elements in the following html. The li elements do not have any distinguishing attributes. However, they do have child link elements with unique attributes - the data-componentcode.

{lang="html"}
~~~~~~~~
<ul>
  <li id="ctl00_EnabledComponentListItem">
    <a id="ctl00_Component" data-componentcode="ItemA" href="#">Item A</a>
    <a href="#">X</a>
  </li>
  <li id="ctl01_EnabledComponentListItem">
    <a id="ctl01_Component" data-componentcode="ItemB" href="X">Item B</a>
    <a href="#">X</a>
  </li>
  <li id="ctl02_EnabledComponentListItem">
    <a id="ctl02_Component" data-componentcode="ItemC" href="#">Item C</a>
    <a href="#">X</a>
  </li> 
</ul>
~~~~~~~~

**Using find**

One approach is to iterate through the li elements until one is found with specified link.

{lang="ruby"}
~~~~~~~~
browser.lis(:id, /EnabledComponentListItem/).find do |li|
  li.a(:data_componentcode, 'ItemC').exists?
end
~~~~~~~~

**Navigate from descendant to parent**

If the html structure is stable, you can locate the descendant link (using standard locators) and then traverse the DOM up to the parent (ie li element).

{lang="ruby"}
~~~~~~~~
browser.a(:data_componentcode, 'ItemC').parent
~~~~~~~~

**Using xpath**

Using xpath, it is possible to get the element directly.

{lang="ruby"}
~~~~~~~~
browser.li(:xpath, "//li[.//a[@data-componentcode='ItemC'']]")
~~~~~~~~


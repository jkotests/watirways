## DOM Traversal

Most often elements are located by traversing down the DOM. However, there are also methods for when travelling up or horizontally is required.

### Parent

The DOM can be traversed upwards to an element's parent.

In the html:

{lang="html"}
~~~~~~~~	
<div class="parent">
  <span class="child">Target</span>
</div>
~~~~~~~~
 
The parent element of the span tag can be retrieved by using the _parent_ method:

{lang="ruby"}
~~~~~~~~
child = browser.span(:class => 'child')
parent = child.parent
parent.tag_name
#=> "div"
~~~~~~~~

### Previous/next sibling

The DOM can also be traversed horizontally between sibling elements. For example, the following page has 4 sibling elements in the body - 2 h1 and 2 ul elements.

{lang="html"}
~~~~~~~~	
<html>
  <body>
    <h1>Heading 1</h1>
    <ul>
      <li>Item 1a</li>
    </ul>
    <h1>Heading 2</h1>
    <ul>
      <li>Item 2a</li>
      <li>Item 2b</li> 
    </ul>
  </body>
</html>
~~~~~~~~

**Watir-Webdriver**

Xpath has a following-sibling axis that can be used to find the next sibling of a given Watir element. This example shows that the next sibling of "Heading 2" is the unordered list with 2 items.

{lang="ruby"}
~~~~~~~~
h1 = browser.h1(:text => 'Heading 2')
ul = h1.element(:xpath => './following-sibling::*')
puts ul.lis.length
#=> 2
~~~~~~~~

The preceding-sibling axis can find previous sibling of the Watir element. The [1] is added to get the adjacent sibling. Otherwise, you would get the first sibling in the tree, which is the "Heading 1" h1 element.

{lang="ruby"}
~~~~~~~~
h1 = browser.h1(:text => 'Heading 2')
ul = h1.element(:xpath => './preceding-sibling::*[1]')
puts ul.lis.length
#=> 1
~~~~~~~~

Note that the element type returned must match what you are looking for. In the above examples, we looked for any element type. You can replace the * and use a specific watir element to look for a specific type. For example, to get the preceding h1:

{lang="ruby"}
~~~~~~~~
start_h1 = browser.h1(:text => 'Heading 2')
end_h1 = start_h1.h1(:xpath => './preceding-sibling::h1[1]')
puts end_h1.text
#=> "Heading 1"
~~~~~~~~

**Watir-Classic**

For some reason, the same xpath solution produces a UnknownObjectException in Watir-Classic. As an alternative, you can use the nextSibling property of the OLE object.

{lang="ruby"}
~~~~~~~~
h1 = browser.h1(:text => 'Heading 2')
ul = browser.ul(:ole_object => h1.document.nextSibling)
puts ul.lis.length
#=> 2
~~~~~~~~

Similarly, you can use the previousSibling property to get the preceding element.

{lang="ruby"}
~~~~~~~~
h1 = browser.h1(:text => 'Heading 2')
ul = browser.ul(:ole_object => h1.document.previousSibling)
puts ul.lis.length
#=> 1
~~~~~~~~
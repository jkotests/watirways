## Counting

Given an element collection, you can check how many elements were found by using the _size_ method.

{lang="html"}
~~~~~~~~
<html>
  <body>
    <div class="title">Title</div>
    <div class="content">Content A</div>
    <div class="content">Content B</div>
  </body>
</html>
~~~~~~~~

There are 3 div elements on the page.

{lang="ruby"}
~~~~~~~~
browser.divs.size
#=> 3
~~~~~~~~

With 2 of the div elements having the class "content".

{lang="ruby"}
~~~~~~~~
browser.divs(:class => 'content').size
#=> 2
~~~~~~~~

Depending on your preferences, you can also use the method _length_ instead of _size_.

{lang="ruby"}
~~~~~~~~
browser.divs.length
#=> 3
~~~~~~~~
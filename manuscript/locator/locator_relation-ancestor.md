## Based on its ancestors

Any element that contains the target element is considered an "ancestor". Ancestor elements can be used to reduce the scope of where Watir searches for an element. The element type method will only look for the element within the html of the calling object. 

  * When the calling object is the browser, the entire page will be searched.
  * When the calling object is an element, only the html of that element will be searched.

As an example, say a page lists a project's team members by their role.

{lang="html"}
~~~~~~~~
<span>Project Managers:</span>
<ul id="project_managers">
  <li>Alicia Mcbride</li>
  <li>Jake Woods</li>
</ul>
<span>Developers:</span>
<ul id="developers">
  <li>Jack Greer</li>
  <li>Cora Williamson</li>
  <li>Albert Gross</li>
</ul>
<span>Testers:</span>
<ul id="testers">
  <li>Owen Francis</li>
  <li>Luis Leonard</li>
</ul>
~~~~~~~~

Consider a test that needs to retrieve the name of one of the testers. It is not possible to locate the tester li elements directly as there are no properties to differentiate them from the other roles. However, the ul element does have an identifying attribute - the id specifies the role being listed. In other words, the test needs to get the first li element within the ul element with id of "testers". This is done by chaining element type methods that identify the unique ancestors.

{lang="ruby"}
~~~~~~~~
browser.ul(:id => 'testers').li.text
#=> "Owen Francis"
~~~~~~~~

In this code, Watir will look for an ul element with id "tester" anywhere within the browser. Then, only within the ul element found, Watir will look for the first li element.

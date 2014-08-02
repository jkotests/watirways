## Index

When locating a single element, Watir will, by default, return the first element matching the criteria. 

For example, given the html:

{lang="html"}
~~~~~~~~
<div>
  <a href="http://www.watir.com">Watir</a>
  <a href="http://watirwebdriver.com">Watir-Webdriver</a>
</div>
~~~~~~~~

The first matching element is returned when no :index is specified or when the :index value is 0.

{lang="ruby"}
~~~~~~~~
browser.link.text
#=> "Watir"
~~~~~~~~

{lang="ruby"}
~~~~~~~~
browser.link(:index => 0).text
#=> "Watir"
~~~~~~~~

The second matching element is found using an :index with value 1. Notice that Watir is using a 0-based index - ie 0 is the first element, 1 is the second element, etc.

{lang="ruby"}
~~~~~~~~
browser.link(:index => 1).text
#=> "Watir-Webdriver"
~~~~~~~~

A couple of items note:

* The value can be an integer or a string.
* The :index locator only applies to locating a single element. An exception will occur when using it to locate an element collection.

  {lang="ruby"}
  ~~~~~~~~
  browser.divs(:text => /Watir/, :index => 1).length
  #=> Watir::Exception::MissinWayOfFindingObjectException
  ~~~~~~~~
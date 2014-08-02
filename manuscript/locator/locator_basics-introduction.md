# Locating an Element - Basics

A locator describes how to find an element amongst all of the other elements on the page. Think of it as giving directions to your house. The uniqueness of the house, who you are talking to, the complexity of your area, etc. affect how detailed the directions need to be.

Say our city has 2 streets and 4 houses with families. 

![](images/locatorstrategies-houses.png)

It is unambiguous to say that you want to go the "Wilson Family" house. There is exactly one house that matches that criteria.

What if you say you want to go to the "Smith Family" house? Now it is ambiguous as there are 2 houses that meet that criteria. We can remove the ambiguity by doing one of the following: 

  1. Providing additional details about the house. For example, the house number is 1.
  2. Providing details about where to look for the house. For example, the house is on Main Street.
  3. Providing details about what is in the house. For example, the house where Ronald and Alice live.
  4. Providing details about what is around the house. For example, the house is beside the Wilson's house.

The same strategies can be used to help Watir find the exact element you want to interact with.

For example, the city's information could be presented as a web page.

{lang="html"}
~~~~~~~~
<div class="city" id="Kitchener">
  <div class="street" id="MainStreet"> 
    <div class="house" data-name="SmithFamily" data-number="1"> 
      <span class="resident">Ronald</span>
      <span class="resident">Alice</span> 
    </div>
    <div class="house" data-name="WilsonFamily" data-number="2">
      <span class="resident">Henry</span>
      <span class="resident">Mary</span>
    </div>
  </div>
  <div class="street" id="CedarStreet">
    <div class="house" data-name="ChanFamily" data-number="1">
      <span class="resident">Blake</span>
      <span class="resident">Terra</span>
    </div> 
    <div class="house" data-name="SmithFamily" data-number="2"> 
      <span class="resident">George</span> 
      <span class="resident">Coraline</span>
    </div> 
  </div>
</div> 
~~~~~~~~

Again, assume that we want to find the "Smith Family" house. To tell Watir to find the div element with the data-name attribute value of "SmithFamily" is ambiguous (ie there are multiple). We can use the same four approaches to remove the ambiguity. 

  1. Providing additional details about the house. For example, the desired div element has a data-number attribute value of 1.
  2. Providing details about where to look for the house. For example, the desired div element is within the div element that has the id of MainStreet.
  3. Providing details about what is in the house. For example, the desired div element that includes the spans with text Ronald and Alice.
  4. Providing details about what is around the house. For example, the desired div element is beside the div element with data-name attribute of "WilsonFamily".

These four strategies can be conceptually generalized based on the relationship of the element we want to find and the structure of elements. The strategies are to use the properties of: 

  1. The Element - This is the specific element that you want to find.
  2. Ancestors - These are the elements that contain the desired element.
  3. Decedents - These are the elements contained within the desired element.
  4. Siblings - These are elements that share the same parent as the desired element.

The following image illustrates the relationship of the elements. 

![](images/city-elementrelationship.png)

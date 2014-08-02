## Based on its siblings

Locating an element by its siblings is often seen when working with tables. For example, in the below table, you might need to find the colour of a specific creature. A user knows which colour belongs to the creature because they are in the same row. In terms of the html, the colour td element is a sibling of the creature td element since they share the same parent element (tr element).

Table: 

| Creature | Colour |
|----------|-------|
| Elf | Blue |
| Dragon | Green |
| Imp | Black |

HTML:

{lang="html"}
~~~~~~~~
<table>
  <tbody>
    <tr>
      <th>Creature</th>
      <th>Colour</th>
    </tr>
    <tr>
      <td>Elf</td>
      <td>Blue</td>
    </tr>
    <tr>
      <td>Dragon</td>
      <td>Green</td>
    </tr>
    <tr>
      <td>Imp</td>
      <td>Black</td>
    </tr>
  </tbody>
</table>
~~~~~~~~

**Sibling to parent to element**

To find an element based on its sibling, the general strategy is: 

  1. Locate the unique sibling element.
  2. Get the parent element using the _parent_ method.
  3. Locate the required element within the scope of the parent.

Applying this strategy to the table, the colour of the dragon can be obtained by:

{lang="ruby"}
~~~~~~~~
#Get the unique element
unique_element = browser.table.td(:text => 'Dragon')

#Get the parent element
parent_element = unique_element.parent

#Get the actual element
parent_element.td(:index => 1).text
#=> "Green"
~~~~~~~~

**Parent by descendent to element**

When the unique element is a cousin (ie a descendent of the sibling element), it is easier to locate the parent based on its descendents. The reason being that it is less fragile - ie ensuring that the correct number of "parent" methods are called becomes more difficult.

{lang="ruby"}
~~~~~~~~
parent_row = browser.table.trs.find do |tr|
  tr.td(:text => 'Dragon').present?
end
parent_row.td(:index => 1).text
#=> "Green"
~~~~~~~~

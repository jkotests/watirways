## UnknownObjectException - Unable to Locate Element

Have you tried to interact with an element, only to get an exception like:

{lang="ruby"}
~~~~~~~~
Watir::Exception::UnknownObjectException: 
  Unable to locate element, using {:tag_name=>["div"]}
  from ../lib/watir-classic/element.rb:66:in `assert_exists'
  from ../lib/watir-classic/element.rb:125:in `text'
  from (irb):5
  from C:/Ruby193/bin/irb:12:in `<main>'
~~~~~~~~

Watir is saying that it cannot find the element. Yet when you manually go and look at the page, you can see the element! Why can't Watir locate it? 

There are a variety of possible reasons, which have been summarized in the table below.

| Problem                  | Solution                                |
|--------------------------|-----------------------------------------|
| Element is in a frame    | You must explicitly tell Watir that the |
|                          | element is within a frame.              |
|                          | `browser.frame.div.text`                |
|--------------------------|-----------------------------------------|
| Element has not finished | Add an explicit wait.                   |
| loading                  |                                         |
|                          | `browser.div.when_present.text`         |
|--------------------------|-----------------------------------------|
| Element locator uses     | Use a regex to only match the stable    |
| dynamic attribute values | part of the attribute.                  |
|                          |                                         |
|                          | The following locator includes random   |
|                          | values (bad):                           |
|                          | `browser.div(:id, 'static_rand5').text` |
|                          |                                         |
|                          | Change the locator to a regex and just  |
|                          | match the static part:                  |
|                          | `browser.div(:id, /static/).text`       |
|--------------------------|-----------------------------------------|
| Element is in a popup    | You must explicitly tell Watir to use   |
| window                   | the popup window.                       |
|                          | `b.window(:title => /window title/) do` |
|                          | `  b.div(:id => 'div_in_popup').text`   |
|                          | `end`                                   |
|--------------------------|-----------------------------------------|
| Element type is incorrect| Verify that you are trying to find the  |
|                          | right element type.                     |
|                          |                                         |
|                          | For example, what looks like a button   |
|                          | might actually be a link.               |
|                          |                                         |
|                          | Results in an UnknownObjectException:   |
|                          | `browser.button.click`                  |
|                          |                                         |
|                          | This will work:                         |
|                          | `browser.link.click`                    |
|--------------------------|-----------------------------------------|
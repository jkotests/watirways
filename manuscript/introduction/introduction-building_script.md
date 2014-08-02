## Building a script

Say we want to explain to someone how to do a Google search for Watir. We might tell them to:

1. Open a browser
2. Enter the url to go the Google search page
3. Input 'watir' into the search field
4. Click the search button
5. Wait for the search results to load
6. Click the link for the main Watir page

If you look carefully, you will notice that each step consists of two parts:

1. Target - Something to interact with (eg browser, element)
2. Action - Something to do with the target (eg click, type, inspect)

We can make these two parts more clear in a table:

| Step | Target | Action |
|------|--------|--------|
| 1 | browser | open |
| 2 | browser | goto url |
| 3 | search field | type 'watir' |
| 4 | search button | click |
| 5 | result link | wait for it to load |
| 6 | result link | click |

Watir is designed to mimic a user's actions, which means that these same directions can be used when creating an automated script. The only complication is the language barrier. Watir understands Ruby, not English. In essence, building a Watir script is translation exercise.

A translation of the previous table into Watir code would be:

| Step | Target | Action |
|------|--------|--------|
| 1 | browser | Watir::Browser.new |
| 2 | browser | goto('http://www.google.com') |
| 3 | text_field(:name => 'q') | set('watir') |
| 4 | button(:name => 'btnG')  | click |
| 5 | link(:text => /Watir\.com/) | wait_until_present |
| 6 | link(:text => /Watir\.com/) | click |

To make an executable script, the target and action need to be combined back into sentences (or lines of code):

{lang="ruby"}
~~~~~~~~
browser = Watir::Browser.new
browser.goto('http://www.google.com')
browser.text_field(:name => 'q').set('watir')
browser.button(:name => 'btnG').click
browser.link(:text => /Watir\.com/).wait_until_present
browser.link(:text => /Watir\.com/).click
~~~~~~~~

The following chapters will discuss how to translate the targets and actions.
# waiting

## General waiting

browser.wait_until
browser.wait_while
2wszx
## Waiting for an element

element.wait_until_present
element.wait_while_present
element.when_present.action

## Changing default wait time

### Individual basis

element.wait_until_present(5)

### For all waits

Watir.default_timeout = 60 # seconds

## Waiting with refresh

Watir’s wait methods assume that the element/block will become present/true due to the page being asynchronously loaded. Unfortunately, some applications, particularly older ones, will not be making use of 
these asynchronous loads. Instead, you have to refresh the browser for the page’s information to be updated.

This situation can be handled by using Browser#wait_until or Browser#wait_while with a block that refreshes the browser.

{lang="ruby"}
~~~~~~~~
browser.wait_until do
  if browser.div.present?
    true
  else
    browser.refresh
    false
end
~~~~~~~~

Alternatively, the “watir-wait_with_refresh” gem can be used. This gem adds wait methods that refresh the page until the element is present or block is true.

To install the gem:

{lang="ruby"}
~~~~~~~~
gem install 'watir-wait_with_refresh'
~~~~~~~~

The methods are made available by requiring the gem:

{lang="ruby"}
~~~~~~~~
require 'watir'
require 'watir/wait_with_refresh'
~~~~~~~~

To refresh the page until an element is present:

{lang="ruby"}
~~~~~~~~	
element.refresh_until_present
~~~~~~~~

To refresh the page while an element is present:
	
{lang="ruby"}
~~~~~~~~		
element.refresh_while_present
~~~~~~~~

To do something after refreshing the page makes the element present:

{lang="ruby"}
~~~~~~~~		
element.when_present_after_refresh.text
~~~~~~~~

To refresh the page until a block evaluates as true:

{lang="ruby"}
~~~~~~~~	
browser.refresh_until{ browser.div.present? }
~~~~~~~~

To refresh the page while a block evaluates as true:
	
{lang="ruby"}
~~~~~~~~		
browser.refresh_while{ browser.div.present? }
~~~~~~~~

A timeout, in seconds, can also be specified for each of the methods:

{lang="ruby"}
~~~~~~~~	
element.refresh_until_present(5)
~~~~~~~~

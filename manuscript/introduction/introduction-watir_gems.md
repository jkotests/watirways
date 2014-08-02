## Watir gems

Watir consists of three gems (or projects):

* Watir - This gem is just a loader. Based on the browser that you want to run and your operating system, the Watir gem will load either Watir-Classic or Watir-Webdriver.
* Watir-Classic - This is the original Watir gem that drives Internet Explorer.
* Watir-Webdriver - This gem allows the driving of additional browsers - eg Chrome and Firefox. It is an API wrapper around the Selenium-Webdriver gem (ie translates the Watir 
commands to Selenium-Webdriver commands).

![](images/watirgems.png)

For most users, the structure of the framework will have no significance or impact.  Scripts only need to require Watir; making the use of Watir-Classic versus Watir-Webdriver transparent.

However, there are occasions where understanding the gem relationship is crucial:

* API differences - The Watir-Classic and Watir-Webdriver projects strive to be API compatible though a common specification called Watirspec. Unfortunately, due to historical reasons, implementation details, etc., there are still some API differences. The code found in this book can be assumed to work in both projects unless otherwise specified.
* Monkey patching - When adding functionality to Watir, the code may need to consider which browser/gem is being used.
* Getting help - Specifying the gem being used helps ensure that solutions are applicable.
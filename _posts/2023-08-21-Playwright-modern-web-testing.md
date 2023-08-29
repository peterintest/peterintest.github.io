---
layout: post
title: Playwright for end-to-end testing web applications
date: 2023-08-29 17:00:00 +0000
categories: [tools, end-to-end, testing, web]
tags: [playwright, automation, python]
image:
  path: /images/playwright.jpg
  alt: Theatre stage with the Playwright logo at the center
---

Working in an agile development team with regular customer and end-user feedback loops is the norm in modern web applications; so automating new end-to-end user journeys is expected.

I previously blogged on different types of testing including [The Testing Pyramid]({% post_url 2023-01-08-Testing-Pyramid %}). Although end-to-end testing is at the top of the pyramid; meaning there should only be a few of these tests; it's still important to test [Critical User Journeys (CUJs)](https://info.userzoom.com/How-UX-drives-business-metrics-at-Google.html).

Over the last few months I have been using Playwright for testing web applications; and will discuss the key features that make it worth considering. 

I started with a small proof of concept back in December 2022 which quickly gained momentum and became more widely adopted.

*Time to set the scene and introduce Playwright!*

## What is Playwright?

- Open source framework by Microsoft for end-to-end testing web applications first released in January 2020
- Cross-language library bindings for web automation (Python, TypeScript, JavaScript, Java and .NET)
- Supports Chromium, Chrome, Edge, Firefox, and WebKit browsers
- Extensive set of APIs for various browser interactions, including navigation, element interaction, screenshots and more
- Emphasis on performance and relability with features like automatic waiting, network interception, and parallel execution

## Why use Playwright? 

There are a number of tools and frameworks already available e.g. Cypress, Selenium, WebdriverIO so why Playwright?

### Cross-language
Library bindings for Playwright span across multiple programming languages including Python, TypeScript, JavaScript, Java, and .NET.

### Cross-browser
Playwright supports all modern rendering engines including Chromium, WebKit, and Firefox.

### Accessibility testing
Playwright can be used to test your application for accessibility issues using [Axe](https://playwright.dev/docs/accessibility-testing).
However, as I mentioned in a [previous post]({% post_url 2023-06-22-BCS-SIGiST-Summer-Conference-2023 %}); using a single accessibility evaluation tool is not recommended; and accessibility evaluation requires a combination of automated and human evaluation and judgement.

### Fast test execution
#### Chrome DevTools Protocol
WebDriver is a popular web standard supported by all major browsers; however it uses HTTP communication to interact with a browser driver; which can be slow.

According to Yeen & Sadym (2023) Playwright and it's predecessor, Puppeteer started using the Chrome Devtools Protocol (CDP); which was originally developed for Chrome DevTools and debugging on Chromium-based browsers. 

The Playwright team have patched Firefox and WebKit browsers to use a similar protocol to CDP let's call it CDP+. CDP uses web socket communication to communicate directly with the browser providing faster performance and low-level control (Yeen & Sadym, 2023).

#### Browser contexts
For every test, Playwright generates a browser context, akin to a fresh browser profile - instead of launching a new browser instance. This approach ensures complete test isolation without any additional load. Establishing a new browser context is a quick process, typically taking just a few milliseconds.

#### Persist authentication state
Playwrite provides an API to presist the authentication state and apply it to browser contexts across tests. This avoids redundant login procedures in each test while maintaining complete separation between individual test cases.

#### Parallel test execution
The node.js version of Playwright comes with a test runner that executes tests concurrently by employing multiple worker processes that operate simultaneously; although the same can be configured using other test runners like [pytest](https://pytest.org/) and the [pytest-xdist](https://pypi.org/project/pytest-xdist/) plugin. By default, test files are processed in parallel, while tests within a single file maintain sequential execution within the same worker process.

### Auto-waiting
Having robust tests is important; Playwright ensures that elements are ready to be interacted with before executing actions, and it provides an extensive range of introspection events. This powerful combination eliminates the necessity for using arbitrary timeouts, which are a major contributor to unreliable tests.

### Web-first assertions
Playwright's assertions are tailored for the web, enabling automatic retries until the required conditions are fulfilled.

### Tracing
Playwright allows to capture execution traces, videos, and screenshots to eliminate flaky tests. The tracing feature can capture screenshots, record network activity and snapshots of the Document Object Model (DOM); these artefacts not only help debug failures but could also be used as evidence of test execution for auditing purposes. Playwright provide a [Trace Viewer](https://playwright.dev/docs/trace-viewer-intro) GUI tool to view the generated traces.

### Regular release cadence
Microsoft have been making regular releases approximately every 2-4 weeks; so bug fixes and new features are added regularly.

### Community
Playwright has recently gained in popularity and has a community of users. The community has a Discord server and hosts frequent conference talks, feature and release videos. More information can be found [here](https://playwright.dev/community/welcome).

## Architecture
Here is a high-level diagram illustrating the client-server architecture of Playwright when using [playwright-python](https://github.com/microsoft/playwright-python), [pytest](https://pytest.org/) and the [playwright-pytest](https://github.com/microsoft/playwright-pytest) plugin.

![A diagram I created of the Playwright architecture using pytest and the python binding]({{ site.baseurl }}/images/playwright_python_arch.png)

### playwright-python
[playwright-python](https://github.com/microsoft/playwright-python) is the python Playwright library.

### Playwright Server
The Playwright Server is a Node.js process that recieves commands from different language bindings through interprocess communication (ICP) using pipes; in this case the Python library is depicted. The server uses the Chrome DevTools Protocol (CDP) or modified protocol (CDP+); as previously discussed, to communicate with browsers.

### playwright-pytest
[playwright-pytest](https://github.com/microsoft/playwright-pytest) is the official Playwright pytest plugin and recommends using it if you choose the python library.
The pytest plugin makes use of synchronous version of Playwright, while an asynchronous version is also available through the library. Further details on the plugin can be found [here](https://playwright.dev/python/docs/test-runners). The plugin provides some Playwright specific fixtures for pytest to assist with test case setup.

### Page Object Model
Page Object Models is a well known design pattern used to encapsulate and abstract the interactions and elements of a web page, promoting maintainability and reusability in automated tests. Here is a simple example using Bing search with Playwright locators.
```python
class SearchPage:
    def __init__(self, page):
        self.page = page
        self.search_term_input = page.locator('[aria-label="Enter your search term"]')

    def navigate(self):
        self.page.goto("https://bing.com")

    def search(self, text):
        self.search_term_input.fill(text)
        self.search_term_input.press("Enter")
```

### Test file
Within Playwright, the expect function is available, ensuring that the code will pause execution until the desired condition is fulfilled.

Here is an example of an assertion in Playwright:
```python
import re
from playwright.sync_api import expect

expect(page).to_have_title(re.compile("Playwright"))
```

and a example of a simple test:

```python
from playwright.sync_api import expect
from models.search import SearchPage


def test_search_page_title(page):
    search_page = SearchPage(page)
    search_page.navigate()
    search_page.search("software testing")
    expect(page).to_have_title(("software testing - Search"))
```

## Recommendations
- Give it a go Playwright is awesome and have fun!
- The Node.js version of Playwright is better suited for a *Batteries Included* experience
- The python/pytest configuration doesn't have complete parity with the Node.js framework this is worth knowing!
- Start a small proof of concept with a few tests first
- Engage with the wider Playwright community!

## References

Yeen, J. and Sadym, M. (2023) A look back in time: The evolution of test automation, Chrome Developers. Available at: https://developer.chrome.com/blog/test-automation-evolution/#webdriver-classic-versus-chrome-devtools-protocol-cdp (Accessed: 29 August 2023). 

Microsoft (2023) Fast and reliable end-to-end testing for modern web apps, Playwright. Available at: https://playwright.dev (Accessed: 28 August 2023).




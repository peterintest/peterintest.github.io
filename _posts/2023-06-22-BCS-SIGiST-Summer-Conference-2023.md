---
layout: post
title: Accessibility evaluation tools you should know about!
date: 2023-06-22 07:44:00 +0000
categories: [accessibility, tools, evaluation]
tags: [accessibility, playwright, cypress]
image:
  path: /images/bcs-sigist-summer-2023.jpg
  alt: Presenting at the BCS SIGiST (Special Interest Group in Software Testing) Summer Conference
---

Last week I attended the BCS SIGiST (Special Interest Group in Software Testing) [Summer Conference](https://www.bcs.org/membership-and-registrations/member-communities/software-testing-specialist-group/conferences/bcs-sigist-summer-conference-2023/) at the British Computer Society in London. It was great to see a community of people focused on solving problems in software quality and testing.

I presented a short talk on accessibility evaluation tools highlighting tools that are widely adopted from my research in this area. My notes from the talk are presented here.

## Importance of web accessibility

- 1.3 billion disabled (16% of the global population)
- There are 16 million disabled people in the UK (Scope, 2022)
- 11% of children in the UK are disabled (Scope, 2022)
- 80% of disabilities are invisible (have hidden impairments)

According to the World Health Organisation (2020) this figure is continuing to grow due to advances in medicine, population growth and the aging process.

## Web Content Accessibility Guidelines (WCAG)

WCAG 2.1 is based on four design principles (POUR): 
### Perceivable 
Information and user interface components must be presentable to users in ways they can perceive.
### Operable
User interface components and navigation must be operable.
### Understandable
Information and the operation of user interface must be understandable.
### Robust
Content must be robust enough that it can be interpreted reliably by a wide variety of user agents, including assistive technologies.

- The WCAG 2.1 design principles are supported by 13 guidelines
For each WCAG guideline there are testable Success Criteria (SC) with conformance levels A, AA, AAA (there are 78 SC in total)
- WCAG 2.1 level AA integrated in UK legislation for public sector websites
At the end of October 2022 the public sector body accessibility regulations were amended to make sure they can continue to operate now that the UK has left the European Union.
-  WCAG 2.2 is due to be published in 2023 Q3 (July, August, September)

## Different types of accessibility evaluation

There are three methodologies for evaluating web accessibility (Abascal, et al., 2019): 
- Automated Testing 
- Manual Inspection 
- User Testing

### Automated testing

Automated testing makes use of software tools running locally or online to parse the source code to identify accessibility violations against a set of rules that test against accessibility guidelines such as WCAG 2.1. 
There are several automated accessibility evaluation tools available and the W3C maintain a comprehensive list of tools (167 at the time of writing).

### Manual inspections

Manual inspections are carried out by expert human evaluators who usually check a webpage against a checklist of evaluation criteria based on accessibility guidelines (Brajnik, 2004).
According to Abascal et al. (2019) manual inspections are convenient to use during the design process as they can help with identifying design issues.

### User Testing

Abascal, et al. (2019) state that user testing is both slow and expensive and in principle is the most reliable accessibility evaluation approach as it usually involves testing participants with disabilities, who are asked to perform a set of tasks while being observed by evaluators.

## Accessibility evaluation tools

### WebAIM's WAVE (Web Accessibility Evaluation Tool)

- Widely adopted!
- Was originally developed in 2001 by WebAIM (Web Accessibility In Mind) at Utah State University.
- WAVE is freely available as an online tool, browser extension as well as commercially through a HTTP API.
- It provides clear visual indicators and explanations of the identified issues, making it easier to understand and address accessibility problems.

![Wave]({{ site.baseurl }}/images/wave.png)

### AChecker

- AChecker is an online accessibility evaluation tool.
- Was originally developed in 2008 by the Inclusive Design Research Centre (IDRC) at the OCAD University in Toronto, Canada.
- Freely accessible to evaluate web pages against various accessibility standards without any cost.
- Analyses web pages against various accessibility standards, including WCAG, Section 508, BITV and Stanca Act.

![AChecker]({{ site.baseurl }}/images/achecker.png)

### SortSite

- SortSite is a web accessibility testing tool developed by PowerMapper Software, in Edinburgh.
- It covers a wide range of accessibility standards, including WCAG 2.1 and Section 508.
- They offer different pricing plans for SortSite, including options for individual users, small teams, education and enterprise solutions. 
- SortSite supports scanning entire websites. It can crawl and scan multiple pages within a website to identify accessibility issues across the site.

![SortSite]({{ site.baseurl }}/images/sortsite.png)

### Axe

- Axe is an open-source accessibility testing tool developed by Deque Systems.
- Axe uses a combination of rules, checks, and algorithms to analyze the HTML structure, CSS styles, and JavaScript interactions of web content.
- Axe supports multiple platforms and environments, including web browsers, command line, and integration with development tools.
- It follows WCAG and other accessibility standards, such as Section 508 and ARIA.

![Axe]({{ site.baseurl }}/images/axe.png)

UI testing frameworks like Playwright, Cypress and WebdriverIO; support writing automated tests using Axe.

```typescript
test('should not have any automatically detectable WCAG A or AA violations', async ({ page }) => {
  await page.goto('https://your-site.com/');

  const accessibilityScanResults = await new AxeBuilder({ page })
    .withTags(['wcag2a', 'wcag2aa', 'wcag21a', 'wcag21aa'])
    .analyze();

  expect(accessibilityScanResults.violations).toEqual([]);
});
```

### TAW

- The TAW (Test de Accesibilidad Web) accessibility tool is an open-source software first released in 2000 and developed by the University of Murcia in Spain.
- TAW is a web application for analysing website accessibility.
- It is designed to evaluate the accessibility of web pages based on the Web WCAG 2.1.
- TAW Standalone (desktop version) available but only supports WCAG 1.0
- TAW provides detailed reports with explanations of accessibility issues found and recommendations for resolving them.

![TAW]({{ site.baseurl }}/images/taw.png)

### Colour Contrast Analyser (CCA)

- The Colour Contrast Analyser (CCA) is a free software tool developed by TPGi (The Paciello Group)
CCA helps ensure that text is legible and accessible to users with visual impairments or low vision.
- It is designed to assess the color contrast between foreground text and background colors on web pages and User Interface Components.
- The tool measures color contrast ratios based on the WCAG 2.1 standards; namely Success Criterion 1.4.3 Contrast (Minimum), 1.4.6 Contrast (Enhanced) and 1.4.11 Non-text Contrast 
- Includes a colour blindness simulator for Monochromacy, Dichromacy and Trichromacy.
- Support for Windows and Mac

![Colour Contrast Analyser]({{ site.baseurl }}/images/colour_contrast_analyser.png)

### Google Lighthouse

- Lighthouse is an open-source tool developed by Google that helps developers improve the quality and performance of web pages.
- It is built on Node.js and is available as a command-line tool, as well as a Chrome DevTools extension.
- It focuses on several key areas, including performance, accessibility, best practices, SEO (Search Engine Optimization), and Progressive Web App (PWA) compliance.
- It checks for accessibility issues such as color contrast, proper heading structure, alt text for images, keyboard navigation, and ARIA (Accessible Rich Internet Applications) attributes.

![Google Lighthouse]({{ site.baseurl }}/images/lighthouse.png)

## What tool should we use? 

Vigo et al. (2013) proposed the following metrics for benchmarking tools:
### Coverage
Counts the number of SC that report real failures
### Completeness
Measures the ratio between the violations caught by the tool and the actual number of violations
### Correctness
Measures how well a tool is able to minimize the number of mistakenly report accessibility violations

### Limitations of automated accessibility evaluation

- **Automated evaluation tools do not replace human evaluation!**
- A seminal study by Vigo et al. (2013) analysed the coverage of six automated evaluation tools based on WCAG 2.0 guidelines and found that, at most, 50% of the success criteria were covered.
- Recent research by Abu Doush et al. (2023) shows that 44% of all WCAG SC can be automatically checked offering conformance details directly from web content.

### Using multiple evaluation tools to improve results

- Vigo et al. (2013) recommends the use of multiple evaluation tools by identifying the weaknesses and strengths of the tools; and combining them to maximise the coverage, completeness and correctness.
- Frazão and Duarte (2020) reported an increase of 10% - 40% more coverage in WCAG 2.1 SC compared to using a single tool.
- However, the aggregating and summarising of the results from multiple tools can be challenging (Abascal, et al., 2019) or time consuming.

### Pilot study

A recent pilot study by Johnson and Lilley (2022) demonstrated how an ensemble of four accessibility evaluation tools (WAVE, Sort-Site, AccessMonitor and Axe) can be combined to produce automatic aggregated results for practitioners to review.

Results from the pilot study below highlight the differences of reported  unmet WCAG 2.1 Success Criteria reported per accessiblity evaluation tool.

| Success criteria                 | Tool A | Tool B | Tool C | Tool D | Total |
| -------------------------------- | :----: | :----: | :----: | :----: | :---: |
| 1.1.1 – Non-text Content         | 0      | 0      | 6      | 0      | 6     | 
| 1.3.1 – Info and Relationships   | 0      | 0      | 2      | 1      | 3     |
| 1.4.11 – Non-text Contrast       | 0      | 5      | 0      | 0      | 5     |
| 1.4.3 – Contrast (Minimum)       | 1      | 0      | 25     | 1      | 27    |
| 1.4.4 – Resize text              | 15     | 0      | 0      | 0      | 15    |
| 2.4.4 – Link Purpose (In Context)| 3      | 2      | 4      | 3      | 12    |
| 2.4.6 – Heading and Labels       | 0      | 0      | 2      | 0      | 2     |
| 2.4.7 – Focus Visible            | 0      | 5      | 0      | 0      | 5     |
| 3.3.2 – Labels and Intructions   | 0      | 0      | 2      | 0      | 2     |
| 4.1.1 – Parsing                  | 14     | 0      | 0      | 1      | 15    |
| 4.1.2 – Name, Role, Value        | 3      | 3      | 0      | 7      | 13    |
| Total                            | 36     | 15     | 41     | 13     | 105   |

## Summary

- Using a single accessibility evaluation tool is not recommended.
- Tools can vary in reported violations of the same success criteria or analyse different success criteria.
- Results from multiple tools can then be compared and aggregated to improve results.
- Accessibility evaluation requires a combination of automated and human evaluation and judgement.

## References

Abascal, J., Arrue, M. and Xabier, X. (2021) Tools for Web Accessibility Evaluation. In: S. Harper and Y. Yesilada, ed., Web Accessibility A Foundation for Research, 2nd ed. London: Springer, pp.479-499.

Abu Doush, I. et al. (2023) ‘Web accessibility automatic evaluation tools: To what extent can they be automated?’, CCF Transactions on Pervasive Computing and Interaction [Preprint]. doi:10.1007/s42486-023-00127-8.

Brajnik, G., (2004) Comparing accessibility evaluation tools: a method for tool effectiveness. Universal Access in the Information Society, 3(3-4), pp.252-263.

Frazão, T. and Duarte, C., 2020. Comparing accessibility evaluation plug-ins. Proceedings of the 17th International Web for All Conference,.

Johnson, P. and Lilley, M. (2022) “Software prototype for the ensemble of Automated Accessibility Evaluation Tools,” Communications in Computer and Information Science, pp. 532–539. Available at: https://doi.org/10.1007/978-3-031-06417-3_71.

Scope (2022) Disability charity Scope UK. Available at: https://www.scope.org.uk/.

Vigo, M., Brown, J. and Conway, V., (2013) Benchmarking web accessibility evaluation tools. Proceedings of the 10th International Cross-Disciplinary Conference on Web Accessibility - W4A '13,.

WHO. (2020) Disability and health. [online] Available at: <https://www.who.int/en/news-room/fact-sheets/detail/disability-and-health> [Accessed 11 June 2023].

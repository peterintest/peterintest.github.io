---
layout: post
title: PyCon UK - Prototype for accessibility research
date: 2023-02-05 11:33:00 +0800
categories: [accessibility, research]
tags: [accessibility, python]
image:
  path: /images/talk.jpg
  alt: Presenting talk at lectern in Cardiff City Hall
---

Last year I presented a talk on how I used Python to create a prototype for web accessibility research.

## Why web accessibility?

According to the World Health Organisation, there are over one billion people living with some form of disability, which accounts for 15 per cent of the global population. The web was designed to be accessible to all people regardless of their individual differences, use of hardware, software, language and location. In order to enable digital equity and to ensure that websites are accessible to the whole population; web developers should design and implement applications that conform to the Web Content Accessibility Guidelines (WCAG); which is known for making web applications accessible to people with impairments.

## Accessibility evaluation

Web accessibility evaluation is important to ensure that violations of WCAG success criteria (SC) are understood and rectified by web developers. There are three main methodologies for conducting web accessibility evaluations: manual inspection, user testing and automated testing (Abascal et al, 2019). The use of multiple automatic evaluation tools is recommended (Frazão and Duarte, 2020; Vigo et al., 2013); due to the increase of 10% - 40% more coverage in WCAG 2.1 SC compared to using a single tool (Frazão and Duarte, 2020). However, aggregating and summarising of the results from multiple tools can be challenging (Abascal, et al., 2019); which could be the reason why fewer evaluation tools are used by practitioners to carry out accessibility evaluations.

## PyCon UK

I presented a talk at PyCon UK, in September 2022 where I demonstrated how an ensemble of four accessibility evaluation tools (WAVE, Sort-Site, AccessMonitor and Axe) can be combined to produce automatic aggregated results for practitioners to review.

A recording of the talk is available below.

{% include embed/youtube.html id='9l7H9s1VRrg' %}

The poster paper published at HCI International 2022 is available [here](https://link.springer.com/chapter/10.1007/978-3-031-06417-3_71).

## References

Abascal, J., Arrue, M. and Xabier, X. (2021) Tools for Web Accessibility Evaluation. In: S. Harper and Y. Yesilada, ed., Web Accessibility A Foundation for Research, 2nd ed. London: Springer, pp.479-499.

Frazão, T. and Duarte, C., 2020. Comparing accessibility evaluation plug-ins. Proceedings of the 17th International Web for All Conference,.

Johnson, P. and Lilley, M. (2022) “Software prototype for the ensemble of Automated Accessibility Evaluation Tools,” Communications in Computer and Information Science, pp. 532–539. Available at: https://doi.org/10.1007/978-3-031-06417-3_71.

Vigo, M., Brown, J. and Conway, V., (2013) Benchmarking web accessibility evaluation tools. Proceedings of the 10th International Cross-Disciplinary Conference on Web Accessibility - W4A '13,.

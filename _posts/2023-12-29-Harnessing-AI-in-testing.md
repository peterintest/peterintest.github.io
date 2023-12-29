---
layout: post
title: Unleashing the power of Large Language Models in Testing
date: 2023-12-29 08:00:00 +0000
categories: [artifical intelligence, software testing, LLM]
tags: [AI, artifical intelligence, test automation, ChatGPT, CoPilot]
image:
  path: /images/pepper_robot.jpg
  alt: A photo I took of Pepper - a social humanoid robot manufactured by SoftBank Robotics
---

Welcome to the ever-evolving landscape of software development, where the intricacies of modern systems collide with the escalating demand for frequent releases. In this agile environment, the pursuit of efficient and effective testing processes has intensified, driven by the need to deliver high-quality software at an accelerated pace. While traditional test automation has aimed to boost test execution speed and improve test coverage, it has introduced challenges stemming from delicate automation scripts and ineffective bug detection (Trudova et al., 2020).

Addressing issues such as system test flakes and ensuring comprehensive test coverage for new features, especially when the number of feature developers surpasses that of test developer. This necessitates more than just a shift-left approach to testing. It calls for a collective effort within the development team, encouraging everyone to identify opportunities for increased efficiency in development and testing activities.

## The opportunity with Large Language Models (LLMs)

Recent strides in generative artificial intelligence (AI) are bringing a new era of possibilities. The widespread availability of Large Language Models (LLMs) by influential companies such as Microsoft, Google, and OpenAI, have significantly lowered the barriers to entry for both individuals and organizations. Prominent examples of such models include OpenAI's Chat Generative Pre-Trained Transformer (ChatGPT) and Microsoft's GitHub Copilot.

These LLMs undergo pre-training on vast corpora, leveraging the transformer architecture introduced by Google in the seminal 2017 paper "Attention Is All You Need." This architecture, featuring multi-head attention layers in a deep neural network, empowers these models to excel in natural language processing (NLP) tasks, as highlighted by Wang et al. (2023).

In the realm of test automation, AI advancements have proven to be transformative. A comprehensive review by Trudova et al. (2020) found that 73% of examined papers recognised the positive impact of AI techniques on testing. These advantages spanned from reducing manual efforts to enhancing test coverage and improving fault and vulnerability detection.

While the application of LLMs in software testing is still in its early stages, a recent survey by Wang et al. (2023) highlights their use in specific testing activities. LLMs are frequently deployed in tasks such as test case preparation, including unit test case generation, test oracle creation, and test input generation. Additionally, they play a valuable role in to bug analysis, debugging processes, and bug fixing.

However, it is crucial to acknowledge the inherent limitations and challenges. Wang et al. (2023) emphasised that LLMs do not replace the entire testing process, particularly in the early stages of the testing life cycle, such as identifying test requirements or formulating a test plan.

This dynamic landscape underscores the evolving nature of AI in testing. The challenges and opportunities tied to integrating LLMs are expected to evolve as the technology matures. The potential for accelerated and precise test case generation, improved debugging capabilities, and overall enhanced testing efficiency signifies promising opportunities.

As ongoing research delves into the intricacies of incorporating LLMs into software testing, a clearer understanding of how to effectively harness their capabilities will emerge; reshaping and optimising the software testing life cycle.

### Pair programming with GitHub Copilot

Tools like GitHub Copilot can significantly enhance coding efficiency by leveraging LLMs to generate code snippets in realtime. It achieves this by analyzing context and providing relevant code suggestions as code is being typed. Research has found that developers who used GitHub Copilot completed programming tasks 55% faster than the developers who didn’t use GitHub Copilot (Kalliamvakou, 2023). 

My experience with using Copilot has been positive as it can assist well with writing small code snippits and generic boilerplate code. GitHub Copilot can also assist with reviewing and describing existing code.

### Behavior-Driven Development (BDD)

The integration of Large Language Models (LLMs) into test automation leverages their proficiency in natural language processing (NLP), enabling the comprehension and manipulation of human language. This capability provides an opportunity to write and execute tests in a natural language format, enhancing accessibility for non-technical stakeholders and fostering collaboration among developers, testers, and other project members.

Optimizing LLMs for test automation involves fine-tuning through training on the documentation or code of the testing framework. Careful prompt engineering enables LLMs to suggest implementations of test scripts, proving advantageous in behavior-driven development (BDD) tools such as behave or cucumber. In BDD, tests are defined in a natural language syntax (e.g., Gherkin) within a feature file, and corresponding test step definitions are maintained in the test framework.

By inputting a Gherkin feature, LLMs can propose test script implementations from existing step definitions, streamlining the creation of executable test scenarios based on natural language specifications. This approach can improve the efficiency of writing test scripts in the context of behavior-driven development.

## Risks and Challenges of using LLMs

In a recent encounter with Pepper, the social humanoid robot from SoftBank Robotics, I was pleasantly surprised by its engaging capabilities in a hotel lobby. Pepper not only welcomed me with entertainment but also seamlessly provided information about the hotel, showcasing its designed proficiency in human interaction. The robot's array of sensors effortlessly detected my movements, enhancing the overall experience. Drawing parallels, I reflected on the similarities with ChatGPT, where users communicate with the large language model through natural language prompts to execute tasks. As AI systems progress toward more anthropomorphic characteristics, it becomes necessary to incorporate human critical thinking, reason, and judgment in our interactions with these evolving technologies. As we embrace more AI into our work and lives, maintaining a thoughtful and discerning approach remains important.

### New skills

New skills in prompt engineering are required to learn how to efficiently and effectively use LLMs.
Prompt engineering is a new discipline focused on optimizing prompts for LLMs. It enhances LLM capabilities in various tasks, from question answering to arithmetic reasoning, and aids developers in designing effective prompting techniques. Beyond prompt creation, it encompasses vital skills for interacting with and understanding LLMs, improving safety, and adding domain knowledge.

OpenAI have released a [guide](https://platform.openai.com/docs/guides/prompt-engineering) on prompt engineering which is worth reading.

### Code quality

We need to exercise caution when using code generated by LLMs, particularly in scenarios involving sensitive or secure applications such as medical devices or handling confidential user data. While LLMs may generate impressive code, it is essential to thoroughly understand and test the code for bugs.

### Bias

LLMs tend to repeat the biases found in the data they are trained on. This happens because they learn from a massive amount of text data collected from various sources like the internet. If the original data contains biases, the model can unintentionally incorporate and reproduce these biases.

### Copywright of generated code

As LLMs have been trained on large datasets of human generated code; for example Github Copilot was trained using millions of GitHub repositories containing open-source code there is a risk of generated code causing licensing problems? 

### Data privacy

Entering sensitive data or source code into a LLM can pose significant risks to data privacy. As these models process vast amounts of information, there is a concern that sensitive or personal data may be inadvertently incorporated into the training data, leading to potential privacy breaches.

## Conclusion

The integration of Large Language Models (LLMs) like ChatGPT and GitHub Copilot in software development and testing offers potential to be more productive. These models enhance coding efficiency, enable natural language testing, and present opportunities for improved testing processes. However, challenges such as bias, copyright concerns, and data privacy risks must be addressed. As we navigate this evolving landscape, ongoing research and the development of new skills in prompt engineering are essential for effectively leveraging the capabilities of LLMs while maintaining ethical and secure practices.

## References

Kalliamvakou, E. (2023) Research: Quantifying github copilot’s impact on developer productivity and happiness, The GitHub Blog. Available at: https://github.blog/2022-09-07-research-quantifying-github-copilots-impact-on-developer-productivity-and-happiness/ (Accessed: 27 December 2023).

Porter, L. and Zingaro, D. (2023) Learn AI-Assisted Python Programming With GitHub Copilot and ChatGPT. Shelter Island, NY: Manning Publications. 

Trudova, A., Dolezel, M. and Buchalcevova, A. (2020) ‘Artificial Intelligence in Software Test Automation: A systematic literature review’, Proceedings of the 15th International Conference on Evaluation of Novel Approaches to Software Engineering [Preprint]. doi:10.5220/0009417801810192.

Wang, J., Huang, Y., Chen, C., Liu, Z., Wang, S. and Wang, Q., 2023. Software testing with large language model: Survey, landscape, and vision. arXiv preprint arXiv:2307.07221.

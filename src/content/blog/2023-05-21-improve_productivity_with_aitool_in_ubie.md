---
title: Case Study on Productivity Improvement Through the Use of AI Tools
description: A blog post introducing examples of productivity improvements through the use of AI tools in Ubie Discovery.
pubDate: 2023-05-21
tags: ['仕事', 'env development']
---


### TL;DR
- [Ubie](http://ubiehealth.com/) is committed to enhancing productivity by leveraging the advancements in AI tools that have been notably significant in recent times.
- Our qualitative survey using GitHub Copilot revealed an average efficiency increase of 38% in coding tasks.
- Beyond this, we've explored a range of tools and have also been designing and implementing productivity improvement tools, keeping a keen eye on the Return on Investment (RoI).
---

The recent advancements in GenerativeAI have unlocked a wide array of possibilities.
Not only is it innovative in terms of creating novel outcomes, but it's also excelling at enhancing the efficiency of existing tasks.

In this post, I will focus on productivity improvements achieved through GenerativeAI. I'll share how it has significantly bolstered productivity within [Ubie](http://ubiehealth.com/), where I am currently positioned, and discuss our approach to its development and operation.


### Benefits and Challenges of Productivity Improvement with GenerativeAI Tools
The benefits of these tools may seem obvious.
The profound impact of using GPT-4 with [ChatGPT](https://openai.com/blog/chatgpt) is something I'll likely always remember.

With its capacity to generate high-quality outputs in a myriad of fields while considering context, it becomes an ideal tool for enhancing productivity.
It's an excellent resource for someone with a certain degree of expertise to brainstorm and refine ideas, or to receive assistance with programming or documentation.

These advantages have been widely discussed, and I believe most people are already aware of them, so I won't delve deeper into them here.
However, it's important to note that there are unique challenges to fully utilizing such tools on an organizational level, not just individually.

The specific challenges that need to be addressed for sustained use include:

- Accurate assessment of RoI
  - Using these tools often requires a financial investment, necessitating a thorough evaluation of whether a corresponding return is achieved. The degree of complexity involved in such an assessment will vary by organization, but in many cases, some qualitative data will be required for a sound judgment.
  - Without careful oversight, widespread use could potentially diminish RoI. It's common for organizations to purchase account-based tools for all employees, but if only a few people use them sufficiently to justify the cost, it's an issue. This type of challenge is even more crucial in larger organizations where cost control is paramount.
- Establishing a system for continuous development and operation
  - A common pitfall is the creation of a useful tool that, once operational, receives little maintenance, even as part of the operations becomes dependent on it, turning it into a liability. While we encourage voluntary development, there's a need for a system that seamlessly connects what we continue to use with operational management.
- Necessary training for effective usage
  - Training is crucial to ensure effective use of the tool. While those with a certain level of expertise can typically use it effectively on their own, this tool is significantly different from previous ones, necessitating various strategies to fully leverage its capabilities. If the goal is to elevate the overall level of competency within the organization, targeted training could be beneficial.
  - Training from a security standpoint is also vital. Depending on the tool and how it's used, confidential information could be compromised, underlining the need for risk management and awareness in this area.

While initial enthusiasm is crucial, these challenges need to be addressed to ensure effective utilization in the medium to long term.

### Specific Examples from Ubie
Whenever new GenerativeAI technologies emerge, a variety of people experiment with different external tools or even create their own.
While this level of initiative is certainly commendable, if left unmanaged, it could lead to uncoordinated efforts and possible chaos.
As such, it's crucial to have someone to orchestrate these various initiatives.

At Ubie, we have adopted [Holacracy (article in Japanese)](https://yoheikikuta.github.io/blog/2022-01-04-ubie_discovery_org_dev_as_software_dev/) and have established roles that are responsible for overseeing productivity enhancement tools and integrating them into the organization.
Both myself and other developers are assigned to these roles (in addition to this, there are teams tasked with creating new value and integrating it into business strategies using Large Language Models, but that's a separate narrative from this productivity improvement and will not be discussed here).

In this role, I am actively involved in selecting, verifying, and promoting external tools that have the potential to create a significant impact.
Additionally, I determine the conditions for continuing or discontinuing our internally developed tools, strategize how to disseminate them throughout the company, and devise mechanisms for such endeavors.

Below, I'll share some specific examples drawn from these initiatives.

#### GitHub Copilot
In February 2023, when [GitHub Copilot for business](https://docs.github.com/en/enterprise-cloud@latest/copilot/overview-of-github-copilot/about-github-copilot-for-business) went into general availability, and anticipation surrounding its effectiveness began to rise, we initiated our evaluation phase in early March, after ensuring there were no issues with its terms of service.

During this assessment period, we set up seats for all developers involved in software development.
However, even among developers, there are those who might not be involved in coding work at certain times, so we aimed to manage these seats effectively.
It's also possible to [assign GitHub Teams as Copilot users](https://docs.github.com/en/enterprise-cloud@latest/copilot/configuring-github-copilot/configuring-github-copilot-settings-in-your-organization#disabling-access-to-github-copilot-for-specific-users-in-your-organization). 
At Ubie, we handle our GitHub accounts with Terraform.
As such, we've adopted a management style that allows us to bulk manage usage, enabling us to easily turn access on and off as required.

<div align="center">
<img src="https://i.imgur.com/S9Nt4VQ.png" width="600">
</div>

After a two-month trial period involving all our team members, we conducted a qualitative survey to gauge its contribution to productivity improvement.
The results were as follows:

- Number of valid responses: 24
- Average of the perceived efficiency increase in coding tasks: 38%
- Standard deviation of the perceived efficiency increase in coding tasks: 24%

Considering these results, with an investment of $20 per person per month (management cost is virtually negligible as it merely involves adjusting Terraform settings), we can roughly expect a return of tens to hundreds of thousands of yen per month.
This range takes into account labor costs and the time spent on coding.
Despite the simplicity of this estimation and the factors it omits, it's quite clear that the return on investment (RoI) is substantial enough that it would be more challenging to find a reason not to invest.

While these efficiency numbers are largely based on intuitive responses, they seem to align with [the 55% faster coding reported in GitHub's official blog](https://github.blog/2022-12-07-github-copilot-is-generally-available-for-businesses/).
We are eagerly anticipating the day when GitHub Copilot X becomes generally available.

As for specific feedback on its usefulness, we received comments like:

- While it may not double productivity, it significantly improves it in numerous small ways, which greatly enhances the development experience.
- I initially underestimated how useful GitHub Copilot would be for SQL, but it turned out to be incredibly helpful.
- It provides a great starting point for areas where I lack familiarity, like with Terraform.
- The pace of testing and routine tasks has accelerated, leading to a significant reduction in stress!
- ...

Since GitHub Copilot is only used by software engineers and is easy to manage, it doesn't require extensive training, making it an incredibly potent tool for productivity enhancement.

#### Notion AI
We are also testing [Notion AI](https://www.notion.so/product/ai).

A tangible accomplishment so far is the English translation of text assets compiled in Notion.
As Ubie is expanding globally, the majority of our text assets are in Japanese, and we're in the process of translating the useful ones into English.
Previously, we outsourced this translation work, but with Notion AI, we've made the process more efficient.
This has sped up the process and reduced costs by decreasing our reliance on outsourcing.

Furthermore, it's being used in a variety of scenarios, such as crafting standardized sentences and creating mermaid-format diagrams.

As for next steps, we're still deciding. However, [the subscription type is for the entire workspace](https://www.notion.so/help/ai-pricing-and-usage), which presents a certain challenge.
While it undeniably improves productivity for some tasks, tools like this are typically used by a select few, leaving the majority unutilized.
Currently, not many at Ubie seem to be using it consistently.

Given that the cumulative cost is significant, we intend to calculate a discussable ROI by the end of the testing period to inform our decision.

If we want Notion AI to be used organization-wide, we'd probably need to invest considerable effort into training and promoting its use so that people of various job types can continually utilize it.

#### In-house developed tools
Ubie is also working on a tool that assesses the business risk of using ChatGPT, as detailed in [this article (in Japanese)](https://note.com/sys1yagi/n/n6b7425df175f).

This tool was developed for internal use, with a specific focus on managing something like ChatGPT.
The detailed information can be found in the linked article.
However, it's worth noting here that in addition to risk mitigation mentioned in the article, this tool is also crucial in addressing the issues outlined in this entry.

For instance, while it might make sense from a productivity standpoint to provide every employee with a paid account for ChatGPT, tools of this nature are often only used by a select few, leaving the majority unutilized (like the case with Notion AI that I mentioned above).
Overcoming this issue requires initiatives such as training and sharing application examples.
It's also crucial to consider whether the return genuinely justifies the investment.

This tool employs OpenAI's Web API, allowing a pay-as-you-go usage across the entire organization.
While it's a self-developed tool and, therefore, requires investment, we're developing it in stages, mapping out a user journey and observing user behavior.
Many internal users have found it highly beneficial for improving productivity, suggesting a return that far outweighs the investment.

To use the tool effectively, a fair amount of training and promotion is necessary, so we're in the process of deploying this tool across the organization.
Concurrently, we're collaborating with Ubie corporate's IT administrator, who oversees the entire Ubie organization, to advance the project, aiming to hand over management once the tool's development has sufficiently progressed, and it's in the main operational phase.

We're also developing and testing various other tools, but due to resource constraints and the potential emergence of useful alternative services, we're clearly defining the testing period and will discontinue the function if the ROI doesn't meet our expectations at that point.
As for what kinds of tools we're working on, you'll have to stay tuned---they might be released by our team once their effectiveness is confirmed.

We're all for the development of diverse tools!
While promoting this initiative, our aim is to ensure their collective effectiveness.

### Summary
Generative AI holds tremendous power when it comes to enhancing productivity.
Nonetheless, in larger organizations, the accumulating costs can't be overlooked, so it's crucial that we continue to leverage it as efficiently as possible.

The tools I've touched upon here only represent a fraction of those we use, so I might delve into other tools at some point in the future.

---
layout: article
title: "Data Visualization Shouldn't be Rocket Science"
date: 2025-10-03
tags: [dashboard-design, data-visualization, business-intelligence, public-sector, usability]
excerpt: "Effective data visualization is not about visual complexity; it is about reducing cognitive load so people can quickly understand what matters and act on it."
---

## Introduction

Data visualization is often treated as a technical craft first and a communication craft second. You can see this in how dashboards are praised: more charts, more interactivity, more filters, more metrics, more “power.” But in practice, the purpose of data visualization is much simpler than that. The goal is to help people understand something they could not easily understand before.

That is especially true in public-sector analytics and business intelligence work. The people using these products are often busy, under pressure, and trying to make decisions with imperfect information. They do not need a demonstration of how much data we can fit on a screen. They need a clear picture of what is happening, why it matters, and what to do next.

When a dashboard is overloaded, it may look sophisticated while failing at its basic job. Users spend their energy interpreting the interface instead of interpreting the data. They hunt for the relevant chart, decode labels, compare competing signals, and second-guess what they are looking at. That is not insight. That is friction.

The strongest data visualizations are often the simplest. They feel obvious once you see them. They translate technical or intimidating concepts into something understandable and useful. In that sense, good visualization design is less about showing complexity and more about carrying complexity responsibly so other people do not have to.

## The Problem

A common mistake in BI and dashboard work is equating complexity with quality. Teams assume that if a page contains more visuals, more detail, or more interactivity, it must be more valuable. In reality, overcomplexity often reduces value because it increases cognitive load.

This happens for understandable reasons. Analysts want to preserve nuance. Stakeholders want their metrics included. Product owners fear leaving something out. Technical teams want to show what the platform can do. Over time, a dashboard becomes less of a decision tool and more of a data inventory.

You can usually spot the symptoms quickly:

- Too many visuals competing for attention on a single page
- Redundant charts answering the same question in different formats
- Technical field names instead of audience-centered labels
- Excessive use of color, legends, annotations, and slicers
- Inconsistent layout patterns across tabs
- Interactivity that feels powerful but makes common tasks slower

The result is predictable. Users take longer to orient themselves. They misinterpret metrics. They ask for repeated walkthroughs. Adoption drops. Eventually, people bypass the dashboard and go back to spreadsheets, screenshots, or verbal summaries because those feel easier to use.

I think often about this tradeoff because I experienced it firsthand while working as a Data Visualization & Reporting Analyst with San Francisco’s COVID-19 Task Force. My colleagues and I closely monitored the widely used Johns Hopkins CSSE global COVID-19 dashboard during the pandemic. It was an extraordinary public-facing data product in many ways. It helped millions of people understand the scale and seriousness of the crisis. At the same time, it was so information-dense and visually overwhelming that it could also demotivate people and heighten fear.

That tension matters. A visualization can be informative and still be emotionally or cognitively difficult to use. In high-stakes situations, that distinction is not academic. It affects whether people understand what applies to them and what action they should take.

## A Better Approach

A better approach is to treat data visualization as decision support, not data display. Start with the user’s question. Then design the simplest possible visual structure that answers it clearly.

This is where “less is more” becomes a practical design principle rather than a stylistic preference. Simplicity is not about removing all nuance or making visuals generic. It is about prioritizing what the audience needs most and reducing the effort required to interpret it.

When I worked on COVID-19 visualizations for San Francisco residents, our team took a much more pared-down approach than large global dashboards. We designed simple visuals with clearly defined purposes and interpretation so people could understand what was happening in their own community and what actions to take. The goal was not to show every possible dimension of the pandemic. The goal was to inform and motivate behavior: wear a mask, get tested, self-quarantine, get vaccinated.

That experience reinforced an important lesson for me: clarity is not a lesser form of analysis. It is often the highest-value output of analysis.

In public-sector contexts, this matters even more because audiences vary widely in technical background, time available, and emotional state. A resident checking a public dashboard may be anxious, multitasking, or unfamiliar with epidemiology terms. A city manager may have two minutes before a briefing. A frontline staff member may need a quick answer, not an exploratory experience. A simple, well-structured visualization respects those realities.

The best dashboards do not make users work to find the message. They present the message clearly, then offer additional detail only when needed.

## Practical Techniques

The easiest way to avoid overcomplicated dashboards is to adopt a few disciplined design habits. Most of these are not advanced. That is exactly the point.

Start with a one-sentence purpose statement for each page before building anything: *This page helps [who] decide [what].* If you cannot finish that sentence clearly, the page is likely trying to do too much. This step alone prevents many “everything dashboard” problems.

Next, identify the top one to three questions the user needs answered. Design the page around those questions, not around the available fields in the dataset. If a visual does not help answer one of those questions, it is probably a candidate for removal, relocation, or a secondary detail page.

Limit visual density deliberately. In many cases, three to five meaningful visuals on a page is more effective than ten or twelve. Use progressive disclosure: create a summary page for orientation, then separate pages or drill-throughs for deeper analysis. This gives users a clear path instead of forcing them to decode the entire model at once.

Default to simple chart types unless a more complex chart clearly improves understanding. Bars, lines, tables, and basic maps solve most business and public-sector reporting needs well. A line chart is usually the best choice for trends over time. A bar chart is usually the clearest choice for comparing categories. A table is often the best choice when exact values matter. Complexity should be justified by comprehension gains, not novelty.

Reduce cognitive load in your labeling and layout. Use chart titles that explain what is shown and include the timeframe. Sort categories intentionally. Standardize date formats, decimal precision, and color usage across the dashboard. Place the most important metric or chart where users look first. Small consistency choices compound into a dashboard that feels easier to use.

Use emphasis sparingly. If everything is highlighted, nothing is highlighted. Choose one accent color or visual emphasis to draw attention to the most important signal and keep supporting elements visually quiet. Avoid decorative effects that compete with the data.

Finally, test for clarity, not just correctness. A dashboard can be numerically correct and still fail as a communication tool. Try a quick “5-second test”: show someone the page briefly and ask what they think it is saying. Ask users to narrate what they believe a chart means. Watch where they hesitate or misread labels. In trainings and demos, pay attention to repeated questions. Those are design signals, not user failures.

A few practical rules of thumb also help:
- If a chart needs a paragraph of explanation in every meeting, redesign it.
- If users need repeated training to read a core visual, simplify it.
- If multiple visuals answer the same question, consolidate them.
- If every metric is labeled “key,” you have not prioritized.

## Common Mistakes

Simplifying dashboards does not mean stripping out context. One common mistake is making a dashboard look clean while removing the information users need to interpret it correctly. A KPI card without a timeframe, denominator, or definition may be visually tidy but analytically weak. Simplicity should reduce confusion, not remove meaning.

Another mistake is hiding too much behind interactivity. Drill-throughs, tooltips, and filters are useful, but they should support a clear structure, not replace it. If users must click through multiple layers to answer a basic question, the dashboard is not actually simple.

Teams also sometimes prioritize aesthetics over readability. Minimalist layouts with tiny fonts, low contrast, and subtle distinctions may look modern in a screenshot while performing poorly in real use. Public-sector dashboards in particular need to work across devices, environments, and levels of visual literacy.

A frequent organizational mistake is treating every stakeholder request as equal. This is how dashboards become cluttered. Saying yes to every requested chart often means saying no to clarity. Good dashboard design requires prioritization at the page level: what is primary, what is secondary, and what belongs elsewhere.

Finally, teams sometimes design for the presenter rather than the end user. A dashboard that works well when narrated live may fail when users open it alone. If the meaning depends on a verbal explanation, the visualization needs improvement.

## Conclusion

Data visualization is not rocket science, but it is disciplined communication. The goal is not to impress people with complexity. The goal is to help them understand what matters and act on it.

In my experience, overcomplicated dashboards often signal a failure to prioritize, not a higher level of sophistication. By contrast, simple visualizations with clear purpose, plain interpretation, and focused design are often more useful, more trustworthy, and more actionable. I saw this clearly during COVID-19 reporting work: broad, information-rich dashboards helped convey the scale of the crisis, but pared-down local visuals were often better at helping residents understand what to do next.

That is the standard I aim for in BI and public-sector visualization work. Start with the user’s question. Reduce cognitive load. Keep only what serves the decision. Then test whether people can interpret the page quickly and confidently. When a visualization feels straightforward, that usually means the designer did the hard work well.

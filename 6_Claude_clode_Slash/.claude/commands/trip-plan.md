---
description: Plan a trip — research a destination, then produce a formatted Trip Brief.
argument-hint: <destination> [YYYY-MM-DD]
allowed-tools: Task, Read, WebSearch, WebFetch
---

Plan a trip to: **$ARGUMENTS**

Run this in two steps, then show the user only the final result:

1. **Delegate the research.** Use the `trip-researcher` subagent to find the
   current weather at the destination and the cheapest flight there. Use the date
   in the arguments if one is given; otherwise assume two weeks from today. Have
   it return raw facts only.

2. **Format the answer.** Take the researcher's findings and format them with the
   **trip-brief** skill. Present only the final Trip Brief.

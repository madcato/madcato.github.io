---
layout:     post
title:      "Ending the Development of Codebender"
subtitle:   "why I leave this project?"
date:       2024-09-26 12:00:00
author:     "Daniel Vela"
locale:     en
lang-ref:   codebender
---

I am ceasing the development of Codebender. While the concept seemed promising, the complexity has proven to be overwhelming for me. I don't believe I'm capable of refining the code in such a way that would make this project function well.

To ensure AI operates effectively, it is necessary to have access to a large volume of similar codes. My intention was to overly specialize the usage of certain codes chosen by users. However, these codes are far from generic, and Large Language Models (LLMs) struggle to function well under these circumstances.

For a code generator to work properly, it needs to include numerous different examples of the same functionality. For instance, to train a model to generate code that uses the Stripe API, many variations of using this API must be included. If only a single example is provided, the LLM might at best replicate that exact example but will never be able to adapt to the particular needs of the user when programming something different.

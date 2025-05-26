# prompt db



## using prompts with github copilot

the github copilot documentation has the "prompt files" and "instructions" mixed in one documentation: https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot

the vscode documentation seems more informative than the github one: [documentation for github copilot prompts](https://code.visualstudio.com/docs/copilot/copilot-customization#_reusable-prompt-files-experimental)

## brainstorming

There are two tricky parts, first prompts can be linked with each other, so if we build a website to share prompts how do we deal with linked prompts, the second difficulty is how to build a good search, do we use regular sql full text search or a RAG with an AI bot?

The problem that will arise is that at some point the database will contain big amounts of prompts that have exactly the same tags or that have very similar goals but the implementation is very different:

* how do we start by measuring how popular a prompt is? 
* how can we make it so that users will be able to find the best prompt if a lot of similar prompts exist? If two prompts are very similar how do we decide which one is best?
* can we use that ai bot to make the search results better?

how do we store / manage connections between prompts, how do we deal with similar prompts (especially as prompts can be linked to others):

Lets imagine that user A creates two prompts, his main prompt describes how to create a react component and that prompt depends on another prompts that instructs the ai to use the rules from the editorconfig when formatting code.
Now user B decides to use the prompt of user A. So he adds the prompt to create a react component to create his own collection, but user B does not have User A's editorconfig prompt, so something is missing for it to work.

* do we use versioning, like npm packages
* do we use a history like wikipedia that allows you to go back to anterior versions (for community prompts)
* I like the idea of nodes in comfy ui. Comfy UI allows users to create, search and use nodes from other users to create complex workflows. When you open a workflow in comfy ui, then you can install the nodes that are being used in the workflow but missing from your library. A similar approach could work for prompts, where you add a prompt to your collection, but because the prompt is linked to a second prompt, we need to somehow retrieve the missing prompt.
* another idea is to take inspiration from npm registry. Each package can have dependencies and when npm installs a package it will check the package.json for dependencies and install those too. so should we use 
* I was also wondering if we should split prompts into two groups, one group is primary prompts that exist on their own and have no dependencies and then you have some sort of secondary prompts that are prompts that have dependencies.
* besides the question how to manage dependencies, another big question is how to deal with situations where you add a prompt to your collection that depends on a prompt to use the editorconfig, however you already have such a prompt in your library but it is not exactly the same, your "use editorconfig" prompt is your own that you wrote yourself, while the dependency from the prompt you just added is a "use editorconfig" prompt from someone else.
* what system do we implement, to allow a user to add a prompt to his library but then use his own prompt as dependency instead of the one defined in the initial prompt (assuming we want this kind of feature in the first place).

where do we store prompts

* do we use a conventional postgresql database, which would be straight forward except for the question how we link prompts together
* or do we for example could we use the github API to retrieve the prompts from user accounts on github? Meaning every user connects using github, when they create a prompt they do so on github, for example using a gist. Next they visit the website, where they can publish their prompt, the website then uses the github API to retrieve the gist!? Then other uses can fork the gist!?
  * the advantage of using the github API would be to reuse tools developers already know and also to reduce the amount of work on our side, by letting github handle the storage and forking mechanism for prompts

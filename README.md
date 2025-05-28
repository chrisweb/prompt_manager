# prompt files db

A community place to post and share prompt files (for developers). Organizing prompts gets messy if your prompt library grows, secondly writing good prompts takes a lot of time and knowledge so being able to reuse and share prompts would be great

## initial idea

My initial idea was to create a visual editor, maybe some kind of visual nodes diagram, where each prompts is displayed as box and then connected by wires to each other, like the systems used in game engines or ai image tools like comfy ui, to be able to create complex workflows containing a lot of prompts that are each linked to each other

For example a "react component prompt" that should use a form would depend on the "react form prompt" which would depend on the "forms (best practices) prompt" which then again could depend on the "form accessibility prompt" (it would be fun to actually have a bot that helps you building a workflow but constantly giving tips and suggestions that you can accept into the workflow or just ignore, like hey I noticed you are using a form prompt, the accessibility prompt is often combined with form prompts, do you want to search for accessibility prompts?)

## using prompts with github copilot

on windows put the prompts into: `C:\Users\YOUR_USERNAME\AppData\Roaming\Code\User\prompts`
or put them into the `.github/prompts` directory of your workspace (your project)

to use prompts the docs state you can use `ctrl + shift + p`, then write "Chat: Run prompt" to run a prompt
but you can type `/` in the chat to get a list of your custom prompts

to create prompts either put them manually into the respective folders, or use `ctrl + shift + p`, then type "Chat: New", then select "Chat: New Prompt file..."

## documentation

the github copilot documentation has the "prompt files" and "instructions" mixed in one documentation: [github docs: copilot chat prompt files](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot)

the vscode documentation seems more informative than the github one: [VSCode documentation: github copilot prompts](https://code.visualstudio.com/docs/copilot/copilot-customization#_reusable-prompt-files-experimental)

## brainstorming

There are several tricky parts, first prompts can be linked with each other, so if we build a website to share prompts how do we deal with linked prompts, the second difficulty is how to build a good search, do we use regular sql full text search or a RAG with an AI bot?

The problem that will arise is that at some point the database will contain big amounts of prompts that have exactly the same tags but slightly different content, or that have very similar goals but the implementation is very different:

* how do we start by measuring how popular a prompt is? 
* how can we make it so that users will be able to find the best prompt if a lot of similar prompts exist? If two prompts are very similar how do we decide which one is best?
* can we use that ai bot to make the search results better?

how do we store / manage / visualize connections between prompts, how do we deal with similar prompts (especially as prompts can be linked to others):

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

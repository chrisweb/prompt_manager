---
mode: 'agent'
---

# Next.js Starter Kit

In the current directory, create a basic next.js project using create-next-app

## installation phase

This is CNA you will have execute in the terminal, but before you execute it you need to check which flags need to get added: 

```bash
npx create-next-app@latest . --app --turbopack --import-alias "@/*" --use-npm
```

if ${input:src-dir:true} is true, add the `--src-dir` flag to the end of the command else add the `--no-src-dir` flag
if ${input:typescript:true} is false, add the `--javascript` flag to the end of the command else add the `--typescript` flag
if ${input:tailwind:true} is false do nothing, else add the `--tailwind` flag to the end of the command
if ${input:eslint:true} is false do nothing, else add the `--eslint` flag to the end of the command

## cleanup phase

To get a starterkit with no content, when the installation is complete, we do the following cleanup:

* delete all files in the /public folder
* simplify the code of the /app/page.tsx file to the bare minimum
* simplify the code of the /app/layout.tsx to the bare minimum
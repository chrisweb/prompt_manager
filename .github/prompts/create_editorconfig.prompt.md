---
mode: 'agent'
---

create an .editorconfig file (in the root of the project) and then add the following content:

```
root = true

[*]
indent_style = space
indent_size = 4
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true

[*.{md,mdx}]
indent_size = 2
insert_final_newline = true

[*.{js,jsx,mjs,ts,tsx,mts,json}]
indent_size = 4
```
## ⚠️ Breaking Change: Structured Agent Inputs

APP agent invocation has moved from **free-form prompt inputs** to **spec-defined structured inputs**.

### Before

Agent specs defined a single generic `query` input:

```yaml
inputs:
  query:
    type: string
    required: true
    description: Repository, branch, and file to retrieve.
```
to 
```yaml

inputs:
  repository:
    type: string
    required: true
    description: Repository name.

  branch:
    type: string
    required: true
    description: Repository branch.

  file:
    type: string
    required: true
    description: File path.



```

## Before  :

```js

const agent = await app(
  "github_file_reader@1.0.0",
  "Read src/index.js from test_repo on the main branch."
);

```


## After :

```js

const agent = await app("github_file_reader@1.0.0", {
  repository: "test_repo",
  branch: "main",
  file: "src/index.js"
});

```


> Why? Free-form prompts force developers to repeatedly describe how an agent should operate, leaking agent logic into application code.
Structured inputs keep behavior inside the versioned spec — callers provide only the data the agent needs.

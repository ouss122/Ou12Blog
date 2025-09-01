---
author: Hugo Authors
title: Math Typesetting - use Mathematical notation in blog posts
date: 2023-04-01
description: A brief guide to setup KaTeX
math: true
---

Mathematical notation in a Hugo project can be enabled by using
[third party JavaScript libraries](https://github.com/hugo-sid/hugo-blog-awesome/blob/main/layouts/partials/helpers/katex.html).

<!--more-->

In this example we will be using [KaTeX](https://katex.org/).

- To enable KaTeX globally, set the parameter `math` to `true` in a project's
  configuration file as follows.
  - `hugo.toml`
    ```toml
    [params]
      math = true
    ```
  - `hugo.yaml`
    ```yaml
    params:
      math: true
    ```
- To enable KaTeX on a per page basis, include the parameter `math: true` in
  Front Matter of Markdown content file as follows.

  ```
  ---
  math: true
  ---
  ```

**Note:** The online reference of
[Supported TeX Functions](https://katex.org/docs/supported.html) is a helpful resource.

### Examples

This sentence uses `$` delimiters to show math inline: $\sqrt{3x-1}+(1+x)^2$

- Block math:

  $$
  \varphi = 1+\frac{1} {1+\frac{1} {1+\frac{1} {1+\cdots} } }
  $$

- Inline math:

  This is an inline polynomial: $5x^2 + 2y -7$.



> [!Definitions]
> We can rewrite the theorem (or the statement) as :
> 
> $$
> \text{If } P \text{ then } Q 
> $$
> or more mathematically :
> $$
> P \implies Q
> $$
> 
> where :
> 
> - $\implies$ is called implication
> - $P$ : $n^2$ is even
> 
> - $Q$ : $n$ is even
> 
> 
> As you can notice from the example above, "the theorem is true" means that whenever $n^2$ is even (which mean $P$ is true) then n must be even (Q must be true)
> 
> In other words, The statement is false only when $P$ is true and $Q$ is false
> 
> and that where the table come from :
> 


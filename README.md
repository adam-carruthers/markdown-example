# Documentation in ASCS

We have a few different options regarding how we could do documentation for the user's survey.

- What is the scope of the documentation that we put in the code? How do we avoid duplicating the methodology report?
- The documentation is a written output of our team, what quality standards do we hold it to?
- Within the codebase, how do we structure our documentation?
  - `docs` folder?
  - In markdown files throughout the codebase?
  - Docstrings?
  - Inline comments?
  - Where do design decisions go?
  - Where do explanations of process go?

## How documentation works in the GitLab repo

This brief explainer explains the different ways that there are of doing documentation.

Firstly, within the code, there are comments, which come in two forms:

```python
# This is an inline comment

def some_function():
    """
    This here is called a docstring
    """
    return 5+6
```

Comments are a form of documentation. They can be useful because they are right there in the code, right by the code they describe. Also, docstrings normally work very well with VSCode and autocomplete, when people are using a function in the code the docstring will normally display next to it.

However, docstrings aren't perfect. They are simple text so lack nice formatting options. Also, they very easily become clutter.

Comments in the code are normally short, the other tool you can use for documentation is called **markdown**. Markdown is a way of writing documents with formatting that works very well with git.

<details>
<summary>See an example of how markdown works (click me)</summary>

````markdown
### This is a markdown document

> It is just a simple file filled with text, like a `.txt` file or a `.csv` file

When you use things like _underscores_ and **stars** it becomes a nice formatted output.

You can do things like [links to websites](www.google.com)

- You
- can
- have
- lists

```python
print("You can even write python code and it will show it with formatting")
```

<details>
  <summary>You can even have expandable sections</summary>
  
  ## Heading
  1. A numbered
  2. list
     * With some
     * Sub bullets
</details>

Markdown has support for maths equations, both inline $x = /frac{5}{2}$, and in big mode

$$
E[X] = \frac{p_j p_k}{n^2}
$$

It also has support for images.
````

When you open this text in an editor, or in GitLab, or on GitHub, you will see

---
### This is a markdown document

> It is just a simple file filled with text, like a `.txt` file or a `.csv` file

When you use things like _underscores_ and **stars** it becomes a nice formatted output.

You can do things like [links to websites](www.google.com)

- You
- can
- have
- lists

```python
print("You can even write python code and it will show it with formatting")
```

<details>
  <summary>You can even have expandable sections</summary>
  
  ## Heading
  1. A numbered
  2. list
     * With some
     * Sub bullets
</details>

Markdown has support for maths equations, both inline $\alpha = 5/2$, and in big mode

$$
E[X] = \frac{p_j p_k}{n^2}
$$

It also has support for images.

---
</details>

Markdown files work really well with version control, so most version control websites like GitHub and GitLab have very strong support for them. Markdown documents can do lots of the things that a word document can. They are very powerful.

You can try an online interactive markdown editor here: https://dillinger.io/

The RAP team at NHS Digital have written all of their documentation in markdown files, see here: https://github.com/NHSDigital/rap-community-of-practice



## What is the scope of the documentation we put in our code?

### Basic explanation of the problem

We are currently writing documentation for the following reasons:
1. Small helpful hints and explanations, written into the Python code
2. Documentation to explain how a process works, like the stratified weighted mean (normally in a markdown file)
3. Documentation to explain design decisions (in a markdown file)

In our code, we are writing the docs that we view as necessary for people to be able to understand the code.

The trouble is, our code does some complex maths. We write docs to explain why we do the complex maths, but then we end up duplicating information that is in the methodology report.

The question is, what is it our job to explain in the documentation? When we have the code that creates the column for the different strata, do we explain what the strata mean? Do we then go and explain why those strata were picked? Doesn't this duplicate the methodology report that explains it? Where do we stop?

The idea of RAP is that it is meant to help increase communication about how data is being used. The idea is that the code won't lie and people (other analysts, the public, researchers) can see exactly what transformations are being done to the data. Does this not suggest that it is in the codebase where the accurate and complete explanation of the process should lie, rather than in some PDF methodology report?

### Options regarding overlap and duplication between the methodology report and the code docs

1. **Don't put as much stuff in the docs**

   This has the downside of making it harder for the person who's reading the code to understand what's going on. Also, you miss out on having the explanation of the maths right next to the code that does the maths.

2. **Put everything in both**

   This has the downside of duplicating effort, and also means the people reading the code _and_ the methodology report end up having to read stuff twice.

3. **Don't put as much stuff in the methodology report**

   This has the downside of forcing people who want to read the methodology into going onto GitHub. However, there are ways of making the docs nice and easy to read on GitHub, even if you're not a tech whiz.

4. **Directly exporting from the markdown to the methodology report**

   This would save us from having to write stuff twice, although working out how to do that export stuff might be a little tricky.

Markdown files on git also have the downside of meaning that everyone who interacted with them would have to use git. For people familiar with word documents the process of working on git with markdown would take getting used to.

On the other hand, being on git is also an upside. The version control features of git mean that you'd have very clear tracking of changes to a document.

Also, if code and documentation were stored together, then when the process were updated it would be easier for people to ensure everything was up to date. Everything would be together, stored coherently.

### What are the things that could be in scope for the ASCS docs?

Together we need to decide what is within scope for the documentation from the following list of things:

- Maths
- Explanation of the reasoning behind doing certain maths
- Survey features (like describing the 4 strata)
- Explanation of the reasoning behind having different survey features (like the 4 strata)
- Coding design decisions
- Examples of how to use certain bits of our code
- Explanations of the data flow through our program
- Outputs of the publication
- Deeper explanation of what we want from the outputs of the publication, why we collect them, what they show us
- Recording the structure of the data inputs to the publication (a data dictionary explaining what the columns are)
- When things change, will we record the changes that have been made to the code in a changelog file (as is standard practice). Will we record the changes to the survey? Will we record the reasoning?

There may be more things that haven't occured to me yet.


## What quality standard do we hold the docs to?

I presume there is a quality checking process that happens before the methodology report is released. It presumably checks that stuff makes sense and that there aren't gramatical errors.

If the methodology report has a quality checking process, it seems only right that the documentation has some sort of quality checking process. Reasearchers are going to end up reading both to understand how ASCS works.

## Within the codebase, how do we structure our documentation?

- Do we put it in a `docs` folder?
- Do we put the markdown files in the same folders as the code that they are relevant to?
- How much information do we put in docstrings?
- Where do design decisions go?
- Where do explanations of process go?

Also, there exist tools that can make really nice documentation that is readable in a web browser: https://www.sphinx-doc.org/en/master/index.html

Is it worth considering using those?

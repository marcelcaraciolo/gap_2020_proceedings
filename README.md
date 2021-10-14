# GAP 2020 Proceedings TCC

This is Marcel Caraciolo Conclusion Thesis for the Specialization Program Agile Management Projects at CESAR SCHOOL University.

https://www.cesar.school/gestao-agil-de-projetos/

### General Information and Guidelines for Authors:

- Papers are formatted using reStructuredText.
- Example papers are provided in `papers/00_bibderwalt` and `papers/00_vanderwalt`.
    - These papers provide examples of how to:
        - Label figures, equations and tables
        - Use math markup
        - Include code snippets
    - `00_bibderwalt` shows how to use a bib file for citations.
- For your paper to be found by the build system at http://procbuild.scipy.org
  your PR needs to have a title that begins with "Paper:". If you do not do
  this, the co-chairs will change your title on your behalf.
- Authors may include a project or consortium (e.g. [The Jupyter Project](https://raw.githubusercontent.com/scipy-conference/scipy_proceedings/2018/papers/project_jupyter/paper.rst))
- There must be at least one corresponding author, and this must be a specific person with a valid email address
- All citations that have DOIs should include those DOIs in the paper's
  references section, see [`mybib.bib`](./papers/00_bibderwalt/mybib.bib).
- All figures and tables should have captions.
- Figures and tables should be positioned inline, close to their explanatory text.
- License conditions on images and figures must be respected (Creative Commons,
  etc.).
- Images and figures should be reasonably sized and formatted for viewing online; typically a few hundred kilobytes and less than 1 MB.
- Code snippets should be formatted to fit inside a single column without
  overflow.
- Avoid custom LaTeX markup where possible.
- Do not modify any files outside of your paper directory.
- The compiled version of the paper (PDF) should be at most 8 pages,
  including figures but not including references.

### Author Workflow

Below we outline the steps to submit a paper.

Before you begin, you should have a GitHub account. If we refer to `<username>`
in code examples, you should replace that with your GitHub username.

More generally, angle brackets with a value inside are meant to be replaced with
the value that applies to you.

For example, if your GitHub username was `mpacer`, you would transform

```
git clone https://github.com/<username>/scipy_proceedings
```

into:

```
git clone https://github.com/mpacer/scipy_proceedings
```

#### Author workflow steps

1. Get a local copy of the `scipy_proceedings` repo.
2. Update your local copy of the `scipy_proceedings` repo.
3. [Create a new branch](#creating-a-new-branch-based-off-of-2021) for your paper based off the latest `2021` branch.
    - If you submit multiple papers, you will need a new branch for each.
4. [Set up your environment](#setting-up-your-environment).
5. [Write your paper](#write-your-paper), [commit changes](#commit-your-changes), and [build your paper](#build-your-paper)
6. [Create a PR](#create-a-paper-pr) or [push changes to your PR's branch](#push-your-changes) and [check your paper](#check-your-paper) on http://procbuild.scipy.org.
    - If you want to alter the build system, do not include it in your
      submission's PR, create a separate PR against `dev`
      ([see below](creating-build-system-prs) for more details).
7. Repeat steps 5 and 6, while also responding to reviewer feedback.

#### Getting a local copy of the scipy_proceedings repo

- If you do not have a GitHub account, create one.
- Fork the
  [scipy_proceedings](https://github.com/scipy-conference/scipy_proceedings)
  repository on GitHub.
- Clone the repo locally
    - `git clone https://github.com/<username>/scipy_proceedings`
    - `cd scipy_proceedings/`
- Add the `scipy-conference` repository as your `upstream` remote
    - `git remote add upstream https://github.com/scipy-conference/scipy_proceedings`

If you run `git remote -v  ` you should see something like the following:
```
origin	https://github.com/<username>/scipy_proceedings.git (fetch)
origin	https://github.com/<username>/scipy_proceedings.git (push)
upstream	https://github.com/scipy-conference/scipy_proceedings.git (fetch)
upstream	https://github.com/scipy-conference/scipy_proceedings.git (push)
```

#### Getting the latest `2021` branch

- Fetch the latest version of the `scipy_proceedings` repo
    - `git fetch upstream`
- Check out the upstream `2021` branch
    - `git checkout -b 2021 --track upstream/2021`

#### Creating a new branch based off of `2021`

If you are submitting only one paper, you can use the `2021` branch directly.

Otherwise, you will need to create a new branch based on `2021` and set its
upstream to origin.

```
git checkout 2021
git checkout -b <your_branch_name>
git push --set-upstream origin <your_branch_name>
```

#### Setting up your environment

- Create a new environment (using your choice of environment manager, e.g., `pyenv` or `conda`).
- Install/update the required python libraries (`pip install -U -r requirements.txt`).
- Install LaTeX and any other non-python dependencies
- Create a new directory `papers/<your_directory_name>`
    - if you are submitting one paper, we recommend you use `<firstname_surname>`
    - if you are submitting more than one paper, you will need to use a different
      directory name for each paper

#### Write your paper

- Copy an example paper into your directory.
    - You must have only one reST file in the top level of `<your_directory_name>`.
- As you make changes to your paper, commit those changes in discrete chunks.

#### Commit your changes

- Commit any changes inside the `paper/<your_directory_name>`
- When you push your commits to your PR's branch, the paper will be autobuilt
- Do not commit any changes to files outside of your paper directory.

If you want to change the way the build system works, we use a separate
submission procedure ([see below](creating-build-system-prs)).

#### Build your paper

- Run `./make_paper.sh papers/firstname_surname` to make a PDF of your paper
- Check the output in `output/<your_directory_name>/paper.pdf`.
- Check that this output matches what you see on the
  [build server](http://procbuild.scipy.org).

## Requirements

 - Install the requirements in the requirements.txt file: `pip install -r requirements.txt`
 - IEEETran (often packaged as ``texlive-publishers``, or download from
   [CTAN](http://www.ctan.org/tex-archive/macros/latex/contrib/IEEEtran/)) LaTeX
   class
 - AMSmath LaTeX classes (included in most LaTeX distributions)
 - alphaurl (often packaged as ``texlive-bibtex-extra``, or download from
   [CTAN](https://www.ctan.org/pkg/urlbst)) urlbst BibTeX style

### Debian-like distributions:

```
sudo apt-get install python-docutils texlive-latex-base texlive-publishers \
                     texlive-latex-extra texlive-fonts-recommended \
                     texlive-bibtex-extra
```

Note you will still need to install `docutils` with `pip` even on a Debian system.

### Fedora

On Fedora, the package names are slightly different:

```
su -c `dnf install python-docutils texlive-collection-basic texlive-collection-fontsrecommended texlive-collection-latex texlive-collection-latexrecommended texlive-collection-latexextra texlive-collection-publishers texlive-collection-bibtexextra`
```

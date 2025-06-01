# Table of Contents for README.md

1. [Introduction](#introduction)  
2. [Student Requirements](#student-requirements)  
3. [History](#history)  
   3.1 [License](#license)  
   3.2 [Key Features](#key-features)  
   3.3 [Contributions](#contributions)  
4. [GitHub Pages Setup](#github-pages-setup)  
   4.1 [Activate GitHub Pages Actions](#activate-github-pages-actions)  
   4.2 [Update `_config.yml`](#update-_configyml)  
   4.3 [Set Repository Name in Makefile](#set-repository-name-in-makefile)  
   4.4 [Tool Requirements](#tool-requirements)  
   4.5 [Development Environment Setup](#development-environment-setup)  
       4.5.1 [Clone Repo](#clone-repo)  
       4.5.2 [Windows WSL and Ubuntu Users](#windows-wsl-and-ubuntu-users)  
       4.5.3 [macOS Users](#macos-users)  
       4.5.4 [Kasm Cloud Desktop Users](#kasm-cloud-desktop-users)  
5. [Run Server on Localhost](#run-server-on-localhost)  
   5.1 [Bundle Install](#bundle-install)  
   5.2 [Start the Server](#start-the-server)  
   5.3 [Load Web Application into the Browser](#load-web-application-into-the-browser)  
   5.4 [Regeneration of Web Application](#regeneration-of-web-application)  
   5.5 [Other `make` Commands](#other-make-commands)  
       5.5.1 [Stop the Preview Server](#stop-the-preview-server)  
       5.5.2 [Clean the Local Web Application Environment](#clean-the-local-web-application-environment)  
       5.5.3 [Observe Build Errors](#observe-build-errors)  
6. [Development Support](#development-support)  
   6.1 [File Naming in `_posts` and `_notebooks`](#File-Names-in-_posts-_notebooks)  
   6.2 [Tags](#tags)  
   6.3 [Search](#search)  
   6.4 [Navigation Bar](#navigation-bar)  
   6.5 [Blog Page](#blog-page)  
   6.6 [SASS Support](#sass-support)  
   6.7 [Includes](#includes)  
   6.8 [Layouts](#layouts)  
   6.9 [Metadata](#metadata)

## Introduction

The Open Coding Society community provides courses and projects to help students in Computer Science and Software Engineering. It offers resources like tech talks, code examples, and educational blogs. Students can customize their GitHub Pages to support their learning as they progress through courses using JavaScript, Python/Flask, and Java/Spring.  

## Student Requirements

Students must maintain a blog throughout the course and review their GitHub Pages at each midterm and final, compiling their work for each grading period. Both students and teachers use GitHub Pages for lessons, coding exercises, JavaScript games, and as a frontend for full-stack apps. Information can be shared via files, templates, forks, and other collaborative methods.

---

## History

This project is now in its 4th major revision (4.0). It began as a fork of Fastpages, but has since evolved into an independent platform. The transition away from Fastpages was prompted by its deprecation and a shift in direction by its original authors toward Quarto, which no longer aligned with the needs of our community.

Open Coding Society GitHub Pages projects are intentionally designed to be more hands-on and technically rigorous, emphasizing raw development and blogging. The goal is to provide a platform that supports deep technical learning, rather than a lightweight or out-of-the-box solution.

### License

This project continues to use the Apache license inherited from its Fastpages origins. While the licensing remains, the majority of the codebase has significantly diverged and evolved, reflecting the project's shift toward independent, technically rigorous development.

### Key Features

- **Code Examples**: Practical coding examples in JavaScript (including an rpg and platformer game) and frontend code for user databases using Python and Java backends.
- **Educational Blogs**: Instructional content on topics such as developer tools setup, AWS deployment, SQL databases, machine learning, and data structures. Includes interactive lessons and coding challenges using Jupyter Notebooks.
- **Tools and Integrations**: GitHub Actions for blog publishing, Utterances for blog commenting, local development support via Makefile and scripts, styling with the Minima or Minimal Themes and SASS, and integration with GitHub Projects and Issues.

### Contributions

- **Notable Contributions**: Highlights significant contributions to the project, including theme development, search and tagging functionality, GitHub API integration, and the incorporation of GitHub Projects into GitHub pages. Contributors such as Tirth Thakker, Mirza Beg, and Toby Ledder have played crucial roles in these developments.

- **Blog Contributions**:  Often students contribute articles and blogs to this project.  Their names are typically listed in the front matter of their contributing post.

---

## GitHub Pages setup

The absolutes in setup up...

**Activate GitHub Pages Actions**: This step involves enabling GitHub Pages Actions for your project. By doing so, your project will be automatically deployed using GitHub Pages Actions, ensuring that your project is always up to date with the latest changes you push to your repository.

- On the GitHub website for the repository go to the menu: Settings -> Pages ->Build
- Under the Deployment location on the page, select "GitHub Actions".

**Update `_config.yml`**: You need to modify the `_config.yml` file to reflect your repository's name. This configuration is crucial because it ensures that your project's styling is correctly applied, making your deployed site look as intended rather than unstyled or broken.

```text
github_repo: "student_2025" 
baseurl: "/student_2025"
```

- Change `owner_name` to your full name (ex. Jane Doe)
- Change `github_username` to your GitHub username (ex. jdoe123)
- Change `github_repo` to the name of your repository (ex. jane_student)
- Change `baseurl` to a slash and the name of your repository (ex. `/jane_student`)

**GitHub Pages Setup using `_config.yml`**

 - Change `owner_name` to your full name (ex. Jane Doe)
 - Change `github_username` to your GitHub username (ex. jdoe123)
 - Change `github_repo` to the name of your repository (ex. jane_student)
 - Change `baseurl` to a slash and the name of your repository (ex. `/jane_student`)\
 - Choose between [jekyll/minima](https://jekyll.github.io/minima/) or [pages-themes/minimal@v0.2.0](https://pages-themes.github.io/minimal/) by changing the value of `remote_theme`

**Changing Navbar setup in GitHub Pages Theme**

 1. Change `remote_theme` to your desired value in `_config.yml` (ex. `remote_theme: jekyll/minima` or `remote_theme: pages-themes/minimal@v0.2.0`)
 2. If using jekyll/minima, add the relative path to your desired pages using `nav_pages: `.
 3. If using minimal, set `nav: true` in the front matter of the desired page (front matter is the YAML enclosed in "`---`" at the beginning of a file)

**Set Repository Name in Makefile**: Adjust the `REPO_NAME` variable in your Makefile to match your GitHub repository's name. This action facilitates the automatic updating of posts and notebooks on your local development server, improving the development process.

```make
# Configuration, override port with usage: make PORT=4200
PORT ?= 4100
REPO_NAME ?= student_2025
LOG_FILE = /tmp/jekyll$(PORT).log
```

### Tool requirements

All `GitHub Pages` websites are managed on GitHub infrastructure and use GitHub version control.  Each time we change files in GitHub it initiates a GitHub Action, a continuous integration and development toolset, that rebuilds and publishes the site with Jekyll.  

- GitHub uses `Jekyll` to transform your markdown and HTML content into static websites and blogs. [Jekyll](https://jekyllrb.com/).
- A Linux shell is required to work with this project integration with GitHub Pages, GitHub and VSCode.  Ubuntu is the preferred shell, though MacOS shell is supported as well.  There will be some key setup scripts that follow in the README.
- Visual Studio Code is the Open Coding Society author's preferred code editor and extensible development environment.  VSCode has a rich ecosystem of developer extensions that ease working with GitHub Pages, GitHub, and many programming languages.  Setting up VSCode and extensions will be elaborated upon in this document.
- An anatomy section in this README will describe GitHub Pages and conventions that are used to organize content and files.  This includes file names, key coding files, metadata tagging of blogs, styling tooling for blogs, etc.

### Development Environment Setup

Comprehensive start. A topic-by-topic guide to getting this project running is published [here](https://nighthawkcoders.github.io/portfolio_2025/devops/tools/home).

Quick start.  A quick start below is a reminder, but is dependent on your knowledge.  Only follow this instruction if you need a refresher.  Always default to the comprehensive start if any problem occurs.

#### Clone Repo

Run these commands to obtain the project, then locate into the project directory with the terminal, install an extensive set of tools, and make.

```bash
git clone <this-repo> # git clone https://github.com/nighthawkcoders/student_2025.git 
cd <repo-dir>/scripts # cd student_2025
```

#### Windows WSL and/or Ubuntu Users

- Execute the script: `./activate_ubuntu.sh`

#### macOS Users

- Execute the script: `./activate_macos.sh`

#### Kasm Cloud Desktop Users

- Execute the script: `./activate.sh`

## Run Server on localhost

To preview the project you will need to "make" the project.

### Bundle install

The very first time you clone run project you will need to run this Ruby command as the final part of your setup.

```bash
bundle install
```

### Start the Server  

This requires running terminal commands `make`, `make stop`, `make clean`, or `make convert` to manage the running server.  Logging of details will appear in the terminal.   A `Makefile` has been created in the project to support commands and start processes.

Start the server, this is the best choice for initial and iterative development.  Note. after the initial `make`, you should see files automatically refresh in the terminal on VSCode save.

  ```bash
  make
  ```

### Load web application into the Browser

Start the preview server in the terminal,
The terminal output from `make` shows the server address. "Cmd" or "Ctl" click the http location to open the preview server in a browser. Here is an example Server address message, click on the Server address to load:...

  ```text
  http://0.0.0.0:4100/student_2025/
  ```

### Regeneration of web application

Save on ".ipynb" or ".md" file activiates "regeneration". An example terminal message is below.  Refresh the browser to see updates after the message displays.

  ```text
  Regenerating: 1 file(s) changed at 2023-07-31 06:54:32
      _notebooks/2024-01-04-cockpit-setup.ipynb
  ```

### Other "make" commands

Terminal messages are generated from background processes.  At any time, click return or enter in a terminal window to obtain a prompt.  Once you have the prompt you can use the terminal as needed for other tasks.  Always return to the root of project `cd ~/vscode/student_2025` for all "make" actions.

#### Stop the preview server

Stopping the server ends the web server applications running process.  However, it leaves constructed files in the project in a ready state for the next time you run `make`.

  ```bash
  make stop
  ```

### Clean the local web application environment

This command will top the server and "clean" all previously constructed files (ie .ipynb -> .md). This is the best choice when renaming files has created duplicates that are visible when previewing work.

  ```bash
  make clean
  ```

### Observe build errors

Test Jupyter Notebook conversions (ie .ipynb -> .md), this is the best choice to see if an IPYNB conversion error is occurring.

  ```bash
  make convert
  ```

---

## Development Support

### File Names in "_posts", "_notebooks"

There are two primary directories for creating blogs.  The "_posts" directory is for authoring in markdown only.  The "_notebooks" allows for markdown, pythons, javascript and more.

To name a file, use the following structure (If dates are in the future, review your config.yml setting if you want them to be viewed).  Review these naming conventions.

- For markdown files in _posts:
  - year-month-day-fileName.md
    - GOOD EXAMPLE: 2021-08-02-First-Day.md
    - BAD EXAMPLE: 2021-8-2-first-day.md
    - BAD EXAMPLE: first-day.md
    - BAD EXAMPLE: 2069-12-31-First-Day.md

- For Jupyter notebooks in _notebooks:
  - year-month-day-fileName.ipynb
    - GOOD EXAMPLE: 2021-08-02-First-Day.ipynb
    - BAD EXAMPLE: 2021-8-2-first-day.ipynb
    - BAD EXAMPLE: first-day.ipynb
    - BAD EXAMPLE: 2069-12-31-First-Day.ipynb

### Tags

Tags are used to organize pages by their tag the way to add tags is to add the following to your front matter such as the example seen here `categories: [Tools]` Each item in the same category will be lumped together to be seen easily on the search page.

### Search

All pages can be searched for using the built-in search bar. This search bar will search for any word in the title of a page or in the page itself. This allows for easily finding pages and information that you are looking for. However, sometimes this may not be desirable so to hide a page from the search you need to add `search_exclude: true` to the front matter of the page. This will hide the page from appearing when the viewer uses search.

### Navigation Bar

To add pages to the top navigation bar use _config.yml to order and determine which menus you want and how to order them.  Review the_config.yml in this project for an example.

### Blog Page

There is a blog page that has options for images and a description of the page. This page can help the viewer understand what the page is about and what they can expect to find on the page. The way to add images to a page is to have the following front matter `image: /images/file.jpg` and then the name of the image that you want to use. The image must be in the `images` folder. Furthermore, if you would like the file to not show up on the blog page `hide: true` can be added to the front matter.

### SASS support

Open Coding Society support a variety of different themes that are each overlaid on top of minima. To use each theme, go to the "_sass/minima/custom-styles.scss" file and simply comment or uncomment the theme you want to use.

To learn about the minima themes search for "GitHub Pages minima" and review the README.

To find a new theme search for "Github Pages Themes".

### Includes

- Open Coding Society uses liquid syntax to import many common page elements that are present throughout the repository. These common elements are imported from the _includes directory. If you want to add one of these common elements, use liquid syntax to import the desired element to your file. Here’s an example of the liquid syntax used to import: `{%- include posts/post_list.html -%}` Note that the liquid syntax is surrounded by curly braces and percent signs. This can be used anywhere in the repository.

### Layouts

- To use or create a custom page layout, make an HTML page inside the _layouts directory, and when you want to use that layout in a file, use the following front matter `layout: [your layout here]`.  All layouts will be written in liquid to define the structure of the page.

### Metadata

Metadata, also known as "front matter", is a set of key-value pairs that can provide additional information to GitHub Pages about .md and .ipynb files. This can and probably will be used in other file types (ie doc, pdf) if we add them to the system.

In the front matter, you can also define things like a title and description for the page.  Additional front matter is defined to place content on the "Computer Science Lab Notebook" page.  The `courses:` key will place data on a specific page with the nested `week:` placing data on a specific row on the page.  The `type:` key in "front matter" will place the blog under the plans, hacks(ToDo), and tangibles columns.

- In our files, the front matter is defined at the top of the page or the first markdown cell.

  - First, open one of the .md or .ipynb files already included in either your _posts|_notebooks folder.

  - In the .md file, you should notice something similar to this at the top of the page. To see this in your .ipynb files you will need to double-click the markdown cell at the top of the file.

  ```yaml
  ---
  toc: true
  comments: true
  layout: post
  title: Jupyter Python Sample
  description: Example Blog!!!  This shows code and notes from hacks.
  type: ccc
  courses: { csa: {week: 5} }
  ---
  ```

- The front matter will always have '---' at the top and bottom to distinguish it and each key-value pair will be separated by a ':'.

- Here we can modify things like the title and description.

- The type value will tell us which column this is going to appear under the time box supported pages.  The "ccc" stands for Code, Code, Code.

- The courses will tell us which menu item it will be under, in this case, the `csa` menu, and the `week` tells it what row (week) it will appear under that menu.


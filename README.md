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
7. [Lessons](#lessons)  
   7.1 [Help Page](#help-page)
   7.2 [Lesson Creation](#lesson-creation)   

# Introduction

Open Coding Society is a project designed to support students in their Computer Science and Software Engineering education. It offers a wide range of resources including tech talks, code examples, and educational blogs.

GitHub Pages can be customized by the blogger to support computer science learnings as the student works through the pathway of using Javascript, Python/Flask, Java/Spring.  

## Student Requirements

Open Coding Society students will be required to review their personal GitHub Pages at each midterm and final. This review will contain a compilation of personal work performed within each significant grading period.

In general, Students and Teachers are expected to use GitHub pages to build lessons, complete classroom hacks, perform work on JavaScript games, and serve as a frontend to full-stack applications.

Exchange of information could be:

1. sharing a file: `wget "raw-link.ipynb"`
2. creating a template from this repository
3. sharing a fork among team members
4. etc.

---

## History

This project is in its 3rd revision (aka 3.0).

The project was initially based on Fastpages. But this project has diverged from those roots into an independent entity. The decision to separate from Fastpages was influenced by the deprecation of Fastpages by authors. It is believed by our community that the authors of Fastpages turned toward Quatro. After that change of direction, Fastpages did not align with the Teacher's goals and student needs. The Open Coding Society project has more of a raw development blogging need.

### License

The Apache license has its roots in Fastpages. Thus, it carries its license forward. However, most of the code is likely unrecognizable from those roots.

### Key Features

- **Code Examples**: Provides practical coding examples in JavaScript, including a platformer game, and frontend code for user databases using Python and Java backends.
- **Educational Blogs**: Offers instructional content on various topics such as developer tools setup, deployment on AWS, SQL databases, machine learning, and data structures. It utilizes Jupyter Notebooks for interactive lessons and coding challenges.
- **Tools and Integrations**: Features GitHub actions for blog publishing, Utterances for blog commenting, local development support via Makefile and scripts, and styling with the Minima Theme and SASS. It also includes a new integration with GitHub Projects and Issues.

### Contributions

- **Notable Contributions**: Highlights significant contributions to the project, including theme development, search and tagging functionality, GitHub API integration, and the incorporation of GitHub Projects into GitHub Pages. Contributors such as Tirth Thakker, Mirza Beg, and Toby Ledder have played crucial roles in these developments.
- **Blog Contributions**: Often students contribute articles and blogs to this project. Their names are typically listed in the front matter of their contributing post.

---

## GitHub Pages Setup

The absolutes in setup up...

### Activate GitHub Pages Actions

This step involves enabling GitHub Pages Actions for your project. By doing so, your project will be automatically deployed using GitHub Pages Actions, ensuring that your project is always up to date with the latest changes you push to your repository.

- On the GitHub website for the repository go to the menu: Settings -> Pages -> Build
- Under the Deployment location on the page, select "GitHub Actions".

### Update `_config.yml`

You need to modify the `_config.yml` file to reflect your repository's name. This configuration is crucial because it ensures that your project's styling is correctly applied, making your deployed site look as intended rather than unstyled or broken.

```yaml

github_repo: "student_2026"
baseurl: "/student_2026"

```

### Set Repository Name in Makefile

Adjust the `REPO_NAME` variable in your Makefile to match your GitHub repository's name. This action facilitates the automatic updating of posts and notebooks on your local development server, improving the development process.

```make
# Configuration, override port with usage: make PORT=4200
PORT ?= 4100
REPO_NAME ?= student_2026
LOG_FILE = /tmp/jekyll$(PORT).log
```

### Tool Requirements

All `GitHub Pages` websites are managed on GitHub infrastructure and use GitHub version control. Each time we change files in GitHub it initiates a GitHub Action, a continuous integration and development toolset, that rebuilds and publishes the site with Jekyll.

- GitHub uses `Jekyll` to transform your markdown and HTML content into static websites and blogs. [Jekyll](https://jekyllrb.com/).
- A Linux shell is required to work with this project integration with GitHub Pages, GitHub and VSCode. Ubuntu is the preferred shell, though MacOS shell is supported as well. There will be some key setup scripts that follow in the README.
- Visual Studio Code is the Open Coding Society author's preferred code editor and extensible development environment. VSCode has a rich ecosystem of developer extensions that ease working with GitHub Pages, GitHub, and many programming languages. Setting up VSCode and extensions will be elaborated upon in this document.

### Development Environment Setup

Comprehensive start. A topic-by-topic guide to getting this project running is published [here](https://opencodingsociety.github.io/portfolio_2025/devops/tools/home).

Quick start. A quick start below is a reminder, but is dependent on your knowledge. Only follow this instruction if you need a refresher. Always default to the comprehensive start if any problem occurs.

#### Clone Repo

Run these commands to obtain the project, then locate into the project directory with the terminal, install an extensive set of tools, and make.

```bash
git clone <this-repo> # git clone https://github.com/opencodingsociety/student_2026.git
cd <repo-dir>/scripts # cd student_2026
```

#### Windows WSL and/or Ubuntu Users

- Execute the script: `./activate_ubuntu.sh`

#### macOS Users

- Execute the script: `./activate_macos.sh`

#### Kasm Cloud Desktop Users

- Execute the script: `./activate.sh`

---

## Run Server on Localhost

To preview the project you will need to "make" the project.

### Bundle Install

The very first time you clone run project you will need to run this Ruby command as the final part of your setup.

```bash
bundle install
```

### Start the Server  

This requires running terminal commands `make`, `make stop`, `make clean`, or `make convert` to manage the running server. Logging of details will appear in the terminal. A `Makefile` has been created in the project to support commands and start processes.

Start the server, this is the best choice for initial and iterative development. Note: after the initial `make`, you should see files automatically refresh in the terminal on VSCode save.

```bash
make
```

### Load Web Application into the Browser

Start the preview server in the terminal,
The terminal output from `make` shows the server address. "Cmd" or "Ctl" click the http location to open the preview server in a browser. Example:

```text
http://0.0.0.0:4100/student_2026/
```

### Regeneration of Web Application

Save on ".ipynb" or ".md" file activates "regeneration". Example message:

```text
Regenerating: 1 file(s) changed at 2023-07-31 06:54:32
    _notebooks/2024-01-04-cockpit-setup.ipynb
```

### Other `make` Commands

#### Stop the Preview Server

```bash
make stop
```

#### Clean the Local Web Application Environment

```bash
make clean
```

#### Observe Build Errors

```bash
make convert
```

---

## Development Support

### File Naming in `_posts`, `_notebooks`

There are two primary directories for creating blogs. `_posts` is for markdown (`.md`) only; `_notebooks` allows for Jupyter Notebooks (`.ipynb`) or markdown.

Markdown files in `_posts`:

- `year-month-day-fileName.md`
  - Example: `2021-08-02-First-Day.md`

Jupyter notebooks in `_notebooks`:

- `year-month-day-fileName.ipynb`
  - Example: `2021-08-02-First-Day.ipynb`

### Tags

Tags organize pages for search and grouping.

Example front matter:

```yaml
categories: [Tools]
```

### Search

Use the search bar to find pages. To exclude a page from search:

```yaml
search_exclude: true
```

### Navigation Bar

Use `nav: true` in a page's front matter to make it appear in the navigation bar for the **Minimal** theme.

Example:

```yaml
nav: true
title: About
```

The order of items can be customized in `_config.yml` if using Minima.

### Blog Page

To add images and descriptions:

```yaml
image: /images/file.jpg
hide: true # optional
```

### SASS Support and Theme Switching

We support both **Minima** and **Minimal** themes.

- For **Minima**: The default theme with extensive SASS support.
- For **Minimal**: Custom Tailwind-based layout with navigation controlled by `nav: true` in front matter.

Theme switching is handled via `_config.yml`:

```yaml
theme: minima # for classic Minima
# theme: minimal # for Tailwind-enhanced minimal layout
```

Or for custom theme variants:

```yaml
remote_theme: opencodingsociety/your-theme-name
```

Customization of the SASS stylesheets can be done inside `_sass/minima/custom-styles.scss`.

### Includes

We use Liquid includes for common HTML fragments. Example:

```liquid
{%- include posts/post_list.html -%}
```

### Layouts

Custom page layouts can be placed inside `_layouts/`.

Front matter to use them:

```yaml
layout: your-layout
```

### Metadata

Use YAML front matter to define metadata:

```yaml
---
toc: true
comments: true
layout: post
title: Jupyter Python Sample
description: Example Blog!!! This shows code and notes from hacks.
type: ccc
courses: { csa: {week: 5} }
---
```

### Issue Templates and Contribution Guidelines

We provide templates for Issue creation and Pull Requests.

Templates are located in:

```
.github/ISSUE_TEMPLATE/bug_report.md
.github/ISSUE_TEMPLATE/feature_request.md
.github/PULL_REQUEST_TEMPLATE.md
```

- **Bug Reports**: Fill out the issue template to report a bug.
- **Feature Requests**: Use the feature request template to propose improvements.
- **Pull Requests**: Pull requests must fill out the provided PR template before merging.

This ensures all contributions follow a consistent standard.

---

# Lessons

## Help Page
## Overview
This documentation covers HTML lesson layouts and interactive features for coding education. The system uses Jekyll with various interactive components to create engaging learning experiences.

## Core Files

### 1. `lesson.html` - Base Template
The foundation template providing:
- Responsive CSS styling with dark theme
- JavaScript for animations and interactivity
- Local storage for student responses
- Code execution capabilities (JavaScript and Python)
- Feedback poll system

**Usage:** Serves as the base layout - don't modify directly unless changing global styles.

### 2. `cover.html` - Sample Lesson
Example lesson demonstrating feature integration:

```yaml
---
layout: lesson
title: Introduction to Functions
video_url: https://www.youtube.com/watch?v=zvzjaqMBEso
hack_prompt: "Write a Python function that calculates factorial"
permalink: /lesson-url
---
```

**Content includes:** Explanations, examples, and interactive elements via "include" directives.

## Interactive Features

### Video Player
**Setup:**
1. Add `video_url: VIDEO_ID` to lesson frontmatter
2. Include `video.html` in content

**Features:** HD playback, responsive design, fullscreen support

### Live Whiteboard (`whiteboard.html`)
**Teacher workflow:**
1. Create board at whiteboard.team
2. Get board code from URL (e.g., `svVDABAW`)
3. Students enter code to view live drawing

**Features:** Real-time updates, fullscreen mode, color picker

### AI Comprehension Checker
**Student usage:**
1. Select question type (Multiple Choice/Short Answer)
2. Choose difficulty (Easy/Medium/Hard)
3. Generate AI questions based on lesson content
4. Receive immediate feedback

**Requirements:** Valid Groq API key for llama3-8b-8192 model

### Popcorn Hack (Coding Challenges)
**Setup:** Add `hack_prompt` to lesson frontmatter

**Student features:**
- Code in Python or JavaScript
- Save responses locally
- Execute code with output display
- Clear and restart functionality

### Flashcards System

#### Teacher-Provided (`flashcards.html`)
**Setup:** Create `_data/flashcards.yml`:
```yaml
cards:
  - term: Loop
    definition: A programming structure that repeats code
  - term: Variable
    definition: A container for storing data
```

#### Student-Created (`flashcard-notes.html`)
**Features:**
- Create custom term/definition pairs
- Practice with flip animations
- Progress tracking
- Local storage for persistence

### Multiplayer Quiz Game (`game.html`)
**Technical stack:**
- Frontend: HTML5, Socket.IO, CSS3
- Backend: Flask, Flask-SocketIO
- Content: YAML question files


**Features:**
- Real-time multiplayer competition
- Difficulty-based timing
- Live leaderboard
- Progress tracking

**Setup:**
1. Configure `_data/game_questions.yml`
2. Run Flask backend with Socket.IO
3. Update CORS settings for deployment

### Feedback Poll (`poll.html`)
**Integration:**
1. Create Google Form with thumbs up/down field
2. Link to Google Sheet
3. Publish sheet to web
4. Update JavaScript with form URL and field IDs

**Features:**
- Thumbs up/down voting
- Optional text comments
- Live response dashboard
- Google Sheets integration

### Interactive Sidebar
**Components:**
- **Dictionary:** Word definitions and examples
- **Notes:** Personal note-taking with highlight integration
- **Read Text:** Text-to-speech for selected content
- **Highlight:** Color-coded text marking with note attachments

**Student workflow:**
1. Click sidebar icons to access features
2. Select text for reading or highlighting
3. Add contextual notes linked to highlights
4. All data stored locally

## Quick Start Guide

1. **Copy `cover.html`** as template for new lessons
2. **Update frontmatter** with lesson-specific content:
   - `title`: Lesson name
   - `video_url`: YouTube video ID
   - `hack_prompt`: Coding challenge
   - `permalink`: Lesson URL
3. **Customize content** within `<div id="lesson-content">`
4. **Add features** using `include feature.html` tags
5. **Create supporting files** (flashcards.yml, game_questions.yml, etc.)

## Best Practices

### For Teachers
- Test all interactive features before lessons
- Provide clear instructions for student interactions
- Use different highlight colors for categorization
- Pre-configure API keys and external services

### For Students
- Use highlights and notes for active reading
- Practice with flashcards for retention
- Engage with AI comprehension checks
- Provide feedback through polls

#### Sidebar Which Includes:
### Sidebar Features

#### Sidebar Overview
The interactive sidebar enhances the learning experience by providing quick access to essential tools. It is designed for seamless integration with lesson content.

#### Components
2. **Notes**
  - Take personal notes while studying.
  - Attach notes to highlighted text for better organization.

3. **Read Text**
  - Convert selected text to speech for auditory learning.
  - Adjustable playback speed and voice options.

4. **Highlight**
  - Mark text with color-coded highlights.
  - Categorize highlights for better comprehension.

#### Student Workflow
- Click sidebar icons to access features.
- Select text for reading or highlighting.
- Add contextual notes linked to highlights.
- All data is stored locally for persistence.

#### Benefits
- Encourages active reading and note-taking.
- Supports multimodal learning styles.
- Improves retention through interactive tools.
- Provides a personalized study experience.


## Technical Requirements
- Jekyll static site generator
- Modern web browser with JavaScript enabled
- External API keys (Groq, VoiceRSS) for advanced features
- Google Forms/Sheets for feedback collection
- Flask backend for multiplayer features

## File Structure
```
├── _layouts/
│   └── lesson.html
├── _includes/
│   ├── video.html
│   ├── whiteboard.html
│   ├── ai_comprehension.html
│   ├── hack.html
│   ├── flashcards.html
│   ├── flashcard-notes.html
│   ├── game.html
│   └── poll.html
├── _data/
│   ├── flashcards.yml
│   └── game_questions.yml
└── lessons/
    └── cover.html
```

This system provides a comprehensive, interactive learning environment that engages students through multiple modalities while giving teachers powerful tools for content delivery and assessment.


## Lesson Creation


# How to Build a Coding Lesson with Layouts

This guide walks you through how to design, build, and deploy an interactive coding lesson using `lesson.html` and `cover.html`. These layout templates are part of a modular system that makes it easy for teachers to assemble consistent, polished, and engaging lessons. The system supports multimedia, code execution, student input, live feedback, and collaborative tools.

---

##  Step 1: Understand the Purpose of Each File

###  `lesson.html` (Base Layout)

This is the **core layout** used by all coding lessons. It defines the structure and style and includes embedded functionality such as localStorage, animations, and in-browser code execution. Think of this as the underlying skeleton.

>  You **do not** need to modify this file. It automatically wraps your lesson content.

**Key Features Included:**

* Stylish code formatting and dark theme styling
* Popcorn Hack support for both JavaScript and Python
* Feedback poll integration for student input
* Smooth section animations
* Automatic saving of responses via local storage

### `cover.html` (Lesson Template)

This file demonstrates how to use the `lesson.html` base layout and inject lesson-specific content. It contains the content area, lesson instructions, and references to interactive components.

At the top is a YAML frontmatter block that sets the lesson metadata:

```yaml
layout: lesson
title: Introduction to Functions
video_url: https://youtube.com/yourvideo
hack_prompt: Write a function that adds two numbers.
permalink: /functions
```

You’ll customize this file every time you create a new lesson.

---

## Step 2: Create a New Lesson File

1. **Duplicate `cover.html`**
   Rename it based on your lesson topic: `loops.html`, `arrays.html`, etc.

2. **Edit the Frontmatter**
   Update:

   * `title`: Displayed at the top of the lesson
   * `video_url`: YouTube video to support the topic
   * `hack_prompt`: Coding challenge or discussion question
   * `permalink`: The URL path for the lesson

3. **Write Your Lesson Content**
   Inside `<div id="lesson-content">`, add your instructions, code snippets, visuals, and explanations.

```html
<div id="lesson-content">
  <h2>What is a Loop?</h2>
  <p>Loops let you run the same block of code multiple times.</p>
  <pre><code>for (let i = 0; i < 5; i++) {
  console.log(i);
}</code></pre>
</div>
```

---
## Step 3: Add Interactive Components

Pick the features that fit your lesson. All components are modular and easy to include:

| Feature              | Include Syntax                  | Description                                              |
| -------------------- | ------------------------------- | -------------------------------------------------------- |
| Video Player      | `include video.html`            | Shows a YouTube video defined in frontmatter             |
| Whiteboard Viewer | `include whiteboard.html`       | Lets students see a live whiteboard via board code       |
| AI Quiz Tool      | `include ai_comprehension.html` | Students can generate practice questions using AI        |
| Code Prompt       | `include hack.html`             | Lets students type, run, and save code responses         |
| Flashcards        | `include flashcards.html`       | Pulls cards from YAML, allows flipping, review, tracking |
| Student Notes     | `include flashcard-notes.html`  | Students build and review their own flashcards           |
| Quiz Game         | `include game.html`             | Multiplayer quiz game with leaderboard and timers        |
| Poll              | `include poll.html`             | Students rate the lesson and add comments                |
| Sidebar           | `include slim_sidebar.html`     | Tools: dictionary, notes, read-aloud, highlights         |

These features enhance engagement and memory retention.

---

##  Step 4: Check and Deploy

1. **Verify Includes Exist**
   If you added `include game.html`, make sure that file exists in your project.

2.  **Test the Page**
   Open the file in a local preview environment. Interact with every component:

   * Click through flashcards
   * Enter and run code
   * Submit the poll
   * Try the AI comprehension checker

3.  **Deploy It**
   Once everything works, publish it to your lesson site or LMS.

---

## Best Practices for Teachers

* **Keep Each Lesson Focused:** Target one concept per lesson (e.g., “while loops” or “if statements”).
* **Use Visuals Early:** Embed videos or show a whiteboard before diving into code.
* **Prompt Reflection:** Include polls, notes, or AI questions to get students thinking.
* **Encourage Review:** Use flashcards at the end to reinforce terminology.
* **Save Time with Reusables:** Once you build a tool like `whiteboard.html`, you can reuse it in all lessons.

---

## Summary Checklist

Here’s a quick reference when building a new lesson:

* [ ] Duplicate `cover.html`
* [ ] Fill in frontmatter (title, video, prompt, permalink)
* [ ] Add content inside `lesson-content`
* [ ] Choose and insert interactive components
* [ ] Confirm `include` files exist
* [ ] Preview and test locally
* [ ] Deploy when everything is working

With this layout system, you can build high-quality, interactive lessons that are modular, student-friendly, and easy to maintain. Whether you're teaching loops, functions, or arrays, these templates give you a powerful way to bring your content to life.

---


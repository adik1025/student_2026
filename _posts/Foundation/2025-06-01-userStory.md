---
layout: post 
show_reading_time: false
permalink: /userstory
title: User Story
---

## **User Story:**

As a coding teacher building digital lessons,
I want to use a modular layout system to create interactive lesson pages,
so that I can easily deliver content, engage students, and track their learning—all in one place.

---

## **Feature Details:**

### **Setup and Access:**

* Lessons are built using the Jekyll platform.
* Start by duplicating `cover.html`, which includes lesson-specific content.
* Metadata like `title`, `video_url`, and `hack_prompt` are set in the frontmatter.

---

### **Core Layout: `lesson.html`**

* Base structure used across all lessons.
* Injects styles, animations, local storage, and in-browser code execution.
* Should not be modified directly.

---

### **Lesson Content: `cover.html`**

* Template file used to build new lessons.
* Includes a section for instructional content (`#lesson-content`) and modular features via `include` statements.

---

### **Available Components:**

#### Video Player

* Embed YouTube videos using `video.html`.

#### Code Prompt

* Students write and run code (Python/JavaScript) using `hack.html`.

#### AI Comprehension Checker

* Generates quiz questions from lesson content with `ai_comprehension.html`.

#### Feedback Poll

* Collects thumbs-up/down and comments via Google Forms using `poll.html`.

#### Flashcards

* `flashcards.html` pulls teacher-provided cards; `flashcard-notes.html` allows student creation.

#### Whiteboard

* Live board viewer through `whiteboard.html` using a shared board code.

#### Multiplayer Quiz Game

* Real-time quiz game using `game.html` with Flask backend and YAML questions.

#### Sidebar Tools

* `slim_sidebar.html` adds dictionary, highlights, notes, and read-aloud tools.

---

### **Lesson Creation Workflow:**

1. Duplicate `cover.html` and rename for the new lesson.
2. Update frontmatter values (title, video, prompt, permalink).
3. Add content inside `#lesson-content`.
4. Include desired features using `include` tags.
5. Test the page locally.
6. Deploy once everything works.

---

### **Best Practices:**

* One concept per lesson.
* Start with visuals or video.
* Include code prompts and AI checks to reinforce learning.
* Use polls and flashcards for reflection and review.

---

### **Requirements:**

* Jekyll site
* Browser with JavaScript
* API keys (Groq, VoiceRSS)
* Google Sheets/Form for poll integration
* Flask backend for quiz game (optional)

---

### **Directory Overview:**

```
_includes/       → Component files (video, poll, hack, etc.)
_layouts/        → Base layout file (`lesson.html`)
_data/           → Flashcards and quiz questions (YAML)
lessons/         → Your individual lesson files (e.g., functions.html)
```

---

---
layout: page
title: Checklist
permalink: /checklist/
---

<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Course Checklist</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #1A252F;
      color: #fff;
      padding: 0;
      margin: 0;
    }
    h1, h2 {
      text-align: center;
      color: cyan;
    }
    .container {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin: 20px auto;
      padding: 20px;
      border: 1px solid #28cee8;
      border-radius: 10px;
      width: 90%;
      max-width: 800px;
      background-color: #1A252F;
    }
    ul {
      list-style-type: none;
      padding: 0;
      width: 100%;
    }
    li {
      background-color: #263544;
      margin: 10px 0;
      padding: 10px;
      border-radius: 5px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      border: 1px solid #28cee8;
    }
    .complete {
      text-decoration: line-through;
      color: #aaa;
    }
    .checkbox-label {
      display: flex;
      align-items: center;
      gap: 10px;
      flex-grow: 1;
    }
    .confetti-message {
      text-align: center;
      font-size: 24px;
      color: lime;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <h1>Checklist</h1>
  <p style="text-align:center;">Mark tasks as complete to celebrate progress!</p>

  <div class="container" id="checklist-container"></div>
  <div id="confetti-message" class="confetti-message"></div>

  <script type="module">
    import confetti from 'https://cdn.skypack.dev/canvas-confetti';
    import { pythonURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';

    const checklistContainer = document.getElementById('checklist-container');
    const confettiMessage = document.getElementById('confetti-message');

    async function fetchChecklistItems() {
      try {
        const response = await fetch(`${pythonURI}/api/checklist`, {
          ...fetchOptions,
          method: 'GET',
          headers: { 'Content-Type': 'application/json' }
        });
        const data = await response.json();
        renderChecklist(data);
      } catch (error) {
        console.error('Error fetching checklist:', error);
      }
    }

    function renderChecklist(items) {
      const pages = {};
      checklistContainer.innerHTML = '';

      // Group by page
      items.forEach(item => {
        if (!pages[item.page]) pages[item.page] = [];
        pages[item.page].push(item);
      });

      Object.entries(pages).forEach(([page, tasks]) => {
        const section = document.createElement('div');
        section.innerHTML = `<h2>Page ${page}</h2>`;
        const list = document.createElement('ul');

        tasks.forEach(task => {
          const li = document.createElement('li');
          const label = document.createElement('label');
          label.className = 'checkbox-label';

          const checkbox = document.createElement('input');
          checkbox.type = 'checkbox';
          checkbox.checked = task.completed;
          checkbox.addEventListener('change', () => updateCompletion(task.id, checkbox.checked));

          const span = document.createElement('span');
          span.textContent = task.title;
          if (task.completed) span.classList.add('complete');

          label.appendChild(checkbox);
          label.appendChild(span);
          li.appendChild(label);
          list.appendChild(li);
        });

        section.appendChild(list);
        checklistContainer.appendChild(section);
      });

      checkAllComplete(items);
    }

    async function updateCompletion(id, completed) {
      try {
        await fetch(`${pythonURI}/api/checklist/${id}`, {
          ...fetchOptions,
          method: 'PUT',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ completed })
        });
        fetchChecklistItems();
      } catch (error) {
        console.error('Error updating item:', error);
      }
    }

    function checkAllComplete(items) {
      if (items.every(item => item.completed)) {
        confetti();
        confettiMessage.textContent = '🎉 All tasks complete! Great job! 🎉';
      } else {
        confettiMessage.textContent = '';
      }
    }

    fetchChecklistItems();
  </script>
</body>
</html>

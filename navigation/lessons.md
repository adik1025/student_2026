---
layout: page
title: Lessons Directory
permalink: /tools/lessons
toc: true
---

<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: #f0f2f8;
      margin: 0;
      padding: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
    }
    .directory-container {
      text-align: center;
      background: white;
      padding: 40px;
      border-radius: 12px;
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
      max-width: 600px;
      width: 90vw;
    }
    h1 {
      color: #ffffff;
      margin-bottom: 24px;
    }
    .button {
      display: block;
      width: 100%;
      margin: 12px 0;
      background:rgb(217, 90, 0);         /* light gray */
      border-radius: 6px;
      padding: 16px;
      border: 1px solid #ccc;
      color: #222;                 /* black text */
      font-size: 16px;
      cursor: pointer;
      transition: background 0.2s ease, color 0.2s ease, transform 0.2s ease;
      box-sizing: border-box;
      text-align: center;
      text-decoration: none;
    }
    .button:hover {
      background: rgb(159, 66, 0);
      transform: scale(1.03);
    }
    .points-section {
      margin-top: 30px;
      background: rgb(255, 255, 255);
      padding: 10px;
      border-radius: 8px;
      font-size: 18px;        /* Larger font for points */
      color: #333;
    }
    #pointsDisplay {
      font-size: 18px;        /* Match .points-section font size */
      margin-bottom: 8px;
    }
    #resetPointsBtn {
      margin-top: 10px;
      background: #888;
      font-size: 14px;        
      padding: 8px 0;         /* Half the .button padding */
      width: 50%;
      border-radius: 6px;
      color: #fff;
      border: none;
      cursor: pointer;
      transition: background 0.2s ease, color 0.2s ease, transform 0.2s ease;
      display: block;
      margin-left: auto;
      margin-right: auto;
    }
    #resetPointsBtn:hover {
      background: #555;
    }
    .footer {
      margin-top: 20px;
      font-size: 12px;
      color: #888;
    }
  </style>
</head>
<body>

  <div class="directory-container">
    <a href="{{ site.baseurl }}/tools/github/workflow" class="button">GitHub Workflow</a>
    <a href="{{ site.baseurl }}/tools/github/pages" class="button">GitHub Pages</a>
    <a href="{{ site.baseurl }}/tools/accounts" class="button">Accounts</a>
    <div class="points-section">
      <div id="pointsDisplay">Current Points: 100</div>
      <button id="resetPointsBtn">Reset Points</button>
    </div>
    <div class="footer">
      Complete all lessons and lose the least amount of points!
    </div>
  </div>

  <script>
    const POINTS_KEY = 'global_quiz_points';
    const QUIZ_KEYS = ['quiz_workflow_done', 'quiz_pages_done', 'quiz_accounts_done'];
    const pointsDisplay = document.getElementById("pointsDisplay");
    const resetPointsBtn = document.getElementById("resetPointsBtn");

    function getPoints() {
      return parseInt(localStorage.getItem(POINTS_KEY) || '100', 10);
    }

    function setPoints(value) {
      localStorage.setItem(POINTS_KEY, value.toString());
      updatePointsDisplay();
    }

    function updatePointsDisplay() {
      pointsDisplay.textContent = `Points: ${getPoints()}`;
    }

    resetPointsBtn.addEventListener("click", () => {
      const incomplete = QUIZ_KEYS.filter(key => localStorage.getItem(key) !== 'true');
      if (incomplete.length > 0) {
        alert(`You must complete all quizzes before resetting points.\nQuizzes remaining: ${incomplete.length}`);
        return;
      }

      setPoints(100);

      // Reset quiz status
      QUIZ_KEYS.forEach(key => localStorage.setItem(key, 'false'));
      alert("Points reset to 100 and quiz completion reset.");
    });

    updatePointsDisplay();
  </script>
</body>
</html>
---
title: Quiz on Github Pages Lesson
search_exclude: true
permalink: /githubquiz_2/
---

<html lang="en">
<head>
  <meta charset="UTF-8">
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f6f6fa;
      color: #222;
      margin: 0;
      padding: 24px;
    }
    .quiz-container {
      max-width: 600px;
      margin: 40px auto;
      background: #fff;
      border-radius: 12px;
      box-shadow: 0 2px 8px #0001;
      padding: 32px;
    }
    h2 {
      color: #2c2a5d;
    }
    .question {
      margin-bottom: 24px;
      font-weight: bold;
      font-size: 16px;
      color: #222;
    }
    .options label {
      margin: 8px 0;
      cursor: pointer;
      background: #e6e8ff; /* changed for contrast */
      border-radius: 6px;
      padding: 10px 14px;
      border: 1px solid #ccc;
      color: #222;
      transition: background 0.2s;
    }
    .options label:hover {
      background: #d1d5ff;
    }
    .options input[type="radio"] {
      accent-color: #2c2a5d;
      margin-right: 10px;
    }
    button {
      background: #2c2a5d;
      color: #fff;
      border: none;
      padding: 12px 24px;
      border-radius: 8px;
      font-size: 16px;
      cursor: pointer;
      margin-right: 10px;
    }
    button:disabled {
      background: #aaa;
    }
    .score {
      font-size: 1.2em;
      margin-top: 24px;
    }
    .correct {
      color: green;
    }
    .incorrect {
      color: red;
    }
  </style>
</head>
<body>

  <div class="quiz-container">
    <div id="quiz"></div>
    <button id="submitBtn">Submit Quiz</button>
    <button id="retryBtn" style="display: none;">Retry Quiz</button>
    <div class="score" id="score"></div>
  </div>

  <script>
    const questions = [
      {
        q: "What is the primary use of GitHub Pages?",
        options: [
          "Hosting full-stack web applications",
          "Running JavaScript servers in the cloud",
          "Hosting static websites directly from a GitHub repository",
          "Managing GitHub repositories with extra memory"
        ],
        answer: 2
      },
      {
        q: "What makes the browser version of VSCode especially useful for students?",
        options: [
          "It automatically publishes your website",
          "It allows editing code directly in the browser without installing anything",
          "It adds hosting to your GitHub Pages project",
          "It only works with Node.js projects"
        ],
        answer: 1
      },
      {
        q: "Which of the following is a required step to publish your site with GitHub Pages?",
        options: [
          "Installing VSCode extensions",
          "Using a fork of the original repository",
          "Enabling GitHub Pages in the repository’s Settings tab",
          "Switching your repository to private mode"
        ],
        answer: 2
      },
      {
        q: "When using the browser version of VSCode, what is the correct format for opening your repo?",
        options: [
          "github.dev/username/repo",
          "vscode.github.io/username/repo",
          "github.vscode.com/repo-name",
          "vscode.dev/github/your_username/your_repository"
        ],
        answer: 3
      },
      {
        q: "After enabling GitHub Pages, where will your site be available?",
        options: [
          "github.com/pages/your_site",
          "your_github_username.github.io/your_repository_name/",
          "vscode.dev/your_site",
          "localhost:3000"
        ],
        answer: 1
      }
    ];
    
    const quizContainer = document.getElementById("quiz");
    const submitBtn = document.getElementById("submitBtn");
    const retryBtn = document.getElementById("retryBtn");
    const scoreDiv = document.getElementById("score");

    function renderQuiz() {
      quizContainer.innerHTML = "";
      questions.forEach((question, index) => {
        const questionDiv = document.createElement("div");
        questionDiv.className = "question";
        questionDiv.textContent = `Q${index + 1}: ${question.q}`;

        const optionsDiv = document.createElement("div");
        optionsDiv.className = "options";

        question.options.forEach((option, i) => {
          const optionId = `q${index}_opt${i}`;
          const label = document.createElement("label");
          label.htmlFor = optionId;
          label.innerHTML = `
            <input type="radio" name="q${index}" id="${optionId}" value="${i}">
            ${option}
          `;
          optionsDiv.appendChild(label);
        });

        quizContainer.appendChild(questionDiv);
        quizContainer.appendChild(optionsDiv);
      });
    }

    function checkAnswers() {
      let score = 0;
      let feedback = [];

      questions.forEach((question, index) => {
        const selected = document.querySelector(`input[name="q${index}"]:checked`);
        const selectedIndex = selected ? parseInt(selected.value) : -1;
        if (selectedIndex === question.answer) {
          score++;
          feedback.push(`<span class="correct">Q${index + 1}: Correct</span>`);
        } else {
          feedback.push(`<span class="incorrect">Q${index + 1}: Incorrect</span>`);
        }
      });

      scoreDiv.innerHTML = `You scored <b>${score} / ${questions.length}</b>.<br><br>${feedback.join("<br>")}`;
      submitBtn.disabled = true;
      retryBtn.style.display = "inline-block";
    }

    function resetQuiz() {
      renderQuiz();
      scoreDiv.innerHTML = "";
      submitBtn.disabled = false;
      retryBtn.style.display = "none";
    }

    submitBtn.addEventListener("click", checkAnswers);
    retryBtn.addEventListener("click", resetQuiz);

    renderQuiz(); // initial render
  </script>

<!-- Input form -->
<div class="score-input-box">
  <h2>Submit Your Score</h2>
  <input type="text" id="player-name" placeholder="Enter your name" />
  <input type="number" id="player-score" placeholder="Enter your score" />
  <button id="submit-score">Submit Score</button>
</div>

<style>
  .score-input-box {
    width: 300px;
    margin: 40px auto;
    padding: 20px;
    background-color: #f9fafc;
    border: 2px solid #4a90e2;
    border-radius: 15px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }

  .score-input-box h2 {
    text-align: center;
    margin-bottom: 15px;
    color: #333;
  }

  .score-input-box input {
    width: 100%;
    margin-bottom: 15px;
    padding: 10px;
    border: 2px solid #ccc;
    border-radius: 8px;
    font-size: 14px;
    background-color: #ffffff;
    transition: border 0.3s ease;
  }

  .score-input-box input:focus {
    border-color: #4a90e2;
    outline: none;
  }

  .score-input-box button {
    width: 100%;
    padding: 10px;
    background-color: #4a90e2;
    color: white;
    font-weight: bold;
    border: none;
    border-radius: 8px;
    font-size: 15px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .score-input-box button:hover {
    background-color: #357ABD;
  }
</style>

<script type="module">
  import { pythonURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';
  async function submitScore() {
    const player_name = document.getElementById('player-name').value;
    const score = parseInt(document.getElementById('player-score').value);

    try {
      const response = await fetch(`${pythonURI}/api/leaderboard`, {
        ...fetchOptions,
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ player_name, score })
      });

      if (!response.ok) {
        throw new Error('Failed to add score: ' + response.statusText);
      }

      alert('Score added successfully!');
      document.getElementById('player-name').value = '';
      document.getElementById('player-score').value = '';

      // Optionally, refresh leaderboard or score list
      // fetchScores();
    } catch (error) {
      console.error('Error adding score:', error);
      alert('Error adding score: ' + error.message);
    }
  }

  document.getElementById('submit-score').addEventListener('click', submitScore);
</script>

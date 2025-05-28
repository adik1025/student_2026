---
title: Quiz on Github Workflow Lesson
search_exclude: true
permalink: /githubquiz_1/
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
      display: block;
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
        q: "You want to contribute a bug fix to a repository you do not have direct access to. What is the most appropriate GitHub workflow to follow?",
        options: [
          "Clone the repository, make changes on main, and push directly",
          "Fork the repository, edit on main, and request a merge via PR",
          "Fork the repository, create a feature branch, make changes, and submit a pull request",
          "Request write access and push directly to the upstream repository"
        ],
        answer: 2
      },
      {
        q: "In a team project using the Scrum Master + Contributors model, who is responsible for merging new code into the main repository?",
        options: [
          "Each contributor, after testing their feature",
          "The person who writes the most code",
          "All team members equally",
          "The Scrum Master, after reviewing submitted pull requests"
        ],
        answer: 3
      },
      {
        q: "Which of the following actions is least aligned with GitHub best practices for collaborative development?",
        options: [
          "Committing directly to main to speed up delivery",
          "Creating a feature/payment-gateway branch before starting a new feature",
          "Writing commit messages like 'Fix auth redirect logic'",
          "Pulling the latest changes from main before pushing your branch"
        ],
        answer: 0
      },
      {
        q: "Why might a student choose to clone the pages repository rather than fork it?",
        options: [
          "They want to contribute to the class curriculum",
          "They want to deploy it using GitHub Pages",
          "They want to explore or run the code locally without making contributions",
          "They need to take ownership of the repository and manage pull requests"
        ],
        answer: 2
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

</body>
</html>

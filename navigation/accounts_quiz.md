---
title: Quiz on PII and Accounts Lesson
search_exclude: true
permalink: /piiquiz/
---

<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>PII & Account Security Quiz</title>
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
    <h2>PII & Account Security Quiz</h2>
    <div id="quiz"></div>
    <button id="submitBtn">Submit Quiz</button>
    <button id="retryBtn" style="display: none;">Retry Quiz</button>
    <div class="score" id="score"></div>
  </div>

  <script>
    const questions = [
      {
        q: "Which of the following is the best example of Highly Confidential Information?",
        options: [
          "Your high school name",
          "Your full birth date",
          "Your Wi-Fi password",
          "Your city of residence"
        ],
        answer: 2
      },
      {
        q: "Why is it recommended to use different email accounts for different purposes?",
        options: [
          "To make it easier to remember passwords",
          "To separate types of information and reduce risk if one account is compromised",
          "Because email providers require it",
          "To avoid receiving any spam"
        ],
        answer: 1
      },
      {
        q: "Which of these is NOT a good security practice?",
        options: [
          "Enabling multi-factor authentication",
          "Using the same password for all accounts",
          "Regularly updating your software",
          "Using a password manager"
        ],
        answer: 1
      },
      {
        q: "If you receive an unexpected email asking for your login credentials, what should you do?",
        options: [
          "Reply with your credentials to be helpful",
          "Click any links to see where they go",
          "Ignore or report the email as phishing",
          "Forward it to your friends"
        ],
        answer: 2
      },
      {
        q: "Which of the following is considered Sensitive (but not Highly Confidential) Information?",
        options: [
          "Your favorite food",
          "Your street address",
          "Your GitHub profile picture",
          "Your public portfolio link"
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

</body>
</html>

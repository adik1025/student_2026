---
toc: false
comments: true
layout: bootstrap
title: Final Score
dcategories: [DevOps]
permalink: /devops/tools/finalscore
menu: nav/tools_setup.html
toc: true
comments: true
---


<head>
  <meta charset="UTF-8">
  <title>Submit Score</title>
  <style>
    body {
      background-color: #007BFF; /* Blue background */
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      color: #fff;
      margin: 0;
      padding: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
    }
    .score-container {
      background-color: #ffffff;
      color: #333;
      padding: 40px;
      border-radius: 16px;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
      text-align: center;
      max-width: 400px;
      width: 100%;
    }
    h1 {
      margin-bottom: 20px;
      color: #007BFF;
    }
    #submitScoreBtn {
      background-color: #007BFF;
      color: white;
      border: none;
      padding: 12px 24px;
      font-size: 16px;
      border-radius: 8px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    #submitScoreBtn:hover {
      background-color: #0056b3;
    }
  </style>
</head>
<body>
    <h2>Click this button once you are happy with your scores!</h2>
    <div id="score-display" style="font-size: 1.5em; color: lightblue;"></div>
    <script>
        const quiz1 = parseInt(localStorage.getItem("quiz1Score") || "0");
        const quiz2 = parseInt(localStorage.getItem("quiz2Score") || "0");
        const total = quiz1 + quiz2;
        document.getElementById("score-display").innerText = `Your combined score: ${total}`;
    </script>
  <div class="score-container">
    <h1>Submit Your Final Score</h1>
    <button id="submitScoreBtn">Submit Final Score</button>
  </div>

  <script type="module">
    import { pythonURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';

    document.getElementById("submitScoreBtn").addEventListener("click", sendCombinedScore);

    async function sendCombinedScore() {
        const quiz1 = parseInt(localStorage.getItem("quiz1Score") || "0");
        const quiz2 = parseInt(localStorage.getItem("quiz2Score") || "0");
        const totalScore = quiz1 + quiz2;
        const sectionId = 1;

        const token = localStorage.getItem("jwtToken");
        if (!token) {
            alert("You must be logged in to submit your score.");
            return;
        }

        try {
            const response = await fetch(`${pythonURI}/api/scores`, {
                ...fetchOptions,
                method: "POST",
                headers: {
                    ...fetchOptions.headers,
                    "Authorization": `Bearer ${token}`
                },
                body: JSON.stringify({
                    value: totalScore,
                    section_id: sectionId
                })
            });

            if (!response.ok) {
                const result = await response.json();
                throw new Error(result.message || `Error: ${response.status}`);
            }

            alert("Score submitted successfully!");
        } catch (error) {
            console.error("Failed to submit score:", error.message || error);
            alert("Failed to submit score: " + error.message);
        }
    }
  </script>

</body>

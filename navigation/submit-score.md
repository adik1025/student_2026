---
layout: page
title: Submit Final Score
---

<h2>Ready to Submit Your Score?</h2>
<p>This will add your scores from both quizzes and send it to the backend.</p>
<button onclick="sendCombinedScore()">Submit Final Score</button>

<script>
  async function sendCombinedScore() {
    const quiz1 = parseInt(localStorage.getItem("quiz1Score") || "0");
    const quiz2 = parseInt(localStorage.getItem("quiz2Score") || "0");
    const totalScore = quiz1 + quiz2;

    const sectionId = 1; // constant

    const token = localStorage.getItem("jwt"); // change to "token" if needed

    if (!token) {
      alert("You must be logged in to submit your score.");
      return;
    }

    const response = await fetch("/api/score", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": `Bearer ${token}`
      },
      body: JSON.stringify({
        score: totalScore,
        section_id: sectionId
      })
    });

    if (response.ok) {
      alert("Score submitted successfully!");
      localStorage.removeItem("quiz1Score");
      localStorage.removeItem("quiz2Score");
    } else {
      const result = await response.json();
      alert("Failed to submit score: " + (result.message || response.statusText));
    }
  }
</script>

---
layout: page
title: Submit Final Score
permalink: /finalscore
---

<h2>Ready to Submit Your Score?</h2>
<p>This will add your scores from both quizzes and send it to the backend.</p>
<button onclick="sendCombinedScore()">Submit Final Score</button>

<script type="module">
import { pythonURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';

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
                score: totalScore,
                section_id: sectionId
            })
        });

        if (!response.ok) {
            const result = await response.json();
            throw new Error(result.message || `Error: ${response.status}`);
        }

        alert("Score submitted successfully!");
        localStorage.removeItem("quiz1Score");
        localStorage.removeItem("quiz2Score");
    } catch (error) {
        console.error("Failed to submit score:", error.message || error);
        alert("Failed to submit score: " + error.message);
    }
}

// Attach function to global scope or bind to button
window.sendCombinedScore = sendCombinedScore;
</script>

---
layout: page
title: Leaderboard
permalink: /leaderboard/
---


<title>Leaderboard</title>
<style>
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 40px 20px;
    display: flex;
    justify-content: center;
}
.container {
    background: #fff;
    max-width: 600px;
    width: 100%;
    padding: 30px;
    border-radius: 12px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}
h1 {
    text-align: center;
    color: #333;
    margin-bottom: 25px;
}
ul#leaderboard-list {
    list-style-type: none;
    padding: 0;
    margin: 0;
}
li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #e0e7ff;
    margin-bottom: 12px;
    padding: 14px 20px;
    border-radius: 8px;
    font-size: 16px;
}
.rank {
    font-weight: bold;
    color: #4b0082;
}
.score {
    font-size: 18px;
    font-weight: bold;
    color: #2e2e2e;
}
</style>

<h2>Leaderboard</h2>

<div class="container" id="leaderboard-box" style="border: 2px solid #333; border-radius: 10px; padding: 16px; background-color: #f9f9f9;">
  <ul id="leaderboard-list"></ul>
</div>

<script type="module">
import { pythonURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';

async function fetchLeaderboard() {
    try {
        const response = await fetch(`${pythonURI}/api/leaderboard`, {
            ...fetchOptions,
            method: 'GET'
        });

        if (!response.ok) {
            console.error('Response not OK:', response.status, response.statusText);
            throw new Error('Failed to fetch leaderboard');
        }

        const data = await response.json();
        console.log('Received data:', data);

        const leaderboardList = document.getElementById('leaderboard-list');
        leaderboardList.innerHTML = '';

        if (!Array.isArray(data)) {
            throw new Error('Data is not an array');
        }

        data.sort((a, b) => parseInt(b.score) - parseInt(a.score));

        data.forEach((player, index) => {
            const listItem = document.createElement('li');
            listItem.innerHTML = `
                <span><strong>#${index + 1}</strong> ${player.player_name}</span>
                <span>${player.score}</span>
            `;
            leaderboardList.appendChild(listItem);
        });

    } catch (error) {
        console.error('Error loading leaderboard:', error?.message || error);
        const leaderboardList = document.getElementById('leaderboard-list');
        leaderboardList.innerHTML = '<li style="color:red;">Failed to load leaderboard data. See console for details.</li>';
    }
}

window.onload = fetchLeaderboard;
</script>


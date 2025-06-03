---
layout: page 
title: Calendar
search_exclude: true
permalink: /calendar/
---


<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Calendar</title>
<style>
  body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    padding: 20px;
    background: #f5f7fa;
    color: #333;
  }
  h1 {
    text-align: center;
    margin-bottom: 1rem;
    color: #2c3e50;
  }
  .controls {
    max-width: 900px;
    margin: 0 auto 15px auto;
    text-align: center;
  }
  select {
    font-size: 1rem;
    padding: 6px 10px;
    margin: 0 10px;
    border-radius: 6px;
    border: 1.5px solid #2980b9;
    outline: none;
    cursor: pointer;
  }
  select:focus {
    border-color: #1f6391;
  }
  .calendar {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 6px;
    background: white;
    padding: 15px;
    border-radius: 12px;
    max-width: 900px;
    margin: 0 auto 2rem auto;
    box-shadow: 0 4px 10px rgba(0,0,0,0.1);
  }
  .day-name, .day {
    padding: 12px 8px;
    border-radius: 8px;
    text-align: center;
    user-select: none;
  }
  .day-name {
    font-weight: 700;
    background: #2980b9;
    color: white;
    font-size: 0.95rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }
  .day {
    min-height: 110px;
    background: #ecf0f1;
    text-align: left;
    display: flex;
    flex-direction: column;
    box-shadow: inset 0 0 5px #bdc3c7;
    transition: background-color 0.3s ease;
  }
  .day:hover {
    background: #d0d7df;
  }
  .day-number {
    font-weight: 600;
    font-size: 1.1rem;
    margin-bottom: 8px;
    padding-left: 6px;
    color: #34495e;
  }
  .event {
    background: #3498db;
    color: white;
    font-size: 0.85rem;
    padding: 4px 6px;
    margin: 3px 8px 3px 6px;
    border-radius: 4px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  .empty {
    background: transparent;
    box-shadow: none;
  }
  #toggle-btn {
    display: block;
    margin: 0 auto 20px auto;
    background-color: #2980b9;
    color: white;
    border: none;
    padding: 10px 18px;
    font-size: 1rem;
    border-radius: 8px;
    cursor: pointer;
    box-shadow: 0 3px 6px rgba(41,128,185,0.4);
    transition: background-color 0.25s ease;
  }
  #toggle-btn:hover {
    background-color: #1f6391;
  }
  #calendar-data-container {
    max-width: 900px;
    margin: 0 auto;
    background: #2c3e50;
    color: #ecf0f1;
    border-radius: 12px;
    padding: 15px;
    font-family: 'Consolas', 'Courier New', monospace;
    font-size: 14px;
    line-height: 1.4;
    white-space: pre-wrap;
    overflow-x: auto;
    max-height: 300px;
    box-shadow: inset 0 0 10px #1a252f;
    display: none;
    user-select: text;
  }
</style>
</head>
<body>

<h1>Calendar</h1>

<div class="controls">
  <label for="month-select">Month:</label>
  <select id="month-select" aria-label="Select month"></select>

  <label for="year-select">Year:</label>
  <select id="year-select" aria-label="Select year"></select>
</div>

<button id="toggle-btn" aria-expanded="false">Show Calendar Data</button>

<div class="calendar" id="calendar"></div>

<!-- Editable calendar data container -->
<pre id="calendar-data-container" contenteditable spellcheck="false">
{
  "month": 5,
  "year": 2025,
  "events": [
    {
      "date": "2025-05-21",
      "events": [
        {"time": "10:00 AM", "title": "Team Standup Meeting"}
      ]
    },
    {
      "date": "2025-05-22",
      "events": {"time": "9:00 AM", "title": "Checkpoint with Mr. Mort"}
    }
  ]
}
</pre>

<script>
const calendarEl = document.getElementById('calendar');
const calendarDataContainer = document.getElementById('calendar-data-container');
const toggleBtn = document.getElementById('toggle-btn');
const monthSelect = document.getElementById('month-select');
const yearSelect = document.getElementById('year-select');

function renderCalendar(data, monthOverride, yearOverride) {
  const month = (typeof monthOverride === 'number') ? monthOverride : data.month;
  const year = (typeof yearOverride === 'number') ? yearOverride : data.year;
  const events = data.events || [];

  const dayNames = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'];
  calendarEl.innerHTML = '';

  for(let dn of dayNames) {
    const dnEl = document.createElement('div');
    dnEl.className = 'day-name';
    dnEl.textContent = dn;
    calendarEl.appendChild(dnEl);
  }

  const firstDay = new Date(year, month -1, 1);
  const lastDay = new Date(year, month, 0);
  const numDays = lastDay.getDate();

  const startDay = firstDay.getDay();

  for(let i=0; i < startDay; i++) {
    const emptyCell = document.createElement('div');
    emptyCell.className = 'day empty';
    calendarEl.appendChild(emptyCell);
  }

  for(let day=1; day <= numDays; day++) {
    const dayEl = document.createElement('div');
    dayEl.className = 'day';

    const dayNumberEl = document.createElement('div');
    dayNumberEl.className = 'day-number';
    dayNumberEl.textContent = day;
    dayEl.appendChild(dayNumberEl);

    const dateStr = `${year}-${String(month).padStart(2,'0')}-${String(day).padStart(2,'0')}`;

    const dayEvents = events.find(e => e.date === dateStr);
    if(dayEvents) {
      // Normalize events to array even if single object
      const evList = Array.isArray(dayEvents.events) ? dayEvents.events : [dayEvents.events];
      for(let ev of evList) {
        const evEl = document.createElement('div');
        evEl.className = 'event';
        evEl.textContent = ev.time + ' - ' + ev.title;
        dayEl.appendChild(evEl);
      }
    }

    calendarEl.appendChild(dayEl);
  }
}

function loadAndRender(monthOverride, yearOverride) {
  try {
    const jsonText = calendarDataContainer.textContent.trim();
    if (!jsonText) throw new Error("Calendar data is empty");
    const data = JSON.parse(jsonText);
    renderCalendar(data, monthOverride, yearOverride);
    return data;
  } catch (e) {
    calendarEl.innerHTML = `<p style="color:red; text-align:center;">Error parsing calendar data:<br>${e.message}</p>`;
    return null;
  }
}

function populateMonthSelect(selectedMonth) {
  monthSelect.innerHTML = '';
  const monthNames = [
    'January', 'February', 'March', 'April', 'May', 'June',
    'July', 'August', 'September', 'October', 'November', 'December'
  ];
  monthNames.forEach((name, i) => {
    const option = document.createElement('option');
    option.value = i+1;
    option.textContent = name;
    if (i+1 === selectedMonth) option.selected = true;
    monthSelect.appendChild(option);
  });
}

function populateYearSelect(selectedYear) {
  yearSelect.innerHTML = '';
  const currentYear = new Date().getFullYear();
  const startYear = currentYear - 10;
  const endYear = currentYear + 10;
  for(let y = startYear; y <= endYear; y++) {
    const option = document.createElement('option');
    option.value = y;
    option.textContent = y;
    if (y === selectedYear) option.selected = true;
    yearSelect.appendChild(option);
  }
}

let calendarData = null;
let currentMonth, currentYear;

function updateCalendar() {
  currentMonth = parseInt(monthSelect.value);
  currentYear = parseInt(yearSelect.value);
  renderCalendar(calendarData, currentMonth, currentYear);
}

// Initial setup
calendarData = loadAndRender();
if(calendarData) {
  populateMonthSelect(calendarData.month);
  populateYearSelect(calendarData.year);
  currentMonth = calendarData.month;
  currentYear = calendarData.year;
  updateCalendar();
}

// Event listeners
monthSelect.addEventListener('change', updateCalendar);
yearSelect.addEventListener('change', updateCalendar);

toggleBtn.addEventListener('click', () => {
  const isVisible = calendarDataContainer.style.display === 'block';
  if (isVisible) {
    calendarDataContainer.style.display = 'none';
    toggleBtn.setAttribute('aria-expanded', 'false');
    toggleBtn.textContent = 'Show Calendar Data';
    // Reload data and update calendar on hide
    calendarData = loadAndRender(currentMonth, currentYear);
  } else {
    calendarDataContainer.style.display = 'block';
    toggleBtn.setAttribute('aria-expanded', 'true');
    toggleBtn.textContent = 'Hide Calendar Data';
  }
});

// Auto-update calendar if JSON edited and blurred
calendarDataContainer.addEventListener('blur', () => {
  calendarData = loadAndRender(currentMonth, currentYear);
});
</script>

</body>
</html>

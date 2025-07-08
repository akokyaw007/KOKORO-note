# KOKORO-note
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>こころノート</title>
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@700&display=swap" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body {
      margin: 0;
      background: #e6f3fa;
      font-family: 'Noto Sans JP', Arial, sans-serif;
      min-height: 100vh;
    }
    .header {
      margin-top: 48px;
      text-align: center;
    }
    .header-title {
      font-size: 5rem;
      color: #3d4b5a;
      letter-spacing: 0.15em;
      text-shadow: 4px 6px 16px #b8c7d0, 0 2px 0 #fff;
      font-family: 'Noto Sans JP', Arial, sans-serif;
      font-weight: 700;
      margin-bottom: 0.9em;
    }
    .divider {
      width: 90%;
      margin: 2rem auto 2.5rem auto;
      border: none;
      border-top: 8px solid #ff9362;
      border-radius: 4px;
      box-shadow: 0 4px 12px #ffc1a7a0;
    }
    .nav-row {
      display: flex;
      justify-content: center;
      gap: 2rem;
      margin-top: 0;
      margin-bottom: 3rem;
      flex-wrap: wrap;
    }
    .nav-card {
      flex: 1 1 180px;
      max-width: 220px;
      background: #f6fafc;
      border-radius: 28px;
      box-shadow: 0 6px 24px #b8c7d022, 0 1.5px 4px #fff;
      padding: 36px 20px 22px 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      transition: box-shadow 0.2s, background 0.2s, transform 0.15s;
      cursor: pointer;
      border: none;
      outline: none;
      position: relative;
      margin-bottom: 12px;
    }
    .nav-card.active {
      background: linear-gradient(150deg, #ff9362, #ffa783 80%);
      box-shadow: 0 10px 36px #ff936250, 0 2px 12px #fff;
      color: #fff;
      transform: translateY(-8px) scale(1.04);
    }
    .nav-card .icon {
      font-size: 3.1rem;
      margin-bottom: 22px;
      text-shadow: 0 6px 12px #ffc1a7a0;
    }
    .nav-card .label {
      font-size: 1.35rem;
      font-weight: bold;
      letter-spacing: 0.04em;
      color: inherit;
      text-shadow: 0 1px 0 #fff;
    }
    .nav-card.active .label {
      color: #fff;
      text-shadow: 0 1px 0 #ffbfa1;
    }
    @media (max-width: 900px) {
      .nav-row {
        flex-direction: column;
        align-items: center;
        gap: 1.5rem;
      }
      .nav-card {
        width: 90%;
        max-width: 330px;
      }
    }
    .section {
      display: none;
      max-width: 500px;
      margin: 0 auto 32px auto;
      padding: 32px 22px 28px 22px;
      background: #fff;
      border-radius: 24px;
      box-shadow: 0 4px 22px #b8c7d022;
      font-size: 1.1rem;
      animation: fadein 0.36s;
    }
    .section.active {
      display: block;
    }
    @keyframes fadein {
      from { opacity: 0; transform: scale(0.96);}
      to { opacity: 1; transform: scale(1);}
    }
    .section h2 {
      font-size: 1.5rem;
      margin-top: 0;
      color: #ff9362;
      text-shadow: 0 1px 0 #fff, 0 2px 8px #ffd4b7;
      margin-bottom: 18px;
      font-weight: bold;
      text-align: center;
    }
    .section label {
      font-weight: bold;
      color: #3d4b5a;
      margin-bottom: 6px;
      display: block;
    }
    .section input[type="text"], .section textarea, .section select {
      width: 100%;
      padding: 10px 12px;
      margin-bottom: 18px;
      font-size: 1rem;
      border-radius: 10px;
      border: 1px solid #c2d1e0;
      background: #f5fafd;
      transition: border 0.2s;
      font-family: inherit;
      box-sizing: border-box;
    }
    .section textarea {
      min-height: 80px;
      resize: vertical;
    }
    .section button {
      padding: 11px 38px;
      background: linear-gradient(150deg, #ff9362, #ffa783 80%);
      color: #fff;
      border: none;
      border-radius: 10px;
      font-size: 1.1rem;
      font-weight: bold;
      cursor: pointer;
      transition: background 0.18s, box-shadow 0.18s;
      box-shadow: 0 2px 8px #ffd4b7a0;
      margin-bottom: 12px;
    }
    .section button:hover {
      background: linear-gradient(150deg, #ffa783 10%, #ff9362 90%);
      box-shadow: 0 4px 22px #ffd4b7b0;
    }
    .todo-list li {
      background: #f7f7ff;
      padding: 10px 10px;
      border-radius: 8px;
      margin-bottom: 8px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 1.08em;
      box-shadow: 0 2px 6px #c2d1e022;
      cursor: pointer;
      transition: background 0.14s;
    }
    .todo-list li.done {
      text-decoration: line-through;
      color: #aaa;
      background: #e5e5e7;
    }
    .todo-list button {
      padding: 3px 12px;
      font-size: 0.9em;
      background: #e68d61;
      border-radius: 6px;
      border: none;
      color: #fff;
      margin-left: 10px;
      box-shadow: none;
    }
    .todo-list button:hover {
      background: #9a4e28;
    }
    .mood-emoji {
      font-size: 2.5em;
      margin-bottom: 6px;
      display: block;
    }
    .journal-item {
      background: #f9fafc;
      margin-bottom: 12px;
      border-radius: 10px;
      padding: 12px 10px 8px 10px;
      box-shadow: 0 2px 10px #c2d1e022;
    }
    .journal-item .date {
      color: #aaa;
      font-size: 0.95em;
      margin-bottom: 4px;
    }
    .journal-item .text {
      white-space: pre-wrap;
      margin-bottom: 4px;
    }
    /* みんなのノート */
    .public-note-title {
      color: #ff9362;
      font-size: 2rem;
      text-align: center;
      margin-top: 20px;
      margin-bottom: 18px;
      font-weight: bold;
      letter-spacing: 0.06em;
    }
    .public-journal-list {
      margin-top: 10px;
    }
    .public-journal-item {
      background: #f7fafd;
      border-radius: 10px;
      padding: 13px 12px 8px 12px;
      margin-bottom: 16px;
      box-shadow: 0 2px 10px #c2d1e022;
    }
    .public-journal-item .date {
      color: #aaa;
      font-size: 0.97em;
    }
    .public-journal-item .text {
      white-space: pre-wrap;
      margin: 4px 0 4px 0;
      font-size: 1.07em;
    }
    .public-reactions {
      margin: 5px 0 2px 0;
      display: flex;
      gap: 6px;
      align-items: center;
    }
    .public-reactions button {
      background: #fff0e6;
      border: 1px solid #ffd0b0;
      border-radius: 8px;
      font-size: 1.1em;
      padding: 2px 10px;
      cursor: pointer;
      transition: background 0.14s;
    }
    .public-reactions button.selected {
      background: #ffd0b0;
      color: #ff9362;
      font-weight: bold;
    }
    .public-comments {
      margin-top: 10px;
      padding-left: 8px;
    }
    .public-comment {
      padding: 4px 0;
      font-size: 0.99em;
      color: #444;
    }
    .public-comment-input-row {
      display: flex;
      gap: 8px;
      margin-top: 5px;
    }
    .public-comment-input-row input {
      flex: 1;
      padding: 6px 8px;
      border-radius: 6px;
      border: 1px solid #c2d1e0;
      font-size: 1em;
    }
    .public-comment-input-row button {
      padding: 6px 18px;
      font-size: 1em;
      border-radius: 6px;
      background: #ff9362;
      color: #fff;
      border: none;
      cursor: pointer;
      transition: background 0.13s;
    }
    .public-comment-input-row button:hover {
      background: #e67c44;
    }
    .mood-graph-section {
      margin-top: 24px;
      background: #f7fafd;
      padding: 16px;
      border-radius: 16px;
      box-shadow: 0 2px 8px #b8c7d022;
    }
    .mood-graph-section h3 {
      font-size: 1.1em;
      margin-bottom: 8px;
      color: #ff9362;
      font-weight: bold;
      text-align: center;
    }
    #moodChart {
      max-width: 100%;
      max-height: 240px;
      margin: 0 auto;
      display: block;
    }
  </style>
</head>
<body>
  <div class="header">
    <div class="header-title">こころノート</div>
    <hr class="divider">
  </div>
  <div class="nav-row">
    <button class="nav-card active" id="nav-todo">
      <span class="icon">📝</span>
      <span class="label">ToDo</span>
    </button>
    <button class="nav-card" id="nav-mood">
      <span class="icon">😊</span>
      <span class="label">今日の気分</span>
    </button>
    <button class="nav-card" id="nav-journal">
      <span class="icon">📖</span>
      <span class="label">日記</span>
    </button>
    <button class="nav-card" id="nav-public">
      <span class="icon">🌍</span>
      <span class="label">みんなのノート</span>
    </button>
  </div>
  <!-- ToDo Section -->
  <div class="section active" id="section-todo">
    <h2>ToDo</h2>
    <input type="text" id="todo-input" placeholder="新しいタスクを追加">
    <button id="todo-add-btn">追加</button>
    <ul class="todo-list" id="todo-list"></ul>
  </div>
  
  <!-- Journal Section -->
  <div class="section" id="section-journal">
    <h2>日記</h2>
    <textarea id="journal-input" placeholder="今日の出来事や感じたことを自由に書いてください"></textarea>
    <div>
      <input type="checkbox" id="journal-public-checkbox">
      <label for="journal-public-checkbox">この日記を「みんなのノート」で公開する</label>
    </div>
    <button id="journal-save-btn">保存</button>
    <div class="journal-list" id="journal-list"></div>
  </div>
  <!-- Mood Section -->
<div class="section" id="section-mood">
  <h2>今日の気分</h2>
  <label for="mood-select">気分を選んでください</label>
  <select id="mood-select">
    <option value="5">😍 嬉しい</option>
    <option value="4">😊 いい感じ</option>
    <option value="3">😐 普通</option>
    <option value="2">😞 ちょっと落ち込み</option>
    <option value="1">😡 怒り</option>
  </select>
  <div style="margin:15px 0;">
    <span class="mood-emoji" id="mood-emoji">😍</span>
  </div>
  <!-- Add this below the mood selector -->
  <label for="mood-photo">写真をアップロード</label>
  <input type="file" id="mood-photo" accept="image/*">
  <div id="mood-photo-preview" style="margin:10px 0;"></div>
  <button id="mood-save-btn">保存</button>
  <div id="mood-history" style="margin-top:20px;"></div>
  <div class="mood-graph-section">
    <h3>気分のグラフ</h3>
    <canvas id="moodChart" width="400" height="180"></canvas>
  </div>
</div>
  <!-- みんなのノート Section -->
  <div class="section" id="section-public">
    <div class="public-note-title">みんなのノート</div>
    <div style="text-align:center;margin-bottom:18px;color:#666;">
      他の人が共有した日記を読んで、リアクションやコメントを送りましょう。
    </div>
    <div class="public-journal-list" id="public-list"></div>
  </div>
  <script>
    // --- Section Navigation
    const navs = [
      { btn: "nav-todo", section: "section-todo" },
      { btn: "nav-mood", section: "section-mood" },
      { btn: "nav-journal", section: "section-journal" },
      { btn: "nav-public", section: "section-public" }
    ];
    navs.forEach((nav) => {
      document.getElementById(nav.btn).onclick = () => {
        navs.forEach((n) => {
          document.getElementById(n.btn).classList.remove("active");
          document.getElementById(n.section).classList.remove("active");
        });
        document.getElementById(nav.btn).classList.add("active");
        document.getElementById(nav.section).classList.add("active");
        // On mood tab, re-render the chart (fixes canvas blank bug on switch)
        if(nav.section==="section-mood") setTimeout(drawMoodChart,100);
      };
    });

    // --- ToDo Section (localStorage)
    const todoInput = document.getElementById('todo-input');
    const todoAddBtn = document.getElementById('todo-add-btn');
    const todoListEl = document.getElementById('todo-list');
    let todos = JSON.parse(localStorage.getItem('kokoro_todos') || '[]');
    function renderTodos() {
      todoListEl.innerHTML = '';
      todos.forEach((todo, i) => {
        const li = document.createElement('li');
        li.textContent = todo.text;
        if(todo.done) li.classList.add('done');
        li.onclick = () => {
          todos[i].done = !todos[i].done;
          localStorage.setItem('kokoro_todos', JSON.stringify(todos));
          renderTodos();
        };
        const delBtn = document.createElement('button');
        delBtn.textContent = '削除';
        delBtn.onclick = (e) => {
          e.stopPropagation();
          todos.splice(i,1);
          localStorage.setItem('kokoro_todos', JSON.stringify(todos));
          renderTodos();
        };
        li.appendChild(delBtn);
        todoListEl.appendChild(li);
      });
    }
    todoAddBtn.onclick = () => {
      const val = todoInput.value.trim();
      if(val) {
        todos.unshift({text: val, done: false});
        localStorage.setItem('kokoro_todos', JSON.stringify(todos));
        todoInput.value = '';
        renderTodos();
      }
    };
    renderTodos();

    // --- Mood Section (localStorage & Chart.js)
    const moodSelect = document.getElementById('mood-select');
    const moodEmoji = document.getElementById('mood-emoji');
    const moodSaveBtn = document.getElementById('mood-save-btn');
    const moodHistory = document.getElementById('mood-history');
    const moodMap = {
      "5": "😍", "4": "😊", "3": "😐", "2": "😞", "1": "😡"
    };
    let moods = JSON.parse(localStorage.getItem('kokoro_moods') || '[]');
    moodSelect.onchange = () => {
      moodEmoji.textContent = moodMap[moodSelect.value];
    };
    moodSaveBtn.onclick = () => {
      const val = moodSelect.value;
      moods.push({v:val, date: new Date().toLocaleDateString("ja-JP")});
      localStorage.setItem('kokoro_moods', JSON.stringify(moods));
      renderMoods();
      drawMoodChart();
    };
    function renderMoods() {
      moodHistory.innerHTML = '<b>最近の気分：</b><br>' +
        moods.slice(-8).reverse().map(m=> `<span style="font-size:1.5em">${moodMap[m.v]}</span> (${m.date})`).join('<br>');
    }
    renderMoods();

    // --- Mood Chart ---
    let moodChartInstance = null;
    function drawMoodChart() {
      const ctx = document.getElementById('moodChart').getContext('2d');
      if(moodChartInstance) moodChartInstance.destroy();
      if(moods.length < 2) {
        ctx.clearRect(0,0,400,180);
        return;
      }
      const data = moods.slice(-30); // Last 30
      const labels = data.map(m=>m.date);
      const values = data.map(m=>Number(m.v));
      moodChartInstance = new Chart(ctx, {
        type: 'line',
        data: {
          labels: labels,
          datasets: [{
            label: '気分',
            data: values,
            borderColor: '#ff9362',
            backgroundColor: 'rgba(255,147,98,0.12)',
            fill: true,
            tension: 0.3,
            pointRadius: 5,
            pointBackgroundColor: '#ff9362'
          }]
        },
        options: {
          responsive: false,
          scales: {
            y: {
              min: 1,
              max: 5,
              ticks: {
                stepSize: 1,
                callback: function(value) { return moodMap[value.toString()] || value; }
              }
            }
          },
          plugins: {
            legend: { display: false },
            tooltip: {
              callbacks: {
                label: function(context) {
                  const v = context.parsed.y;
                  return `${moodMap[v.toString()]||""} ${v}`;
                }
              }
            }
          }
        }
      });
    }
    drawMoodChart();

    // --- Journal and Public Note Section (localStorage)
    let journals = JSON.parse(localStorage.getItem('kokoro_journals') || '[]');
    let publicJournals = JSON.parse(localStorage.getItem('kokoro_public_journals') || '[]');
    const journalInput = document.getElementById('journal-input');
    const journalSaveBtn = document.getElementById('journal-save-btn');
    const journalList = document.getElementById('journal-list');
    const journalPublicCheckbox = document.getElementById('journal-public-checkbox');

    function renderJournals() {
      journalList.innerHTML = journals.slice().reverse().map(j =>
        `<div class="journal-item"><div class="date">${j.date}</div><div class="text">${j.text}</div></div>`
      ).join('');
    }
    journalSaveBtn.onclick = () => {
      const text = journalInput.value.trim();
      if (!text) return;
      const data = {text, date: new Date().toLocaleString("ja-JP")};
      journals.push(data);
      localStorage.setItem('kokoro_journals', JSON.stringify(journals));
      if (journalPublicCheckbox.checked) {
        // Save to public with empty reactions/comments if not already present
        publicJournals.push({...data, reactions: {}, comments: []});
        localStorage.setItem('kokoro_public_journals', JSON.stringify(publicJournals));
      }
      journalInput.value = '';
      journalPublicCheckbox.checked = false;
      renderJournals();
      renderPublic();
    };
    renderJournals();

    // --- みんなのノート Section ---
    function renderPublic() {
      const publicList = document.getElementById('public-list');
      publicJournals = JSON.parse(localStorage.getItem('kokoro_public_journals') || '[]');
      publicList.innerHTML = publicJournals.slice().reverse().map((j, idx) => `
        <div class="public-journal-item">
          <div class="date">${j.date}</div>
          <div class="text">${j.text}</div>
          <div class="public-reactions">
            <button ${j._userReact==="like"?"class='selected'":""} onclick="reactPublic(${idx},'like')">👍${j.reactions?.like||0}</button>
            <button ${j._userReact==="love"?"class='selected'":""} onclick="reactPublic(${idx},'love')">❤️${j.reactions?.love||0}</button>
            <button ${j._userReact==="haha"?"class='selected'":""} onclick="reactPublic(${idx},'haha')">😂${j.reactions?.haha||0}</button>
            <button ${j._userReact==="wow"?"class='selected'":""} onclick="reactPublic(${idx},'wow')">😮${j.reactions?.wow||0}</button>
          </div>
          <div class="public-comments">
            ${(j.comments||[]).map(c=>`<div class="public-comment">${escapeHTML(c)}</div>`).join('')}
          </div>
          <div class="public-comment-input-row">
            <input type="text" id="cinput${idx}" placeholder="コメントを追加">
            <button onclick="addCommentPublic(${idx})">送信</button>
          </div>
        </div>
      `).join('');
    }
    // inline helpers for reactions/comments
    window.reactPublic = function(idx, type) {
      let pj = JSON.parse(localStorage.getItem('kokoro_public_journals') || '[]');
      pj[pj.length-1-idx].reactions = pj[pj.length-1-idx].reactions || {};
      ["like","love","haha","wow"].forEach(r=>{ 
        if(pj[pj.length-1-idx]._userReact===r && r!==type) {
          pj[pj.length-1-idx].reactions[r] = Math.max(0,(pj[pj.length-1-idx].reactions[r]||0)-1)
        }
      });
      if(pj[pj.length-1-idx]._userReact === type) {
        pj[pj.length-1-idx].reactions[type] = Math.max(0,(pj[pj.length-1-idx].reactions[type]||0)-1);
        pj[pj.length-1-idx]._userReact = null;
      } else {
        pj[pj.length-1-idx].reactions[type] = (pj[pj.length-1-idx].reactions[type]||0)+1;
        pj[pj.length-1-idx]._userReact = type;
      }
      localStorage.setItem('kokoro_public_journals', JSON.stringify(pj));
      renderPublic();
    }
    window.addCommentPublic = function(idx) {
      const input = document.getElementById('cinput'+idx);
      let pj = JSON.parse(localStorage.getItem('kokoro_public_journals') || '[]');
      if(!input.value.trim()) return;
      pj[pj.length-1-idx].comments = pj[pj.length-1-idx].comments||[];
      pj[pj.length-1-idx].comments.push(input.value);
      input.value = '';
      localStorage.setItem('kokoro_public_journals', JSON.stringify(pj));
      renderPublic();
    }
    function escapeHTML(str) {
      return (str||"").replace(/[<>"'&]/g, c=>({ '<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;','&':'&amp;'})[c]);
    }
    renderPublic();
  </script>:const moodPhotoInput = document.getElementById('mood-photo');
const moodPhotoPreview = document.getElementById('mood-photo-preview');
let moodPhotoDataUrl = null;

// Show preview when a photo is chosen
moodPhotoInput.onchange = function(event) {
  const file = event.target.files[0];
  if (file) {
    const reader = new FileReader();
    reader.onload = function(e) {
      moodPhotoDataUrl = e.target.result;
      moodPhotoPreview.innerHTML = `<img src="${moodPhotoDataUrl}" style="max-width:120px;max-height:120px;border-radius:12px;">`;
    };
    reader.readAsDataURL(file);
  } else {
    moodPhotoDataUrl = null;
    moodPhotoPreview.innerHTML = '';
  }
};

// When saving mood, store photo if present
moodSaveBtn.onclick = () => {
  const val = moodSelect.value;
  moods.push({
    v: val,
    date: new Date().toLocaleDateString("ja-JP"),
    photo: moodPhotoDataUrl
  });
  localStorage.setItem('kokoro_moods', JSON.stringify(moods));
  moodPhotoInput.value = "";
  moodPhotoPreview.innerHTML = "";
  moodPhotoDataUrl = null;
  renderMoods();
  drawMoodChart();
};

// Show photo in mood history, if present
function renderMoods() {
  moodHistory.innerHTML = '<b>最近の気分：</b><br>' +
    moods.slice(-8).reverse().map(m => {
      let html = `<span style="font-size:1.5em">${moodMap[m.v]}</span> (${m.date})`;
      if (m.photo) {
        html += `<br><img src="${m.photo}" style="max-width:90px;max-height:90px;border-radius:8px;margin:4px 0;">`;
      }
      return html;
    }).join('<br>');
}
</body>
</html>

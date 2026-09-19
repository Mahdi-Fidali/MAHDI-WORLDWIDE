<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Mahdi WorldWide News & Interactive Hub</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" />
  <style>
    .fade-in { animation: fadeIn 0.3s ease-in-out; }
    @keyframes fadeIn { from { opacity: 0; transform: translateY(6px); } to { opacity: 1; transform: translateY(0); } }
    @keyframes shake { 0%, 100% { transform: translate(0, 0); } 20%, 60% { transform: translate(-5px, 5px); } 40%, 80% { transform: translate(5px, -5px); } }
    .shake-screen { animation: shake 0.3s ease-in-out infinite; }
    .dyslexia-font { font-family: 'OpenDyslexic', 'Comic Sans MS', sans-serif !important; }
    .reduce-motion * { animation: none !important; transition: none !important; }
    .high-contrast { background-color: #000000 !important; color: #ffffff !important; }
    .sepia { background-color: #704214 !important; color: #fbf0d9 !important; }
  </style>
</head>
<body id="main-body" class="bg-slate-900 text-slate-100 min-h-screen flex flex-col font-sans antialiased selection:bg-sky-500 selection:text-white">

  <!-- TOP TICKER & NAV -->
  <header class="sticky top-0 z-40 bg-slate-900/95 backdrop-blur border-b border-slate-800">
    <div class="bg-sky-900/40 text-sky-300 text-xs py-1 px-4 flex items-center justify-between border-b border-sky-800/40">
      <div class="flex items-center space-x-2 overflow-hidden">
        <span class="bg-sky-500 text-slate-950 font-extrabold text-[10px] px-2 py-0.5 rounded uppercase tracking-wider shrink-0">Live</span>
        <marquee id="ticker-text" scrollamount="5" class="text-slate-300">Breaking: Global space agencies report major milestones in lunar base design — Next-gen autonomous AI networks show breakthrough efficiency in climate modeling...</marquee>
      </div>
      <div class="shrink-0 pl-4 flex items-center gap-2">
        <select id="lang-select" onchange="changeLanguage(this.value)" class="bg-slate-800 text-slate-200 text-xs px-2 py-0.5 rounded border border-slate-700 outline-none cursor-pointer"></select>
      </div>
    </div>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 py-3 flex items-center justify-between gap-4">
      <div class="flex items-center gap-3 cursor-pointer" onclick="resetView()">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-sky-500 to-indigo-600 flex items-center justify-center text-white font-black text-xl shadow-lg shadow-sky-500/20">M</div>
        <div>
          <h1 class="font-extrabold text-lg sm:text-xl tracking-tight text-white flex items-center gap-2">MAHDI <span class="text-sky-400 font-light text-xs sm:text-sm border border-sky-500/40 px-2 py-0.5 rounded-full">WorldWide</span></h1>
          <p class="text-[10px] text-slate-400 font-medium">Independent Digital Journalism & Interactive Hub</p>
        </div>
      </div>

      <!-- Controls -->
      <div class="flex items-center gap-2 sm:gap-3">
        <button onclick="toggleBalloonDrawer()" class="px-3 py-1.5 rounded-xl bg-gradient-to-r from-pink-500 to-rose-500 hover:from-pink-600 hover:to-rose-600 text-white text-xs font-bold shadow-lg shadow-rose-500/20 flex items-center gap-1.5 transition">
          <i class="fa-solid fa-gamepad"></i> <span class="hidden sm:inline">Pop Balloons</span>
        </button>

        <button onclick="openFavorites()" class="relative p-2 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-300 hover:text-amber-400 transition border border-slate-700">
          <i class="fa-solid fa-star text-sm"></i>
          <span id="fav-count" class="absolute -top-1 -right-1 bg-amber-500 text-slate-950 text-[10px] font-black px-1.5 py-0.2 rounded-full">0</span>
        </button>

        <button onclick="toggleSettingsDrawer()" class="p-2 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-300 transition border border-slate-700">
          <i class="fa-solid fa-sliders text-sm"></i>
        </button>

        <button onclick="openAuthModal()" class="px-3 py-1.5 rounded-xl bg-sky-600 hover:bg-sky-500 text-white text-xs font-bold shadow-lg shadow-sky-600/20 transition flex items-center gap-1.5">
          <i class="fa-solid fa-user-circle text-sm"></i> <span id="auth-btn-label">Sign In</span>
        </button>
      </div>
    </div>

    <!-- Category Nav -->
    <div class="max-w-7xl mx-auto px-4 sm:px-6 py-2 overflow-x-auto flex items-center space-x-2 scrollbar-none border-t border-slate-800/80" id="category-bar"></div>
  </header>

  <!-- MAIN CONTENT CONTAINER -->
  <main class="max-w-7xl mx-auto px-4 sm:px-6 py-6 flex-1 w-full grid grid-cols-1 lg:grid-cols-12 gap-6">

    <!-- LEFT / MAIN FEED COLUMN -->
    <section class="lg:col-span-8 space-y-6">

      <!-- SEARCH & VIEW CONTROLS -->
      <div class="bg-slate-800/60 border border-slate-700/80 p-4 rounded-2xl flex flex-col sm:flex-row items-center justify-between gap-3 shadow-md">
        <div class="relative w-full sm:w-72">
          <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400 text-xs"></i>
          <input type="text" id="search-input" onkeyup="handleSearch()" placeholder="Search articles or categories..." class="w-full bg-slate-900 border border-slate-700 rounded-xl pl-9 pr-3 py-2 text-xs text-slate-200 placeholder-slate-500 outline-none focus:border-sky-500 transition" />
        </div>
        <div class="flex items-center justify-between w-full sm:w-auto gap-3">
          <span id="article-count-badge" class="text-xs font-semibold text-slate-400 bg-slate-900 px-3 py-1.5 rounded-xl border border-slate-700">0 articles</span>
          <div class="flex items-center bg-slate-900 p-1 rounded-xl border border-slate-700">
            <button id="view-grid-btn" onclick="setLayoutMode('grid')" class="px-2.5 py-1 text-xs rounded-lg text-sky-400 bg-slate-800 font-medium transition"><i class="fa-solid fa-grip"></i> Grid</button>
            <button id="view-compact-btn" onclick="setLayoutMode('compact')" class="px-2.5 py-1 text-xs rounded-lg text-slate-400 hover:text-white transition"><i class="fa-solid fa-list"></i> Compact</button>
          </div>
        </div>
      </div>

      <!-- ARTICLES DISPLAY -->
      <div id="articles-grid" class="grid grid-cols-1 sm:grid-cols-2 gap-5"></div>
      
      <div class="text-center pt-2">
        <button id="load-more-btn" onclick="loadMoreArticles()" class="px-6 py-2.5 bg-slate-800 hover:bg-slate-700 border border-slate-700 text-sky-400 font-bold text-xs rounded-xl shadow-md transition">Load More Articles</button>
      </div>

      <!-- AI JOB IMPACT MATRIX -->
      <div class="bg-slate-800/60 border border-slate-700/80 rounded-2xl p-5 shadow-xl space-y-4">
        <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between gap-2 border-b border-slate-700/80 pb-3">
          <div>
            <h2 id="ai-tool-title" class="text-lg font-bold text-white flex items-center gap-2"><i class="fa-solid fa-robot text-sky-400"></i> AI Automation Impact Matrix</h2>
            <p id="ai-tool-desc" class="text-xs text-slate-400">Interactive safety ratings & threat analysis across professions</p>
          </div>
          <div class="flex items-center gap-2">
            <label id="filter-risk-label" for="risk-filter" class="text-xs text-slate-400 font-semibold">Filter:</label>
            <select id="risk-filter" onchange="filterAiJobs()" class="bg-slate-900 border border-slate-700 text-xs text-slate-200 px-3 py-1.5 rounded-xl outline-none">
              <option value="all">All Roles</option>
              <option value="safe">Safe Roles (&lt;35%)</option>
              <option value="medium">Medium Risk (35-70%)</option>
              <option value="high">High Risk (&gt;70%)</option>
            </select>
          </div>
        </div>
        <div class="overflow-x-auto">
          <table class="w-full text-left text-xs text-slate-300">
            <thead class="bg-slate-900/80 uppercase text-[10px] text-slate-400 tracking-wider">
              <tr>
                <th class="py-3 px-4 rounded-l-xl">Profession</th>
                <th class="py-3 px-4 text-center">Automation %</th>
                <th class="py-3 px-4">Risk Status</th>
                <th class="py-3 px-4 rounded-r-xl">Industry Forecast</th>
              </tr>
            </thead>
            <tbody id="ai-jobs-tbody" class="divide-y divide-slate-700/50"></tbody>
          </table>
        </div>
      </div>

    </section>

    <!-- RIGHT SIDEBAR -->
    <aside class="lg:col-span-4 space-y-6">

      <!-- FEATURED VIDEO MEDIA PLAYER -->
      <div class="bg-slate-800/60 border border-slate-700/80 rounded-2xl p-4 shadow-xl space-y-3">
        <h3 class="font-bold text-sm text-white flex items-center gap-2"><i class="fa-brands fa-youtube text-red-500 text-base"></i> Video Desk</h3>
        <div class="aspect-video w-full bg-slate-950 rounded-xl overflow-hidden border border-slate-700/80">
          <iframe id="featured-video-iframe" class="w-full h-full" src="" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
        </div>
        <p id="featured-video-caption" class="text-xs font-semibold text-slate-300 truncate">Loading video...</p>
        <div id="youtube-videos-list" class="space-y-2 max-h-48 overflow-y-auto pr-1"></div>
      </div>

      <!-- DAILY POLL -->
      <div id="poll-widget" class="bg-slate-800/60 border border-slate-700/80 rounded-2xl p-4 shadow-xl"></div>

      <!-- EXPANDED KNOWLEDGE QUIZ -->
      <div class="bg-slate-800/60 border border-slate-700/80 rounded-2xl p-4 shadow-xl space-y-3">
        <div class="flex items-center justify-between border-b border-slate-700/60 pb-2">
          <h3 class="font-bold text-sm text-white flex items-center gap-2"><i class="fa-solid fa-graduation-cap text-emerald-400"></i> Interactive Knowledge Challenge</h3>
          <span id="quiz-score-badge" class="bg-emerald-950 text-emerald-400 border border-emerald-800 text-[10px] font-black px-2 py-0.5 rounded-full">Score: 0</span>
        </div>
        <div id="quiz-widget"></div>
      </div>

      <!-- READING HISTORY -->
      <div class="bg-slate-800/60 border border-slate-700/80 rounded-2xl p-4 shadow-xl space-y-3">
        <div class="flex items-center justify-between">
          <h3 class="font-bold text-xs text-slate-300 uppercase tracking-wider"><i class="fa-solid fa-clock-rotate-left mr-1 text-sky-400"></i> Recent History</h3>
          <button onclick="clearHistory()" class="text-[10px] text-slate-500 hover:text-slate-300">Clear</button>
        </div>
        <div id="history-list-widget" class="space-y-2 text-xs"></div>
      </div>

    </aside>
  </main>

  <!-- SCREECH RED BUTTON (BOTTOM LEFT FIXED) -->
  <div class="fixed bottom-6 left-6 z-50 flex flex-col items-center">
    <div id="screech-tooltip" class="hidden mb-2 bg-red-950 border border-red-600 text-red-200 text-[10px] font-bold px-2 py-1 rounded shadow-lg animate-bounce">
      🔊 HIGH PITCH SCREECH WARNING!
    </div>
    <button id="screech-red-btn" onclick="triggerHighPitchScreech()" onmouseenter="document.getElementById('screech-tooltip').classList.remove('hidden')" onmouseleave="document.getElementById('screech-tooltip').classList.add('hidden')" class="w-16 h-16 rounded-full bg-gradient-to-b from-red-500 to-red-800 border-4 border-red-950 shadow-2xl shadow-red-600/50 hover:scale-110 active:scale-95 transition-all flex items-center justify-center cursor-pointer group">
      <span class="text-white font-black text-xs uppercase tracking-wider group-hover:animate-pulse text-center leading-tight">DO NOT<br>PRESS</span>
    </button>
  </div>

  <!-- STANDALONE AI ASSISTANT FAB BUTTON -->
  <button onclick="toggleAiPanel()" class="fixed bottom-6 right-6 z-50 w-14 h-14 rounded-full bg-sky-500 hover:bg-sky-400 text-slate-950 font-black text-2xl shadow-2xl shadow-sky-500/40 flex items-center justify-center transition hover:scale-105 active:scale-95">
    <i class="fa-solid fa-robot"></i>
  </button>

  <!-- AI ASSISTANT CHAT PANEL MODAL -->
  <div id="ai-panel" class="fixed bottom-24 right-6 z-50 w-96 max-w-[calc(100vw-3rem)] bg-slate-900 border border-slate-700 rounded-2xl shadow-2xl flex-col hidden overflow-hidden fade-in">
    <div class="bg-slate-800 px-4 py-3 border-b border-slate-700 flex items-center justify-between">
      <div class="flex items-center gap-2">
        <div class="w-2.5 h-2.5 rounded-full bg-emerald-400 animate-pulse"></div>
        <h3 class="font-extrabold text-xs text-white uppercase tracking-wider">Standalone AI Assistant</h3>
      </div>
      <button onclick="toggleAiPanel()" class="text-slate-400 hover:text-white text-sm"><i class="fa-solid fa-xmark"></i></button>
    </div>

    <!-- PRESET 3-OPTION ROBLOX STORY STYLE PROMPTS -->
    <div class="p-3 bg-slate-950 border-b border-slate-800 space-y-1.5">
      <p class="text-[10px] font-bold text-sky-400 uppercase tracking-wider">Quick Select Questions (Choose One):</p>
      <div class="flex flex-col gap-1.5">
        <button onclick="sendPresetQuery('Explain the AI Job Risk Matrix in simple terms.')" class="text-left text-xs bg-slate-800/90 hover:bg-sky-900/60 text-slate-200 hover:text-sky-300 px-2.5 py-1.5 rounded-lg border border-slate-700 transition line-clamp-1">
          1️⃣ Explain the AI Job Risk Matrix in simple terms.
        </button>
        <button onclick="sendPresetQuery('What are the latest updates in space exploration?')" class="text-left text-xs bg-slate-800/90 hover:bg-sky-900/60 text-slate-200 hover:text-sky-300 px-2.5 py-1.5 rounded-lg border border-slate-700 transition line-clamp-1">
          2️⃣ What are the latest updates in space exploration?
        </button>
        <button onclick="sendPresetQuery('How does the four-day workweek pilot program work?')" class="text-left text-xs bg-slate-800/90 hover:bg-sky-900/60 text-slate-200 hover:text-sky-300 px-2.5 py-1.5 rounded-lg border border-slate-700 transition line-clamp-1">
          3️⃣ How does the four-day workweek pilot program work?
        </button>
      </div>
    </div>

    <div id="ai-chat-log" class="p-4 h-64 overflow-y-auto space-y-3 text-xs"></div>

    <div class="p-3 bg-slate-800 border-t border-slate-700 flex items-center gap-2">
      <input type="text" id="ai-chat-input" onkeydown="if(event.key==='Enter') sendAiMessage()" placeholder="Ask anything about the news..." class="flex-1 bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-xs text-slate-200 outline-none focus:border-sky-500" />
      <button onclick="sendAiMessage()" class="px-3 py-2 bg-sky-500 hover:bg-sky-400 text-slate-950 font-bold text-xs rounded-xl transition"><i class="fa-solid fa-paper-plane"></i></button>
    </div>
  </div>

  <!-- SLIDE-OUT BALLOON POPPING GAME DRAWER -->
  <div id="balloon-drawer" class="fixed inset-y-0 right-0 z-50 w-80 max-w-full bg-slate-900 border-l border-slate-800 shadow-2xl transform translate-x-full transition-transform duration-300 flex flex-col">
    <div class="p-4 bg-slate-800 border-b border-slate-700 flex items-center justify-between">
      <h3 class="font-extrabold text-sm text-white flex items-center gap-2"><i class="fa-solid fa-balloon text-pink-500"></i> Balloon Pop Minigame</h3>
      <button onclick="toggleBalloonDrawer()" class="text-slate-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
    </div>
    <div class="p-4 flex-1 flex flex-col justify-between">
      <div class="flex items-center justify-between text-xs font-bold text-slate-300 bg-slate-800/80 p-2.5 rounded-xl border border-slate-700">
        <span>Score: <span id="balloon-score" class="text-pink-400 font-extrabold">0</span></span>
        <span>Popped: <span id="balloon-popped-count" class="text-emerald-400 font-extrabold">0</span></span>
      </div>
      
      <!-- Interactive Game Area -->
      <div id="balloon-canvas" class="relative w-full flex-1 bg-slate-950 rounded-2xl border border-slate-800 my-4 overflow-hidden flex items-center justify-center">
        <p id="balloon-start-msg" class="text-xs text-slate-500 italic text-center px-4">Click "Start Game" to spawn floating balloons!</p>
      </div>

      <div class="flex gap-2">
        <button onclick="startBalloonGame()" class="flex-1 py-2.5 bg-gradient-to-r from-pink-500 to-rose-500 text-white font-extrabold text-xs rounded-xl shadow-lg transition">Start Game</button>
        <button onclick="resetBalloonGame()" class="px-4 py-2.5 bg-slate-800 text-slate-300 font-bold text-xs rounded-xl border border-slate-700">Reset</button>
      </div>
    </div>
  </div>

  <!-- ARTICLE MODAL -->
  <div id="article-modal" class="fixed inset-0 z-50 bg-slate-950/80 backdrop-blur-md hidden flex items-center justify-center p-4">
    <div class="bg-slate-900 border border-slate-700 max-w-2xl w-full max-h-[90vh] rounded-2xl overflow-hidden shadow-2xl flex flex-col fade-in">
      <div class="p-4 bg-slate-800/80 border-b border-slate-700 flex items-center justify-between">
        <span id="modal-tag" class="text-[10px] font-extrabold uppercase px-2.5 py-1 bg-sky-950 text-sky-400 border border-sky-800 rounded-full">Category</span>
        <div class="flex items-center gap-2">
          <button id="modal-fav-btn" onclick="toggleFavorite(currentArticleId)" class="p-2 text-slate-400 hover:text-amber-400 transition"><i class="fa-regular fa-star"></i></button>
          <button onclick="speakArticleContent()" class="p-2 text-slate-400 hover:text-sky-400 transition" title="Read Aloud"><i class="fa-solid fa-volume-high"></i></button>
          <button onclick="translateArticleAI()" class="p-2 text-slate-400 hover:text-emerald-400 transition" title="Auto Translate"><i class="fa-solid fa-language"></i></button>
          <button onclick="closeModal()" class="p-2 text-slate-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
        </div>
      </div>
      <div class="p-6 overflow-y-auto space-y-4">
        <h2 id="modal-title" class="text-xl font-black text-white leading-tight"></h2>
        <p id="modal-meta" class="text-xs text-slate-400 font-semibold border-b border-slate-800 pb-2"></p>
        <img id="modal-img" src="" alt="Cover" class="w-full h-56 object-cover rounded-xl border border-slate-800" />
        <div id="modal-translate-note" class="text-xs text-emerald-400 bg-emerald-950/60 p-2.5 rounded-xl border border-emerald-800/80 hidden"></div>
        <div id="modal-content" class="space-y-3 text-xs sm:text-sm text-slate-300 leading-relaxed"></div>
      </div>
    </div>
  </div>

  <!-- FAVORITES MODAL -->
  <div id="favorites-modal" class="fixed inset-0 z-50 bg-slate-950/80 backdrop-blur-md hidden items-center justify-center p-4">
    <div class="bg-slate-900 border border-slate-700 max-w-md w-full rounded-2xl p-5 shadow-2xl space-y-4">
      <div class="flex items-center justify-between border-b border-slate-800 pb-3">
        <h3 class="font-bold text-white text-sm"><i class="fa-solid fa-star text-amber-400 mr-2"></i> Saved Bookmarks</h3>
        <button onclick="closeFavorites()" class="text-slate-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      </div>
      <div id="favorites-list" class="space-y-2 max-h-60 overflow-y-auto"></div>
    </div>
  </div>

  <!-- SETTINGS DRAWER -->
  <div id="settings-drawer" class="fixed inset-y-0 right-0 z-50 w-72 bg-slate-900 border-l border-slate-800 shadow-2xl transform translate-x-full transition-transform duration-300 p-5 space-y-5">
    <div class="flex items-center justify-between border-b border-slate-800 pb-3">
      <h3 class="font-bold text-white text-sm"><i class="fa-solid fa-sliders mr-2 text-sky-400"></i> Settings</h3>
      <button onclick="toggleSettingsDrawer()" class="text-slate-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
    </div>
    
    <div class="space-y-3 text-xs">
      <div>
        <label class="font-bold text-slate-300 block mb-1">Theme Contrast</label>
        <div class="grid grid-cols-2 gap-2">
          <button onclick="setTheme('dark')" class="p-2 rounded-lg bg-slate-800 border border-slate-700 text-slate-200 font-semibold">Dark</button>
          <button onclick="setTheme('high-contrast')" class="p-2 rounded-lg bg-black border border-white text-white font-semibold">Contrast</button>
        </div>
      </div>

      <div>
        <label class="font-bold text-slate-300 block mb-1">Font Size</label>
        <select onchange="setFontSize(this.value)" class="w-full bg-slate-800 border border-slate-700 rounded-lg p-2 text-slate-200 outline-none">
          <option value="14px">Small</option>
          <option value="16px" selected>Normal</option>
          <option value="18px">Large</option>
        </select>
      </div>

      <div class="pt-2 border-t border-slate-800 space-y-2">
        <label class="flex items-center justify-between cursor-pointer">
          <span class="text-slate-300 font-semibold">Reduce Motion</span>
          <input type="checkbox" id="s-reducemotion" class="rounded bg-slate-800 border-slate-700 text-sky-500 focus:ring-0" />
        </label>
        <label class="flex items-center justify-between cursor-pointer">
          <span class="text-slate-300 font-semibold">Dyslexia Font</span>
          <input type="checkbox" id="s-dyslexia" class="rounded bg-slate-800 border-slate-700 text-sky-500 focus:ring-0" />
        </label>
        <label class="flex items-center justify-between cursor-pointer">
          <span class="text-slate-300 font-semibold">Data Saver Mode</span>
          <input type="checkbox" id="s-datasaver" class="rounded bg-slate-800 border-slate-700 text-sky-500 focus:ring-0" />
        </label>
      </div>

      <button onclick="exportMyData()" class="w-full py-2 bg-slate-800 hover:bg-slate-700 text-sky-400 font-bold rounded-xl border border-slate-700 transition mt-4">Export Backup Data</button>
    </div>
  </div>

  <!-- AUTH DEMO MODAL -->
  <div id="auth-modal" class="fixed inset-0 z-50 bg-slate-950/80 backdrop-blur-md hidden flex items-center justify-center p-4">
    <div class="bg-slate-900 border border-slate-700 max-w-sm w-full rounded-2xl p-6 shadow-2xl space-y-4">
      <div class="flex items-center justify-between border-b border-slate-800 pb-3">
        <h3 class="font-bold text-white text-sm">Account Sign In</h3>
        <button onclick="closeAuthModal()" class="text-slate-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      </div>
      <form onsubmit="handleLoginSubmit(event)" class="space-y-3 text-xs">
        <div>
          <label class="block font-semibold text-slate-300 mb-1">Username / Email</label>
          <input type="text" id="auth-email" required placeholder="Enter username..." class="w-full bg-slate-800 border border-slate-700 rounded-xl p-2.5 text-slate-200 outline-none focus:border-sky-500" />
        </div>
        <p id="auth-status-msg" class="text-[10px] text-emerald-400 italic"></p>
        <button type="submit" class="w-full py-2.5 bg-sky-500 hover:bg-sky-400 text-slate-950 font-extrabold rounded-xl transition">Sign In (Local Demo)</button>
      </form>
    </div>
  </div>

  <!-- COOKIE BANNER -->
  <div id="cookie-banner" class="fixed bottom-0 inset-x-0 z-40 bg-slate-900 border-t border-slate-800 p-4 shadow-2xl flex flex-col sm:flex-row items-center justify-between gap-3 text-xs">
    <p class="text-slate-400">We use essential local browser storage to save your preferences and bookmarks.</p>
    <div class="flex gap-2">
      <button onclick="acceptCookies(false)" class="px-3 py-1.5 bg-slate-800 text-slate-300 rounded-lg border border-slate-700">Essential</button>
      <button onclick="acceptCookies(true)" class="px-3 py-1.5 bg-sky-600 text-white font-bold rounded-lg">Accept All</button>
    </div>
  </div>

  <!-- APPLICATION DATA & LOGIC -->
  <script>
    /* ============ DATA STRUCTURES ============ */
    const LANGS = [
      { code: 'en', name: 'English', dir: 'ltr' },
      { code: 'fr', name: 'Français', dir: 'ltr' },
      { code: 'ar', name: 'العربية', dir: 'rtl' }
    ];

    const uiStrings = {
      en: { topStories: "Top Stories", search: "Search articles...", aiTitle: "AI Automation Matrix", aiDesc: "Risk predictions for major jobs", filterRisk: "Risk:", signIn: "Sign In", readMore: "Read Story", loadMore: "Load More Articles", breaking: "Breaking: Space & tech innovations hit new operational peaks..." },
      fr: { topStories: "A la une", search: "Rechercher...", aiTitle: "Matrice d'IA", aiDesc: "Risques d'automatisation des métiers", filterRisk: "Risque:", signIn: "Connexion", readMore: "Lire l'article", loadMore: "Charger plus", breaking: "En direct: Avancées technologiques majeures enregistrées..." },
      ar: { topStories: "أبرز الأخبار", search: "بحث في الأخبار...", aiTitle: "مصفوفة الذكاء الاصطناعي", aiDesc: "مؤشرات أتمتة الوظائف", filterRisk: "المخاطر:", signIn: "تسجيل الدخول", readMore: "اقرأ المزيد", loadMore: "تحميل المزيد", breaking: "عاجل: إنجازات جديدة في مجالات الفضاء والتقنية..." }
    };

    const categoryNames = {
      en: { Technology: "Technology", Space: "Space", Society: "Society", Science: "Science", Health: "Health" },
      fr: { Technology: "Technologie", Space: "Espace", Society: "Société", Science: "Science", Health: "Santé" },
      ar: { Technology: "تكنولوجيا", Space: "فضاء", Society: "مجتمع", Science: "علوم", Health: "صحة" }
    };

    const articles = [
      { id: "space-debris", cat: "Space", img: "https://picsum.photos/seed/debris/800/600", title: "Orbital Debris Tracking Systems Expanded Globally", p: ["Space tracking radar networks have increased capacity to catalog small orbital debris. Operational satellites face constant collision avoidance maneuvers.", "Active cleanup projects utilizing harpoons and robotic catch nets are undergoing testing to safely deorbit defunct satellites."] },
      { id: "moon-water", cat: "Space", img: "https://picsum.photos/seed/moon/800/600", title: "Water Ice Deposits Confirmed in Lunar Craters", p: ["Spectroscopic data confirms significant water ice concentrations inside shadowed polar craters.", "Resources could be converted to drinking water, oxygen, and liquid propellant for deep space travel."] },
      { id: "astronaut-training", cat: "Space", img: "https://picsum.photos/seed/astronaut/800/600", title: "How Astronauts Train for Deep Space Confinement", p: ["Isolation experiments inside sealed terrestrial research pods simulate mental stress for deep space journeys.", "Automated emergency drill routines ensure crew quick-response capabilities under extreme pressure."] },
      { id: "pedestrian-streets", cat: "Society", img: "https://picsum.photos/seed/city/800/600", title: "Urban Centers Redesigning Transit for Pedestrians", p: ["Metropolitan zones converting multi-lane roads into car-free plazas report boosts in local foot traffic.", "Integrated public transport connections prove vital to prevent traffic congestion spillover into neighboring residential streets."] },
      { id: "digital-identity", cat: "Society", img: "https://picsum.photos/seed/digital/800/600", title: "Digital ID Frameworks Adopted Across Nations", p: ["National digital verification platforms offer streamlined access to public services while raising privacy concerns.", "Zero-knowledge proof cryptography enables age verification without sharing identity records."] },
      { id: "four-day-week", cat: "Society", img: "https://picsum.photos/seed/work/800/600", title: "Global Four-Day Workweek Pilots Show Positive Output", p: ["Trial programs across office-based industries demonstrate steady productivity alongside reduced burnout.", "Client-facing service roles adapt shift rotations to maintain uninterrupted weekly coverage."] },
      { id: "aging-pensions", cat: "Society", img: "https://picsum.photos/seed/pension/800/600", title: "Economic Models Adjusting for Aging Demographics", p: ["Shifting demographic pyramids prompt structural adjustments to national public pension systems.", "Policy measures combine retirement age adjustments with private savings incentives."] },
      { id: "local-news", cat: "Society", img: "https://picsum.photos/seed/news/800/600", title: "Nonprofit Models Reshaping Community Newsrooms", p: ["Reader-funded journalism initiatives fill coverage gaps left by traditional print advertising declines.", "Independent local outlets preserve civic transparency and regional council reporting."] }
    ];

    const aiJobsDatabase = [
      { id: "dev", title: "Software Developer", risk: "medium", score: 60, note: "AI speeds boilerplate writing; architecture stays human-led." },
      { id: "music", title: "Music Producer / Composer", risk: "safe", score: 25, note: "Generative tools assist sound design; artistic vision remains human." },
      { id: "chess", title: "Chess Coach", risk: "safe", score: 15, note: "Engines calculate moves; psychological coaching remains human." },
      { id: "data", title: "Data Entry Specialist", risk: "high", score: 92, note: "Automated OCR agents replace routine manual entry." },
      { id: "nurse", title: "Registered Nurse", risk: "safe", score: 14, note: "Patient care and critical physical triage require human presence." }
    ];

    const youtubeVideos = [
      { id: "GAAs2Q3Yh-Q", title: "Avengers: Doomsday Announcement" },
      { id: "L7SDkHafU7k", title: "Robert Downey Jr. as Doctor Doom" },
      { id: "hI9HQfCAw64", title: "Starship Space Exploration Test" }
    ];

    const dailyPoll = {
      question: "Which field requires the most expansion this year?",
      options: ["AI & Automation", "Deep Space Missions", "Urban Renewal", "Renewable Energy"]
    };

    const quizQuestions = [
      { q: "What does spaced repetition improve?", opts: ["Long-term memory retention", "Screen resolution", "Battery life"], correct: 0 },
      { q: "What is a 'passkey' designed to replace?", opts: ["Passwords", "Usernames", "IP addresses"], correct: 0 },
      { q: "What creates the color variations in auroras?", opts: ["Atmospheric gas type & altitude", "Lunar phases", "Ocean surface reflections"], correct: 0 },
      { q: "What is the primary benefit of reusable rocket boosters?", opts: ["Cutting launch costs drastically", "Eliminating fuel usage", "Permanent orbital stationing"], correct: 0 },
      { q: "What drives interest in supply chain nearshoring?", opts: ["Mitigating single-source disruption risk", "Doubling transit distances", "Avoiding automation"], correct: 0 },
      { q: "What cryptocurrency concept enables privacy-first verification?", opts: ["Zero-Knowledge Proofs", "Proof of Work", "Centralized Ledger"], correct: 0 },
      { q: "Which gas is primarily processed from lunar polar ice?", opts: ["Oxygen & Hydrogen", "Argon", "Methane"], correct: 0 },
      { q: "What is the key goal of urban pedestrianization?", opts: ["Boosting foot traffic & reducing noise", "Increasing street parking", "Higher vehicle speeds"], correct: 0 },
      { q: "What does LLM stand for in modern AI?", opts: ["Large Language Model", "Linear Logic Matrix", "Local Learning Mechanism"], correct: 0 },
      { q: "What feature preserves readability in low light?", opts: ["High Contrast Dark Mode", "Increased Gamma", "Blue Light Amplification"], correct: 0 }
    ];

    /* ============ APP STATE ============ */
    let currentLang = 'en';
    let currentCategory = 'all';
    let currentLayout = 'grid';
    let visibleCount = 6;
    let currentArticleId = null;
    let currentUser = null;
    let quizIndex = 0;
    let quizScore = 0;

    /* ============ STORAGE HELPERS ============ */
    function lsGet(key, fallback){ try{ const v = localStorage.getItem(key); return v ? JSON.parse(v) : fallback; }catch(e){ return fallback; } }
    function lsSet(key, val){ try{ localStorage.setItem(key, JSON.stringify(val)); }catch(e){} }

    /* ============ UI & RENDERERS ============ */
    function populateLangSelect(){
      const sel = document.getElementById('lang-select');
      sel.innerHTML = LANGS.map(l => `<option value="${l.code}">${l.name}</option>`).join('');
      sel.value = currentLang;
    }

    function changeLanguage(lang){
      currentLang = lang;
      lsSet('mahdi_lang', lang);
      const meta = LANGS.find(l=>l.code===lang) || LANGS[0];
      document.getElementById('main-body').setAttribute('dir', meta.dir);
      const t = uiStrings[lang] || uiStrings.en;
      document.getElementById('ticker-text').innerText = t.breaking;
      document.getElementById('search-input').placeholder = t.search;
      document.getElementById('ai-tool-title').innerText = t.aiTitle;
      document.getElementById('ai-tool-desc').innerText = t.aiDesc;
      document.getElementById('filter-risk-label').innerText = t.filterRisk;
      document.getElementById('auth-btn-label').innerText = currentUser ? currentUser.name : t.signIn;
      document.getElementById('load-more-btn').innerText = t.loadMore;
      renderCategories();
      renderArticles();
      renderAiJobsTable();
      renderPoll();
      renderQuiz();
    }

    function renderCategories(){
      const t = categoryNames[currentLang] || categoryNames.en;
      const cats = ['all', 'Space', 'Society', 'Technology'];
      const bar = document.getElementById('category-bar');
      bar.innerHTML = cats.map(cat => {
        const label = cat === 'all' ? (uiStrings[currentLang]?.topStories || 'All') : (t[cat] || cat);
        return `<button class="px-3.5 py-1.5 rounded-lg text-xs font-semibold transition ${cat===currentCategory?'bg-sky-600 text-white shadow-md':'bg-slate-800/80 text-slate-300 hover:bg-slate-700'}" onclick="filterCategory('${cat}')">${label}</button>`;
      }).join('');
    }
    function filterCategory(cat){ currentCategory = cat; visibleCount = 6; renderCategories(); renderArticles(); }

    function renderArticles(searchQ=""){
      const grid = document.getElementById('articles-grid');
      let filtered = articles;
      if (currentCategory !== 'all') filtered = filtered.filter(a => a.cat === currentCategory);
      const q = (searchQ || document.getElementById('search-input').value || "").trim().toLowerCase();
      if (q) filtered = filtered.filter(a => a.title.toLowerCase().includes(q) || a.cat.toLowerCase().includes(q));

      document.getElementById('article-count-badge').innerText = `${filtered.length} articles`;
      const shown = filtered.slice(0, visibleCount);
      document.getElementById('load-more-btn').style.display = shown.length < filtered.length ? 'inline-block' : 'none';

      grid.innerHTML = "";
      const t = uiStrings[currentLang] || uiStrings.en;
      const cn = categoryNames[currentLang] || categoryNames.en;
      const favs = lsGet('mahdi_favorites', []);

      shown.forEach(item => {
        const card = document.createElement('div');
        const isFav = favs.includes(item.id);
        if (currentLayout === 'grid'){
          card.className = "bg-slate-800/60 border border-slate-700/80 rounded-2xl overflow-hidden shadow-xl hover:border-sky-500/60 transition group cursor-pointer flex flex-col fade-in";
          card.innerHTML = `
            <div class="h-40 overflow-hidden relative" onclick="openArticle('${item.id}')">
              <img src="${item.img}" loading="lazy" alt="Cover" class="w-full h-full object-cover group-hover:scale-105 transition duration-500">
              <span class="absolute top-3 left-3 bg-slate-900/80 backdrop-blur text-sky-400 text-[10px] font-extrabold px-2.5 py-1 rounded-full border border-slate-700 uppercase">${cn[item.cat]||item.cat}</span>
              <button onclick="event.stopPropagation();toggleFavorite('${item.id}')" class="absolute top-3 right-3 w-7 h-7 rounded-full bg-slate-900/80 flex items-center justify-center ${isFav?'text-amber-400':'text-slate-300'} hover:text-amber-400"><i class="fa-${isFav?'solid':'regular'} fa-star text-xs"></i></button>
            </div>
            <div class="p-4 flex-1 flex flex-col justify-between space-y-3" onclick="openArticle('${item.id}')">
              <h3 class="font-bold text-slate-100 group-hover:text-sky-400 transition leading-snug line-clamp-2 text-sm">${item.title}</h3>
              <div class="flex items-center justify-between text-xs text-slate-400 pt-2 border-t border-slate-700/50">
                <span class="text-[10px]"><i class="fa-regular fa-clock mr-1"></i> Sept 19, 2026</span>
                <span class="text-sky-400 font-semibold text-xs flex items-center gap-1">${t.readMore} <i class="fa-solid fa-arrow-right text-[10px]"></i></span>
              </div>
            </div>`;
        } else {
          card.className = "bg-slate-800/60 border border-slate-700/80 rounded-xl p-3 flex items-center justify-between hover:border-sky-500/60 transition cursor-pointer fade-in";
          card.onclick = () => openArticle(item.id);
          card.innerHTML = `
            <div class="flex items-center space-x-3">
              <img src="${item.img}" loading="lazy" class="w-14 h-14 rounded-lg object-cover">
              <div><span class="text-[9px] font-bold text-sky-400 uppercase">${cn[item.cat]||item.cat}</span>
              <h4 class="font-bold text-xs text-slate-100 line-clamp-1">${item.title}</h4></div>
            </div>
            <i class="fa-solid fa-chevron-right text-slate-500 text-xs"></i>`;
        }
        grid.appendChild(card);
      });
    }
    function loadMoreArticles(){ visibleCount += 4; renderArticles(); }
    function handleSearch(){ visibleCount = 6; renderArticles(document.getElementById('search-input').value); }
    function setLayoutMode(mode){
      currentLayout = mode;
      document.getElementById('view-grid-btn').className = mode==='grid' ? "px-2.5 py-1 text-xs rounded-md text-sky-400 bg-slate-700 font-medium transition" : "px-2.5 py-1 text-xs rounded-md text-slate-400 hover:text-white transition";
      document.getElementById('view-compact-btn').className = mode==='compact' ? "px-2.5 py-1 text-xs rounded-md text-sky-400 bg-slate-700 font-medium transition" : "px-2.5 py-1 text-xs rounded-md text-slate-400 hover:text-white transition";
      renderArticles();
    }

    /* ============ ARTICLE MODAL & SPEECH ============ */
    function openArticle(id){
      const item = articles.find(a => a.id === id);
      if (!item) return;
      currentArticleId = id;
      const cn = categoryNames[currentLang] || categoryNames.en;
      document.getElementById('modal-tag').innerText = cn[item.cat] || item.cat;
      document.getElementById('modal-title').innerText = item.title;
      document.getElementById('modal-meta').innerText = `Mahdi WorldWide Bureau • Sept 19, 2026`;
      document.getElementById('modal-img').src = item.img;
      document.getElementById('modal-translate-note').classList.add('hidden');
      document.getElementById('modal-content').innerHTML = item.p.map(p => `<p>${p}</p>`).join('');
      document.getElementById('article-modal').classList.remove('hidden');
      updateModalFavIcon();

      let history = lsGet('mahdi_news_history', []);
      history.unshift({title:item.title, date:new Date().toLocaleTimeString()});
      lsSet('mahdi_news_history', history.slice(0,6));
      updateHistoryWidget();
    }
    function closeModal(){
      document.getElementById('article-modal').classList.add('hidden');
      if ('speechSynthesis' in window) window.speechSynthesis.cancel();
    }
    function speakArticleContent(){
      if (!('speechSynthesis' in window)) { alert("Text-to-speech isn't supported in this browser."); return; }
      window.speechSynthesis.cancel();
      const text = document.getElementById('modal-title').innerText + ". " + document.getElementById('modal-content').innerText;
      const u = new SpeechSynthesisUtterance(text);
      u.rate = 1.0;
      window.speechSynthesis.speak(u);
    }
    function translateArticleAI(){
      const note = document.getElementById('modal-translate-note');
      note.classList.remove('hidden');
      note.innerText = "✨ Auto-translated using embedded local language engine.";
    }

    /* ============ BOOKMARKS & HISTORY ============ */
    function toggleFavorite(id){
      let favs = lsGet('mahdi_favorites', []);
      if (favs.includes(id)) favs = favs.filter(f => f !== id); else favs.push(id);
      lsSet('mahdi_favorites', favs);
      document.getElementById('fav-count').innerText = favs.length;
      updateModalFavIcon();
      renderArticles();
    }
    function updateModalFavIcon(){
      const favs = lsGet('mahdi_favorites', []);
      const btn = document.getElementById('modal-fav-btn');
      if (!btn || !currentArticleId) return;
      btn.innerHTML = favs.includes(currentArticleId) ? '<i class="fa-solid fa-star text-amber-400"></i>' : '<i class="fa-regular fa-star"></i>';
    }
    function openFavorites(){
      const favs = lsGet('mahdi_favorites', []);
      const list = document.getElementById('favorites-list');
      if (!favs.length){ list.innerHTML = '<p class="italic text-slate-500 text-xs">No saved articles yet — tap the star on any story.</p>'; }
      else {
        list.innerHTML = favs.map(id => {
          const a = articles.find(x=>x.id===id);
          if (!a) return '';
          return `<div class="flex items-center justify-between p-2 bg-slate-800/60 rounded-lg border border-slate-700/50 text-xs">
            <span class="cursor-pointer hover:text-sky-400 font-medium truncate max-w-[200px]" onclick="closeFavorites();openArticle('${a.id}')">${a.title}</span>
            <button onclick="toggleFavorite('${a.id}');openFavorites();" class="text-amber-400 hover:text-red-400"><i class="fa-solid fa-xmark"></i></button>
          </div>`;
        }).join('');
      }
      document.getElementById('favorites-modal').classList.remove('hidden');
      document.getElementById('favorites-modal').classList.add('flex');
    }
    function closeFavorites(){ document.getElementById('favorites-modal').classList.add('hidden'); document.getElementById('favorites-modal').classList.remove('flex'); }

    function updateHistoryWidget(){
      const widget = document.getElementById('history-list-widget');
      const history = lsGet('mahdi_news_history', []);
      if (!history.length){ widget.innerHTML = `<p class="italic text-slate-500">No recent articles read yet.</p>`; return; }
      widget.innerHTML = history.map(h => `
        <div class="p-2 bg-slate-900/60 rounded-lg border border-slate-700/50 flex items-center justify-between">
          <span class="font-medium text-slate-200 truncate max-w-[160px]">${h.title}</span>
          <span class="text-[9px] text-slate-500">${h.date}</span>
        </div>`).join('');
    }
    function clearHistory(){ lsSet('mahdi_news_history', []); updateHistoryWidget(); }

    /* ============ AI JOBS TABLE ============ */
    function renderAiJobsTable(filterRisk="all"){
      const tbody = document.getElementById('ai-jobs-tbody');
      let list = aiJobsDatabase;
      if (filterRisk !== "all") list = list.filter(j => j.risk === filterRisk);
      tbody.innerHTML = list.map(job => {
        let badge = job.risk === 'high'
          ? `<span class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-red-950 text-red-400 border border-red-800">High (${job.score}%)</span>`
          : job.risk === 'medium'
          ? `<span class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-amber-950 text-amber-400 border border-amber-800">Medium (${job.score}%)</span>`
          : `<span class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-emerald-950 text-emerald-400 border border-emerald-800">Safe (${job.score}%)</span>`;
        return `<tr class="hover:bg-slate-800/50 transition">
          <td class="py-2.5 px-4 font-bold text-slate-200">${job.title}</td>
          <td class="py-2.5 px-4 text-center"><div class="w-full bg-slate-900 rounded-full h-1.5 max-w-[70px] mx-auto overflow-hidden"><div class="h-full ${job.score>70?'bg-red-500':job.score>35?'bg-amber-500':'bg-emerald-500'}" style="width:${job.score}%"></div></div></td>
          <td class="py-2.5 px-4">${badge}</td>
          <td class="py-2.5 px-4 text-[11px] text-slate-400">${job.note}</td>
        </tr>`;
      }).join('');
    }
    function filterAiJobs(){ renderAiJobsTable(document.getElementById('risk-filter').value); }

    /* ============ MEDIA & POLL ============ */
    function renderYouTubeSidebar(){
      document.getElementById('youtube-videos-list').innerHTML = youtubeVideos.map(v => `
        <div onclick="playVideo('${v.id}','${v.title.replace(/'/g,"\\'")}')" class="p-2 rounded-xl bg-slate-900/80 border border-slate-700/60 hover:border-sky-500 flex items-center space-x-2.5 cursor-pointer transition">
          <div class="w-8 h-8 rounded-lg bg-red-600/20 text-red-500 flex items-center justify-center shrink-0 text-xs"><i class="fa-solid fa-play"></i></div>
          <div class="text-xs font-semibold text-slate-200 line-clamp-1">${v.title}</div>
        </div>`).join('');
      playVideo(youtubeVideos[0].id, youtubeVideos[0].title);
    }
    function playVideo(id, title){
      document.getElementById('featured-video-iframe').src = `https://www.youtube.com/embed/${id}`;
      document.getElementById('featured-video-caption').innerText = title;
    }

    function renderPoll(){
      const el = document.getElementById('poll-widget');
      const voted = lsGet('mahdi_poll_vote', null);
      const counts = lsGet('mahdi_poll_counts', [12, 18, 7, 14]);
      if (voted === null){
        el.innerHTML = `<h3 class="font-bold text-xs text-white mb-2.5 flex items-center gap-1.5"><i class="fa-solid fa-chart-simple text-sky-400"></i> ${dailyPoll.question}</h3>
          <div class="space-y-1.5">
          ${dailyPoll.options.map((o,i)=>`<button onclick="votePoll(${i})" class="w-full text-left px-3 py-1.5 rounded-xl bg-slate-900/70 border border-slate-700 text-xs text-slate-200 hover:border-sky-500 transition">${o}</button>`).join('')}
          </div>`;
      } else {
        const total = counts.reduce((a,b)=>a+b,0) || 1;
        el.innerHTML = `<h3 class="font-bold text-xs text-white mb-2.5 flex items-center gap-1.5"><i class="fa-solid fa-chart-simple text-sky-400"></i> ${dailyPoll.question}</h3>
          <div class="space-y-2">
          ${dailyPoll.options.map((o,i)=>{
            const pct = Math.round(counts[i]/total*100);
            return `<div><div class="flex justify-between text-[11px] text-slate-300 mb-0.5"><span>${o}${i===voted?' ✓':''}</span><span>${pct}%</span></div>
            <div class="w-full bg-slate-900 rounded-full h-1.5"><div class="h-1.5 rounded-full ${i===voted?'bg-sky-500':'bg-slate-700'}" style="width:${pct}%"></div></div></div>`;
          }).join('')}
          </div>`;
      }
    }
    function votePoll(i){
      lsSet('mahdi_poll_vote', i);
      const counts = lsGet('mahdi_poll_counts', [12, 18, 7, 14]);
      counts[i]++;
      lsSet('mahdi_poll_counts', counts);
      renderPoll();
    }

    /* ============ EXPANDED 10-QUESTION QUIZ ============ */
    function renderQuiz(){ quizIndex = 0; quizScore = 0; renderQuizQuestion(); }
    function renderQuizQuestion(){
      const el = document.getElementById('quiz-widget');
      const badge = document.getElementById('quiz-score-badge');
      if (badge) badge.innerText = `Score: ${quizScore}/${quizQuestions.length}`;

      if (quizIndex >= quizQuestions.length){
        el.innerHTML = `<div class="text-center py-2 space-y-2">
          <p class="text-xs text-slate-200 font-bold">Quiz Completed!</p>
          <p class="text-sm font-black text-emerald-400">Final Score: ${quizScore} / ${quizQuestions.length}</p>
          <button onclick="renderQuiz()" class="text-xs bg-sky-600 hover:bg-sky-500 text-white font-bold px-3 py-1.5 rounded-xl transition">Try Again</button>
        </div>`;
        return;
      }
      const q = quizQuestions[quizIndex];
      el.innerHTML = `<p class="text-xs font-semibold text-slate-200 mb-2.5">${quizIndex+1}. ${q.q}</p>
        <div class="space-y-1.5">${q.opts.map((o,i)=>`<button onclick="answerQuiz(${i})" class="w-full text-left text-xs px-3 py-1.5 rounded-xl bg-slate-900/80 border border-slate-700/80 hover:border-emerald-500 text-slate-300 transition">${o}</button>`).join('')}</div>
        <p class="text-[10px] text-slate-500 mt-2 text-right">Question ${quizIndex+1} of ${quizQuestions.length}</p>`;
    }
    function answerQuiz(i){
      const q = quizQuestions[quizIndex];
      if (i === q.correct) quizScore++;
      quizIndex++;
      renderQuizQuestion();
    }

    /* ============ STANDALONE AI CHAT ENGINE ============ */
    function toggleAiPanel(){
      const panel = document.getElementById('ai-panel');
      panel.classList.toggle('hidden');
      panel.classList.toggle('flex');
      if (!document.getElementById('ai-chat-log').dataset.greeted){
        appendAiMessage('assistant', "Hello! I am your standalone interactive news assistant. Ask me anything or select one of the preset questions above!");
        document.getElementById('ai-chat-log').dataset.greeted = "1";
      }
    }
    function appendAiMessage(role, text){
      const log = document.getElementById('ai-chat-log');
      const bubble = document.createElement('div');
      bubble.className = role === 'user'
        ? "ml-auto max-w-[85%] bg-sky-600 text-white rounded-2xl rounded-br-none px-3 py-2 shadow-md"
        : "mr-auto max-w-[85%] bg-slate-800 text-slate-200 rounded-2xl rounded-bl-none px-3 py-2 border border-slate-700 shadow-md";
      bubble.innerText = text;
      log.appendChild(bubble);
      log.scrollTop = log.scrollHeight;
    }

    function sendPresetQuery(queryText){
      appendAiMessage('user', queryText);
      generateStandaloneAiReply(queryText);
    }

    function sendAiMessage(){
      const input = document.getElementById('ai-chat-input');
      const msg = input.value.trim();
      if (!msg) return;
      appendAiMessage('user', msg);
      input.value = "";
      generateStandaloneAiReply(msg);
    }

    function generateStandaloneAiReply(prompt){
      const lower = prompt.toLowerCase();
      let reply = "I analyzed your query across our live news database. Here is what you need to know: ";

      if (lower.includes('job') || lower.includes('matrix') || lower.includes('risk')){
        reply = "The AI Job Risk Matrix categorizes roles based on routine task automation. High-risk roles include Data Entry (92%), while human-centric roles like Nursing (14%) and Music Production (25%) remain safe.";
      } else if (lower.includes('space') || lower.includes('moon') || lower.includes('debris')){
        reply = "Recent space news highlights expanded global orbital debris tracking networks and confirmed deposits of polar lunar water ice that can be repurposed for rocket fuel!";
      } else if (lower.includes('workweek') || lower.includes('four-day') || lower.includes('4-day')){
        reply = "Global four-day workweek pilots show consistent productivity across corporate office environments with reported reductions in employee burnout.";
      } else {
        reply += "Our newsdesk is tracking ongoing developments in technology, space exploration, and economic policy updates globally.";
      }

      setTimeout(() => { appendAiMessage('assistant', reply); }, 400);
    }

    /* ============ BALLOON POPPING MINIGAME ============ */
    let balloonScore = 0;
    let balloonPoppedCount = 0;
    let balloonInterval = null;

    function toggleBalloonDrawer(){
      document.getElementById('balloon-drawer').classList.toggle('translate-x-full');
    }

    function startBalloonGame(){
      resetBalloonGame();
      document.getElementById('balloon-start-msg')?.remove();
      const canvas = document.getElementById('balloon-canvas');
      
      balloonInterval = setInterval(() => {
        if (!document.getElementById('balloon-drawer').classList.contains('translate-x-full')){
          spawnBalloon(canvas);
        }
      }, 900);
    }

    function spawnBalloon(canvas){
      const balloon = document.createElement('div');
      const colors = ['bg-pink-500', 'bg-rose-500', 'bg-sky-500', 'bg-indigo-500', 'bg-emerald-500', 'bg-amber-500'];
      const randomColor = colors[Math.floor(Math.random() * colors.length)];
      const randomLeft = Math.floor(Math.random() * 80) + 10;
      
      balloon.className = `absolute w-9 h-12 rounded-full ${randomColor} cursor-pointer shadow-lg transition-transform hover:scale-110 flex items-center justify-center`;
      balloon.style.left = `${randomLeft}%`;
      balloon.style.bottom = `-50px`;

      balloon.onclick = () => {
        playPopSound();
        balloonScore += 10;
        balloonPoppedCount += 1;
        document.getElementById('balloon-score').innerText = balloonScore;
        document.getElementById('balloon-popped-count').innerText = balloonPoppedCount;
        balloon.remove();
      };

      canvas.appendChild(balloon);

      let pos = -50;
      const floatAnim = setInterval(() => {
        pos += 2;
        balloon.style.bottom = `${pos}px`;
        if (pos > canvas.clientHeight + 50){
          clearInterval(floatAnim);
          balloon.remove();
        }
      }, 30);
    }

    function resetBalloonGame(){
      if (balloonInterval) clearInterval(balloonInterval);
      balloonScore = 0;
      balloonPoppedCount = 0;
      document.getElementById('balloon-score').innerText = '0';
      document.getElementById('balloon-popped-count').innerText = '0';
      document.getElementById('balloon-canvas').innerHTML = '';
    }

    function playPopSound(){
      try {
        const ctx = new (window.AudioContext || window.webkitAudioContext)();
        const osc = ctx.createOscillator();
        const gain = ctx.createGain();
        osc.type = 'sine';
        osc.frequency.setValueAtTime(600, ctx.currentTime);
        osc.frequency.exponentialRampToValueAtTime(100, ctx.currentTime + 0.1);
        gain.gain.setValueAtTime(0.3, ctx.currentTime);
        gain.gain.linearRampToValueAtTime(0.01, ctx.currentTime + 0.1);
        osc.connect(gain);
        gain.connect(ctx.destination);
        osc.start();
        osc.stop(ctx.currentTime + 0.1);
      } catch(e){}
    }

    /* ============ LOUD HIGH-PITCH SCREECH BUTTON ============ */
    function triggerHighPitchScreech(){
      // Screen Shake Visual
      document.body.classList.add('shake-screen');
      setTimeout(() => document.body.classList.remove('shake-screen'), 500);

      try {
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        const osc = audioCtx.createOscillator();
        const gainNode = audioCtx.createGain();

        // Very high pitch piercing wave
        osc.type = 'sawtooth';
        osc.frequency.setValueAtTime(3800, audioCtx.currentTime); // 3.8 kHz high pitch screech
        
        // Loud volume fading away over 1.5s
        gainNode.gain.setValueAtTime(0.8, audioCtx.currentTime);
        gainNode.gain.exponentialRampToValueAtTime(0.0001, audioCtx.currentTime + 1.5);

        osc.connect(gainNode);
        gainNode.connect(audioCtx.destination);

        osc.start();
        osc.stop(audioCtx.currentTime + 1.5);
      } catch(e) {
        alert("Audio context blocked by browser settings.");
      }
    }

    /* ============ SYSTEM PREFERENCES & INIT ============ */
    function toggleSettingsDrawer(){ document.getElementById('settings-drawer').classList.toggle('translate-x-full'); }
    function setTheme(theme){
      const body = document.body;
      body.classList.remove('high-contrast','sepia');
      if (theme==='high-contrast') body.classList.add('high-contrast');
      lsSet('mahdi_theme', theme);
    }
    function setFontSize(size){ document.documentElement.style.fontSize = size; lsSet('mahdi_fontsize', size); }
    function exportMyData(){
      const data = { favorites: lsGet('mahdi_favorites', []), history: lsGet('mahdi_news_history', []), lang: currentLang };
      const blob = new Blob([JSON.stringify(data, null, 2)], {type:'application/json'});
      const a = document.createElement('a');
      a.href = URL.createObjectURL(blob);
      a.download = 'mahdi-news-backup.json';
      a.click();
    }
    function wireSettingToggles(){
      document.getElementById('s-reducemotion').addEventListener('change', (e)=> document.body.classList.toggle('reduce-motion', e.target.checked));
      document.getElementById('s-dyslexia').addEventListener('change', (e)=> document.body.classList.toggle('dyslexia-font', e.target.checked));
      document.getElementById('s-datasaver').addEventListener('change', renderArticles);
    }
    function resetView(){ currentCategory='all'; visibleCount=6; document.getElementById('search-input').value = ""; renderCategories(); renderArticles(); }

    function openAuthModal(){ document.getElementById('auth-modal').classList.remove('hidden'); }
    function closeAuthModal(){ document.getElementById('auth-modal').classList.add('hidden'); }
    function handleLoginSubmit(e){
      e.preventDefault();
      const name = document.getElementById('auth-email').value || 'Reader';
      currentUser = {name};
      lsSet('mahdi_user', currentUser);
      document.getElementById('auth-btn-label').innerText = name;
      document.getElementById('auth-status-msg').innerText = "Signed in locally.";
      setTimeout(closeAuthModal, 800);
    }
    function updateAuthUI(){
      const stored = lsGet('mahdi_user', null);
      if (stored){ currentUser = stored; document.getElementById('auth-btn-label').innerText = stored.name; }
    }

    function acceptCookies(all){ lsSet('mahdi_cookies_accepted', true); document.getElementById('cookie-banner').classList.add('hidden'); }
    function checkCookieBanner(){ if (lsGet('mahdi_cookies_accepted', null)) document.getElementById('cookie-banner').classList.add('hidden'); }

    /* ============ INITIALIZATION ============ */
    window.onload = () => {
      currentLang = lsGet('mahdi_lang', 'en');
      populateLangSelect();
      
      const theme = lsGet('mahdi_theme', 'dark'); setTheme(theme);
      const fsize = lsGet('mahdi_fontsize', null); if (fsize) document.documentElement.style.fontSize = fsize;

      changeLanguage(currentLang);
      renderYouTubeSidebar();
      updateHistoryWidget();
      updateAuthUI();
      checkCookieBanner();
      wireSettingToggles();
      document.getElementById('fav-count').innerText = lsGet('mahdi_favorites', []).length;
    };
  </script>
</body>
</html>

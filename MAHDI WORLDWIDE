<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mahdi WorldWide News Hub</title>
<script src="https://cdn.tailwindcss.com"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=Noto+Sans+Arabic:wght@400;600;700&display=swap" rel="stylesheet">
<script>
tailwind.config = { darkMode: 'class', theme: { extend: {
  colors: { brand: { 50:'#f0f7ff',100:'#e0effe',500:'#0284c7',600:'#0369a1',700:'#075985',900:'#0c4a6e' } },
  fontFamily: { sans: ['Inter','Noto Sans Arabic','sans-serif'] }
}}}
</script>
<style>
  body.high-contrast { background:#000!important; color:#fff!important; }
  body.high-contrast .card,body.high-contrast .bg-slate-800,body.high-contrast .bg-slate-900{background:#111!important;border-color:#fff!important;}
  body.high-contrast button{border:2px solid #fff!important;}
  body.sepia{ background:#f4ecd8!important; color:#3b2f1e!important; }
  body.sepia .bg-slate-800,body.sepia .bg-slate-900,body.sepia .bg-slate-800\/60{background:#e9dfc4!important;color:#3b2f1e!important;border-color:#c9b98f!important;}
  body.dyslexia-font, body.dyslexia-font * { font-family: 'Comic Sans MS', 'Comic Sans', cursive !important; letter-spacing: 0.02em; }
  body.reduce-motion *, body.reduce-motion *::before, body.reduce-motion *::after { animation-duration: 0.001ms !important; animation-iteration-count: 1 !important; transition-duration: 0.001ms !important; }
  @keyframes marquee { 0%{transform:translateX(100%);} 100%{transform:translateX(-100%);} }
  .animate-marquee{display:inline-block;white-space:nowrap;animation:marquee 25s linear infinite;}
  .animate-marquee:hover{animation-play-state:paused;}
  ::-webkit-scrollbar{width:8px;height:8px;}
  ::-webkit-scrollbar-track{background:#0f172a;}
  ::-webkit-scrollbar-thumb{background:#334155;border-radius:4px;}
  ::-webkit-scrollbar-thumb:hover{background:#0284c7;}
  .video-container{position:relative;padding-bottom:56.25%;height:0;overflow:hidden;}
  .video-container iframe{position:absolute;top:0;left:0;width:100%;height:100%;}
  .glass{background:rgba(30,41,59,.7);backdrop-filter:blur(12px);-webkit-backdrop-filter:blur(12px);border:1px solid rgba(255,255,255,.1);}
  .fade-in{animation:fadeIn .25s ease-out;}
  @keyframes fadeIn{from{opacity:0;transform:translateY(6px);}to{opacity:1;transform:translateY(0);}}
</style>
</head>
<body class="bg-slate-900 text-slate-100 font-sans min-h-screen flex flex-col transition-colors duration-200" id="main-body">

<header class="sticky top-0 z-40 glass border-b border-slate-800 shadow-lg">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex items-center justify-between h-16 gap-4">
      <div class="flex items-center space-x-3 cursor-pointer" onclick="resetView()">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-sky-500 to-indigo-600 flex items-center justify-center text-white font-bold text-xl shadow-lg shadow-sky-500/30">M</div>
        <span class="text-xl font-extrabold tracking-tight bg-gradient-to-r from-sky-400 via-indigo-300 to-white bg-clip-text text-transparent">MAHDI <span class="text-sky-500 font-light">WORLDWIDE</span></span>
      </div>
      <div class="hidden md:flex flex-1 max-w-md mx-4">
        <div class="relative w-full">
          <span class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none text-slate-400"><i class="fa-solid fa-magnifying-glass"></i></span>
          <input type="text" id="search-input" onkeyup="handleSearch()" placeholder="Search global news..." class="w-full pl-10 pr-4 py-2 bg-slate-800/80 border border-slate-700/80 rounded-full text-sm text-slate-200 placeholder-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 transition">
        </div>
      </div>
      <div class="flex items-center space-x-3">
        <select id="lang-select" onchange="changeLanguage(this.value)" class="bg-slate-800 border border-slate-700 text-xs rounded-lg px-2.5 py-1.5 font-medium text-slate-200 hover:border-sky-500 transition focus:outline-none max-w-[130px]"></select>
        <button id="auth-btn" onclick="openAuthModal()" class="flex items-center space-x-2 bg-sky-600 hover:bg-sky-500 text-white text-xs font-semibold px-3 py-1.5 rounded-lg transition shadow-md shadow-sky-600/20">
          <i class="fa-solid fa-user"></i><span id="auth-btn-label">Sign In</span>
        </button>
        <button onclick="toggleSettingsDrawer()" class="p-2 rounded-lg bg-slate-800 border border-slate-700 text-slate-300 hover:text-white hover:border-sky-500 transition" title="Settings"><i class="fa-solid fa-gear"></i></button>
      </div>
    </div>
  </div>
</header>

<div class="bg-slate-950 border-b border-slate-800 overflow-hidden flex items-center h-10 text-xs">
  <div class="bg-sky-600 text-white font-bold px-4 py-2 flex items-center space-x-2 shrink-0 z-10 shadow-md">
    <i class="fa-solid fa-bolt animate-pulse"></i><span id="ticker-label">BREAKING</span>
  </div>
  <div class="overflow-hidden whitespace-nowrap w-full relative flex items-center">
    <div id="ticker-text" class="animate-marquee font-medium text-slate-300 px-4">Loading latest global headlines...</div>
  </div>
</div>

<main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 flex-1 w-full">

  <div class="flex items-center justify-between gap-4 mb-6 overflow-x-auto pb-2">
    <div id="category-bar" class="flex space-x-2 shrink-0"></div>
    <div class="flex items-center gap-2 shrink-0">
      <button onclick="openFavorites()" class="px-2.5 py-1.5 text-xs rounded-lg bg-slate-800/80 border border-slate-700 text-amber-400 hover:border-amber-400 transition" title="Favorites"><i class="fa-solid fa-star"></i> <span id="fav-count">0</span></button>
      <div class="flex items-center bg-slate-800/80 p-1 rounded-lg border border-slate-700">
        <button id="view-grid-btn" onclick="setLayoutMode('grid')" class="px-2.5 py-1 text-xs rounded-md text-sky-400 bg-slate-700 font-medium transition" title="Grid"><i class="fa-solid fa-grip-vertical"></i></button>
        <button id="view-compact-btn" onclick="setLayoutMode('compact')" class="px-2.5 py-1 text-xs rounded-md text-slate-400 hover:text-white transition" title="Compact"><i class="fa-solid fa-list"></i></button>
      </div>
    </div>
  </div>

  <!-- Daily Poll -->
  <div id="poll-widget" class="mb-8 bg-slate-800/60 border border-slate-700/80 rounded-2xl p-5 shadow-xl"></div>

  <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
    <section class="lg:col-span-8 space-y-8">
      <div class="flex items-center justify-between border-b border-slate-800 pb-3">
        <h2 id="section-title" class="text-xl font-bold text-slate-100 flex items-center gap-2"><i class="fa-solid fa-newspaper text-sky-500"></i>Top Stories</h2>
        <span id="article-count-badge" class="text-xs bg-slate-800 text-sky-400 font-semibold px-2.5 py-1 rounded-full border border-slate-700">50 Articles</span>
      </div>
      <div id="articles-grid" class="grid grid-cols-1 md:grid-cols-2 gap-6"></div>
      <div class="flex justify-center pt-2">
        <button id="load-more-btn" onclick="loadMoreArticles()" class="px-5 py-2.5 rounded-lg bg-slate-800 border border-slate-700 text-sm font-semibold text-slate-200 hover:border-sky-500 transition">Load more</button>
      </div>

      <div id="ai-job-safety-section" class="mt-6 bg-slate-800/50 border border-slate-700/80 rounded-2xl p-6 shadow-xl">
        <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 mb-6">
          <div>
            <span class="text-xs font-bold uppercase tracking-wider text-sky-400 bg-sky-950 px-3 py-1 rounded-full border border-sky-800/50">AI Automation Index</span>
            <h2 id="ai-tool-title" class="text-2xl font-extrabold text-white mt-2">Is Your Career Safe From AI?</h2>
            <p id="ai-tool-desc" class="text-sm text-slate-400 mt-1">Illustrative estimates for discussion, not a scientific study — automation exposure varies a lot by employer and region.</p>
          </div>
          <div class="flex items-center space-x-2 shrink-0">
            <span class="text-xs text-slate-400 font-medium" id="filter-risk-label">Filter Risk:</span>
            <select id="risk-filter" onchange="filterAiJobs()" class="bg-slate-900 border border-slate-700 text-xs rounded-lg px-3 py-2 text-slate-200 focus:outline-none focus:border-sky-500">
              <option value="all">All</option><option value="high">High</option><option value="medium">Medium</option><option value="safe">Safe</option>
            </select>
          </div>
        </div>
        <div class="overflow-x-auto rounded-xl border border-slate-700/60 shadow-inner">
          <table class="w-full text-left text-sm text-slate-300">
            <thead class="bg-slate-900/90 text-xs uppercase tracking-wider text-slate-400 border-b border-slate-700">
              <tr><th class="py-3.5 px-4">Role</th><th class="py-3.5 px-4 text-center">Rating</th><th class="py-3.5 px-4">Risk</th><th class="py-3.5 px-4">Notes</th></tr>
            </thead>
            <tbody id="ai-jobs-tbody" class="divide-y divide-slate-800 bg-slate-900/40"></tbody>
          </table>
        </div>
      </div>
    </section>

    <aside class="lg:col-span-4 space-y-8">
      <div class="bg-slate-800/60 border border-slate-700/80 rounded-2xl p-5 shadow-xl">
        <div class="flex items-center justify-between border-b border-slate-700/80 pb-3 mb-4">
          <h3 class="font-bold text-slate-100 flex items-center gap-2"><i class="fa-brands fa-youtube text-red-500 text-lg"></i>Media & Video Desk</h3>
        </div>
        <div class="mb-4 rounded-xl overflow-hidden border border-slate-700 bg-black shadow-lg">
          <div class="video-container"><iframe id="featured-video-iframe" src="" title="Featured Video" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
          <div id="featured-video-caption" class="p-3 bg-slate-900 text-xs font-semibold text-slate-200"></div>
        </div>
        <div id="youtube-videos-list" class="space-y-3 max-h-72 overflow-y-auto pr-1"></div>
      </div>

      <div class="bg-slate-800/60 border border-slate-700/80 rounded-2xl p-5 shadow-xl">
        <div class="flex items-center justify-between border-b border-slate-700/80 pb-3 mb-4">
          <h3 class="font-bold text-slate-100 flex items-center gap-2"><i class="fa-solid fa-bookmark text-amber-400"></i>Reading History</h3>
          <button onclick="clearHistory()" class="text-xs text-slate-400 hover:text-red-400 transition">Clear</button>
        </div>
        <div id="history-list-widget" class="space-y-2 text-xs text-slate-400"></div>
      </div>

      <div class="bg-slate-800/60 border border-slate-700/80 rounded-2xl p-5 shadow-xl">
        <div class="flex items-center justify-between border-b border-slate-700/80 pb-3 mb-4">
          <h3 class="font-bold text-slate-100 flex items-center gap-2"><i class="fa-solid fa-circle-question text-emerald-400"></i>Quick Quiz</h3>
        </div>
        <div id="quiz-widget"></div>
      </div>
    </aside>
  </div>
</main>

<!-- Article Modal -->
<div id="article-modal" class="fixed inset-0 z-50 bg-slate-950/80 backdrop-blur-md hidden overflow-y-auto p-4 sm:p-6 md:p-10">
  <div class="max-w-4xl mx-auto bg-slate-900 border border-slate-700 rounded-2xl shadow-2xl overflow-hidden my-8 relative">
    <div class="sticky top-0 bg-slate-900/90 backdrop-blur border-b border-slate-800 px-6 py-4 flex items-center justify-between z-10">
      <span id="modal-tag" class="text-xs font-extrabold uppercase px-3 py-1 bg-sky-950 text-sky-400 border border-sky-800 rounded-full">Category</span>
      <div class="flex items-center space-x-3">
        <button onclick="toggleFavorite(currentArticleId)" id="modal-fav-btn" class="p-2 text-slate-400 hover:text-amber-400 transition" title="Save"><i class="fa-regular fa-star"></i></button>
        <button onclick="translateArticleAI()" class="p-2 text-slate-400 hover:text-sky-400 transition" title="AI Translate"><i class="fa-solid fa-language"></i></button>
        <button onclick="speakArticleContent()" class="p-2 text-slate-400 hover:text-sky-400 transition" title="Read Aloud"><i class="fa-solid fa-volume-high"></i></button>
        <button onclick="closeModal()" class="p-2 text-slate-400 hover:text-white transition"><i class="fa-solid fa-xmark text-xl"></i></button>
      </div>
    </div>
    <div class="p-6 sm:p-8 space-y-6">
      <h1 id="modal-title" class="text-2xl sm:text-3xl font-extrabold text-slate-100 leading-tight">Article Title</h1>
      <div id="modal-meta" class="text-xs text-slate-400 border-b border-slate-800 pb-4">Published Sept 19, 2026</div>
      <div class="rounded-xl overflow-hidden border border-slate-800 max-h-96"><img id="modal-img" src="" alt="Article cover" class="w-full h-full object-cover"></div>
      <div id="modal-translate-note" class="hidden text-xs text-amber-400 bg-amber-950/40 border border-amber-800/50 rounded-lg px-3 py-2"></div>
      <div id="modal-content" class="prose prose-invert max-w-none text-slate-300 leading-relaxed space-y-4 text-base"></div>
    </div>
  </div>
</div>

<!-- Favorites Modal -->
<div id="favorites-modal" class="fixed inset-0 z-50 bg-slate-950/80 backdrop-blur-md hidden items-center justify-center p-4">
  <div class="max-w-lg w-full bg-slate-900 border border-slate-700 rounded-2xl p-6 shadow-2xl relative max-h-[80vh] overflow-y-auto">
    <button onclick="closeFavorites()" class="absolute top-4 right-4 text-slate-400 hover:text-white"><i class="fa-solid fa-xmark text-lg"></i></button>
    <h3 class="text-xl font-bold text-white mb-4"><i class="fa-solid fa-star text-amber-400"></i> Saved Articles</h3>
    <div id="favorites-list" class="space-y-2 text-sm"></div>
  </div>
</div>

<!-- Auth Modal -->
<div id="auth-modal" class="fixed inset-0 z-50 bg-slate-950/80 backdrop-blur-md hidden flex items-center justify-center p-4">
  <div class="max-w-md w-full bg-slate-900 border border-slate-700 rounded-2xl p-6 shadow-2xl relative">
    <button onclick="closeAuthModal()" class="absolute top-4 right-4 text-slate-400 hover:text-white"><i class="fa-solid fa-xmark text-lg"></i></button>
    <div class="text-center mb-6">
      <div class="w-12 h-12 bg-sky-500/20 text-sky-400 rounded-full flex items-center justify-center mx-auto text-xl mb-3"><i class="fa-solid fa-user-lock"></i></div>
      <h3 class="text-xl font-bold text-white">Account Portal</h3>
      <p class="text-xs text-slate-400 mt-1">This is a front-end demo only — no account is actually created or stored on a server.</p>
    </div>
    <form onsubmit="handleLoginSubmit(event)" class="space-y-4">
      <div><label class="block text-xs font-semibold text-slate-300 mb-1">Display name</label>
        <input type="text" id="auth-email" required placeholder="e.g. Reader123" class="w-full bg-slate-800 border border-slate-700 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-sky-500"></div>
      <button type="submit" class="w-full bg-sky-600 hover:bg-sky-500 text-white font-bold py-2.5 rounded-lg text-sm transition shadow-lg shadow-sky-600/30">Continue (local only)</button>
    </form>
    <div id="auth-status-msg" class="text-xs text-center mt-3 text-sky-400 font-medium"></div>
  </div>
</div>

<!-- Settings Drawer -->
<div id="settings-drawer" class="fixed inset-y-0 right-0 z-50 w-80 bg-slate-900 border-l border-slate-700 p-6 shadow-2xl transform translate-x-full transition-transform duration-300 ease-in-out overflow-y-auto">
  <div class="flex items-center justify-between border-b border-slate-800 pb-4 mb-6">
    <h3 class="font-bold text-lg text-slate-100 flex items-center gap-2"><i class="fa-solid fa-sliders text-sky-500"></i>Settings</h3>
    <button onclick="toggleSettingsDrawer()" class="text-slate-400 hover:text-white"><i class="fa-solid fa-xmark text-lg"></i></button>
  </div>
  <div class="space-y-6 text-sm">
    <div>
      <label class="block text-xs font-semibold text-slate-400 mb-2">Appearance theme</label>
      <div class="grid grid-cols-2 gap-2">
        <button onclick="setTheme('dark')" class="setting-btn bg-slate-800 border border-slate-700 p-2 rounded-lg text-center text-xs hover:border-sky-500">Dark</button>
        <button onclick="setTheme('light')" class="setting-btn bg-slate-800 border border-slate-700 p-2 rounded-lg text-center text-xs hover:border-sky-500">Light</button>
        <button onclick="setTheme('sepia')" class="setting-btn bg-slate-800 border border-slate-700 p-2 rounded-lg text-center text-xs hover:border-sky-500">Sepia</button>
        <button onclick="setTheme('high-contrast')" class="setting-btn bg-slate-800 border border-slate-700 p-2 rounded-lg text-center text-xs hover:border-sky-500">High Contrast</button>
      </div>
    </div>
    <div>
      <label class="block text-xs font-semibold text-slate-400 mb-2">Text size</label>
      <div class="grid grid-cols-4 gap-2">
        <button onclick="setFontSize('14px')" class="bg-slate-800 border border-slate-700 p-2 rounded-lg text-center text-xs hover:border-sky-500">S</button>
        <button onclick="setFontSize('16px')" class="bg-slate-800 border border-slate-700 p-2 rounded-lg text-center text-xs hover:border-sky-500">M</button>
        <button onclick="setFontSize('18px')" class="bg-slate-800 border border-slate-700 p-2 rounded-lg text-center text-xs hover:border-sky-500">L</button>
        <button onclick="setFontSize('21px')" class="bg-slate-800 border border-slate-700 p-2 rounded-lg text-center text-xs hover:border-sky-500">XL</button>
      </div>
    </div>
    <div>
      <label class="block text-xs font-semibold text-slate-400 mb-2">Reading depth</label>
      <select id="reading-level-select" onchange="setReadingLevel(this.value)" class="w-full bg-slate-800 border border-slate-700 rounded-lg px-2 py-2 text-xs">
        <option value="summary">Summary only</option>
        <option value="standard" selected>Standard</option>
        <option value="full">Full detail</option>
      </select>
    </div>
    <div class="space-y-3 pt-2 border-t border-slate-800">
      <div class="flex items-center justify-between"><span class="text-xs text-slate-300">Auto-refresh feed</span><input type="checkbox" id="s-autorefresh" checked class="setting-toggle rounded border-slate-700 bg-slate-800 text-sky-500"></div>
      <div class="flex items-center justify-between"><span class="text-xs text-slate-300">Sound effects</span><input type="checkbox" id="s-sfx" checked class="setting-toggle rounded border-slate-700 bg-slate-800 text-sky-500"></div>
      <div class="flex items-center justify-between"><span class="text-xs text-slate-300">Autoplay videos</span><input type="checkbox" id="s-autoplay" class="setting-toggle rounded border-slate-700 bg-slate-800 text-sky-500"></div>
      <div class="flex items-center justify-between"><span class="text-xs text-slate-300">Data saver (smaller images)</span><input type="checkbox" id="s-datasaver" class="setting-toggle rounded border-slate-700 bg-slate-800 text-sky-500"></div>
      <div class="flex items-center justify-between"><span class="text-xs text-slate-300">Reduce motion</span><input type="checkbox" id="s-reducemotion" class="setting-toggle rounded border-slate-700 bg-slate-800 text-sky-500"></div>
      <div class="flex items-center justify-between"><span class="text-xs text-slate-300">Dyslexia-friendly font</span><input type="checkbox" id="s-dyslexia" class="setting-toggle rounded border-slate-700 bg-slate-800 text-sky-500"></div>
      <div class="flex items-center justify-between"><span class="text-xs text-slate-300">Desktop notifications</span><input type="checkbox" id="s-notifications" class="setting-toggle rounded border-slate-700 bg-slate-800 text-sky-500"></div>
      <div class="flex items-center justify-between"><span class="text-xs text-slate-300">Show sensitive-topic warnings</span><input type="checkbox" id="s-contentwarn" checked class="setting-toggle rounded border-slate-700 bg-slate-800 text-sky-500"></div>
      <div class="flex items-center justify-between"><span class="text-xs text-slate-300">Personalize by location</span><input type="checkbox" id="s-location" class="setting-toggle rounded border-slate-700 bg-slate-800 text-sky-500"></div>
      <div class="flex items-center justify-between"><span class="text-xs text-slate-300">Weekly email digest</span><input type="checkbox" id="s-digest" class="setting-toggle rounded border-slate-700 bg-slate-800 text-sky-500"></div>
      <div>
        <label class="block text-xs font-semibold text-slate-400 mb-1 mt-2">Read-aloud speed</label>
        <input type="range" id="s-ttsrate" min="0.5" max="2" step="0.1" value="1" class="w-full">
      </div>
    </div>
    <div class="pt-4 border-t border-slate-800 space-y-2">
      <button onclick="exportMyData()" class="w-full bg-slate-800 hover:bg-slate-700 text-slate-300 py-2 rounded-lg text-xs font-medium transition"><i class="fa-solid fa-download"></i> Export my local data</button>
      <button onclick="resetView()" class="w-full bg-slate-800 hover:bg-slate-700 text-slate-300 py-2 rounded-lg text-xs font-medium transition">Reset display options</button>
    </div>
  </div>
</div>

<!-- Cookie Banner -->
<div id="cookie-banner" class="fixed bottom-20 left-4 right-4 md:left-8 md:right-auto md:max-w-md z-50 bg-slate-900 border border-slate-700 p-5 rounded-2xl shadow-2xl flex flex-col space-y-3">
  <div class="flex items-start space-x-3">
    <i class="fa-solid fa-cookie-bite text-amber-400 text-xl mt-1"></i>
    <div><h4 class="text-sm font-bold text-white">Privacy & Cookie Preferences</h4>
    <p class="text-xs text-slate-400 mt-1">We store your reading history, favorites and settings locally in your browser only. Nothing is sent to a server by this demo site.</p></div>
  </div>
  <div class="flex items-center justify-end space-x-2 pt-2">
    <button onclick="acceptCookies(false)" class="text-xs text-slate-400 hover:text-white px-3 py-1.5 rounded-lg border border-slate-800">Essential only</button>
    <button onclick="acceptCookies(true)" class="text-xs bg-sky-600 hover:bg-sky-500 text-white font-bold px-4 py-1.5 rounded-lg transition shadow-md">Accept all</button>
  </div>
</div>

<!-- AI Assistant floating button + panel -->
<button onclick="toggleAiPanel()" class="fixed bottom-4 right-4 z-50 w-14 h-14 rounded-full bg-gradient-to-tr from-sky-500 to-indigo-600 shadow-2xl shadow-sky-600/40 flex items-center justify-center text-white text-xl hover:scale-105 transition" title="Ask the AI assistant">
  <i class="fa-solid fa-wand-magic-sparkles"></i>
</button>
<div id="ai-panel" class="fixed bottom-20 right-4 z-50 w-[340px] max-w-[90vw] bg-slate-900 border border-slate-700 rounded-2xl shadow-2xl hidden flex-col overflow-hidden" style="height:420px;">
  <div class="p-4 border-b border-slate-800 flex items-center justify-between bg-slate-950">
    <span class="font-bold text-sm text-slate-100"><i class="fa-solid fa-wand-magic-sparkles text-sky-400"></i> Ask the AI Assistant</span>
    <button onclick="toggleAiPanel()" class="text-slate-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
  </div>
  <div id="ai-chat-log" class="flex-1 overflow-y-auto p-4 space-y-3 text-sm"></div>
  <div class="p-3 border-t border-slate-800 flex gap-2">
    <input id="ai-chat-input" type="text" placeholder="Explain this article, a term..." class="flex-1 bg-slate-800 border border-slate-700 rounded-lg px-3 py-2 text-xs text-white focus:outline-none focus:border-sky-500" onkeydown="if(event.key==='Enter') sendAiMessage()">
    <button onclick="sendAiMessage()" class="bg-sky-600 hover:bg-sky-500 text-white rounded-lg px-3 text-xs font-semibold">Ask</button>
  </div>
</div>

<footer class="border-t border-slate-800 bg-slate-950 py-8 text-center text-xs text-slate-500 mt-auto">
  <div class="max-w-7xl mx-auto px-4 space-y-3">
    <p>© 2026 Mahdi WorldWide Media Corporation.</p>
    <p class="text-slate-600 max-w-2xl mx-auto">Demo content for a portfolio project. Articles are illustrative and not verified news reporting; the AI job-risk table shows rough, non-scientific estimates for discussion.</p>
    <div class="flex justify-center space-x-6">
      <a href="#" onclick="alert('Privacy: all data (history, favorites, settings) is stored only in your browser (localStorage). Nothing is uploaded.'); return false;" class="hover:text-slate-400">Privacy Policy</a>
      <a href="#" onclick="alert('Terms: demo content for educational/portfolio purposes only.'); return false;" class="hover:text-slate-400">Terms</a>
      <a href="#" onclick="toggleSettingsDrawer(); return false;" class="hover:text-slate-400">Cookie Settings</a>
    </div>
  </div>
</footer>

<script>
/* ============ LANGUAGES ============ */
const LANGS = [
  {code:'en',name:'English',dir:'ltr'},{code:'fr',name:'Français',dir:'ltr'},{code:'ar',name:'العربية',dir:'rtl'},
  {code:'es',name:'Español',dir:'ltr'},{code:'de',name:'Deutsch',dir:'ltr'},{code:'it',name:'Italiano',dir:'ltr'},
  {code:'pt',name:'Português',dir:'ltr'},{code:'ru',name:'Русский',dir:'ltr'},{code:'zh',name:'中文',dir:'ltr'},
  {code:'ja',name:'日本語',dir:'ltr'},{code:'ko',name:'한국어',dir:'ltr'},{code:'hi',name:'हिन्दी',dir:'ltr'},
  {code:'tr',name:'Türkçe',dir:'ltr'},{code:'nl',name:'Nederlands',dir:'ltr'},{code:'pl',name:'Polski',dir:'ltr'},
  {code:'sv',name:'Svenska',dir:'ltr'},{code:'el',name:'Ελληνικά',dir:'ltr'},{code:'he',name:'עברית',dir:'rtl'},
  {code:'id',name:'Bahasa Indonesia',dir:'ltr'},{code:'vi',name:'Tiếng Việt',dir:'ltr'}
];

const uiStrings = {
en:{breaking:"BREAKING: Robert Downey Jr. confirmed as Doctor Doom in Avengers: Doomsday",topStories:"Top Stories",search:"Search global news...",aiTitle:"Is Your Career Safe From AI?",aiDesc:"Illustrative estimates for discussion, not a scientific study.",readMore:"Read",signIn:"Sign In",loadMore:"Load more",filterRisk:"Filter Risk:",close:"Close",acceptAll:"Accept all",essential:"Essential only",favorites:"Favorites",askAI:"Ask"},
fr:{breaking:"FLASH INFO : Robert Downey Jr. confirmé dans le rôle du Docteur Doom",topStories:"Actualités Principales",search:"Rechercher des actualités...",aiTitle:"Votre métier est-il menacé par l'IA ?",aiDesc:"Estimations illustratives pour la discussion, pas une étude scientifique.",readMore:"Lire",signIn:"Connexion",loadMore:"Charger plus",filterRisk:"Filtrer :",close:"Fermer",acceptAll:"Tout accepter",essential:"Essentiel uniquement",favorites:"Favoris",askAI:"Demander"},
ar:{breaking:"عاجل: تأكيد مشاركة روبرت داوني جونيور بدور الدكتور دوم",topStories:"أبرز الأخبار",search:"ابحث في الأخبار العالمية...",aiTitle:"هل وظيفتك آمنة من الذكاء الاصطناعي؟",aiDesc:"تقديرات توضيحية للنقاش، وليست دراسة علمية.",readMore:"اقرأ",signIn:"تسجيل الدخول",loadMore:"عرض المزيد",filterRisk:"تصفية:",close:"إغلاق",acceptAll:"قبول الكل",essential:"الأساسي فقط",favorites:"المفضلة",askAI:"اسأل"},
es:{breaking:"ÚLTIMA HORA: Robert Downey Jr. confirmado como Doctor Doom",topStories:"Titulares Principales",search:"Buscar noticias...",aiTitle:"¿Está tu profesión a salvo de la IA?",aiDesc:"Estimaciones ilustrativas para el debate, no un estudio científico.",readMore:"Leer",signIn:"Iniciar sesión",loadMore:"Cargar más",filterRisk:"Filtrar:",close:"Cerrar",acceptAll:"Aceptar todo",essential:"Solo esencial",favorites:"Favoritos",askAI:"Preguntar"},
de:{breaking:"EILMELDUNG: Robert Downey Jr. als Doctor Doom bestätigt",topStories:"Top-Meldungen",search:"Nachrichten suchen...",aiTitle:"Ist Ihr Beruf sicher vor KI?",aiDesc:"Anschauliche Schätzungen zur Diskussion, keine wissenschaftliche Studie.",readMore:"Lesen",signIn:"Anmelden",loadMore:"Mehr laden",filterRisk:"Filtern:",close:"Schließen",acceptAll:"Alle akzeptieren",essential:"Nur essenziell",favorites:"Favoriten",askAI:"Fragen"},
it:{breaking:"ULTIM'ORA: Robert Downey Jr. confermato come Dottor Destino",topStories:"Notizie Principali",search:"Cerca notizie...",aiTitle:"Il tuo lavoro è al sicuro dall'IA?",aiDesc:"Stime illustrative per la discussione, non uno studio scientifico.",readMore:"Leggi",signIn:"Accedi",loadMore:"Carica altro",filterRisk:"Filtra:",close:"Chiudi",acceptAll:"Accetta tutto",essential:"Solo essenziali",favorites:"Preferiti",askAI:"Chiedi"},
pt:{breaking:"URGENTE: Robert Downey Jr. confirmado como Doutor Destino",topStories:"Principais Notícias",search:"Pesquisar notícias...",aiTitle:"Sua profissão está segura da IA?",aiDesc:"Estimativas ilustrativas para debate, não um estudo científico.",readMore:"Ler",signIn:"Entrar",loadMore:"Carregar mais",filterRisk:"Filtrar:",close:"Fechar",acceptAll:"Aceitar tudo",essential:"Somente essencial",favorites:"Favoritos",askAI:"Perguntar"},
ru:{breaking:"СРОЧНО: Роберт Дауни-младший подтверждён в роли Доктора Дума",topStories:"Главные новости",search:"Поиск новостей...",aiTitle:"В безопасности ли ваша профессия от ИИ?",aiDesc:"Иллюстративные оценки для обсуждения, а не научное исследование.",readMore:"Читать",signIn:"Войти",loadMore:"Загрузить ещё",filterRisk:"Фильтр:",close:"Закрыть",acceptAll:"Принять всё",essential:"Только необходимое",favorites:"Избранное",askAI:"Спросить"},
zh:{breaking:"突发：小罗伯特·唐尼确认出演末日博士",topStories:"头条新闻",search:"搜索全球新闻...",aiTitle:"你的职业能抵御人工智能吗？",aiDesc:"仅供讨论的示意性估计，并非科学研究。",readMore:"阅读",signIn:"登录",loadMore:"加载更多",filterRisk:"筛选：",close:"关闭",acceptAll:"全部接受",essential:"仅必要",favorites:"收藏",askAI:"提问"},
ja:{breaking:"速報：ロバート・ダウニー・Jr.がドクター・ドゥーム役で出演確定",topStories:"トップニュース",search:"ニュースを検索...",aiTitle:"あなたの仕事はAIに奪われない？",aiDesc:"議論のための例示的な推定であり、科学的研究ではありません。",readMore:"続きを読む",signIn:"サインイン",loadMore:"もっと見る",filterRisk:"絞り込み:",close:"閉じる",acceptAll:"すべて同意",essential:"必須のみ",favorites:"お気に入り",askAI:"質問する"},
ko:{breaking:"속보: 로버트 다우니 주니어, 닥터 둠 역 확정",topStories:"주요 뉴스",search:"뉴스 검색...",aiTitle:"당신의 직업은 AI로부터 안전한가요?",aiDesc:"논의를 위한 예시적 추정치이며 과학적 연구가 아닙니다.",readMore:"읽기",signIn:"로그인",loadMore:"더 보기",filterRisk:"필터:",close:"닫기",acceptAll:"모두 동의",essential:"필수만",favorites:"즐겨찾기",askAI:"질문하기"},
hi:{breaking:"ब्रेकिंग: रॉबर्ट डाउनी जूनियर डॉक्टर डूम की भूमिका में",topStories:"मुख्य समाचार",search:"समाचार खोजें...",aiTitle:"क्या आपकी नौकरी AI से सुरक्षित है?",aiDesc:"चर्चा के लिए उदाहरणात्मक अनुमान, कोई वैज्ञानिक अध्ययन नहीं।",readMore:"पढ़ें",signIn:"साइन इन करें",loadMore:"और लोड करें",filterRisk:"फ़िल्टर:",close:"बंद करें",acceptAll:"सभी स्वीकार करें",essential:"केवल आवश्यक",favorites:"पसंदीदा",askAI:"पूछें"},
tr:{breaking:"SON DAKİKA: Robert Downey Jr. Doctor Doom rolünde onaylandı",topStories:"Öne Çıkan Haberler",search:"Haber ara...",aiTitle:"Mesleğiniz yapay zekaya karşı güvende mi?",aiDesc:"Tartışma için örnek tahminler, bilimsel bir çalışma değildir.",readMore:"Oku",signIn:"Giriş yap",loadMore:"Daha fazla yükle",filterRisk:"Filtrele:",close:"Kapat",acceptAll:"Tümünü kabul et",essential:"Yalnızca gerekli",favorites:"Favoriler",askAI:"Sor"},
nl:{breaking:"BREAKING: Robert Downey Jr. bevestigd als Doctor Doom",topStories:"Topverhalen",search:"Zoek nieuws...",aiTitle:"Is jouw beroep veilig voor AI?",aiDesc:"Illustratieve schattingen ter discussie, geen wetenschappelijk onderzoek.",readMore:"Lees",signIn:"Inloggen",loadMore:"Meer laden",filterRisk:"Filter:",close:"Sluiten",acceptAll:"Alles accepteren",essential:"Alleen essentieel",favorites:"Favorieten",askAI:"Vraag"},
pl:{breaking:"PILNE: Robert Downey Jr. potwierdzony jako Doktor Doom",topStories:"Najważniejsze wiadomości",search:"Szukaj wiadomości...",aiTitle:"Czy twój zawód jest bezpieczny przed AI?",aiDesc:"Poglądowe szacunki do dyskusji, nie badanie naukowe.",readMore:"Czytaj",signIn:"Zaloguj się",loadMore:"Załaduj więcej",filterRisk:"Filtruj:",close:"Zamknij",acceptAll:"Akceptuj wszystko",essential:"Tylko niezbędne",favorites:"Ulubione",askAI:"Zapytaj"},
sv:{breaking:"NYHET: Robert Downey Jr. bekräftad som Doctor Doom",topStories:"Huvudnyheter",search:"Sök nyheter...",aiTitle:"Är ditt jobb säkert från AI?",aiDesc:"Illustrativa uppskattningar för diskussion, ingen vetenskaplig studie.",readMore:"Läs",signIn:"Logga in",loadMore:"Ladda fler",filterRisk:"Filtrera:",close:"Stäng",acceptAll:"Acceptera alla",essential:"Endast nödvändiga",favorites:"Favoriter",askAI:"Fråga"},
el:{breaking:"ΕΚΤΑΚΤΟ: Ο Ρόμπερτ Ντάουνι Τζούνιορ επιβεβαιώθηκε ως Δόκτωρ Καταστροφή",topStories:"Κύριες Ειδήσεις",search:"Αναζήτηση ειδήσεων...",aiTitle:"Είναι το επάγγελμά σας ασφαλές από την ΤΝ;",aiDesc:"Ενδεικτικές εκτιμήσεις για συζήτηση, όχι επιστημονική μελέτη.",readMore:"Διάβασε",signIn:"Σύνδεση",loadMore:"Φόρτωσε περισσότερα",filterRisk:"Φίλτρο:",close:"Κλείσιμο",acceptAll:"Αποδοχή όλων",essential:"Μόνο απαραίτητα",favorites:"Αγαπημένα",askAI:"Ρώτησε"},
he:{breaking:"מבזק: רוברט דאוני ג׳וניור אושר לתפקיד ד״ר דום",topStories:"הכתבות המובילות",search:"חיפוש חדשות...",aiTitle:"האם המקצוע שלך בטוח מבינה מלאכותית?",aiDesc:"הערכות להמחשה בלבד לצורך דיון, לא מחקר מדעי.",readMore:"קרא",signIn:"התחברות",loadMore:"טען עוד",filterRisk:"סינון:",close:"סגור",acceptAll:"קבל הכול",essential:"חיוני בלבד",favorites:"מועדפים",askAI:"שאל"},
id:{breaking:"BREAKING: Robert Downey Jr. dikonfirmasi sebagai Doctor Doom",topStories:"Berita Utama",search:"Cari berita...",aiTitle:"Apakah pekerjaan Anda aman dari AI?",aiDesc:"Perkiraan ilustratif untuk diskusi, bukan studi ilmiah.",readMore:"Baca",signIn:"Masuk",loadMore:"Muat lebih banyak",filterRisk:"Filter:",close:"Tutup",acceptAll:"Terima semua",essential:"Hanya esensial",favorites:"Favorit",askAI:"Tanya"},
vi:{breaking:"KHẨN: Robert Downey Jr. xác nhận vai Doctor Doom",topStories:"Tin Nổi Bật",search:"Tìm kiếm tin tức...",aiTitle:"Công việc của bạn có an toàn trước AI không?",aiDesc:"Ước tính minh họa để thảo luận, không phải nghiên cứu khoa học.",readMore:"Đọc",signIn:"Đăng nhập",loadMore:"Tải thêm",filterRisk:"Lọc:",close:"Đóng",acceptAll:"Chấp nhận tất cả",essential:"Chỉ thiết yếu",favorites:"Yêu thích",askAI:"Hỏi"}
};

const categoryNames = {
en:{Technology:"Technology",Science:"Science",Health:"Health",Business:"Business",Environment:"Environment",Culture:"Culture",Sports:"Sports",Education:"Education",Space:"Space",Society:"Society"},
fr:{Technology:"Technologie",Science:"Science",Health:"Santé",Business:"Économie",Environment:"Environnement",Culture:"Culture",Sports:"Sport",Education:"Éducation",Space:"Espace",Society:"Société"},
ar:{Technology:"تقنية",Science:"علوم",Health:"صحة",Business:"أعمال",Environment:"بيئة",Culture:"ثقافة",Sports:"رياضة",Education:"تعليم",Space:"فضاء",Society:"مجتمع"},
es:{Technology:"Tecnología",Science:"Ciencia",Health:"Salud",Business:"Negocios",Environment:"Medio ambiente",Culture:"Cultura",Sports:"Deportes",Education:"Educación",Space:"Espacio",Society:"Sociedad"},
de:{Technology:"Technologie",Science:"Wissenschaft",Health:"Gesundheit",Business:"Wirtschaft",Environment:"Umwelt",Culture:"Kultur",Sports:"Sport",Education:"Bildung",Space:"Raumfahrt",Society:"Gesellschaft"},
it:{Technology:"Tecnologia",Science:"Scienza",Health:"Salute",Business:"Economia",Environment:"Ambiente",Culture:"Cultura",Sports:"Sport",Education:"Istruzione",Space:"Spazio",Society:"Società"},
pt:{Technology:"Tecnologia",Science:"Ciência",Health:"Saúde",Business:"Negócios",Environment:"Meio ambiente",Culture:"Cultura",Sports:"Esportes",Education:"Educação",Space:"Espaço",Society:"Sociedade"},
ru:{Technology:"Технологии",Science:"Наука",Health:"Здоровье",Business:"Бизнес",Environment:"Экология",Culture:"Культура",Sports:"Спорт",Education:"Образование",Space:"Космос",Society:"Общество"},
zh:{Technology:"科技",Science:"科学",Health:"健康",Business:"商业",Environment:"环境",Culture:"文化",Sports:"体育",Education:"教育",Space:"太空",Society:"社会"},
ja:{Technology:"テクノロジー",Science:"科学",Health:"健康",Business:"ビジネス",Environment:"環境",Culture:"文化",Sports:"スポーツ",Education:"教育",Space:"宇宙",Society:"社会"},
ko:{Technology:"기술",Science:"과학",Health:"건강",Business:"비즈니스",Environment:"환경",Culture:"문화",Sports:"스포츠",Education:"교육",Space:"우주",Society:"사회"},
hi:{Technology:"तकनीक",Science:"विज्ञान",Health:"स्वास्थ्य",Business:"व्यापार",Environment:"पर्यावरण",Culture:"संस्कृति",Sports:"खेल",Education:"शिक्षा",Space:"अंतरिक्ष",Society:"समाज"},
tr:{Technology:"Teknoloji",Science:"Bilim",Health:"Sağlık",Business:"İş Dünyası",Environment:"Çevre",Culture:"Kültür",Sports:"Spor",Education:"Eğitim",Space:"Uzay",Society:"Toplum"},
nl:{Technology:"Technologie",Science:"Wetenschap",Health:"Gezondheid",Business:"Zaken",Environment:"Milieu",Culture:"Cultuur",Sports:"Sport",Education:"Onderwijs",Space:"Ruimte",Society:"Samenleving"},
pl:{Technology:"Technologia",Science:"Nauka",Health:"Zdrowie",Business:"Biznes",Environment:"Środowisko",Culture:"Kultura",Sports:"Sport",Education:"Edukacja",Space:"Kosmos",Society:"Społeczeństwo"},
sv:{Technology:"Teknik",Science:"Vetenskap",Health:"Hälsa",Business:"Ekonomi",Environment:"Miljö",Culture:"Kultur",Sports:"Sport",Education:"Utbildning",Space:"Rymden",Society:"Samhälle"},
el:{Technology:"Τεχνολογία",Science:"Επιστήμη",Health:"Υγεία",Business:"Επιχειρήσεις",Environment:"Περιβάλλον",Culture:"Πολιτισμός",Sports:"Αθλητισμός",Education:"Εκπαίδευση",Space:"Διάστημα",Society:"Κοινωνία"},
he:{Technology:"טכנולוגיה",Science:"מדע",Health:"בריאות",Business:"עסקים",Environment:"סביבה",Culture:"תרבות",Sports:"ספורט",Education:"חינוך",Space:"חלל",Society:"חברה"},
id:{Technology:"Teknologi",Science:"Sains",Health:"Kesehatan",Business:"Bisnis",Environment:"Lingkungan",Culture:"Budaya",Sports:"Olahraga",Education:"Pendidikan",Space:"Luar Angkasa",Society:"Masyarakat"},
vi:{Technology:"Công nghệ",Science:"Khoa học",Health:"Sức khỏe",Business:"Kinh doanh",Environment:"Môi trường",Culture:"Văn hóa",Sports:"Thể thao",Education:"Giáo dục",Space:"Không gian",Society:"Xã hội"}
};

/* ============ ARTICLES (50) ============ */
function img(seed){ return `https://picsum.photos/seed/${seed}/800/600`; }

const articles = [
{id:"doomsday",cat:"Culture",img:img("doomsday1"),title:"Avengers: Doomsday — Robert Downey Jr. Returns, This Time as Doctor Doom",p:["Marvel Studios confirmed that Robert Downey Jr. is returning to the MCU — not as Tony Stark, but as the villain Victor von Doom, in the upcoming Avengers: Doomsday.","Directors Joe and Anthony Russo have said the casting lets Doom carry real emotional weight rather than being a stock villain, since audiences already have a decade of history with the actor.","The film draws on multiverse-collapse storylines from recent Marvel comics and animated specials, and is scheduled for a wide theatrical release in December 2026."]},
{id:"wanda",cat:"Culture",img:img("wanda1"),title:"Why Wanda Maximoff Remains One of the MCU's Most Powerful Characters",p:["Across the Marvel Cinematic Universe, few characters have been shown gaining power as quickly as Wanda Maximoff, also known as the Scarlet Witch.","Her ability, described in the films as 'chaos magic,' lets her reshape her immediate surroundings — most memorably during the WandaVision series, where she unknowingly altered an entire town.","In Avengers: Endgame, she single-handedly overwhelmed Thanos in combat, a scene often cited by fans as a turning point in how the franchise treated her character."]},
{id:"detective-fiction",cat:"Culture",img:img("detective1"),title:"The Enduring Appeal of Detective Fiction",p:["From Sherlock Holmes to modern Nordic noir, detective fiction has stayed one of publishing's most reliable genres for over a century.","Researchers who study reading habits point to the genre's built-in structure — a puzzle with a guaranteed resolution — as part of its comfort, especially during uncertain times.","Television adaptations have only expanded the audience, with streaming services commissioning new detective series at a steady pace each year."]},
{id:"game-soundtracks",cat:"Culture",img:img("gamemusic1"),title:"How Video Game Soundtracks Became Concert Hall Staples",p:["Orchestras around the world now regularly perform live scores from games like Final Fantasy and The Legend of Zelda, filling venues once reserved for classical repertoire.","Composers working in games have gained recognition alongside film composers, in part because interactive scores demand unusually flexible, modular writing.","The trend has also introduced younger audiences to orchestral music, with many attending a symphony concert for the first time because of a game soundtrack."]},
{id:"street-photography",cat:"Culture",img:img("streetphoto1"),title:"Street Photography in the Age of Smartphones",p:["With a camera in nearly everyone's pocket, street photography has shifted from a specialist practice to something millions of people do casually every day.","Photography educators note that the core skills — timing, framing, patience — haven't changed, even as the tools have become smaller and more automatic.","Some cities have also seen renewed debate over privacy and consent as candid street photography becomes easier to shoot and share instantly."]},

{id:"quantum-2026",cat:"Technology",img:img("quantum1"),title:"Quantum Computing Passes a Key Reliability Milestone",p:["Several research labs reported progress in 2026 on error correction, one of the biggest practical obstacles to useful quantum computers.","Unlike classical bits, quantum bits are extremely sensitive to noise, so reducing error rates has long been considered more important than simply adding more qubits.","Experts caution that broadly useful quantum computers are likely still years away, even as these incremental improvements accumulate."]},
{id:"on-device-ai",cat:"Technology",img:img("ondevice1"),title:"The Rise of On-Device AI: Why Phones Are Getting Smarter Without the Cloud",p:["Newer smartphones increasingly run AI features locally rather than sending data to remote servers, thanks to dedicated chips built for machine learning tasks.","This shift can improve privacy and reduce latency, since photos, messages, and voice recordings don't need to leave the device to be processed.","The trade-off is that on-device models are usually smaller and less capable than their cloud-based counterparts, so manufacturers often blend both approaches."]},
{id:"warehouse-robots",cat:"Technology",img:img("warehouse1"),title:"Robotics in Warehouses: How Automation Is Reshaping Logistics",p:["Automated storage systems and mobile picking robots have become common in large distribution centers, speeding up order fulfillment during peak shopping periods.","Rather than replacing workers outright, many facilities now pair robots with human staff, with machines handling repetitive lifting and humans handling exceptions and quality checks.","Labor groups continue to push for retraining programs, arguing that the transition should come with a clear path to new roles within the same facilities."]},
{id:"right-to-repair",cat:"Technology",img:img("repair1"),title:"What a Right-to-Repair Law Actually Changes for Consumers",p:["Right-to-repair laws generally require manufacturers to make parts, tools, and documentation available so consumers and independent shops can fix devices themselves.","Supporters argue this extends product lifespans and reduces electronic waste, while manufacturers have historically raised concerns about safety and counterfeit parts.","Several regions have passed versions of these laws in recent years, with electronics and even agricultural equipment among the most discussed categories."]},
{id:"passwordless-login",cat:"Technology",img:img("passkey1"),title:"Why Passwordless Login Is Finally Catching On",p:["Passkeys — a login method based on device-stored cryptographic keys rather than typed passwords — have been adopted by a growing number of major websites and apps.","The approach is designed to resist common attacks like phishing, since there's no password to trick someone into typing into a fake site.","Adoption has been gradual because it requires both websites and devices to support the same standard, but momentum has picked up as major tech companies align on it."]},

{id:"deep-sea-vents",cat:"Science",img:img("vents1"),title:"Deep-Sea Vents and the Search for Life's Origins",p:["Hydrothermal vents on the ocean floor host communities of organisms that survive on chemical energy rather than sunlight, reshaping ideas about where life can exist.","Some researchers think similar chemical environments could exist on icy moons like Europa or Enceladus, making vent ecosystems a useful analogue for astrobiology.","Exploring these vents requires specialized submersibles able to withstand crushing pressure and near-freezing temperatures just meters from scalding mineral-rich water."]},
{id:"tree-rings",cat:"Science",img:img("treerings1"),title:"How Tree Rings Reveal Centuries of Climate History",p:["Each year, trees typically add a growth ring whose width and density reflect that year's temperature and rainfall, creating a natural climate record.","Dendrochronologists cross-reference rings from living trees with preserved wood from old buildings and buried logs to build timelines stretching back thousands of years.","This record has helped scientists identify past droughts, volcanic winters, and warm periods that predate written historical accounts."]},
{id:"northern-lights",cat:"Science",img:img("aurora1"),title:"The Physics Behind Northern Lights",p:["Auroras occur when charged particles from the sun collide with gases in Earth's upper atmosphere, causing them to glow in bands of green, red, and purple.","The color depends on which gas is struck and at what altitude — oxygen typically produces green and red, while nitrogen tends toward blue and purple.","Increased solar activity in recent years has pushed auroras visible further from the poles than usual, letting more people see them for the first time."]},
{id:"limb-regrowth",cat:"Science",img:img("regrow1"),title:"Why Some Animals Can Regrow Limbs",p:["Salamanders and certain fish can regenerate entire limbs or fins, a capability humans largely lost apart from partial regrowth in fingertips in early childhood.","Researchers studying these animals are trying to identify which genetic pathways enable regrowth, hoping the insights could eventually inform human tissue repair.","Progress has been slow, since regeneration involves a complex mix of cell signaling that isn't yet fully understood even in the animals that do it well."]},
{id:"universe-age",cat:"Science",img:img("telescope1"),title:"New Telescope Data Refines the Age of the Universe",p:["Newer space telescopes have provided sharper measurements of the cosmic microwave background, the faint afterglow of the early universe.","These refinements have narrowed estimates of the universe's age to roughly 13.8 billion years, though small discrepancies between measurement methods remain an active area of research.","Resolving that discrepancy, sometimes called the 'Hubble tension,' is considered one of the more interesting open problems in modern cosmology."]},

{id:"sleep-debt",cat:"Health",img:img("sleep1"),title:"Sleep Debt: What the Research Actually Shows",p:["Studies consistently link chronic short sleep to impaired concentration, mood changes, and higher long-term risk for several chronic conditions.","Researchers note that 'catching up' on sleep over a weekend helps somewhat but doesn't fully reverse the effects of a week of insufficient sleep.","Most sleep guidelines for adults still recommend roughly seven to nine hours nightly, though individual needs vary."]},
{id:"walking-breaks",cat:"Health",img:img("walking1"),title:"Why Walking Breaks Beat Long Sitting Sessions",p:["Research on sedentary behavior suggests that breaking up long periods of sitting with short walks can improve blood sugar and circulation markers, even without a formal workout.","This is sometimes described as 'exercise snacking' — brief bouts of movement spread through the day rather than one long session.","Public health guidance increasingly emphasizes reducing total sitting time as a complement to, not a replacement for, regular structured exercise."]},
{id:"gut-microbiome",cat:"Health",img:img("gut1"),title:"The Basics of Gut Microbiome Research",p:["The human gut hosts trillions of bacteria that help digest food, produce certain vitamins, and interact with the immune system in ways researchers are still mapping.","Diet, especially fiber intake, appears to be one of the biggest levers for shaping which bacterial species thrive in the gut.","Despite growing public interest in probiotics and gut health products, researchers caution that the science on many specific supplements remains preliminary."]},
{id:"vaccines-immune",cat:"Health",img:img("vaccine1"),title:"How Vaccines Train the Immune System",p:["Vaccines work by exposing the immune system to a harmless piece or weakened version of a pathogen, prompting it to build defenses without causing the disease itself.","This creates 'memory' immune cells that can respond much faster if the body later encounters the real pathogen.","Different vaccine technologies — including mRNA, viral vector, and traditional protein-based approaches — achieve this in different ways, each with its own strengths."]},
{id:"mental-health-apps",cat:"Health",img:img("mentalapp1"),title:"Mental Health Apps: What They Can and Can't Do",p:["Apps offering guided meditation, mood tracking, or structured cognitive behavioral exercises have grown into a large and popular category.","Clinical researchers say some of these tools show modest benefits for mild stress or sleep issues, but they are not a substitute for therapy in more serious cases.","Experts generally recommend treating these apps as a supplement to, rather than a replacement for, professional care when symptoms are significant or persistent."]},

{id:"remote-work-5years",cat:"Business",img:img("remote1"),title:"Remote Work Five Years On: What Actually Stuck",p:["After the sharp shift to remote work in the early 2020s, most companies have settled into hybrid arrangements rather than fully returning to the office or staying fully remote.","Surveys suggest employees generally value flexibility highly, while many managers report it's harder to build team cohesion without some regular in-person time.","The debate has shifted from 'remote versus office' to more specific questions, like how many in-office days actually deliver collaboration benefits."]},
{id:"interest-rates",cat:"Business",img:img("rates1"),title:"How Interest Rate Changes Ripple Through Everyday Prices",p:["When central banks raise interest rates, borrowing becomes more expensive for both businesses and consumers, which tends to cool spending over time.","This affects everything from mortgage payments to how much it costs a business to finance new equipment, with knock-on effects on prices and hiring.","Because these effects take months to show up fully in the economy, central banks generally act on where they expect the economy to be, not just where it is."]},
{id:"small-business-lending",cat:"Business",img:img("smallbiz1"),title:"Small Business Lending in a Tightening Market",p:["When credit conditions tighten, small businesses — which often rely more heavily on loans than large corporations with access to public markets — tend to feel it first.","Community banks and credit unions play an outsized role in small business lending, since larger banks often favor bigger, lower-risk loans.","Some regions have expanded loan guarantee programs to help small businesses maintain access to credit during tighter lending cycles."]},
{id:"airline-pricing",cat:"Business",img:img("airline1"),title:"The Economics of Airline Ticket Pricing",p:["Airline pricing changes constantly based on demand forecasting models that factor in how far in advance a ticket is booked, the route, and even the day of the week.","This is why two passengers on the same flight can pay very different fares depending on exactly when and how they booked.","Fuel costs and airport fees also shift regularly, adding another layer of volatility that airlines try to smooth out through dynamic pricing."]},
{id:"supply-chains",cat:"Business",img:img("supplychain1"),title:"Why Supply Chains Are Being Rebuilt Closer to Home",p:["After disruptions exposed the fragility of long, single-source supply chains, many companies have moved toward 'friend-shoring' or nearshoring production.","This often means paying more per unit in exchange for shorter shipping times and fewer points of failure during global disruptions.","Governments in several regions have also offered incentives to bring manufacturing of critical goods, like semiconductors, closer to home."]},

{id:"urban-heat",cat:"Environment",img:img("heat1"),title:"Urban Heat Islands and How Cities Are Cooling Down",p:["Dense concentrations of asphalt, concrete, and buildings can make cities several degrees warmer than surrounding rural areas, a phenomenon known as the urban heat island effect.","Cities have experimented with reflective 'cool' pavements, expanded tree canopy, and green roofs to reduce peak temperatures in the hottest neighborhoods.","Because heat exposure isn't distributed evenly, lower-income neighborhoods with less greenery often experience the sharpest temperature differences."]},
{id:"battery-recycling",cat:"Environment",img:img("battery1"),title:"Battery Recycling: The Next Big Materials Challenge",p:["As electric vehicles and grid storage batteries reach the end of their usable life, recovering materials like lithium, cobalt, and nickel is becoming an important recycling category.","Current recycling processes can recover a large share of these metals, but building enough recycling capacity to keep up with demand remains a work in progress.","Some manufacturers are also designing batteries to be easier to disassemble, anticipating future recycling requirements."]},
{id:"coral-restoration",cat:"Environment",img:img("coral1"),title:"How Coral Restoration Projects Actually Work",p:["Coral restoration typically involves growing coral fragments in nurseries before transplanting them onto damaged reef sections.","Some projects are experimenting with selectively breeding corals that tolerate warmer water better, aiming to build more heat-resistant reefs over time.","Scientists are clear that restoration can't outpace the underlying causes of reef decline, like warming oceans, without broader action to address those causes too."]},
{id:"wildfire-models",cat:"Environment",img:img("wildfire1"),title:"Wildfire Prediction Models Are Getting Sharper",p:["Newer wildfire models combine satellite data, weather forecasts, and vegetation moisture readings to estimate fire risk with more precision than in the past.","This has helped some fire agencies pre-position crews and equipment in high-risk areas before conditions turn dangerous, rather than reacting after a fire starts.","Even with better models, officials stress that public evacuation preparedness remains one of the most important factors in reducing harm."]},
{id:"circular-packaging",cat:"Environment",img:img("packaging1"),title:"The Push for Circular Packaging in Retail",p:["More retailers are testing reusable packaging systems, where containers are returned, cleaned, and refilled rather than discarded after a single use.","Early pilots have shown mixed results — convenience and return logistics matter as much as the packaging design itself for these programs to succeed.","Packaging researchers say the biggest gains often come from simply using less material in the first place, before considering reuse or recycling."]},

{id:"sports-analytics",cat:"Sports",img:img("analytics1"),title:"The Analytics Revolution in Everyday Coaching",p:["Data analysis once reserved for professional teams has trickled down to college and even youth sports, helping coaches make more informed decisions about strategy and player development.","Wearable trackers now let coaches monitor player workload in practice, aiming to reduce injury risk from overtraining.","Some coaches caution against over-relying on data, arguing that experience and in-game feel still matter for decisions analytics can't fully capture."]},
{id:"altitude-training",cat:"Sports",img:img("altitude1"),title:"How Altitude Training Camps Actually Work",p:["Training at high altitude forces the body to adapt to lower oxygen levels, which can boost red blood cell production and improve endurance once athletes return to sea level.","The effect typically takes a few weeks of consistent exposure to develop, which is why endurance athletes often schedule multi-week altitude camps before major events.","Not every athlete responds equally — individual variation in how bodies adapt to altitude is one reason results aren't guaranteed."]},
{id:"womens-leagues",cat:"Sports",img:img("womensports1"),title:"The Rise of Women's Professional Leagues Worldwide",p:["Attendance and broadcast viewership for women's professional leagues in sports like soccer and basketball have grown significantly in recent years.","This growth has translated into larger sponsorship deals and, in some leagues, meaningful increases in player salaries and facilities investment.","Advocates argue sustained media coverage — not just occasional highlight moments — has been one of the biggest drivers of this growth."]},
{id:"athlete-recovery",cat:"Sports",img:img("recovery1"),title:"Recovery Science: What Elite Athletes Do Differently",p:["Modern sports science treats recovery as seriously as training itself, with structured sleep tracking, nutrition timing, and load management built into weekly schedules.","Techniques like compression therapy and contrast water immersion remain popular, though researchers note evidence for some recovery tools is stronger than for others.","Sports scientists generally agree that consistent sleep is the single most reliable recovery tool, ahead of most specialized equipment."]},
{id:"youth-specialization",cat:"Sports",img:img("youthsport1"),title:"Youth Sports and the Debate Over Early Specialization",p:["Many youth athletes now focus on a single sport year-round from an early age, hoping it improves their chances of reaching elite levels later.","Sports medicine researchers have raised concerns that early specialization is linked to higher rates of overuse injury and burnout in young athletes.","Some youth sports organizations have started encouraging multi-sport participation, pointing to research suggesting it may build more well-rounded athleticism."]},

{id:"spaced-repetition",cat:"Education",img:img("study1"),title:"What Spaced Repetition Actually Does to Memory",p:["Spaced repetition — reviewing material at increasing intervals over time — is one of the most well-supported techniques in memory research for long-term retention.","The method works by prompting recall right before information would otherwise be forgotten, which strengthens the memory more than repeated short-term cramming.","Many language-learning and flashcard apps now build spaced repetition scheduling directly into their study algorithms."]},
{id:"financial-literacy",cat:"Education",img:img("finlit1"),title:"The Case for Teaching Financial Literacy Earlier",p:["A growing number of school systems have added personal finance courses to their curriculum, covering topics like budgeting, credit, and basic investing concepts.","Advocates argue that early exposure to these concepts can meaningfully shape financial habits before young people encounter loans, credit cards, or salaries on their own.","Critics note that a single course can't fully substitute for hands-on financial experience, and ongoing reinforcement outside school also matters."]},
{id:"adaptive-learning",cat:"Education",img:img("adaptive1"),title:"How Adaptive Learning Software Personalizes Practice",p:["Adaptive learning platforms adjust the difficulty and type of practice questions in real time based on how a student is performing.","This is meant to keep students in a productive difficulty range — challenging enough to promote learning, but not so hard it causes frustration or disengagement.","Early studies show promise for skill-building subjects like math, though researchers note more evidence is needed for subjects that rely heavily on open-ended writing or discussion."]},
{id:"vocational-training",cat:"Education",img:img("vocational1"),title:"Vocational Training's Comeback in a Tight Labor Market",p:["Trade and vocational programs have seen renewed interest as employers report shortages of skilled workers in fields like electrical work, plumbing, and advanced manufacturing.","Some high schools have expanded partnerships with local employers, offering apprenticeship pathways alongside traditional academic tracks.","Supporters argue this gives students a genuine alternative to a four-year degree, particularly in fields with strong demand and solid pay."]},
{id:"reading-aloud",cat:"Education",img:img("reading1"),title:"Reading Aloud: Why It Still Matters at Every Age",p:["Reading aloud to young children is strongly linked to vocabulary growth and later reading comprehension, according to decades of literacy research.","Educators note the benefits aren't limited to early childhood — reading aloud in classrooms at any grade level can model fluency and expose students to vocabulary above their independent reading level.","Some libraries have expanded read-aloud programs for adults too, citing benefits for language learners and community building."]},

{id:"reusable-rockets",cat:"Space",img:img("rocket1"),title:"Reusable Rockets and the Falling Cost of Reaching Orbit",p:["Reusable rocket boosters, which land and fly again rather than being discarded after a single launch, have significantly reduced the cost of sending payloads to orbit.","This has made frequent, lower-cost satellite launches practical, expanding access for smaller companies and research institutions that couldn't previously afford it.","Engineers continue working on reusing more rocket components, including the upper stages, which remain harder to recover than first-stage boosters."]},
{id:"sample-return",cat:"Space",img:img("samplereturn1"),title:"What We're Learning From Sample-Return Missions",p:["Missions that physically bring material back from asteroids or other planetary bodies let scientists study samples with lab equipment far more precise than what can be sent into space.","Analysis of returned samples has provided clues about the early solar system's chemistry and, in some cases, organic compounds relevant to the origins of life.","Sample-return missions are technically demanding, requiring precise navigation for both the initial approach and the eventual return to Earth."]},
{id:"exoplanets",cat:"Space",img:img("exoplanet1"),title:"The Search for Habitable Exoplanets, Explained",p:["Astronomers look for exoplanets in the 'habitable zone' — the range of distances from a star where liquid water could plausibly exist on a planet's surface.","Modern telescopes can now analyze the atmospheres of some exoplanets, searching for gas combinations that might hint at biological activity.","Confirming actual signs of life remains far off, but each new detection method narrows the list of promising candidates worth further study."]},
{id:"space-debris",cat:"Space",img:img("debris1"),title:"Space Debris: The Growing Traffic Problem in Orbit",p:["Decades of satellite launches have left thousands of pieces of debris in orbit, ranging from defunct satellites to fragments from past collisions.","Even small debris fragments can travel fast enough to seriously damage operational satellites or spacecraft, making tracking and avoidance an ongoing operational task.","Several organizations are testing debris-removal technology, including nets, harpoons, and robotic arms designed to capture and deorbit defunct objects."]},
{id:"astronaut-training",cat:"Space",img:img("astronaut1"),title:"How Astronauts Train for Long-Duration Missions",p:["Preparing for months-long missions involves not just technical spacecraft training but also psychological preparation for isolation and confined living conditions.","Astronauts practice emergency procedures repeatedly until they become close to automatic, since quick, correct responses matter most when problems occur far from immediate help.","Simulated missions on Earth, in isolated research stations, are often used to study how crews handle the mental strain of long-duration space travel."]},

{id:"pedestrian-streets",cat:"Society",img:img("pedestrian1"),title:"How Cities Are Redesigning Streets for Pedestrians",p:["A number of cities have converted car-heavy downtown streets into pedestrian zones, aiming to boost foot traffic for local businesses and reduce noise and pollution.","Studies of these conversions show mixed short-term effects on nearby retail sales, though many report positive results once the redesign matures and habits adjust.","Urban planners note that success often depends on nearby transit access, since removing car access without good alternatives can simply push traffic elsewhere."]},
{id:"digital-identity",cat:"Society",img:img("digitalid1"),title:"Digital Identity: Convenience vs. Privacy Trade-offs",p:["Digital ID systems, which let people verify their identity online or via a phone rather than a physical document, are being rolled out in a growing number of countries.","Supporters point to convenience and fraud reduction, while privacy advocates raise concerns about centralized data collection and potential misuse.","Many proposed systems now include privacy-by-design features, such as sharing only the specific fact needed (like 'is over 18') rather than a full identity record."]},
{id:"four-day-week",cat:"Society",img:img("fourday1"),title:"The Global Rise of Four-Day Workweek Pilots",p:["Multiple countries and companies have run trials of a four-day workweek with no reduction in pay, testing whether productivity holds up with fewer working hours.","Many pilot results have reported steady or even improved productivity, alongside higher employee-reported wellbeing and lower burnout.","Skeptics note that results vary by industry, and roles requiring constant customer coverage have found the model harder to implement than office-based work."]},
{id:"aging-pensions",cat:"Society",img:img("aging1"),title:"Aging Populations and the Future of Pension Systems",p:["Many countries are seeing a shrinking ratio of working-age adults to retirees, putting pressure on pension systems that rely on current workers funding current retirees.","Policy responses have included gradually raising retirement ages, encouraging private retirement savings, and adjusting benefit formulas.","Economists generally agree there's no single fix, and most countries are combining several smaller policy adjustments rather than one large reform."]},
{id:"local-news",cat:"Society",img:img("localnews1"),title:"Why Local News Outlets Are Struggling to Survive",p:["Local newspapers have lost a significant share of advertising revenue to online platforms over the past two decades, leading to widespread newsroom downsizing.","Researchers have linked the decline of local news to lower civic engagement and, in some studies, reduced accountability for local government.","Nonprofit newsroom models and reader-funded subscriptions have emerged as partial responses, though they haven't fully replaced lost advertising revenue industry-wide."]}
];

/* ============ AI JOB SAFETY MATRIX ============ */
const aiJobsDatabase = [
{id:"dev",title:"Software Developer",risk:"medium",score:60,note:"LLMs speed up routine code; system design stays human-led."},
{id:"music",title:"Music Producer / Composer",risk:"safe",score:25,note:"AI helps with loops; live performance and artistic voice stay human."},
{id:"chess",title:"Chess Coach",risk:"safe",score:15,note:"Engines win at pure play; teaching and psychology remain human skills."},
{id:"data",title:"Data Entry Specialist",risk:"high",score:92,note:"OCR and automated data agents handle most structured entry."},
{id:"design",title:"Graphic Designer",risk:"medium",score:55,note:"Generative tools speed asset creation; creative direction stays human."},
{id:"cust",title:"Customer Support Agent",risk:"high",score:88,note:"Chat and voice agents resolve most routine tickets."},
{id:"radio",title:"Radiologist",risk:"medium",score:45,note:"AI flags scans for review; final diagnosis needs a physician."},
{id:"account",title:"Junior Accountant",risk:"high",score:80,note:"Automated ledgers handle routine reconciliation and filings."},
{id:"copywriter",title:"Copywriter",risk:"high",score:82,note:"Draft generation is fast; brand voice and strategy still need editing."},
{id:"truck",title:"Long-Haul Truck Driver",risk:"medium",score:65,note:"Highway autonomy is advancing; complex urban driving still needs a driver."},
{id:"teacher",title:"Elementary School Teacher",risk:"safe",score:10,note:"Classroom management and child development need in-person presence."},
{id:"paralegal",title:"Paralegal",risk:"high",score:78,note:"Document review and precedent search are increasingly automated."},
{id:"chef",title:"Head Chef",risk:"safe",score:12,note:"Taste, menu creativity, and kitchen leadership stay human."},
{id:"electrician",title:"Electrician",risk:"safe",score:8,note:"Unpredictable physical environments are hard to automate reliably."},
{id:"prompt",title:"AI Prompt Specialist",risk:"medium",score:50,note:"As models improve at understanding intent, this niche role may shrink."},
{id:"video",title:"Video Editor",risk:"medium",score:58,note:"Rough cuts and color grading can be automated; storytelling stays human."},
{id:"financial",title:"Financial Planner",risk:"medium",score:48,note:"Robo-advisors handle allocation; client trust needs a human relationship."},
{id:"journalist",title:"Investigative Journalist",risk:"safe",score:20,note:"Source-building and field verification are hard to automate."},
{id:"architect",title:"Architect",risk:"safe",score:30,note:"Generative layouts speed early drafts; safety sign-off stays human."},
{id:"event",title:"Event Planner",risk:"safe",score:22,note:"On-site problem-solving and vendor relationships stay human-led."},
{id:"translator",title:"Professional Translator",risk:"high",score:75,note:"Machine translation covers routine text; nuance and certification still need people."},
{id:"nurse",title:"Registered Nurse",risk:"safe",score:14,note:"Direct patient care and judgment calls are not easily automated."},
{id:"warehouse",title:"Warehouse Picker",risk:"high",score:83,note:"Automated picking systems are increasingly common in large facilities."}
];

/* ============ VIDEOS (real IDs, extracted from provided links) ============ */
const youtubeVideos = [
{id:"GAAs2Q3Yh-Q",title:"Avengers: Doomsday Announcement & Cast Reveal"},
{id:"L7SDkHafU7k",title:"Robert Downey Jr. as Doctor Doom Explained"},
{id:"Z-RMCM0NxaY",title:"Scarlet Witch vs Thanos (Full Scene - Endgame)"},
{id:"3HQ9eZkVuXQ",title:"Wanda Maximoff Power Scale & Chaos Magic Breakdown"},
{id:"p_kF_SDB0-c",title:"How AI is Transforming Jobs and the Global Economy"},
{id:"5V0wAcxrUOo",title:"AI Music Creation Tools & Future of Songwriting"},
{id:"hI9HQfCAw64",title:"SpaceX Starship Flight Test - Space Exploration"},
{id:"B3U1NDUiwSA",title:"Quantum Computing Explained in 10 Minutes"}
];

/* ============ DAILY POLL ============ */
const dailyPoll = {
  question: "Which topic do you want more coverage of?",
  options: ["AI & Technology","Space Exploration","Health & Wellness","Culture & Entertainment"]
};

/* ============ QUIZ ============ */
const quizQuestions = [
  {q:"What does spaced repetition improve?", opts:["Long-term memory retention","Screen resolution","Battery life"], correct:0},
  {q:"What is a 'passkey' designed to replace?", opts:["Passwords","Usernames","Email addresses"], correct:0},
  {q:"What causes the aurora's colors?", opts:["Which atmospheric gas is struck, and at what altitude","The season of the year","The phase of the moon"], correct:0},
  {q:"What is a reusable rocket booster designed to do?", opts:["Land and fly again to cut launch costs","Burn up completely after every launch","Stay permanently in orbit"], correct:0},
  {q:"What has driven interest in nearshoring supply chains?", opts:["Reducing risk from long, single-source supply chains","Lowering unit costs above all else","Avoiding all overseas partners entirely"], correct:0}
];

let currentLang = 'en';
let currentCategory = 'all';
let currentLayout = 'grid';
let visibleCount = 10;
let currentArticleId = null;
let currentUser = null;

const ARTICLE_CATS = ["Technology","Science","Health","Business","Environment","Culture","Sports","Education","Space","Society"];

/* ---------- storage helpers ---------- */
function lsGet(key, fallback){ try{ const v = localStorage.getItem(key); return v ? JSON.parse(v) : fallback; }catch(e){ return fallback; } }
function lsSet(key, val){ try{ localStorage.setItem(key, JSON.stringify(val)); }catch(e){} }

/* ---------- language / UI strings ---------- */
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
  document.getElementById('section-title').childNodes[2] ? null : null;
  document.getElementById('section-title').innerHTML = `<i class="fa-solid fa-newspaper text-sky-500"></i> ${t.topStories}`;
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

/* ---------- categories ---------- */
function renderCategories(){
  const t = categoryNames[currentLang] || categoryNames.en;
  const cats = ['all', ...ARTICLE_CATS];
  const bar = document.getElementById('category-bar');
  bar.innerHTML = cats.map(cat => {
    const label = cat === 'all' ? (uiStrings[currentLang]?.topStories || 'All') : (t[cat] || cat);
    return `<button class="px-3.5 py-1.5 rounded-lg text-xs font-semibold transition ${cat===currentCategory?'bg-sky-600 text-white shadow-md':'bg-slate-800/80 text-slate-300 hover:bg-slate-700'}" onclick="filterCategory('${cat}')">${label}</button>`;
  }).join('');
}
function filterCategory(cat){ currentCategory = cat; visibleCount = 10; renderCategories(); renderArticles(); }

/* ---------- articles ---------- */
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
  const dataSaver = document.getElementById('s-datasaver')?.checked;

  shown.forEach(item => {
    const card = document.createElement('div');
    const isFav = favs.includes(item.id);
    const imgUrl = dataSaver ? item.img.replace('/800/600','/400/300') : item.img;
    if (currentLayout === 'grid'){
      card.className = "bg-slate-800/60 border border-slate-700/80 rounded-2xl overflow-hidden shadow-xl hover:border-sky-500/60 transition group cursor-pointer flex flex-col fade-in";
      card.innerHTML = `
        <div class="h-44 overflow-hidden relative" onclick="openArticle('${item.id}')">
          <img src="${imgUrl}" loading="lazy" alt="Cover" class="w-full h-full object-cover group-hover:scale-105 transition duration-500">
          <span class="absolute top-3 left-3 bg-slate-900/80 backdrop-blur text-sky-400 text-[10px] font-extrabold px-2.5 py-1 rounded-full border border-slate-700 uppercase">${cn[item.cat]||item.cat}</span>
          <button onclick="event.stopPropagation();toggleFavorite('${item.id}')" class="absolute top-3 right-3 w-7 h-7 rounded-full bg-slate-900/80 flex items-center justify-center ${isFav?'text-amber-400':'text-slate-300'} hover:text-amber-400"><i class="fa-${isFav?'solid':'regular'} fa-star text-xs"></i></button>
        </div>
        <div class="p-5 flex-1 flex flex-col justify-between space-y-3" onclick="openArticle('${item.id}')">
          <h3 class="font-bold text-slate-100 group-hover:text-sky-400 transition leading-snug line-clamp-2">${item.title}</h3>
          <div class="flex items-center justify-between text-xs text-slate-400 pt-2 border-t border-slate-700/50">
            <span><i class="fa-regular fa-clock mr-1"></i> Sept 19, 2026</span>
            <span class="text-sky-400 font-semibold flex items-center gap-1">${t.readMore} <i class="fa-solid fa-arrow-right text-[10px]"></i></span>
          </div>
        </div>`;
    } else {
      card.className = "bg-slate-800/60 border border-slate-700/80 rounded-xl p-4 flex items-center justify-between hover:border-sky-500/60 transition cursor-pointer fade-in";
      card.onclick = () => openArticle(item.id);
      card.innerHTML = `
        <div class="flex items-center space-x-4">
          <img src="${imgUrl}" loading="lazy" class="w-16 h-16 rounded-lg object-cover">
          <div><span class="text-[10px] font-bold text-sky-400 uppercase">${cn[item.cat]||item.cat}</span>
          <h4 class="font-bold text-sm text-slate-100 line-clamp-1">${item.title}</h4></div>
        </div>
        <i class="fa-solid fa-chevron-right text-slate-500"></i>`;
    }
    grid.appendChild(card);
  });
}
function loadMoreArticles(){ visibleCount += 10; renderArticles(); }
function handleSearch(){ visibleCount = 10; renderArticles(document.getElementById('search-input').value); }
function setLayoutMode(mode){
  currentLayout = mode;
  document.getElementById('view-grid-btn').className = mode==='grid' ? "px-2.5 py-1 text-xs rounded-md text-sky-400 bg-slate-700 font-medium transition" : "px-2.5 py-1 text-xs rounded-md text-slate-400 hover:text-white transition";
  document.getElementById('view-compact-btn').className = mode==='compact' ? "px-2.5 py-1 text-xs rounded-md text-sky-400 bg-slate-700 font-medium transition" : "px-2.5 py-1 text-xs rounded-md text-slate-400 hover:text-white transition";
  renderArticles();
}

/* ---------- article modal ---------- */
function openArticle(id){
  const item = articles.find(a => a.id === id);
  if (!item) return;
  currentArticleId = id;
  const t = uiStrings[currentLang] || uiStrings.en;
  const cn = categoryNames[currentLang] || categoryNames.en;
  document.getElementById('modal-tag').innerText = cn[item.cat] || item.cat;
  document.getElementById('modal-title').innerText = item.title;
  document.getElementById('modal-meta').innerText = `Mahdi WorldWide Bureau • Sept 19, 2026`;
  document.getElementById('modal-img').src = item.img;
  document.getElementById('modal-translate-note').classList.add('hidden');

  const level = document.getElementById('reading-level-select')?.value || 'standard';
  let paras = item.p;
  if (level === 'summary') paras = [item.p[0]];
  if (level === 'full') paras = item.p; // same content; hook point for longer copy later

  document.getElementById('modal-content').innerHTML = paras.map(p => `<p>${p}</p>`).join('');
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
  u.lang = (LANGS.find(l=>l.code===currentLang)||{}).code === 'ar' ? 'ar-SA' : currentLang;
  u.rate = parseFloat(document.getElementById('s-ttsrate')?.value || '1');
  window.speechSynthesis.speak(u);
}

/* ---------- favorites ---------- */
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
  if (!favs.length){ list.innerHTML = '<p class="italic text-slate-500 text-xs">No saved articles yet — tap the star on any article.</p>'; }
  else {
    list.innerHTML = favs.map(id => {
      const a = articles.find(x=>x.id===id);
      if (!a) return '';
      return `<div class="flex items-center justify-between p-2 bg-slate-800/60 rounded-lg border border-slate-700/50">
        <span class="cursor-pointer hover:text-sky-400" onclick="closeFavorites();openArticle('${a.id}')">${a.title}</span>
        <button onclick="toggleFavorite('${a.id}');openFavorites();" class="text-amber-400 text-xs"><i class="fa-solid fa-xmark"></i></button>
      </div>`;
    }).join('');
  }
  document.getElementById('favorites-modal').classList.remove('hidden');
  document.getElementById('favorites-modal').classList.add('flex');
}
function closeFavorites(){
  document.getElementById('favorites-modal').classList.add('hidden');
  document.getElementById('favorites-modal').classList.remove('flex');
}

/* ---------- history ---------- */
function updateHistoryWidget(){
  const widget = document.getElementById('history-list-widget');
  const history = lsGet('mahdi_news_history', []);
  if (!history.length){ widget.innerHTML = `<p class="italic text-slate-500">No recent articles read yet.</p>`; return; }
  widget.innerHTML = history.map(h => `
    <div class="p-2 bg-slate-900/60 rounded-lg border border-slate-700/50 flex items-center justify-between">
      <span class="font-medium text-slate-200 truncate max-w-[180px]">${h.title}</span>
      <span class="text-[10px] text-slate-500">${h.date}</span>
    </div>`).join('');
}
function clearHistory(){ lsSet('mahdi_news_history', []); updateHistoryWidget(); }

/* ---------- AI job matrix ---------- */
function renderAiJobsTable(filterRisk="all"){
  const tbody = document.getElementById('ai-jobs-tbody');
  let list = aiJobsDatabase;
  if (filterRisk !== "all") list = list.filter(j => j.risk === filterRisk);
  tbody.innerHTML = list.map(job => {
    let badge = job.risk === 'high'
      ? `<span class="px-2.5 py-1 rounded-full text-[11px] font-bold bg-red-950 text-red-400 border border-red-800">High (${job.score}%)</span>`
      : job.risk === 'medium'
      ? `<span class="px-2.5 py-1 rounded-full text-[11px] font-bold bg-amber-950 text-amber-400 border border-amber-800">Medium (${job.score}%)</span>`
      : `<span class="px-2.5 py-1 rounded-full text-[11px] font-bold bg-emerald-950 text-emerald-400 border border-emerald-800">Safe (${job.score}%)</span>`;
    return `<tr class="hover:bg-slate-800/50 transition">
      <td class="py-3.5 px-4 font-bold text-slate-200">${job.title}</td>
      <td class="py-3.5 px-4 text-center"><div class="w-full bg-slate-800 rounded-full h-2 max-w-[80px] mx-auto overflow-hidden"><div class="h-full ${job.score>70?'bg-red-500':job.score>35?'bg-amber-500':'bg-emerald-500'}" style="width:${job.score}%"></div></div></td>
      <td class="py-3.5 px-4">${badge}</td>
      <td class="py-3.5 px-4 text-xs text-slate-300">${job.note}</td>
    </tr>`;
  }).join('');
}
function filterAiJobs(){ renderAiJobsTable(document.getElementById('risk-filter').value); }

/* ---------- video sidebar ---------- */
function renderYouTubeSidebar(){
  document.getElementById('youtube-videos-list').innerHTML = youtubeVideos.map(v => `
    <div onclick="playVideo('${v.id}','${v.title.replace(/'/g,"\\'")}')" class="p-2.5 rounded-xl bg-slate-900/80 border border-slate-700/60 hover:border-sky-500 flex items-center space-x-3 cursor-pointer transition">
      <div class="w-10 h-10 rounded-lg bg-red-600/20 text-red-500 flex items-center justify-center shrink-0"><i class="fa-solid fa-play"></i></div>
      <div class="text-xs font-semibold text-slate-200 line-clamp-2">${v.title}</div>
    </div>`).join('');
  playVideo(youtubeVideos[0].id, youtubeVideos[0].title, false);
}
function playVideo(id, title, autoplay){
  const wantsAutoplay = autoplay !== false && document.getElementById('s-autoplay')?.checked;
  document.getElementById('featured-video-iframe').src = `https://www.youtube.com/embed/${id}${wantsAutoplay?'?autoplay=1':''}`;
  document.getElementById('featured-video-caption').innerText = title;
}

/* ---------- daily poll (local only) ---------- */
function renderPoll(){
  const el = document.getElementById('poll-widget');
  const voted = lsGet('mahdi_poll_vote', null);
  const counts = lsGet('mahdi_poll_counts', [3,5,2,4]);
  if (voted === null){
    el.innerHTML = `<h3 class="font-bold text-slate-100 mb-3"><i class="fa-solid fa-square-poll-vertical text-sky-400"></i> ${dailyPoll.question}</h3>
      <div class="grid grid-cols-1 sm:grid-cols-2 gap-2">
      ${dailyPoll.options.map((o,i)=>`<button onclick="votePoll(${i})" class="text-left px-3 py-2 rounded-lg bg-slate-900/70 border border-slate-700 text-sm text-slate-200 hover:border-sky-500 transition">${o}</button>`).join('')}
      </div>`;
  } else {
    const total = counts.reduce((a,b)=>a+b,0) || 1;
    el.innerHTML = `<h3 class="font-bold text-slate-100 mb-3"><i class="fa-solid fa-square-poll-vertical text-sky-400"></i> ${dailyPoll.question}</h3>
      <div class="space-y-2">
      ${dailyPoll.options.map((o,i)=>{
        const pct = Math.round(counts[i]/total*100);
        return `<div><div class="flex justify-between text-xs text-slate-300 mb-1"><span>${o}${i===voted?' ✓':''}</span><span>${pct}%</span></div>
        <div class="w-full bg-slate-900 rounded-full h-2"><div class="h-2 rounded-full ${i===voted?'bg-sky-500':'bg-slate-600'}" style="width:${pct}%"></div></div></div>`;
      }).join('')}
      </div><p class="text-[10px] text-slate-500 mt-3">Poll results are simulated locally in your browser for this demo.</p>`;
  }
}
function votePoll(i){
  lsSet('mahdi_poll_vote', i);
  const counts = lsGet('mahdi_poll_counts', [3,5,2,4]);
  counts[i]++;
  lsSet('mahdi_poll_counts', counts);
  renderPoll();
}

/* ---------- quiz ---------- */
let quizIndex = 0, quizScore = 0;
function renderQuiz(){
  quizIndex = 0; quizScore = 0;
  renderQuizQuestion();
}
function renderQuizQuestion(){
  const el = document.getElementById('quiz-widget');
  if (quizIndex >= quizQuestions.length){
    el.innerHTML = `<p class="text-sm text-slate-200">You scored <span class="font-bold text-emerald-400">${quizScore}/${quizQuestions.length}</span>!</p>
      <button onclick="renderQuiz()" class="mt-3 text-xs bg-slate-800 hover:bg-slate-700 border border-slate-700 rounded-lg px-3 py-1.5">Try again</button>`;
    return;
  }
  const q = quizQuestions[quizIndex];
  el.innerHTML = `<p class="text-sm text-slate-200 mb-3">${q.q}</p>
    <div class="space-y-2">${q.opts.map((o,i)=>`<button onclick="answerQuiz(${i})" class="w-full text-left text-xs px-3 py-2 rounded-lg bg-slate-900/70 border border-slate-700 hover:border-emerald-500 transition">${o}</button>`).join('')}</div>
    <p class="text-[10px] text-slate-500 mt-2">Question ${quizIndex+1} of ${quizQuestions.length}</p>`;
}
function answerQuiz(i){
  const q = quizQuestions[quizIndex];
  if (i === q.correct) quizScore++;
  quizIndex++;
  renderQuizQuestion();
}

/* ---------- settings ---------- */
function toggleSettingsDrawer(){ document.getElementById('settings-drawer').classList.toggle('translate-x-full'); }
function setTheme(theme){
  const body = document.body;
  body.classList.remove('high-contrast','sepia','bg-white','text-slate-900');
  if (theme==='high-contrast') body.classList.add('high-contrast');
  else if (theme==='light') body.classList.add('bg-white','text-slate-900');
  else if (theme==='sepia') body.classList.add('sepia');
  lsSet('mahdi_theme', theme);
}
function setFontSize(size){ document.documentElement.style.fontSize = size; lsSet('mahdi_fontsize', size); }
function setReadingLevel(v){ lsSet('mahdi_reading_level', v); if (currentArticleId) openArticle(currentArticleId); }
function exportMyData(){
  const data = {
    favorites: lsGet('mahdi_favorites', []),
    history: lsGet('mahdi_news_history', []),
    theme: lsGet('mahdi_theme', 'dark'),
    lang: currentLang
  };
  const blob = new Blob([JSON.stringify(data, null, 2)], {type:'application/json'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'mahdi-my-data.json';
  a.click();
}
function wireSettingToggles(){
  ['s-reducemotion','s-dyslexia'].forEach(id=>{
    document.getElementById(id).addEventListener('change', (e)=>{
      if (id==='s-reducemotion') document.body.classList.toggle('reduce-motion', e.target.checked);
      if (id==='s-dyslexia') document.body.classList.toggle('dyslexia-font', e.target.checked);
    });
  });
  document.getElementById('s-datasaver').addEventListener('change', renderArticles);
}
function resetView(){
  currentCategory='all'; visibleCount=10;
  document.getElementById('search-input').value = "";
  renderCategories(); renderArticles();
}

/* ---------- auth (local demo only, no real backend) ---------- */
function openAuthModal(){ document.getElementById('auth-modal').classList.remove('hidden'); }
function closeAuthModal(){ document.getElementById('auth-modal').classList.add('hidden'); }
function handleLoginSubmit(e){
  e.preventDefault();
  const name = document.getElementById('auth-email').value || 'Reader';
  currentUser = {name};
  lsSet('mahdi_user', currentUser);
  document.getElementById('auth-btn-label').innerText = name;
  document.getElementById('auth-status-msg').innerText = "Signed in locally (demo only).";
  setTimeout(closeAuthModal, 900);
}
function updateAuthUI(){
  const stored = lsGet('mahdi_user', null);
  if (stored){ currentUser = stored; document.getElementById('auth-btn-label').innerText = stored.name; }
}

/* ---------- cookies ---------- */
function acceptCookies(all){ lsSet('mahdi_cookies_accepted', all ? 'all' : 'essential'); document.getElementById('cookie-banner').classList.add('hidden'); }
function checkCookieBanner(){ if (lsGet('mahdi_cookies_accepted', null)) document.getElementById('cookie-banner').classList.add('hidden'); }

/* ---------- AI assistant + AI translate ----------
   These call the Anthropic API endpoint the way Claude's own artifact
   preview supports (fetch to /v1/messages, no key needed *inside* that
   preview). If you host this file on your own server outside Claude,
   this call will fail — you'd need to point it at your own backend that
   holds an API key, since a static HTML file can never safely hold one
   itself. The catch block below explains that to the user instead of
   silently breaking. */
async function callClaude(prompt){
  const response = await fetch("https://api.anthropic.com/v1/messages", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
      model: "claude-sonnet-4-6",
      max_tokens: 500,
      messages: [{ role: "user", content: prompt }]
    })
  });
  if (!response.ok) throw new Error("API request failed");
  const data = await response.json();
  return data.content.map(b => b.text || "").join("\n");
}

function toggleAiPanel(){
  const panel = document.getElementById('ai-panel');
  const isHidden = panel.classList.contains('hidden');
  panel.classList.toggle('hidden');
  panel.classList.toggle('flex');
  if (isHidden && !document.getElementById('ai-chat-log').dataset.greeted){
    appendAiMessage('assistant', "Hi! Ask me to explain any article, term, or the AI-risk table above. (Live AI replies only work when this page runs inside Claude's own preview — if you've downloaded and self-hosted this file, you'll need to wire this button to your own backend and API key.)");
    document.getElementById('ai-chat-log').dataset.greeted = "1";
  }
}
function appendAiMessage(role, text){
  const log = document.getElementById('ai-chat-log');
  const bubble = document.createElement('div');
  bubble.className = role === 'user'
    ? "ml-auto max-w-[85%] bg-sky-600 text-white rounded-xl rounded-br-sm px-3 py-2"
    : "mr-auto max-w-[85%] bg-slate-800 text-slate-200 rounded-xl rounded-bl-sm px-3 py-2";
  bubble.innerText = text;
  log.appendChild(bubble);
  log.scrollTop = log.scrollHeight;
}
async function sendAiMessage(){
  const input = document.getElementById('ai-chat-input');
  const msg = input.value.trim();
  if (!msg) return;
  appendAiMessage('user', msg);
  input.value = "";
  appendAiMessage('assistant', "Thinking...");
  const log = document.getElementById('ai-chat-log');
  try {
    const reply = await callClaude(msg);
    log.lastChild.innerText = reply;
  } catch (err){
    log.lastChild.innerText = "I couldn't reach the AI backend from here. This button needs either Claude's own artifact preview, or your own server + API key wired in to callClaude() in app.js.";
  }
}

async function translateArticleAI(){
  const item = articles.find(a => a.id === currentArticleId);
  if (!item) return;
  const note = document.getElementById('modal-translate-note');
  note.classList.remove('hidden');
  note.innerText = "Translating with AI...";
  const targetLang = (LANGS.find(l=>l.code===currentLang)||{}).name || 'the selected language';
  try {
    const prompt = `Translate the following news article into ${targetLang}. Return only the translated title on the first line, then a blank line, then the translated body paragraphs.\n\nTitle: ${item.title}\n\n${item.p.join('\n\n')}`;
    const result = await callClaude(prompt);
    const [titleLine, ...rest] = result.split('\n').filter(Boolean);
    document.getElementById('modal-title').innerText = titleLine || item.title;
    document.getElementById('modal-content').innerHTML = rest.map(p => `<p>${p}</p>`).join('');
    note.innerText = "Translated with AI — may contain errors.";
  } catch (err){
    note.innerText = "AI translation isn't available outside Claude's artifact preview for this demo file. Showing the original English instead.";
  }
}

/* ---------- init ---------- */
window.onload = () => {
  currentLang = lsGet('mahdi_lang', 'en');
  populateLangSelect();
  document.getElementById('lang-select').value = currentLang;
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

<!DOCTYPE html>
<html lang="ckb" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>سیستەمی دابەشکردنی خۆراک - بەڕێوەبردن و کۆگا</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Vazirmatn & Noto Sans Arabic for clean Kurdish typography -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Arabic:wght@300;400;500;600;700;800&family=Vazirmatn:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- FontAwesome for crisp icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Vazirmatn', 'Noto Sans Arabic', 'sans-serif'],
                    },
                    colors: {
                        wheat: {
                            50: '#fdfaf3',
                            100: '#faf2de',
                            200: '#f4e1b8',
                            300: '#ecc987',
                            400: '#e2ab52',
                            500: '#d9912b',
                            600: '#c27520',
                            700: '#a1591c',
                            800: '#83471d',
                            900: '#6b3b1b',
                        },
                        emeraldDark: '#064e3b',
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Vazirmatn', 'Noto Sans Arabic', sans-serif;
            background-color: #f8fafc;
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 9999px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
        /* Print styles */
        @media print {
            .no-print {
                display: none !important;
            }
            body {
                background-color: white !important;
            }
            .print-only {
                display: block !important;
            }
            .shadow-md, .shadow-lg, .shadow-xl {
                box-shadow: none !important;
                border: 1px solid #e2e8f0 !important;
            }
        }
        .wheat-glow {
            filter: drop-shadow(0 4px 10px rgba(217, 145, 43, 0.25));
        }
    </style>
</head>
<body class="text-slate-800 antialiased selection:bg-wheat-200 selection:text-wheat-900">

    <!-- Toast Notification Container (Replaces alert) -->
    <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 max-w-sm w-full pointer-events-none"></div>

    <!-- Custom Confirmation Modal (Replaces confirm) -->
    <div id="confirm-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 hidden items-center justify-center p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl border border-slate-100 transform transition-all">
            <div class="flex items-center gap-3 text-amber-600 mb-3">
                <div class="w-10 h-10 rounded-full bg-amber-100 flex items-center justify-center text-lg">
                    <i class="fa-solid fa-triangle-exclamation"></i>
                </div>
                <h3 id="confirm-title" class="text-lg font-bold text-slate-800">دڵنیاکردنەوە</h3>
            </div>
            <p id="confirm-message" class="text-slate-600 text-sm leading-relaxed mb-6">ئایا دڵنیایت لە ئەنجامدانی ئەم کردارە؟</p>
            <div class="flex items-center justify-end gap-3">
                <button id="confirm-cancel-btn" class="px-4 py-2.5 rounded-xl bg-slate-100 hover:bg-slate-200 text-slate-700 font-medium text-sm transition">پاشگەزبوونەوە</button>
                <button id="confirm-ok-btn" class="px-5 py-2.5 rounded-xl bg-red-600 hover:bg-red-700 text-white font-medium text-sm shadow-sm transition">بەڵێ، جێبەجێی بکە</button>
            </div>
        </div>
    </div>

    <!-- ===================================================================== -->
    <!-- 1. LOGIN SCREEN (پەڕەی چوونەژوورەوە و گۆڕینی پاسۆرد) -->
    <!-- ===================================================================== -->
    <div id="login-screen" class="min-h-screen flex items-center justify-center bg-gradient-to-br from-slate-900 via-emerald-950 to-slate-900 p-4">
        <div class="max-w-md w-full bg-white/95 backdrop-blur-md rounded-3xl shadow-2xl overflow-hidden border border-wheat-200/50">
            <!-- Top Decorative Wheat Banner -->
            <div class="bg-gradient-to-l from-wheat-600 via-wheat-500 to-amber-500 p-6 text-center text-white relative overflow-hidden">
                <div class="w-20 h-20 mx-auto bg-white rounded-2xl shadow-lg flex items-center justify-center mb-3 wheat-glow">
                    <!-- Custom Wheat SVG Logo -->
                    <svg class="w-14 h-14 text-wheat-600" viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M32 58V14" stroke="currentColor" stroke-width="3" stroke-linecap="round"/>
                        <!-- Left Wheat Grains -->
                        <path d="M32 46C24 46 19 41 19 34C26 34 32 39 32 46Z" fill="#d9912b"/>
                        <path d="M32 36C24 36 19 31 19 24C26 24 32 29 32 36Z" fill="#e2ab52"/>
                        <path d="M32 26C24 26 19 21 19 14C26 14 32 19 32 26Z" fill="#d9912b"/>
                        <!-- Right Wheat Grains -->
                        <path d="M32 46C40 46 45 41 45 34C38 34 32 39 32 46Z" fill="#e2ab52"/>
                        <path d="M32 36C40 36 45 31 45 24C38 24 32 29 32 36Z" fill="#d9912b"/>
                        <path d="M32 26C40 26 45 21 45 14C38 14 32 19 32 26Z" fill="#e2ab52"/>
                        <!-- Top Grain -->
                        <path d="M32 16C28 11 28 6 32 3C36 6 36 11 32 16Z" fill="#c27520"/>
                        <!-- Awns (whiskers) -->
                        <path d="M19 34L14 28M19 24L14 18M19 14L14 8M45 34L50 28M45 24L50 18M45 14L50 8" stroke="#a1591c" stroke-width="1.5" stroke-linecap="round"/>
                    </svg>
                </div>
                <h1 class="text-xl sm:text-2xl font-extrabold tracking-tight">سیستەمی دابەشکردنی خۆراك و بەرێوەبردن</h1>
            </div>

            <div class="p-6 sm:p-8">
                <!-- Login Form -->
                <form id="login-form" class="space-y-4">
                    <div>
                        <label for="login-password" class="block text-sm font-bold text-slate-700 mb-1.5">پاسۆردی چوونەژوورەوە بنووسە:</label>
                        <div class="relative">
                            <span class="absolute inset-y-0 right-0 flex items-center pr-3.5 text-slate-400">
                                <i class="fa-solid fa-lock"></i>
                            </span>
                            <input type="password" id="login-password" placeholder="پاسۆرد (بنەڕەتی: 009988)" required
                                class="w-full pr-10 pl-10 py-3 rounded-xl border border-slate-300 focus:border-wheat-500 focus:ring-2 focus:ring-wheat-200 outline-none text-left font-mono text-lg tracking-widest transition" dir="ltr">
                            <button type="button" onclick="togglePasswordVisibility('login-password', this)" class="absolute inset-y-0 left-0 flex items-center pl-3.5 text-slate-400 hover:text-slate-600">
                                <i class="fa-solid fa-eye"></i>
                            </button>
                        </div>
                    </div>

                    <button type="submit" class="w-full py-3.5 px-4 bg-gradient-to-l from-emerald-700 to-emerald-600 hover:from-emerald-800 hover:to-emerald-700 text-white font-bold rounded-xl shadow-lg shadow-emerald-600/20 transition flex items-center justify-center gap-2 text-base">
                        <i class="fa-solid fa-right-to-bracket"></i>
                        <span>چوونەژوورەوە بۆ سیستەم</span>
                    </button>
                </form>

                <!-- Toggle Change Password Section (لە خوارەوە شوێنی گۆڕینی پاسۆردەکە هەبێت) -->
                <div class="mt-6 pt-5 border-t border-slate-200">
                    <button type="button" id="toggle-change-pass-btn" onclick="toggleChangePasswordBox()" class="w-full py-2 px-3 rounded-xl bg-wheat-50 hover:bg-wheat-100 text-wheat-800 font-semibold text-sm flex items-center justify-center gap-2 border border-wheat-200 transition">
                        <i class="fa-solid fa-key text-wheat-600"></i>
                        <span>گۆڕینی پاسۆردی سیستەم</span>
                        <i id="change-pass-chevron" class="fa-solid fa-chevron-down text-xs transition-transform"></i>
                    </button>

                    <!-- Change Password Form (Hidden by default) -->
                    <form id="change-password-form" class="hidden mt-4 space-y-3 bg-slate-50 p-4 rounded-2xl border border-slate-200">
                        <h4 class="text-xs font-bold text-slate-600 uppercase tracking-wider mb-2">نوێکردنەوەی پاسۆرد</h4>
                        <div>
                            <label class="block text-xs font-semibold text-slate-600 mb-1">پاسۆردی ئێستا (کۆن):</label>
                            <input type="password" id="old-password" placeholder="009988" required dir="ltr"
                                class="w-full px-3 py-2 rounded-lg border border-slate-300 focus:border-wheat-500 outline-none text-sm font-mono">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-600 mb-1">پاسۆردی نوێ:</label>
                            <input type="password" id="new-password" placeholder="پاسۆردی نوێ بنووسە" required dir="ltr"
                                class="w-full px-3 py-2 rounded-lg border border-slate-300 focus:border-wheat-500 outline-none text-sm font-mono">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-600 mb-1">دڵنیاکردنەوەی پاسۆردی نوێ:</label>
                            <input type="password" id="confirm-new-password" placeholder="دووبارە پاسۆردی نوێ بنووسە" required dir="ltr"
                                class="w-full px-3 py-2 rounded-lg border border-slate-300 focus:border-wheat-500 outline-none text-sm font-mono">
                        </div>
                        <button type="submit" class="w-full py-2.5 bg-wheat-600 hover:bg-wheat-700 text-white font-bold rounded-xl text-sm transition shadow-sm">
                            پاشەکەوتکردنی پاسۆردی نوێ
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </div>

    <!-- ===================================================================== -->
    <!-- 2. MAIN APPLICATION DASHBOARD -->
    <!-- ===================================================================== -->
    <div id="main-app" class="hidden min-h-screen flex flex-col">
        
        <!-- TOP HEADER -->
        <header class="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-sm no-print">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3">
                <div class="flex flex-col lg:flex-row lg:items-center lg:justify-between gap-4">
                    
                    <!-- Right Side: Wheat Logo & System Title -->
                    <div class="flex items-center justify-between">
                        <div class="flex flex-col items-center sm:items-start">
                            <div class="flex items-center gap-3">
                                <div class="w-12 h-12 rounded-2xl bg-gradient-to-br from-wheat-100 to-amber-50 border border-wheat-300 flex items-center justify-center shadow-sm shrink-0">
                                    <!-- Wheat Logo SVG -->
                                    <svg class="w-9 h-9 text-wheat-600" viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg">
                                        <path d="M32 58V14" stroke="currentColor" stroke-width="3.5" stroke-linecap="round"/>
                                        <path d="M32 46C24 46 19 41 19 34C26 34 32 39 32 46Z" fill="#d9912b"/>
                                        <path d="M32 36C24 36 19 31 19 24C26 24 32 29 32 36Z" fill="#e2ab52"/>
                                        <path d="M32 26C24 26 19 21 19 14C26 14 32 19 32 26Z" fill="#d9912b"/>
                                        <path d="M32 46C40 46 45 41 45 34C38 34 32 39 32 46Z" fill="#e2ab52"/>
                                        <path d="M32 36C40 36 45 31 45 24C38 24 32 29 32 36Z" fill="#d9912b"/>
                                        <path d="M32 26C40 26 45 21 45 14C38 14 32 19 32 26Z" fill="#e2ab52"/>
                                        <path d="M32 16C28 11 28 6 32 3C36 6 36 11 32 16Z" fill="#c27520"/>
                                        <path d="M19 34L14 28M19 24L14 18M19 14L14 8M45 34L50 28M45 24L50 18M45 14L50 8" stroke="#a1591c" stroke-width="1.5" stroke-linecap="round"/>
                                    </svg>
                                </div>
                                <div class="flex items-center gap-2 text-xs text-slate-500">
                                    <span class="inline-flex items-center gap-1.5 text-wheat-800 font-bold bg-wheat-100 px-3 py-1 rounded-full">
                                        <i class="fa-solid fa-calendar-days text-wheat-600 text-xs"></i>
                                        <span id="header-current-day"></span>
                                        <span class="text-wheat-400">|</span>
                                        <span id="header-current-date" dir="ltr"></span>
                                    </span>
                                    <span class="hidden sm:inline text-slate-300">|</span>
                                    <span class="hidden sm:inline font-medium text-emerald-700">پەڕەی چالاک: <strong id="current-sheet-label">لیستی سەرەکی</strong></span>
                                </div>
                            </div>
                            <h1 class="text-base sm:text-lg font-extrabold text-slate-800 leading-tight mt-1.5">سیستەمی دابەشکردنی خۆراك و بەرێوەبردن</h1>
                        </div>

                        <!-- Mobile Logout Button -->
                        <button onclick="logout()" class="lg:hidden p-2.5 rounded-xl bg-red-50 text-red-600 hover:bg-red-100 transition" title="چوونەدەرەوە">
                            <i class="fa-solid fa-power-off"></i>
                        </button>
                    </div>

                    <!-- Top Left: Page Name Input & Send to Archive Button + Online Guide + Logout -->
                    <div class="flex flex-wrap items-center gap-2 bg-slate-50 p-2 rounded-2xl border border-slate-200">
                        <div class="flex items-center flex-1 sm:flex-initial bg-white rounded-xl border border-slate-300 focus-within:border-wheat-500 focus-within:ring-2 focus-within:ring-wheat-200 overflow-hidden">
                            <span class="pr-3 text-wheat-600 text-sm"><i class="fa-solid fa-folder-plus"></i></span>
                            <input type="text" id="archive-page-name-input" placeholder="ناوی فایلی مانگانە (نموونە: مانگی ١١)..." 
                                class="px-2.5 py-2 text-sm outline-none w-full sm:w-56 bg-transparent">
                        </div>
                        <button onclick="openMonthlyFile()" class="px-4 py-2 rounded-xl bg-emerald-700 hover:bg-emerald-800 text-white font-bold text-sm shadow-sm transition flex items-center gap-2 whitespace-nowrap">
                            <i class="fa-solid fa-folder-open"></i>
                            <span>کردنەوەی فایلی مانگانە</span>
                        </button>
                        <button onclick="finishCurrentBasketToArchive()" class="px-4 py-2 rounded-xl bg-wheat-600 hover:bg-wheat-700 text-white font-bold text-sm shadow-sm transition flex items-center gap-2 whitespace-nowrap">
                            <i class="fa-solid fa-flag-checkered"></i>
                            <span>هەموو ئەم سەبەتە کۆتایی هات</span>
                        </button>
                        <button onclick="openOnlineModal()" class="px-3 py-2 rounded-xl bg-sky-50 hover:bg-sky-100 text-sky-700 border border-sky-200 font-semibold text-sm transition flex items-center gap-1.5" title="چۆنیەتی کردنی بە سایت لەسەر ئۆنلاین">
                            <i class="fa-solid fa-globe"></i>
                            <span class="hidden md:inline">ئۆنلاین</span>
                        </button>
                        <button onclick="logout()" class="hidden lg:flex px-3 py-2 rounded-xl bg-red-50 hover:bg-red-100 text-red-600 border border-red-200 font-semibold text-sm transition items-center gap-1.5" title="قفڵکردن و چوونەدەرەوە">
                            <i class="fa-solid fa-lock"></i>
                        </button>
                    </div>

                </div>

                <!-- NAVIGATION TABS -->
                <nav class="flex items-center gap-1.5 sm:gap-2 mt-3 pt-3 border-t border-slate-100 overflow-x-auto pb-1">
                    <button onclick="switchTab('distribution')" id="tab-btn-distribution" class="tab-btn active flex items-center gap-2 px-4 py-2.5 rounded-xl font-bold text-sm transition whitespace-nowrap bg-emerald-700 text-white shadow-sm">
                        <i class="fa-solid fa-hand-holding-heart"></i>
                        <span>دابەشکردنی خۆراک</span>
                    </button>
                    <button onclick="switchTab('beneficiaries')" id="tab-btn-beneficiaries" class="tab-btn flex items-center gap-2 px-4 py-2.5 rounded-xl font-bold text-sm transition whitespace-nowrap bg-slate-100 text-slate-600 hover:bg-slate-200">
                        <i class="fa-solid fa-user-plus"></i>
                        <span>زیادکردنی کەسەکان</span>
                        <span id="badge-beneficiaries-count" class="bg-white/90 text-slate-800 text-xs px-2 py-0.5 rounded-full font-extrabold">0</span>
                    </button>
                    <button onclick="switchTab('warehouse')" id="tab-btn-warehouse" class="tab-btn flex items-center gap-2 px-4 py-2.5 rounded-xl font-bold text-sm transition whitespace-nowrap bg-slate-100 text-slate-600 hover:bg-slate-200">
                        <i class="fa-solid fa-warehouse"></i>
                        <span>کۆگا و زیادکردنی خۆراک</span>
                    </button>
                    <button onclick="switchTab('monitoring')" id="tab-btn-monitoring" class="tab-btn flex items-center gap-2 px-4 py-2.5 rounded-xl font-bold text-sm transition whitespace-nowrap bg-slate-100 text-slate-600 hover:bg-slate-200">
                        <i class="fa-solid fa-clipboard-list"></i>
                        <span>تۆمار</span>
                        <span id="badge-monitoring-count" class="bg-red-100 text-red-700 text-xs px-2 py-0.5 rounded-full font-extrabold">0</span>
                    </button>
                    <button onclick="switchTab('archive')" id="tab-btn-archive" class="tab-btn flex items-center gap-2 px-4 py-2.5 rounded-xl font-bold text-sm transition whitespace-nowrap bg-slate-100 text-slate-600 hover:bg-slate-200">
                        <i class="fa-solid fa-folder-open"></i>
                        <span>ئەرشیفی سەبەتەکان</span>
                        <span id="badge-archive-count" class="bg-wheat-200 text-wheat-900 text-xs px-2 py-0.5 rounded-full font-extrabold">0</span>
                    </button>
                </nav>
            </div>
        </header>

        <!-- MAIN CONTENT AREA -->
        <main class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6">

            <!-- =============================================================== -->
            <!-- TAB 1: DISTRIBUTION (بەشی دابەشکردنی خۆراک) -->
            <!-- =============================================================== -->
            <section id="tab-distribution" class="tab-content space-y-6">
                <!-- Lock Screen when NO Monthly File is active (هیچ دابەشکردنێک ناکرێت تاکو نەچیتە سەر فایلی مانگانە) -->
                <div id="monthly-file-locked-box" class="bg-white rounded-3xl border-2 border-dashed border-wheat-300 shadow-sm p-8 sm:p-12 text-center max-w-2xl mx-auto">
                    <div class="w-16 h-16 mx-auto rounded-2xl bg-wheat-100 text-wheat-700 flex items-center justify-center text-3xl mb-4">
                        <i class="fa-solid fa-folder-closed"></i>
                    </div>
                    <h2 class="text-xl font-extrabold text-slate-800 mb-2">پەڕەی سەرەکی قفڵە — فایلی مانگانە نەکراوەتەوە</h2>
                    <p class="text-sm text-slate-500 mb-6 leading-relaxed">
                        بۆ ئەوەی بتوانیت دابەشکردنی خۆراک ئەنجام بدەیت، سەرەتا ناوی فایلی مانگانە بنووسە و بچۆرە ناوی. تاکو هەموو کەسەکان تەواو نەبن لە ناو ئەو مانگەدا دەمێنیتەوە و هەموو دابەشکردنەکان دەچنە ناوی.
                    </p>
                    <div class="flex flex-col sm:flex-row items-center justify-center gap-3 max-w-md mx-auto">
                        <input type="text" id="start-monthly-file-input" placeholder="ناوی فایلی مانگانە بنووسە (نموونە: مانگی ١١ - ٢٠٢٦)"
                            class="w-full px-4 py-3 rounded-xl border border-slate-300 focus:border-emerald-500 focus:ring-2 focus:ring-emerald-200 outline-none text-sm font-bold">
                        <button type="button" onclick="openMonthlyFileFromBox()" class="w-full sm:w-auto px-6 py-3 rounded-xl bg-emerald-700 hover:bg-emerald-800 text-white font-extrabold text-sm shadow-md transition whitespace-nowrap flex items-center justify-center gap-2">
                            <i class="fa-solid fa-arrow-left"></i>
                            <span>چوونە سەر فایلی مانگانە</span>
                        </button>
                    </div>
                </div>

                <!-- Active Monthly File Workspace (دەردەکەوێت کاتێک لە ناو فایلی مانگانەدایت) -->
                <div id="monthly-file-active-workspace" class="hidden space-y-6">
                    <!-- Active Monthly File Status Header -->
                    <div class="bg-gradient-to-l from-slate-800 via-emerald-950 to-slate-900 text-white p-4 sm:p-5 rounded-2xl shadow-md flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                        <div class="flex items-center gap-3.5">
                            <div class="w-12 h-12 rounded-2xl bg-wheat-500/20 border border-wheat-400/40 text-wheat-300 flex items-center justify-center text-2xl shrink-0">
                                <i class="fa-solid fa-folder-open"></i>
                            </div>
                            <div>
                                <div class="flex items-center gap-2">
                                    <span class="text-[11px] font-bold bg-emerald-500/20 text-emerald-300 border border-emerald-400/30 px-2.5 py-0.5 rounded-full">فایلی مانگانەی چالاک</span>
                                    <span id="monthly-progress-badge" class="text-[11px] font-bold bg-wheat-500/20 text-wheat-200 px-2.5 py-0.5 rounded-full">0 / 0 خێزان تەواوبوون</span>
                                </div>
                                <h2 id="active-monthly-file-title" class="text-lg sm:text-xl font-extrabold mt-1 text-white">مانگی ١١</h2>
                            </div>
                        </div>
                        <button type="button" onclick="finishCurrentBasketToArchive()" class="px-5 py-3 rounded-xl bg-wheat-500 hover:bg-wheat-600 text-slate-950 font-extrabold text-sm shadow-lg transition flex items-center justify-center gap-2 whitespace-nowrap">
                            <i class="fa-solid fa-flag-checkered"></i>
                            <span>هەموو ئەم سەبەتە کۆتایی هات</span>
                        </button>
                    </div>

                    <!-- Auto-Completion Banner (دەردەکەوێت کاتێک هەموو کەسەکان بەشە خۆراکەکانیان وەرگرتبێت) -->
                    <div id="all-completed-banner" class="hidden bg-gradient-to-l from-emerald-800 via-emerald-700 to-teal-700 text-white p-5 rounded-2xl shadow-lg border border-emerald-500 flex flex-col sm:flex-row items-center justify-between gap-4">
                        <div class="flex items-center gap-3.5">
                            <div class="w-12 h-12 rounded-2xl bg-white/15 flex items-center justify-center text-2xl shrink-0">
                                <i class="fa-solid fa-circle-check text-amber-300"></i>
                            </div>
                            <div>
                                <h3 class="text-base sm:text-lg font-extrabold">هەموو خێزانەکانی ناو ئەم مانگە بەشە خۆراکەکانیان وەرگرت!</h3>
                                <p class="text-xs text-emerald-100 mt-0.5">دوگمەی «هەموو ئەم سەبەتە کۆتایی هات» دابگرە بۆ ناردنی تەواوی فایلەکە بۆ ئەرشیف.</p>
                            </div>
                        </div>
                        <button type="button" onclick="finishCurrentBasketToArchive()" class="px-5 py-3 rounded-xl bg-amber-400 hover:bg-amber-300 text-slate-900 font-extrabold text-sm shadow-md transition flex items-center gap-2 whitespace-nowrap shrink-0">
                            <i class="fa-solid fa-box-archive"></i>
                            <span>هەموو ئەم سەبەتە کۆتایی هات</span>
                        </button>
                    </div>

                    <!-- Search & Distribution Form Grid -->
                    <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                        <!-- Left/Right Column: Search Beneficiaries -->
                        <div class="lg:col-span-5 bg-white rounded-2xl border border-slate-200 shadow-sm p-5">
                            <h2 class="text-base font-extrabold text-slate-800 flex items-center gap-2 mb-3">
                                <i class="fa-solid fa-magnifying-glass text-emerald-600"></i>
                                <span>گەڕان بۆ خێزانە زیادکراوەکان</span>
                            </h2>
                            <input type="text" id="dist-search-input" oninput="renderDistBeneficiarySearch()" placeholder="ناو یان ژمارە مۆبایل بنووسە..."
                                class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 focus:border-emerald-500 outline-none text-sm mb-3">
                            <div id="dist-search-results" class="space-y-2 max-h-96 overflow-y-auto pr-1">
                                <!-- Populated by JS -->
                            </div>
                        </div>

                        <!-- Distribution Form Card -->
                        <div class="lg:col-span-7 bg-white rounded-2xl border border-slate-200 shadow-sm p-5">
                            <div id="no-beneficiary-selected" class="bg-slate-50 border border-dashed border-slate-300 rounded-2xl p-6 text-center mb-4">
                                <i class="fa-solid fa-hand-pointer text-2xl text-slate-400 mb-2"></i>
                                <p class="text-sm font-bold text-slate-600">سەرەتا خێزانێک لە لیستی گەڕانەکە هەڵبژێرە</p>
                                <p class="text-xs text-slate-400 mt-1">بڕی خۆراک و پارەکە (٢٠٠٠ دینار بۆ هەر نەفەرێک) بە شێوەیەکی خۆکار هەژمار دەکرێت</p>
                            </div>

                            <div id="beneficiary-selected-details" class="hidden bg-emerald-50/70 border border-emerald-200 rounded-2xl p-4 mb-4">
                                <div class="flex flex-wrap items-center justify-between gap-2">
                                    <div>
                                        <span class="text-xs font-bold text-emerald-700 block">خێزانی هەڵبژێردراو:</span>
                                        <h3 id="sel-ben-name" class="text-lg font-extrabold text-slate-800">-</h3>
                                        <span class="text-xs text-slate-500">مۆبایل: <strong id="sel-ben-phone" dir="ltr">-</strong></span>
                                    </div>
                                    <div class="flex items-center gap-3">
                                        <div class="bg-white px-3.5 py-2 rounded-xl border border-wheat-200 text-center">
                                            <span class="text-[11px] text-slate-500 block">ژمارەی نەفەر</span>
                                            <strong id="sel-ben-members" class="text-base font-black text-wheat-700">0</strong>
                                        </div>
                                        <div class="bg-white px-3.5 py-2 rounded-xl border border-emerald-200 text-center">
                                            <span class="text-[11px] text-slate-500 block">کۆی پارە</span>
                                            <strong class="text-base font-black text-emerald-700"><span id="sel-ben-total-fee">0</span> د.ع</strong>
                                        </div>
                                    </div>
                                </div>
                            </div>

                            <!-- Food Selection Header -->
                            <div class="flex items-center justify-between mb-3">
                                <h3 class="text-sm font-extrabold text-slate-700">هەڵبژاردنی بەشە خۆراکەکان:</h3>
                                <div class="flex gap-2">
                                    <button type="button" onclick="toggleAllFoodCheckboxes(true)" class="text-xs font-bold text-emerald-700 hover:underline">هەمووی دیاری بکە</button>
                                    <span class="text-slate-300">|</span>
                                    <button type="button" onclick="toggleAllFoodCheckboxes(false)" class="text-xs font-bold text-slate-500 hover:underline">لابردنی هەمووی</button>
                                </div>
                            </div>

                            <!-- Food Items Checkboxes -->
                            <div id="dist-food-items-grid" class="grid grid-cols-1 sm:grid-cols-2 gap-2.5 mb-4">
                                <!-- Populated by JS -->
                            </div>

                            <!-- Note Input -->
                            <div class="mb-4">
                                <label class="block text-xs font-bold text-slate-700 mb-1">تێبینی (دەچێتە بەشی تۆمار بۆ ئەم کەسە):</label>
                                <input type="text" id="dist-note-input" placeholder="تێبینی بنووسە ئەگەر هەبێت..."
                                    class="w-full px-3.5 py-2 rounded-xl border border-slate-300 focus:border-emerald-500 outline-none text-sm">
                            </div>

                            <!-- Action Buttons: حساب وصل & باقی حساب -->
                            <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 pt-2 border-t border-slate-100">
                                <button type="button" onclick="submitDistribution('paid')" class="py-3.5 px-4 rounded-xl bg-emerald-700 hover:bg-emerald-800 text-white font-extrabold text-sm shadow-md transition flex items-center justify-center gap-2">
                                    <i class="fa-solid fa-circle-check text-base"></i>
                                    <span>حساب وصل (تۆمارکردن)</span>
                                </button>
                                <button type="button" onclick="submitDistribution('unpaid')" class="py-3.5 px-4 rounded-xl bg-amber-500 hover:bg-amber-600 text-white font-extrabold text-sm shadow-md transition flex items-center justify-center gap-2">
                                    <i class="fa-solid fa-clock text-base"></i>
                                    <span>باقی حساب (تۆمارکردن)</span>
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- =============================================================== -->
            <!-- TAB 2: BENEFICIARIES (بەشی زیادکردنی کەسەکان) -->
            <!-- =============================================================== -->
            <section id="tab-beneficiaries" class="tab-content hidden space-y-6">
                <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                    <!-- Add Beneficiary Form -->
                    <div class="lg:col-span-4 bg-white p-5 rounded-2xl border border-slate-200 shadow-sm h-fit">
                        <h2 class="text-base font-extrabold text-slate-800 flex items-center gap-2 mb-4">
                            <i class="fa-solid fa-user-plus text-emerald-600"></i>
                            <span>زیادکردنی خێزان / کەسی نوێ</span>
                        </h2>
                        <form id="add-beneficiary-form" class="space-y-3.5">
                            <div>
                                <label class="block text-xs font-bold text-slate-700 mb-1">ناوی تەواوی سەرۆک خێزان:</label>
                                <input type="text" id="ben-name-input" placeholder="نموونە: ئەحمەد محەمەد قادر" required
                                    class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 focus:border-emerald-500 outline-none text-sm">
                            </div>
                            <div>
                                <label class="block text-xs font-bold text-slate-700 mb-1">ژمارەی ئەندامانی خێزان (نەفەر):</label>
                                <input type="number" id="ben-members-input" value="4" min="1" required
                                    class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 focus:border-emerald-500 outline-none text-sm font-bold">
                            </div>
                            <div>
                                <label class="block text-xs font-bold text-slate-700 mb-1">ژمارە مۆبایل:</label>
                                <input type="text" id="ben-phone-input" placeholder="0750XXXXXXX" dir="ltr"
                                    class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 focus:border-emerald-500 outline-none text-sm font-mono text-right">
                            </div>
                            <button type="submit" class="w-full py-3 rounded-xl bg-emerald-700 hover:bg-emerald-800 text-white font-extrabold text-sm shadow-sm transition flex items-center justify-center gap-2">
                                <i class="fa-solid fa-plus"></i>
                                <span>زیادکردن بۆ لیست</span>
                            </button>
                        </form>
                    </div>

                    <!-- Beneficiaries List Table -->
                    <div class="lg:col-span-8 bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden">
                        <div class="p-4 sm:p-5 border-b border-slate-100 flex flex-col sm:flex-row sm:items-center justify-between gap-3">
                            <div>
                                <h3 class="text-base font-extrabold text-slate-800">لیستی کەسە تۆمارکراوەکان</h3>
                                <div class="flex items-center gap-2 mt-1">
                                    <div class="w-32 bg-slate-100 rounded-full h-2 overflow-hidden">
                                        <div id="ben-progress-bar" class="bg-emerald-600 h-2 rounded-full" style="width: 0%"></div>
                                    </div>
                                    <span id="ben-progress-text" class="text-xs font-bold text-slate-500">0 / 1,705</span>
                                </div>
                            </div>
                            <input type="text" id="ben-search-input" oninput="renderBeneficiariesTable()" placeholder="گەڕان بە ناو یان مۆبایل..."
                                class="px-3.5 py-2 rounded-xl border border-slate-300 text-sm outline-none focus:border-emerald-500">
                        </div>
                        <div class="overflow-x-auto">
                            <table class="w-full text-right border-collapse">
                                <thead>
                                    <tr class="bg-slate-50 text-slate-600 text-xs font-bold border-b border-slate-200">
                                        <th class="py-3 px-4">#</th>
                                        <th class="py-3 px-4">ناوی سەرۆک خێزان</th>
                                        <th class="py-3 px-4 text-center">ژمارەی نەفەر</th>
                                        <th class="py-3 px-4">ژمارە مۆبایل</th>
                                        <th class="py-3 px-4 text-center">بڕی پارە</th>
                                        <th class="py-3 px-4 text-center">کردار</th>
                                    </tr>
                                </thead>
                                <tbody id="beneficiaries-table-body" class="divide-y divide-slate-100 text-sm">
                                    <!-- Populated by JS -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </section>

            <!-- =============================================================== -->
            <!-- TAB 3: WAREHOUSE (بەشی کۆگا و زیادکردنی خۆراک) -->
            <!-- =============================================================== -->
            <section id="tab-warehouse" class="tab-content hidden space-y-6">
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex flex-col lg:flex-row lg:items-center justify-between gap-4">
                    <div>
                        <h2 class="text-lg font-extrabold text-slate-800 flex items-center gap-2">
                            <i class="fa-solid fa-warehouse text-wheat-600"></i>
                            <span>بەڕێوەبردنی کۆگا و پشکی خۆراک</span>
                        </h2>
                        <p class="text-xs text-slate-500 mt-1">بڕی خۆراکی بەردەست لە کۆگا زیاد بکە یان پشکی هەر نەفەرێک چاک بکە.</p>
                    </div>
                    <div class="flex flex-wrap items-center gap-2">
                        <form id="add-stock-form" class="flex flex-wrap items-center gap-2">
                            <select id="stock-food-select" class="px-3.5 py-2 rounded-xl border border-slate-300 text-sm font-bold text-slate-700 outline-none focus:border-emerald-500 bg-slate-50">
                                <!-- Populated by JS -->
                            </select>
                            <input type="number" step="0.5" id="stock-amount-input" placeholder="بڕی زیادکراو..." required
                                class="w-36 px-3.5 py-2 rounded-xl border border-slate-300 text-sm outline-none focus:border-emerald-500">
                            <button type="submit" class="px-4 py-2 rounded-xl bg-emerald-700 hover:bg-emerald-800 text-white font-bold text-sm transition flex items-center gap-1.5">
                                <i class="fa-solid fa-plus"></i>
                                <span>زیادکردن بۆ کۆگا</span>
                            </button>
                        </form>
                        <button type="button" onclick="openEditRationModal()" class="px-4 py-2 rounded-xl bg-wheat-100 hover:bg-wheat-200 text-wheat-900 font-bold text-sm transition flex items-center gap-1.5">
                            <i class="fa-solid fa-sliders"></i>
                            <span>چاککردنی پشکی گشتی</span>
                        </button>
                    </div>
                </div>

                <!-- Warehouse Food Cards Grid -->
                <div id="warehouse-cards-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                    <!-- Populated by JS -->
                </div>
            </section>

            <!-- =============================================================== -->
            <!-- TAB 4: MONITORING (بەشی تۆماری بەشە خۆراکە وەرنەگیراوەکان) -->
            <!-- =============================================================== -->
            <section id="tab-monitoring" class="tab-content hidden space-y-6">
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <h2 class="text-lg font-extrabold text-slate-800 flex items-center gap-2">
                            <i class="fa-solid fa-clipboard-list text-red-600"></i>
                            <span>لیستی تۆماری بەشە خۆراکە وەرگیراو و وەرنەگیراوەکان</span>
                        </h2>
                        <p class="text-xs text-slate-500 mt-1">لێرەدا هەموو خێزانەکان، حسابەکانیان، بەرواری وەرگرتن و تێبینییەکان بە ڕوونی پیشان دەدرێن.</p>
                    </div>
                    <div class="flex flex-wrap items-center gap-2">
                        <select id="monitoring-status-filter" onchange="renderMonitoringTable()" class="px-3.5 py-2 rounded-xl border border-slate-300 text-sm font-bold text-slate-700 outline-none focus:border-emerald-500 bg-slate-50">
                            <option value="all">هەموو خێزانەکان</option>
                            <option value="missing">ئەوانەی خۆراکیان ماوە وەریبگرن</option>
                            <option value="none_received">ئەوانەی هیچ خۆراکێکیان وەرنەگرتووە</option>
                            <option value="complete">ئەوانەی هەموو خۆراکەکانیان وەرگرتووە</option>
                        </select>
                        <input type="text" id="monitoring-search-input" oninput="renderMonitoringTable()" placeholder="گەڕان بە ناو یان مۆبایل..." 
                            class="px-3.5 py-2 rounded-xl border border-slate-300 text-sm outline-none focus:border-emerald-500">
                    </div>
                </div>

                <!-- Summary Stats Row -->
                <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                    <div class="bg-white p-4 rounded-2xl border border-slate-200 shadow-sm flex items-center justify-between">
                        <div>
                            <span class="text-xs font-bold text-slate-500 block">کۆی گشتی خێزانەکان</span>
                            <span id="mon-stat-total" class="text-2xl font-black text-slate-800 mt-1 block">0</span>
                        </div>
                        <div class="w-11 h-11 rounded-xl bg-slate-100 text-slate-600 flex items-center justify-center text-lg">
                            <i class="fa-solid fa-users"></i>
                        </div>
                    </div>
                    <div class="bg-white p-4 rounded-2xl border border-red-200 shadow-sm flex items-center justify-between">
                        <div>
                            <span class="text-xs font-bold text-red-600 block">خێزانە بەشە خۆراک ماوەکان</span>
                            <span id="mon-stat-missing" class="text-2xl font-black text-red-600 mt-1 block">0</span>
                        </div>
                        <div class="w-11 h-11 rounded-xl bg-red-50 text-red-600 flex items-center justify-center text-lg">
                            <i class="fa-solid fa-triangle-exclamation"></i>
                        </div>
                    </div>
                    <div class="bg-white p-4 rounded-2xl border border-emerald-200 shadow-sm flex items-center justify-between">
                        <div>
                            <span class="text-xs font-bold text-emerald-700 block">تەواوی خۆراکەکانیان وەرگرتووە</span>
                            <span id="mon-stat-complete" class="text-2xl font-black text-emerald-700 mt-1 block">0</span>
                        </div>
                        <div class="w-11 h-11 rounded-xl bg-emerald-50 text-emerald-700 flex items-center justify-center text-lg">
                            <i class="fa-solid fa-circle-check"></i>
                        </div>
                    </div>
                </div>

                <!-- Monitoring Table -->
                <div class="bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden">
                    <div class="overflow-x-auto">
                        <table class="w-full text-right border-collapse">
                            <thead>
                                <tr class="bg-slate-50 text-slate-600 text-xs font-bold border-b border-slate-200">
                                    <th class="py-3.5 px-4">#</th>
                                    <th class="py-3.5 px-4">ناوی سەرۆک خێزان</th>
                                    <th class="py-3.5 px-4 text-center">ژمارەی نەفەر</th>
                                    <th class="py-3.5 px-4">ژمارە مۆبایل</th>
                                    <th class="py-3.5 px-4">ئەو خۆراکانەی وەریگرتووە</th>
                                    <th class="py-3.5 px-4">ئەو بەشە خۆراکانەی وەرینەگرتووە (ماوە)</th>
                                    <th class="py-3.5 px-4 text-center">حساب</th>
                                    <th class="py-3.5 px-4 text-center">بەرواری وەرگرتن</th>
                                    <th class="py-3.5 px-4">تێبینی</th>
                                    <th class="py-3.5 px-4 text-center">کردار</th>
                                </tr>
                            </thead>
                            <tbody id="monitoring-table-body" class="divide-y divide-slate-100 text-sm">
                                <!-- Populated dynamically by JS -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- =============================================================== -->
            <!-- TAB 5: ARCHIVE (بەشی ئەرشیفی سەبەتە خۆراکەکان) -->
            <!-- =============================================================== -->
            <section id="tab-archive" class="tab-content hidden space-y-6">
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex flex-wrap items-center justify-between gap-4">
                    <div>
                        <h2 class="text-lg font-extrabold text-slate-800 flex items-center gap-2">
                            <i class="fa-solid fa-folder-tree text-wheat-600"></i>
                            <span>فایلەکانی ئەرشیف (مانگانە و پەڕە خەزنکراوەکان)</span>
                        </h2>
                        <p class="text-xs text-slate-500 mt-1">هەر پەڕە یان مانگێک کە تەواو دەبێت لێرە وەک فایلێکی سەربەخۆ خەزن دەبێت؛ دەتوانیت فایلی Excel یان HTML دابگریت یان بینێریت.</p>
                    </div>
                </div>

                <!-- Archive Cards Grid -->
                <div id="archive-list-container" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5">
                    <!-- Populated dynamically by JS -->
                </div>
            </section>

        </main>
    </div>

    <!-- ===================================================================== -->
    <!-- UNIVERSAL EDIT & VIEW MODALS (پەنجەرەی چاککردن بۆ هەموو بەشەکان) -->
    <!-- ===================================================================== -->
    
    <!-- Modal Container -->
    <div id="universal-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 hidden items-center justify-center p-4 overflow-y-auto">
        <div class="bg-white rounded-3xl max-w-2xl w-full p-6 shadow-2xl border border-slate-200 my-8">
            <div class="flex items-center justify-between pb-3 border-b border-slate-100 mb-4">
                <h3 id="modal-title" class="text-lg font-extrabold text-slate-800">چاککردنی زانیاری</h3>
                <button onclick="closeUniversalModal()" class="w-8 h-8 rounded-full bg-slate-100 hover:bg-slate-200 text-slate-600 flex items-center justify-center transition">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>
            <div id="modal-body" class="space-y-4">
                <!-- Dynamic Form Content -->
            </div>
        </div>
    </div>

    <!-- ===================================================================== -->
    <!-- JAVASCRIPT LOGIC -->
    <!-- ===================================================================== -->
    <script>
        // --- 1. INITIAL DATA & CONFIGURATION ---
        const STORAGE_KEY = 'kurdish_food_dist_system_v1';

        // Default Food Items & Ration per person
        // ئارد ٩ کگم، برینج ٣ کگم، شەکر ١ کگم، زەیت ١، معجون ١، نیسک ٠.٥ کگم، ئاری نۆک ٠.٥ کگم
        const DEFAULT_FOODS = [
            { id: 'flour', name: 'ئارد', unit: 'کگم', perPerson: 9, stock: 16000 },
            { id: 'rice', name: 'برینج', unit: 'کگم', perPerson: 3, stock: 5500 },
            { id: 'sugar', name: 'شەکر', unit: 'کگم', perPerson: 1, stock: 2000 },
            { id: 'oil', name: 'زەیت', unit: 'دانە', perPerson: 1, stock: 2000 },
            { id: 'paste', name: 'معجون', unit: 'دانە', perPerson: 1, stock: 2000 },
            { id: 'lentils', name: 'نیسک', unit: 'کگم', perPerson: 0.5, stock: 1000 },
            { id: 'chickpea_flour', name: 'ئاری نۆک', unit: 'کگم', perPerson: 0.5, stock: 1000 }
        ];

        // Sample Beneficiaries so the user can test immediately
        const SAMPLE_BENEFICIARIES = [
            { id: 'b1', name: 'ئەحمەد محەمەد قادر', members: 5, phone: '07504412233' },
            { id: 'b2', name: 'کاروان عەلی حەسەن', members: 4, phone: '07701234567' },
            { id: 'b3', name: 'شێرزاد عومەر سەعید', members: 6, phone: '07507894561' },
            { id: 'b4', name: 'هێمن جەلال مستەفا', members: 3, phone: '07512349876' },
            { id: 'b5', name: 'سەلام کەریم ڕەشید', members: 7, phone: '07719988776' }
        ];

        let appState = {
            password: '009988',
            targetPeople: 1705,
            feePerPerson: 2000,
            currentSheetName: '',
            isMonthlyFileOpen: false,
            foods: JSON.parse(JSON.stringify(DEFAULT_FOODS)),
            beneficiaries: [...SAMPLE_BENEFICIARIES],
            distributions: [], // Active sheet distributions
            archives: []       // Archived pages
        };

        let selectedBeneficiaryId = null;
        let currentReportFilter = 'all';

        // --- 2. HELPER FUNCTIONS ---
        
        // Convert Kurdish/Arabic numerals (٠١٢٣٤٥٦٧٨٩) to English (0123456789)
        function normalizeDigits(str) {
            if (!str) return '';
            const arabicNumbers = ['٠', '١', '٢', '٣', '٤', '٥', '٦', '٧', '٨', '٩'];
            const persianNumbers = ['۰', '۱', '۲', '۳', '۴', '۵', '۶', '۷', '۸', '۹'];
            let res = str.toString();
            for (let i = 0; i < 10; i++) {
                res = res.replace(new RegExp(arabicNumbers[i], 'g'), i)
                         .replace(new RegExp(persianNumbers[i], 'g'), i);
            }
            return res;
        }

        function formatNumber(num) {
            return Number(num || 0).toLocaleString('en-US');
        }

        function loadState() {
            try {
                const saved = localStorage.getItem(STORAGE_KEY);
                if (saved) {
                    const parsed = JSON.parse(saved);
                    appState = { ...appState, ...parsed };
                }
            } catch (e) {
                console.error('Error loading state:', e);
            }
        }

        function saveState() {
            try {
                localStorage.setItem(STORAGE_KEY, JSON.stringify(appState));
                updateAllUI();
            } catch (e) {
                showToast('هەڵەیەک ڕوویدا لە پاشەکەوتکردنی داتاکان', 'error');
            }
        }

        // Custom Toast Notification (No alert())
        function showToast(message, type = 'success') {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            
            const colors = {
                success: 'bg-emerald-800 text-white border-emerald-600',
                error: 'bg-red-700 text-white border-red-500',
                warning: 'bg-amber-600 text-white border-amber-400',
                info: 'bg-slate-800 text-white border-slate-600'
            };
            const icons = {
                success: 'fa-circle-check',
                error: 'fa-circle-exclamation',
                warning: 'fa-triangle-exclamation',
                info: 'fa-circle-info'
            };

            toast.className = `pointer-events-auto flex items-center gap-3 px-4 py-3 rounded-2xl shadow-xl border ${colors[type]} transform transition-all duration-300 translate-y-2 opacity-0`;
            toast.innerHTML = `
                <i class="fa-solid ${icons[type]} text-lg"></i>
                <span class="text-sm font-bold flex-1">${message}</span>
            `;
            container.appendChild(toast);

            requestAnimationFrame(() => {
                toast.classList.remove('translate-y-2', 'opacity-0');
            });

            setTimeout(() => {
                toast.classList.add('opacity-0', 'translate-y-2');
                setTimeout(() => toast.remove(), 300);
            }, 3500);
        }

        // Custom Confirm Dialog (No confirm())
        function showConfirm(title, message, onConfirm) {
            const modal = document.getElementById('confirm-modal');
            document.getElementById('confirm-title').textContent = title;
            document.getElementById('confirm-message').textContent = message;
            
            const okBtn = document.getElementById('confirm-ok-btn');
            const cancelBtn = document.getElementById('confirm-cancel-btn');

            const cleanup = () => {
                modal.classList.add('hidden');
                modal.classList.remove('flex');
                okBtn.onclick = null;
                cancelBtn.onclick = null;
            };

            cancelBtn.onclick = cleanup;
            okBtn.onclick = () => {
                cleanup();
                onConfirm();
            };

            modal.classList.remove('hidden');
            modal.classList.add('flex');
        }

        // --- 3. AUTHENTICATION & PASSWORD MANAGEMENT ---
        function togglePasswordVisibility(inputId, btn) {
            const input = document.getElementById(inputId);
            const icon = btn.querySelector('i');
            if (input.type === 'password') {
                input.type = 'text';
                icon.classList.replace('fa-eye', 'fa-eye-slash');
            } else {
                input.type = 'password';
                icon.classList.replace('fa-eye-slash', 'fa-eye');
            }
        }

        function toggleChangePasswordBox() {
            const form = document.getElementById('change-password-form');
            const chevron = document.getElementById('change-pass-chevron');
            form.classList.toggle('hidden');
            chevron.classList.toggle('rotate-180');
        }

        document.getElementById('login-form').addEventListener('submit', function(e) {
            e.preventDefault();
            const entered = normalizeDigits(document.getElementById('login-password').value.trim());
            if (entered === appState.password) {
                document.getElementById('login-screen').classList.add('hidden');
                document.getElementById('main-app').classList.remove('hidden');
                document.getElementById('login-password').value = '';
                updateAllUI();
                showToast('بەخێربێیت بۆ سیستەمی دابەشکردنی خۆراک', 'success');
            } else {
                showToast('پاسۆردەکە هەڵەیە! تکایە دووبارە هەوڵبدەرەوە', 'error');
            }
        });

        document.getElementById('change-password-form').addEventListener('submit', function(e) {
            e.preventDefault();
            const oldPass = normalizeDigits(document.getElementById('old-password').value.trim());
            const newPass = normalizeDigits(document.getElementById('new-password').value.trim());
            const confirmPass = normalizeDigits(document.getElementById('confirm-new-password').value.trim());

            if (oldPass !== appState.password) {
                showToast('پاسۆردی کۆن هەڵەیە!', 'error');
                return;
            }
            if (newPass.length < 4) {
                showToast('پاسۆردی نوێ دەبێت لانیکەم ٤ پیت یان ژمارە بێت', 'warning');
                return;
            }
            if (newPass !== confirmPass) {
                showToast('پاسۆردی نوێ و دڵنیاکردنەوەکە وەک یەک نین!', 'error');
                return;
            }

            appState.password = newPass;
            saveState();
            this.reset();
            toggleChangePasswordBox();
            showToast('پاسۆرد بە سەرکەوتوویی گۆڕدرا!', 'success');
        });

        function logout() {
            document.getElementById('main-app').classList.add('hidden');
            document.getElementById('login-screen').classList.remove('hidden');
            showToast('سیستەم قفڵکرا', 'info');
        }

        // --- 4. TAB NAVIGATION ---
        function switchTab(tabName) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('bg-emerald-700', 'text-white', 'shadow-sm');
                btn.classList.add('bg-slate-100', 'text-slate-600');
            });

            document.getElementById(`tab-${tabName}`).classList.remove('hidden');
            const activeBtn = document.getElementById(`tab-btn-${tabName}`);
            activeBtn.classList.remove('bg-slate-100', 'text-slate-600');
            activeBtn.classList.add('bg-emerald-700', 'text-white', 'shadow-sm');

            updateAllUI();
        }

        // --- 5. BENEFICIARIES MANAGEMENT (زیادکردنی کەسەکان) ---
        const addBeneficiaryForm = document.getElementById('add-beneficiary-form');
        if (addBeneficiaryForm) {
            addBeneficiaryForm.addEventListener('submit', function(e) {
                e.preventDefault();
                const name = document.getElementById('ben-name-input').value.trim();
                const members = parseInt(normalizeDigits(document.getElementById('ben-members-input').value), 10);
                const phone = normalizeDigits(document.getElementById('ben-phone-input').value.trim());

                if (!name || isNaN(members) || members < 1) {
                    showToast('تکایە ناو و ژمارەی ئەندامانی خێزان بە دروستی بنووسە', 'error');
                    return;
                }

                const newBen = {
                    id: 'ben_' + Date.now(),
                    name,
                    members,
                    phone
                };

                appState.beneficiaries.unshift(newBen);
                saveState();
                this.reset();
                document.getElementById('ben-members-input').value = 4;
                showToast(`خێزانی "${name}" بە سەرکەوتوویی زیادکرا`, 'success');
            });
        }

        function renderBeneficiariesTable() {
            const tbody = document.getElementById('beneficiaries-table-body');
            if (!tbody) return;
            const searchInput = document.getElementById('ben-search-input');
            const query = searchInput ? searchInput.value.trim().toLowerCase() : '';

            const filtered = appState.beneficiaries.filter(b =>
                b.name.toLowerCase().includes(query) || normalizeDigits(b.phone).includes(normalizeDigits(query))
            );

            // Update Progress Bar towards 1,705
            const totalMembers = appState.beneficiaries.reduce((sum, b) => sum + Number(b.members), 0);
            const pct = Math.min(100, Math.round((totalMembers / appState.targetPeople) * 100));
            document.getElementById('ben-progress-text').textContent = `${formatNumber(totalMembers)} / ${formatNumber(appState.targetPeople)}`;
            document.getElementById('ben-progress-bar').style.width = `${pct}%`;

            if (filtered.length === 0) {
                tbody.innerHTML = `<tr><td colspan="6" class="py-8 text-center text-slate-400">هیچ کەسێک نەدۆزرایەوە</td></tr>`;
                return;
            }

            tbody.innerHTML = filtered.map((b, idx) => {
                const fee = b.members * appState.feePerPerson;
                return `
                    <tr class="hover:bg-slate-50 transition">
                        <td class="py-3 px-4 font-bold text-slate-400">${idx + 1}</td>
                        <td class="py-3 px-4 font-bold text-slate-800">${b.name}</td>
                        <td class="py-3 px-4 text-center">
                            <span class="bg-wheat-100 text-wheat-800 font-extrabold px-2.5 py-1 rounded-lg text-xs">${b.members} نەفەر</span>
                        </td>
                        <td class="py-3 px-4 font-mono text-slate-600" dir="ltr">${b.phone || '-'}</td>
                        <td class="py-3 px-4 text-center font-bold text-emerald-700">${formatNumber(fee)} د.ع</td>
                        <td class="py-3 px-4 text-center">
                            <div class="flex items-center justify-center gap-1.5">
                                <button onclick="openEditBeneficiaryModal('${b.id}')" class="px-2.5 py-1.5 rounded-lg bg-sky-50 hover:bg-sky-100 text-sky-700 font-bold text-xs transition flex items-center gap-1" title="چاککردن">
                                    <i class="fa-solid fa-pen-to-square"></i> چاککردن
                                </button>
                                <button onclick="deleteBeneficiary('${b.id}')" class="p-1.5 rounded-lg bg-red-50 hover:bg-red-100 text-red-600 transition" title="سڕینەوە">
                                    <i class="fa-solid fa-trash-can"></i>
                                </button>
                            </div>
                        </td>
                    </tr>
                `;
            }).join('');
        }

        function openEditBeneficiaryModal(id) {
            const ben = appState.beneficiaries.find(b => b.id === id);
            if (!ben) return;

            document.getElementById('modal-title').textContent = 'چاککردنی زانیاری کەس / خێزان';
            document.getElementById('modal-body').innerHTML = `
                <form id="edit-ben-form" class="space-y-4">
                    <div>
                        <label class="block text-xs font-bold text-slate-700 mb-1">ناوی تەواو:</label>
                        <input type="text" id="edit-ben-name" value="${ben.name}" required class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 outline-none focus:border-emerald-500 text-sm">
                    </div>
                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="block text-xs font-bold text-slate-700 mb-1">ژمارەی ئەندامان (نەفەر):</label>
                            <input type="number" id="edit-ben-members" value="${ben.members}" min="1" required class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 outline-none focus:border-emerald-500 text-sm font-bold">
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-700 mb-1">ژمارە مۆبایل:</label>
                            <input type="text" id="edit-ben-phone" value="${ben.phone}" dir="ltr" class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 outline-none focus:border-emerald-500 text-sm font-mono text-right">
                        </div>
                    </div>
                    <div class="flex justify-end gap-2 pt-3 border-t border-slate-100">
                        <button type="button" onclick="closeUniversalModal()" class="px-4 py-2 rounded-xl bg-slate-100 text-slate-700 font-bold text-sm">پاشگەزبوونەوە</button>
                        <button type="submit" class="px-5 py-2 rounded-xl bg-emerald-700 text-white font-bold text-sm">پاشەکەوتکردنی گۆڕانکاری</button>
                    </div>
                </form>
            `;

            document.getElementById('edit-ben-form').onsubmit = function(e) {
                e.preventDefault();
                ben.name = document.getElementById('edit-ben-name').value.trim();
                ben.members = parseInt(normalizeDigits(document.getElementById('edit-ben-members').value), 10) || 1;
                ben.phone = normalizeDigits(document.getElementById('edit-ben-phone').value.trim());
                saveState();
                closeUniversalModal();
                showToast('زانیارییەکە بە سەرکەوتوویی چاککرا', 'success');
            };

            openUniversalModal();
        }

        function deleteBeneficiary(id) {
            showConfirm('سڕینەوەی خێزان', 'ئایا دڵنیایت لە سڕینەوەی ئەم خێزانە لە لیستی تۆمارکراوەکان؟', () => {
                appState.beneficiaries = appState.beneficiaries.filter(b => b.id !== id);
                if (selectedBeneficiaryId === id) selectedBeneficiaryId = null;
                saveState();
                showToast('خێزانەکە سڕایەوە', 'info');
            });
        }

        // --- 6. DISTRIBUTION LOGIC (بەشی دابەشکردنی خۆراک) ---
        function renderDistBeneficiarySearch() {
            const container = document.getElementById('dist-search-results');
            const query = document.getElementById('dist-search-input').value.trim().toLowerCase();

            const filtered = appState.beneficiaries.filter(b => 
                b.name.toLowerCase().includes(query) || normalizeDigits(b.phone).includes(normalizeDigits(query))
            );

            if (filtered.length === 0) {
                container.innerHTML = `<div class="text-center py-6 text-slate-400 text-xs">هیچ ئەنجامێک نەدۆزرایەوە. لە بەشی "زیادکردنی کەسەکان" زیادی بکە.</div>`;
                return;
            }

            // Check who already received in current active sheet
            const receivedIds = new Set(appState.distributions.map(d => d.beneficiaryId));

            container.innerHTML = filtered.map(b => {
                const isSelected = b.id === selectedBeneficiaryId;
                const alreadyReceived = receivedIds.has(b.id);
                return `
                    <div onclick="selectBeneficiaryForDist('${b.id}')" 
                        class="p-3 rounded-xl border cursor-pointer transition flex items-center justify-between ${isSelected ? 'bg-emerald-50 border-emerald-500 ring-2 ring-emerald-200' : 'bg-slate-50/70 hover:bg-slate-100 border-slate-200'}">
                        <div>
                            <div class="flex items-center gap-2">
                                <span class="font-bold text-sm text-slate-800">${b.name}</span>
                                ${alreadyReceived ? '<span class="text-[10px] bg-green-100 text-green-800 px-2 py-0.5 rounded-full font-bold">وەرگرتووە</span>' : ''}
                            </div>
                            <span class="text-xs text-slate-500 font-mono" dir="ltr">${b.phone || 'بێ ژمارە'}</span>
                        </div>
                        <div class="text-left">
                            <span class="block text-xs font-extrabold text-wheat-700 bg-wheat-100 px-2.5 py-1 rounded-lg">${b.members} نەفەر</span>
                            <span class="block text-[11px] font-bold text-emerald-700 mt-0.5">${formatNumber(b.members * appState.feePerPerson)} د.ع</span>
                        </div>
                    </div>
                `;
            }).join('');
        }

        function selectBeneficiaryForDist(id) {
            selectedBeneficiaryId = id;
            renderDistBeneficiarySearch();
            renderSelectedBeneficiaryPanel();
        }

        function renderSelectedBeneficiaryPanel() {
            const noSel = document.getElementById('no-beneficiary-selected');
            const details = document.getElementById('beneficiary-selected-details');
            const foodGrid = document.getElementById('dist-food-items-grid');

            const ben = appState.beneficiaries.find(b => b.id === selectedBeneficiaryId);

            if (!ben) {
                noSel.classList.remove('hidden');
                details.classList.add('hidden');
                // Render default 1-person preview
                foodGrid.innerHTML = appState.foods.map(f => `
                    <label class="flex items-center justify-between p-2.5 rounded-xl border border-slate-200 bg-slate-50 opacity-70">
                        <div class="flex items-center gap-2">
                            <input type="checkbox" checked disabled class="w-4 h-4 accent-emerald-600 rounded">
                            <span class="font-bold text-sm text-slate-700">${f.name}</span>
                        </div>
                        <span class="text-xs font-bold text-slate-500">${f.perPerson} ${f.unit} / نەفەر</span>
                    </label>
                `).join('');
                return;
            }

            noSel.classList.add('hidden');
            details.classList.remove('hidden');

            document.getElementById('sel-ben-name').textContent = ben.name;
            document.getElementById('sel-ben-phone').textContent = ben.phone || 'نییە';
            document.getElementById('sel-ben-members').textContent = ben.members;
            document.getElementById('sel-ben-total-fee').textContent = formatNumber(ben.members * appState.feePerPerson);

            // Render interactive food checkboxes with calculated quantities
            foodGrid.innerHTML = appState.foods.map(f => {
                const totalQty = Number((f.perPerson * ben.members).toFixed(2));
                const lowStock = f.stock < totalQty;
                return `
                    <label class="flex items-center justify-between p-3 rounded-xl border ${lowStock ? 'border-red-300 bg-red-50/40' : 'border-slate-200 bg-white hover:border-emerald-400'} cursor-pointer transition shadow-xs">
                        <div class="flex items-center gap-2.5">
                            <input type="checkbox" name="dist-food-check" value="${f.id}" checked class="w-4 h-4 accent-emerald-600 rounded cursor-pointer">
                            <div>
                                <span class="font-bold text-sm text-slate-800 block">${f.name}</span>
                                <span class="text-[10px] text-slate-400">کۆگا: ${formatNumber(f.stock)} ${f.unit}</span>
                            </div>
                        </div>
                        <div class="text-left">
                            <span class="font-extrabold text-sm ${lowStock ? 'text-red-600' : 'text-emerald-700'}">${formatNumber(totalQty)} ${f.unit}</span>
                        </div>
                    </label>
                `;
            }).join('');
        }

        function toggleAllFoodCheckboxes(state) {
            document.querySelectorAll('input[name="dist-food-check"]').forEach(cb => cb.checked = state);
        }

        function submitDistribution(paymentStatus) {
            if (!appState.isMonthlyFileOpen || !appState.currentSheetName) {
                showToast('سەرەتا دەبێت بچیتە سەر فایلی مانگانە پێش دابەشکردن!', 'error');
                return;
            }

            const ben = appState.beneficiaries.find(b => b.id === selectedBeneficiaryId);
            if (!ben) {
                showToast('تکایە سەرەتا خێزانێک لە لیستی گەڕانەکە هەڵبژێرە!', 'warning');
                return;
            }

            const checkedBoxes = Array.from(document.querySelectorAll('input[name="dist-food-check"]:checked'));
            if (checkedBoxes.length === 0) {
                showToast('تکایە لانیکەم یەک جۆر خۆراک هەڵبژێرە!', 'warning');
                return;
            }

            const itemsGiven = [];
            for (const cb of checkedBoxes) {
                const food = appState.foods.find(f => f.id === cb.value);
                if (food) {
                    const qty = Number((food.perPerson * ben.members).toFixed(2));
                    itemsGiven.push({
                        foodId: food.id,
                        name: food.name,
                        unit: food.unit,
                        quantity: qty
                    });
                    // Deduct from warehouse stock
                    food.stock = Math.max(0, Number((food.stock - qty).toFixed(2)));
                }
            }

            const totalFee = ben.members * appState.feePerPerson;
            const note = document.getElementById('dist-note-input').value.trim();

            const record = {
                id: 'dist_' + Date.now(),
                beneficiaryId: ben.id,
                beneficiaryName: ben.name,
                phone: ben.phone,
                members: ben.members,
                items: itemsGiven,
                totalFee: totalFee,
                paymentStatus: paymentStatus, // 'paid' (حساب وصل) or 'unpaid' (باقی حساب)
                note: note,
                monthlyFileName: appState.currentSheetName,
                date: new Date().toLocaleDateString('en-CA') + ' ' + new Date().toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' })
            };

            appState.distributions.unshift(record);
            document.getElementById('dist-note-input').value = '';
            selectedBeneficiaryId = null;
            saveState();

            const statusLabel = paymentStatus === 'paid' ? 'حساب وصل' : 'باقی حساب';
            showToast(`دابەشکردن بۆ "${ben.name}" چووە ناو فایلی "${appState.currentSheetName}" (${statusLabel})`, 'success');
        }

        function openMonthlyFile() {
            const topInput = document.getElementById('archive-page-name-input');
            const boxInput = document.getElementById('start-monthly-file-input');
            const fileName = (topInput?.value || boxInput?.value || '').trim();

            if (!fileName) {
                showToast('تکایە سەرەتا ناوی فایلی مانگانە بنووسە (نموونە: مانگی ١١)!', 'warning');
                if (boxInput && !appState.isMonthlyFileOpen) boxInput.focus();
                else if (topInput) topInput.focus();
                return;
            }

            appState.currentSheetName = fileName;
            appState.isMonthlyFileOpen = true;
            if (topInput) topInput.value = '';
            if (boxInput) boxInput.value = '';
            saveState();
            switchTab('distribution');
            showToast(`چوویتە سەر فایلی مانگانەی "${fileName}" — ئێستا دەتوانیت دابەشکردن بکەیت`, 'success');
        }

        function openMonthlyFileFromBox() {
            const boxInput = document.getElementById('start-monthly-file-input');
            const fileName = (boxInput?.value || '').trim();
            if (!fileName) {
                showToast('تکایە ناوی فایلی مانگانە بنووسە!', 'warning');
                if (boxInput) boxInput.focus();
                return;
            }
            appState.currentSheetName = fileName;
            appState.isMonthlyFileOpen = true;
            boxInput.value = '';
            saveState();
            showToast(`فایلی مانگانەی "${fileName}" کرایەوە`, 'success');
        }

        function isAllBeneficiariesCompleted() {
            if (appState.beneficiaries.length === 0) return false;
            return appState.beneficiaries.every(ben => {
                const benDists = appState.distributions.filter(d => d.beneficiaryId === ben.id);
                const receivedFoodIds = new Set();
                benDists.forEach(d => d.items.forEach(item => receivedFoodIds.add(item.foodId)));
                return appState.foods.every(f => receivedFoodIds.has(f.id));
            });
        }

        function getCompletedBeneficiariesCount() {
            return appState.beneficiaries.filter(ben => {
                const benDists = appState.distributions.filter(d => d.beneficiaryId === ben.id);
                const receivedFoodIds = new Set();
                benDists.forEach(d => d.items.forEach(item => receivedFoodIds.add(item.foodId)));
                return appState.foods.every(f => receivedFoodIds.has(f.id));
            }).length;
        }

        function finishCurrentBasketToArchive() {
            if (!appState.isMonthlyFileOpen || !appState.currentSheetName) {
                showToast('هیچ فایلێکی مانگانەی چالاک نییە!', 'warning');
                return;
            }

            if (appState.distributions.length === 0) {
                showToast('هیچ دابەشکردنێک لە ناو ئەم فایلە مانگانەیەدا تۆمار نەکراوە!', 'warning');
                return;
            }

            const completedCount = getCompletedBeneficiariesCount();
            const totalCount = appState.beneficiaries.length;
            const warningText = completedCount < totalCount
                ? `ئاگاداری: هێشتا (${totalCount - completedCount}) خێزان لە کۆی (${totalCount}) خێزان تەواو نەبوون. ئایا دڵنیایت دەتەوێت کۆتایی بە سەبەتەی "${appState.currentSheetName}" بهێنیت و بینێریتە ناو ئەرشیف؟`
                : `هەموو (${totalCount}) خێزانەکە تەواو بوون. ئایا دڵنیایت دەتەوێت فایلی "${appState.currentSheetName}" بنێریتە ناو ئەرشیف و پەڕەی سەرەکی بۆ مانگی داهاتوو ئامادە بکەیتەوە؟`;

            showConfirm('هەموو ئەم سەبەتە کۆتایی هات', warningText, () => {
                performArchiveAndResetForNextMonth(appState.currentSheetName);
            });
        }

        function performArchiveAndResetForNextMonth(pageName) {
            const totalMembers = appState.distributions.reduce((s, d) => s + d.members, 0);
            const totalPaid = appState.distributions.filter(d => d.paymentStatus === 'paid').reduce((s, d) => s + d.totalFee, 0);
            const totalUnpaid = appState.distributions.filter(d => d.paymentStatus === 'unpaid').reduce((s, d) => s + d.totalFee, 0);

            const archiveEntry = {
                id: 'arch_' + Date.now(),
                name: pageName,
                fileName: `${pageName.replace(/\s+/g, '_')}_${new Date().toLocaleDateString('en-CA')}`,
                date: new Date().toLocaleDateString('en-CA') + ' ' + new Date().toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' }),
                familiesCount: appState.distributions.length,
                totalMembers,
                totalPaid,
                totalUnpaid,
                records: JSON.parse(JSON.stringify(appState.distributions))
            };

            appState.archives.unshift(archiveEntry);
            // Reset distributions and close current monthly file while KEEPING all beneficiaries intact
            appState.distributions = [];
            selectedBeneficiaryId = null;
            appState.currentSheetName = '';
            appState.isMonthlyFileOpen = false;
            const topInput = document.getElementById('archive-page-name-input');
            if (topInput) topInput.value = '';
            saveState();
            showToast(`فایلی "${pageName}" نێردرا بۆ ئەرشیف! بۆ مانگی داهاتوو ناوی فایلی نوێ بنووسە.`, 'success');
        }

        function renderDistributionsTable() {
            const tbody = document.getElementById('distributions-table-body');
            if (!tbody) return;
            const filterEl = document.getElementById('dist-table-filter');
            const filter = filterEl ? filterEl.value.trim().toLowerCase() : '';

            const filtered = appState.distributions.filter(d => 
                d.beneficiaryName.toLowerCase().includes(filter) || 
                normalizeDigits(d.phone).includes(normalizeDigits(filter))
            );

            if (filtered.length === 0) {
                tbody.innerHTML = `<tr><td colspan="7" class="py-8 text-center text-slate-400">هیچ تۆمارێک نییە</td></tr>`;
                return;
            }

            tbody.innerHTML = filtered.map((d, idx) => `
                <tr class="hover:bg-slate-50 transition">
                    <td class="py-3 px-4 font-bold text-slate-400">${idx + 1}</td>
                    <td class="py-3 px-4 font-bold text-slate-800">${d.beneficiaryName}</td>
                    <td class="py-3 px-4 text-center font-bold text-wheat-700">${d.members}</td>
                    <td class="py-3 px-4 text-xs text-slate-600">${d.items.map(i => `${i.name} (${i.quantity} ${i.unit})`).join('، ')}</td>
                    <td class="py-3 px-4 text-center font-bold text-emerald-700">${formatNumber(d.totalFee)} د.ع</td>
                    <td class="py-3 px-4 text-center">
                        <span class="px-2.5 py-1 rounded-full text-xs font-bold ${d.paymentStatus === 'paid' ? 'bg-emerald-100 text-emerald-800' : 'bg-amber-100 text-amber-800'}">
                            ${d.paymentStatus === 'paid' ? 'حساب وصل' : 'باقی حساب'}
                        </span>
                    </td>
                    <td class="py-3 px-4 text-center">
                        <button onclick="deleteDistribution('${d.id}')" class="p-1.5 rounded-lg bg-red-50 hover:bg-red-100 text-red-600 transition" title="سڕینەوە">
                            <i class="fa-solid fa-trash-can"></i>
                        </button>
                    </td>
                </tr>
            `).join('');
        }

        function deleteDistribution(id) {
            const dist = appState.distributions.find(d => d.id === id);
            if (!dist) return;
            showConfirm('سڕینەوەی تۆمار', 'ئایا دڵنیایت لە سڕینەوەی ئەم تۆمارە و گەڕاندنەوەی خۆراکەکان بۆ کۆگا؟', () => {
                dist.items.forEach(item => {
                    const food = appState.foods.find(f => f.id === item.foodId);
                    if (food) {
                        food.stock = Number((food.stock + item.quantity).toFixed(2));
                    }
                });
                appState.distributions = appState.distributions.filter(d => d.id !== id);
                saveState();
                showToast('تۆمارەکە سڕایەوە و خۆراکەکان گەڕانەوە کۆگا', 'info');
            });
        }

        // --- 7. WAREHOUSE MANAGEMENT (بەشی کۆگا) ---
        function renderWarehouse() {
            const grid = document.getElementById('warehouse-cards-grid');
            const select = document.getElementById('stock-food-select');
            if (!grid || !select) return;

            select.innerHTML = appState.foods.map(f => `<option value="${f.id}">${f.name} (${f.unit})</option>`).join('');

            grid.innerHTML = appState.foods.map(f => {
                const requiredTotal = Number((f.perPerson * appState.targetPeople).toFixed(2));
                const pct = requiredTotal > 0 ? Math.min(100, Math.round((f.stock / requiredTotal) * 100)) : 100;
                const isLow = f.stock < requiredTotal;

                return `
                    <div class="bg-white p-4 rounded-2xl border ${isLow ? 'border-amber-200' : 'border-slate-200'} shadow-sm flex flex-col justify-between">
                        <div>
                            <div class="flex items-center justify-between mb-2">
                                <h4 class="font-extrabold text-slate-800 text-base">${f.name}</h4>
                                <span class="text-xs font-bold px-2.5 py-1 rounded-lg bg-wheat-100 text-wheat-800">${f.perPerson} ${f.unit}/نەفەر</span>
                            </div>
                            <div class="my-3">
                                <span class="text-2xl font-black ${isLow ? 'text-amber-600' : 'text-emerald-700'}">${formatNumber(f.stock)}</span>
                                <span class="text-xs font-bold text-slate-500 mr-1">${f.unit} بەردەستە</span>
                            </div>
                            <div class="w-full bg-slate-100 rounded-full h-2 mb-2 overflow-hidden">
                                <div class="${isLow ? 'bg-amber-500' : 'bg-emerald-600'} h-2 rounded-full" style="width: ${pct}%"></div>
                            </div>
                            <p class="text-[11px] text-slate-500">پێداویستی بۆ ${formatNumber(appState.targetPeople)} نەفەر: <strong>${formatNumber(requiredTotal)} ${f.unit}</strong></p>
                        </div>
                        <button onclick="openEditSingleFoodModal('${f.id}')" class="mt-4 w-full py-2 rounded-xl bg-slate-50 hover:bg-slate-100 text-slate-700 font-bold text-xs border border-slate-200 transition flex items-center justify-center gap-1.5">
                            <i class="fa-solid fa-pen-to-square text-wheat-600"></i>
                            <span>چاککردنی بڕ و پشک</span>
                        </button>
                    </div>
                `;
            }).join('');
        }

        document.getElementById('add-stock-form').addEventListener('submit', function(e) {
            e.preventDefault();
            const foodId = document.getElementById('stock-food-select').value;
            const amount = parseFloat(normalizeDigits(document.getElementById('stock-amount-input').value));

            if (isNaN(amount) || amount <= 0) {
                showToast('تکایە بڕێکی دروست بنووسە', 'error');
                return;
            }

            const food = appState.foods.find(f => f.id === foodId);
            if (food) {
                food.stock = Number((food.stock + amount).toFixed(2));
                saveState();
                this.reset();
                showToast(`بڕی ${formatNumber(amount)} ${food.unit} بۆ "${food.name}" زیادکرا`, 'success');
            }
        });

        function openEditSingleFoodModal(foodId) {
            const food = appState.foods.find(f => f.id === foodId);
            if (!food) return;

            document.getElementById('modal-title').textContent = `چاککردنی زانیاری: ${food.name}`;
            document.getElementById('modal-body').innerHTML = `
                <form id="edit-single-food-form" class="space-y-4">
                    <div>
                        <label class="block text-xs font-bold text-slate-700 mb-1">بڕی بەردەست لە کۆگا (${food.unit}):</label>
                        <input type="number" step="0.5" id="edit-food-stock" value="${food.stock}" required class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 outline-none focus:border-wheat-500 text-sm font-bold">
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-700 mb-1">پشکی هەر نەفەرێک (${food.unit}):</label>
                        <input type="number" step="0.1" id="edit-food-per-person" value="${food.perPerson}" required class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 outline-none focus:border-wheat-500 text-sm font-bold">
                    </div>
                    <div class="flex justify-end gap-2 pt-3 border-t border-slate-100">
                        <button type="button" onclick="closeUniversalModal()" class="px-4 py-2 rounded-xl bg-slate-100 text-slate-700 font-bold text-sm">پاشگەزبوونەوە</button>
                        <button type="submit" class="px-5 py-2 rounded-xl bg-wheat-600 text-white font-bold text-sm">پاشەکەوتکردن</button>
                    </div>
                </form>
            `;

            document.getElementById('edit-single-food-form').onsubmit = function(e) {
                e.preventDefault();
                food.stock = parseFloat(normalizeDigits(document.getElementById('edit-food-stock').value)) || 0;
                food.perPerson = parseFloat(normalizeDigits(document.getElementById('edit-food-per-person').value)) || 0;
                saveState();
                closeUniversalModal();
                showToast('زانیاری خۆراکەکە نوێکرایەوە', 'success');
            };

            openUniversalModal();
        }

        function openEditRationModal() {
            document.getElementById('modal-title').textContent = 'چاککردنی پشکی نەفەر، ئامانج و نرخی ٢٠٠٠ دینار';
            document.getElementById('modal-body').innerHTML = `
                <form id="edit-global-ration-form" class="space-y-4">
                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="block text-xs font-bold text-slate-700 mb-1">نرخی هەر نەفەرێک (د.ع):</label>
                            <input type="number" id="edit-fee-per-person" value="${appState.feePerPerson}" required class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 outline-none focus:border-wheat-500 text-sm font-bold">
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-700 mb-1">ژمارەی گشتی نەفەر (ئامانج):</label>
                            <input type="number" id="edit-target-people" value="${appState.targetPeople}" required class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 outline-none focus:border-wheat-500 text-sm font-bold">
                        </div>
                    </div>
                    <div class="space-y-2 max-h-60 overflow-y-auto pr-1">
                        <p class="text-xs font-bold text-slate-600">پشکی هەر نەفەرێک بۆ هەر خۆراکێک:</p>
                        ${appState.foods.map(f => `
                            <div class="flex items-center justify-between bg-slate-50 p-2.5 rounded-xl border border-slate-200">
                                <span class="font-bold text-sm text-slate-700">${f.name} (${f.unit})</span>
                                <input type="number" step="0.1" data-food-id="${f.id}" value="${f.perPerson}" class="ration-input w-24 px-2.5 py-1.5 rounded-lg border border-slate-300 text-center font-bold text-sm">
                            </div>
                        `).join('')}
                    </div>
                    <div class="flex justify-end gap-2 pt-3 border-t border-slate-100">
                        <button type="button" onclick="closeUniversalModal()" class="px-4 py-2 rounded-xl bg-slate-100 text-slate-700 font-bold text-sm">پاشگەزبوونەوە</button>
                        <button type="submit" class="px-5 py-2 rounded-xl bg-emerald-700 text-white font-bold text-sm">پاشەکەوتکردنی هەمووی</button>
                    </div>
                </form>
            `;

            document.getElementById('edit-global-ration-form').onsubmit = function(e) {
                e.preventDefault();
                appState.feePerPerson = parseInt(normalizeDigits(document.getElementById('edit-fee-per-person').value), 10) || 2000;
                appState.targetPeople = parseInt(normalizeDigits(document.getElementById('edit-target-people').value), 10) || 1705;
                document.querySelectorAll('.ration-input').forEach(inp => {
                    const f = appState.foods.find(item => item.id === inp.dataset.foodId);
                    if (f) f.perPerson = parseFloat(normalizeDigits(inp.value)) || 0;
                });
                saveState();
                closeUniversalModal();
                showToast('هەموو ڕێکخستنەکان بە سەرکەوتوویی نوێکرانەوە', 'success');
            };

            openUniversalModal();
        }

        // --- 8. ARCHIVE MANAGEMENT (بەشی ئەرشیف) ---
        function archiveCurrentPage() {
            finishCurrentBasketToArchive();
        }

        function renderArchiveList() {
            const container = document.getElementById('archive-list-container');
            if (!container) return;

            if (appState.archives.length === 0) {
                container.innerHTML = `
                    <div class="col-span-full bg-white p-10 rounded-2xl border border-slate-200 text-center text-slate-400">
                        <i class="fa-solid fa-folder-open text-4xl mb-3 text-slate-300"></i>
                        <p class="font-bold text-slate-600">هێشتا هیچ فایلێک لە ئەرشیفدا خەزن نەکراوە</p>
                        <p class="text-xs mt-1">دوای تەواوبوونی دابەشکردنی خۆراک یان بە داگرتنی دوگمەی "خەزن لە ئەرشیف و مانگی نوێ"، فایلەکە لێرە دروست دەبێت.</p>
                    </div>
                `;
                return;
            }

            container.innerHTML = appState.archives.map(arch => `
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex flex-col justify-between hover:border-wheat-400 transition">
                    <div>
                        <div class="flex items-start justify-between gap-2 mb-3">
                            <div class="flex items-center gap-3">
                                <div class="w-11 h-11 rounded-2xl bg-wheat-100 text-wheat-700 flex items-center justify-center text-xl shrink-0">
                                    <i class="fa-solid fa-file-excel"></i>
                                </div>
                                <div>
                                    <span class="text-[11px] font-bold text-wheat-700 bg-wheat-50 border border-wheat-200 px-2 py-0.5 rounded-full" dir="ltr">${arch.date}</span>
                                    <h3 class="text-base font-extrabold text-slate-800 mt-1">${arch.name}</h3>
                                </div>
                            </div>
                            <button onclick="deleteArchive('${arch.id}')" class="p-2 rounded-xl bg-red-50 hover:bg-red-100 text-red-600 transition" title="سڕینەوەی فایل">
                                <i class="fa-solid fa-trash-can"></i>
                            </button>
                        </div>
                        <div class="grid grid-cols-2 gap-2 bg-slate-50 p-3 rounded-xl border border-slate-100 text-xs mb-4">
                            <div>
                                <span class="text-slate-400 block">ژمارەی خێزان</span>
                                <strong class="text-slate-800 text-sm">${arch.familiesCount} خێزان</strong>
                            </div>
                            <div>
                                <span class="text-slate-400 block">کۆی نەفەر</span>
                                <strong class="text-wheat-700 text-sm">${formatNumber(arch.totalMembers)} نەفەر</strong>
                            </div>
                            <div>
                                <span class="text-slate-400 block">حساب وصل</span>
                                <strong class="text-emerald-700 text-sm">${formatNumber(arch.totalPaid)} د.ع</strong>
                            </div>
                            <div>
                                <span class="text-slate-400 block">باقی حساب</span>
                                <strong class="text-amber-600 text-sm">${formatNumber(arch.totalUnpaid)} د.ع</strong>
                            </div>
                        </div>
                    </div>

                    <div class="space-y-2">
                        <button onclick="viewArchiveDetails('${arch.id}')" class="w-full py-2.5 rounded-xl bg-slate-800 hover:bg-slate-900 text-white font-bold text-xs transition flex items-center justify-center gap-2">
                            <i class="fa-solid fa-eye"></i>
                            <span>کردنەوەی ناوەڕۆکی فایل</span>
                        </button>
                        <div class="grid grid-cols-3 gap-1.5">
                            <button onclick="downloadArchiveCSV('${arch.id}')" class="py-2 px-2 rounded-xl bg-emerald-50 hover:bg-emerald-100 text-emerald-800 border border-emerald-200 font-bold text-xs transition flex items-center justify-center gap-1" title="داگرتن وەک فایلی Excel">
                                <i class="fa-solid fa-download"></i>
                                <span>Excel</span>
                            </button>
                            <button onclick="downloadArchiveHTML('${arch.id}')" class="py-2 px-2 rounded-xl bg-wheat-50 hover:bg-wheat-100 text-wheat-800 border border-wheat-200 font-bold text-xs transition flex items-center justify-center gap-1" title="خەزنکردن وەک فایل">
                                <i class="fa-solid fa-floppy-disk"></i>
                                <span>خەزنکردن</span>
                            </button>
                            <button onclick="shareArchiveFile('${arch.id}')" class="py-2 px-2 rounded-xl bg-sky-50 hover:bg-sky-100 text-sky-800 border border-sky-200 font-bold text-xs transition flex items-center justify-center gap-1" title="ناردن و هاوبەشکردن">
                                <i class="fa-solid fa-share-nodes"></i>
                                <span>ناردن</span>
                            </button>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        function buildArchiveCSVContent(arch) {
            const headers = ['#', 'ناوی سەرۆک خێزان', 'ژمارەی نەفەر', 'ژمارە مۆبایل', 'خۆراکە وەرگیراوەکان', 'بڕی پارە (د.ع)', 'دۆخی حساب', 'بەروار', 'تێبینی'];
            const rows = arch.records.map((r, i) => [
                i + 1,
                `"${(r.beneficiaryName || '').replace(/"/g, '""')}"`,
                r.members,
                `"${r.phone || '-'}"`,
                `"${r.items.map(it => `${it.name} (${it.quantity} ${it.unit})`).join(' - ')}"`,
                r.totalFee,
                r.paymentStatus === 'paid' ? 'حساب وصل' : 'باقی حساب',
                `"${r.date}"`,
                `"${(r.note || '').replace(/"/g, '""')}"`
            ]);
            return '\uFEFF' + [headers.join(','), ...rows.map(row => row.join(','))].join('\n');
        }

        function downloadArchiveCSV(archiveId) {
            const arch = appState.archives.find(a => a.id === archiveId);
            if (!arch) return;
            const csvContent = buildArchiveCSVContent(arch);
            const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement('a');
            link.href = url;
            link.download = `${arch.name}.csv`;
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            URL.revokeObjectURL(url);
            showToast(`فایلی "${arch.name}.csv" دابەزێنرا`, 'success');
        }

        function downloadArchiveHTML(archiveId) {
            const arch = appState.archives.find(a => a.id === archiveId);
            if (!arch) return;

            const htmlDoc = `<!DOCTYPE html>
<html lang="ckb" dir="rtl">
<head>
<meta charset="UTF-8">
<title>ئەرشیفی دابەشکردنی خۆراک - ${arch.name}</title>
<style>
  body { font-family: Tahoma, Arial, sans-serif; padding: 24px; color: #1e293b; }
  h1 { color: #92400e; margin-bottom: 4px; }
  .meta { background: #fef3c7; padding: 12px; border-radius: 8px; margin-bottom: 16px; font-size: 14px; }
  table { width: 100%; border-collapse: collapse; font-size: 13px; }
  th, td { border: 1px solid #cbd5e1; padding: 8px 10px; text-align: right; }
  th { background: #f1f5f9; }
</style>
</head>
<body>
  <h1>سیستەمی دابەشکردنی خۆراك و بەرێوەبردن - ${arch.name}</h1>
  <div class="meta">بەروار: <strong>${arch.date}</strong> | ژمارەی خێزان: <strong>${arch.familiesCount}</strong> | کۆی نەفەر: <strong>${arch.totalMembers}</strong> | حساب وصل: <strong>${formatNumber(arch.totalPaid)} د.ع</strong> | باقی حساب: <strong>${formatNumber(arch.totalUnpaid)} د.ع</strong></div>
  <table>
    <thead>
      <tr><th>#</th><th>ناو</th><th>نەفەر</th><th>مۆبایل</th><th>خۆراکەکان</th><th>بڕی پارە</th><th>حساب</th><th>تێبینی</th></tr>
    </thead>
    <tbody>
      ${arch.records.map((r, i) => `<tr><td>${i + 1}</td><td>${r.beneficiaryName}</td><td>${r.members}</td><td>${r.phone || '-'}</td><td>${r.items.map(it => `${it.name} (${it.quantity} ${it.unit})`).join('، ')}</td><td>${formatNumber(r.totalFee)} د.ع</td><td>${r.paymentStatus === 'paid' ? 'حساب وصل' : 'باقی حساب'}</td><td>${r.note || '-'}</td></tr>`).join('')}
    </tbody>
  </table>
</body>
</html>`;

            const blob = new Blob([htmlDoc], { type: 'text/html;charset=utf-8;' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement('a');
            link.href = url;
            link.download = `${arch.name}.html`;
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            URL.revokeObjectURL(url);
            showToast(`فایلی "${arch.name}.html" خەزنکرا`, 'success');
        }

        async function shareArchiveFile(archiveId) {
            const arch = appState.archives.find(a => a.id === archiveId);
            if (!arch) return;

            const summaryText = `📋 ئەرشیفی دابەشکردنی خۆراک: ${arch.name}\n📅 بەروار: ${arch.date}\n👨‍👩‍👧‍👦 ژمارەی خێزان: ${arch.familiesCount} (${arch.totalMembers} نەفەر)\n✅ حساب وصل: ${formatNumber(arch.totalPaid)} د.ع\n⏳ باقی حساب: ${formatNumber(arch.totalUnpaid)} د.ع\n\n` +
                arch.records.map((r, i) => `${i + 1}. ${r.beneficiaryName} (${r.members} نەفەر) - ${r.paymentStatus === 'paid' ? 'حساب وصل' : 'باقی حساب'}`).join('\n');

            try {
                const csvContent = buildArchiveCSVContent(arch);
                const file = new File([csvContent], `${arch.name}.csv`, { type: 'text/csv' });

                if (navigator.canShare && navigator.canShare({ files: [file] })) {
                    await navigator.share({
                        title: `ئەرشیف: ${arch.name}`,
                        text: summaryText,
                        files: [file]
                    });
                    showToast('فایلەکە بە سەرکەوتوویی نێردرا', 'success');
                    return;
                } else if (navigator.share) {
                    await navigator.share({
                        title: `ئەرشیف: ${arch.name}`,
                        text: summaryText
                    });
                    showToast('داتاکان هاوبەشکران', 'success');
                    return;
                }
            } catch (err) {
                if (err && err.name === 'AbortError') return;
            }

            // Fallback: Copy summary to clipboard & offer WhatsApp link
            const tempTextarea = document.createElement('textarea');
            tempTextarea.value = summaryText;
            document.body.appendChild(tempTextarea);
            tempTextarea.select();
            document.execCommand('copy');
            document.body.removeChild(tempTextarea);

            document.getElementById('modal-title').textContent = `ناردنی فایل: ${arch.name}`;
            document.getElementById('modal-body').innerHTML = `
                <div class="space-y-4">
                    <p class="text-xs text-emerald-700 bg-emerald-50 border border-emerald-200 p-3 rounded-xl font-bold">
                        <i class="fa-solid fa-check-circle ml-1"></i> پوختەی فایلەکە کۆپی کرا! دەتوانیت لە هەر بەرنامەیەک Paste بکەیت یان ڕاستەوخۆ بە واتسئەپ بینێریت:
                    </p>
                    <textarea readonly rows="6" class="w-full p-3 rounded-xl border border-slate-300 bg-slate-50 text-xs font-mono">${summaryText}</textarea>
                    <div class="flex flex-wrap justify-end gap-2">
                        <a href="https://wa.me/?text=${encodeURIComponent(summaryText)}" target="_blank" rel="noopener noreferrer" class="px-4 py-2 rounded-xl bg-green-600 hover:bg-green-700 text-white font-bold text-sm flex items-center gap-1.5">
                            <i class="fa-brands fa-whatsapp text-base"></i> ناردن بە واتسئەپ
                        </a>
                        <button type="button" onclick="downloadArchiveCSV('${arch.id}')" class="px-4 py-2 rounded-xl bg-wheat-600 text-white font-bold text-sm flex items-center gap-1.5">
                            <i class="fa-solid fa-file-excel"></i> داگرتنی فایلی Excel
                        </button>
                        <button type="button" onclick="closeUniversalModal()" class="px-4 py-2 rounded-xl bg-slate-100 text-slate-700 font-bold text-sm">داخستن</button>
                    </div>
                </div>
            `;
            openUniversalModal();
        }

        function deleteArchive(id) {
            showConfirm('سڕینەوەی ئەرشیف', 'ئایا دڵنیایت لە سڕینەوەی ئەم پەڕە ئەرشیفکراوە بە یەکجاری؟', () => {
                appState.archives = appState.archives.filter(a => a.id !== id);
                saveState();
                showToast('ئەرشیفەکە سڕایەوە', 'info');
            });
        }

        // --- 8.5 MONITORING LOGIC (چاودێریکردنی بەشە خۆراکە وەرنەگیراوەکان) ---
        function renderMonitoringTable() {
            const tbody = document.getElementById('monitoring-table-body');
            if (!tbody) return;

            const query = (document.getElementById('monitoring-search-input')?.value || '').trim().toLowerCase();
            const statusFilter = document.getElementById('monitoring-status-filter')?.value || 'all';

            let totalFamilies = appState.beneficiaries.length;
            let missingCount = 0;
            let completeCount = 0;

            const analyzedList = appState.beneficiaries.map(ben => {
                // Collect all food IDs this beneficiary has received in the current sheet
                const benDists = appState.distributions.filter(d => d.beneficiaryId === ben.id);
                const receivedFoodIds = new Set();
                benDists.forEach(d => {
                    d.items.forEach(item => receivedFoodIds.add(item.foodId));
                });

                const receivedFoods = appState.foods.filter(f => receivedFoodIds.has(f.id));
                const missingFoods = appState.foods.filter(f => !receivedFoodIds.has(f.id));

                if (missingFoods.length > 0) {
                    missingCount++;
                } else {
                    completeCount++;
                }

                return {
                    ...ben,
                    receivedFoods,
                    missingFoods
                };
            });

            // Update stats & badge
            const badgeEl = document.getElementById('badge-monitoring-count');
            if (badgeEl) badgeEl.textContent = missingCount;
            if (document.getElementById('mon-stat-total')) document.getElementById('mon-stat-total').textContent = totalFamilies;
            if (document.getElementById('mon-stat-missing')) document.getElementById('mon-stat-missing').textContent = missingCount;
            if (document.getElementById('mon-stat-complete')) document.getElementById('mon-stat-complete').textContent = completeCount;

            // Filter list
            const filtered = analyzedList.filter(item => {
                const matchesQuery = item.name.toLowerCase().includes(query) || normalizeDigits(item.phone).includes(normalizeDigits(query));
                if (!matchesQuery) return false;

                if (statusFilter === 'missing') return item.missingFoods.length > 0;
                if (statusFilter === 'none_received') return item.receivedFoods.length === 0;
                if (statusFilter === 'complete') return item.missingFoods.length === 0;
                return true;
            });

            if (filtered.length === 0) {
                tbody.innerHTML = `<tr><td colspan="10" class="py-8 text-center text-slate-400">هیچ خێزانێک لەم بەشەدا نەدۆزرایەوە</td></tr>`;
                return;
            }

            tbody.innerHTML = filtered.map((item, idx) => {
                const benDists = appState.distributions.filter(d => d.beneficiaryId === item.id);
                const latestDist = benDists.length > 0 ? benDists[0] : null;
                const hasUnpaid = benDists.some(d => d.paymentStatus === 'unpaid');
                const totalFee = item.members * appState.feePerPerson;

                const notesList = benDists.map(d => d.note).filter(n => n && n.trim() !== '');
                const noteTextHtml = notesList.length > 0
                    ? `<span class="text-xs text-slate-700 bg-amber-50 border border-amber-200 px-2.5 py-1 rounded-lg inline-block max-w-xs">${notesList.join(' | ')}</span>`
                    : `<span class="text-xs text-slate-400">-</span>`;
                const noteHtml = `
                    <div class="flex items-center gap-1.5">
                        ${noteTextHtml}
                        <button onclick="openEditRecordNoteModal('${item.id}')" class="px-2 py-1 rounded-lg bg-sky-50 hover:bg-sky-100 text-sky-700 font-bold text-[11px] transition flex items-center gap-1 shrink-0" title="چاککردنی تێبینی">
                            <i class="fa-solid fa-pen-to-square"></i> چاککردن
                        </button>
                    </div>
                `;

                let accountHtml = `<span class="text-xs text-slate-400">-</span>`;
                if (benDists.length > 0) {
                    accountHtml = hasUnpaid
                        ? `<div class="flex flex-col items-center gap-0.5"><span class="px-2.5 py-0.5 rounded-full text-[11px] font-bold bg-amber-100 text-amber-800 whitespace-nowrap">باقی حساب</span><span class="text-[11px] font-bold text-slate-600">${formatNumber(totalFee)} د.ع</span></div>`
                        : `<div class="flex flex-col items-center gap-0.5"><span class="px-2.5 py-0.5 rounded-full text-[11px] font-bold bg-emerald-100 text-emerald-800 whitespace-nowrap">حساب وصل</span><span class="text-[11px] font-bold text-emerald-700">${formatNumber(totalFee)} د.ع</span></div>`;
                }

                const dateHtml = latestDist
                    ? `<span class="text-xs font-mono text-slate-600 whitespace-nowrap" dir="ltr">${latestDist.date}</span>`
                    : `<span class="text-xs text-slate-400 italic">وەرنەگیراوە</span>`;

                const receivedHtml = item.receivedFoods.length > 0
                    ? item.receivedFoods.map(f => `<span class="inline-block bg-emerald-50 text-emerald-700 border border-emerald-200 text-xs font-bold px-2 py-0.5 rounded-lg m-0.5">${f.name}</span>`).join('')
                    : `<span class="text-xs text-slate-400 italic">هیچی وەرنەگرتووە</span>`;

                const missingHtml = item.missingFoods.length > 0
                    ? item.missingFoods.map(f => {
                        const qty = Number((f.perPerson * item.members).toFixed(2));
                        return `<span class="inline-block bg-red-50 text-red-700 border border-red-200 text-xs font-bold px-2 py-0.5 rounded-lg m-0.5">${f.name} (${qty} ${f.unit})</span>`;
                    }).join('')
                    : `<span class="inline-flex items-center gap-1 bg-emerald-100 text-emerald-800 text-xs font-extrabold px-2.5 py-1 rounded-full"><i class="fa-solid fa-check"></i> هەمووی وەرگرتووە</span>`;

                return `
                    <tr class="hover:bg-slate-50 transition">
                        <td class="py-3 px-4 font-bold text-slate-400">${idx + 1}</td>
                        <td class="py-3 px-4 font-bold text-slate-800">${item.name}</td>
                        <td class="py-3 px-4 text-center">
                            <span class="bg-wheat-100 text-wheat-800 font-extrabold px-2.5 py-1 rounded-lg text-xs">${item.members} نەفەر</span>
                        </td>
                        <td class="py-3 px-4 font-mono text-slate-600 text-xs" dir="ltr">${item.phone || '-'}</td>
                        <td class="py-3 px-4">${receivedHtml}</td>
                        <td class="py-3 px-4">${missingHtml}</td>
                        <td class="py-3 px-4 text-center">${accountHtml}</td>
                        <td class="py-3 px-4 text-center">${dateHtml}</td>
                        <td class="py-3 px-4">${noteHtml}</td>
                        <td class="py-3 px-4 text-center">
                            ${item.missingFoods.length > 0 ? `
                                <button onclick="goToDistributeFor('${item.id}')" class="px-3 py-1.5 rounded-xl bg-emerald-700 hover:bg-emerald-800 text-white font-bold text-xs transition whitespace-nowrap shadow-xs">
                                    پێدانی خۆراک
                                </button>
                            ` : `<span class="text-xs text-emerald-600 font-bold">تەواو</span>`}
                        </td>
                    </tr>
                `;
            }).join('');
        }

        function openEditRecordNoteModal(beneficiaryId) {
            const ben = appState.beneficiaries.find(b => b.id === beneficiaryId);
            if (!ben) return;

            const benDists = appState.distributions.filter(d => d.beneficiaryId === beneficiaryId);
            const currentNotes = benDists.map(d => d.note).filter(n => n && n.trim() !== '').join(' | ');

            document.getElementById('modal-title').textContent = `چاککردنی تێبینی بۆ: ${ben.name}`;
            document.getElementById('modal-body').innerHTML = `
                <form id="edit-record-note-form" class="space-y-4">
                    <div>
                        <label class="block text-xs font-bold text-slate-700 mb-1.5">تێبینی بنووسە یان دەستکاری بکە:</label>
                        <textarea id="edit-record-note-input" rows="3" placeholder="تێبینی لێرە بنووسە..."
                            class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 outline-none focus:border-emerald-500 text-sm">${currentNotes}</textarea>
                    </div>
                    <div class="flex justify-end gap-2 pt-3 border-t border-slate-100">
                        <button type="button" onclick="closeUniversalModal()" class="px-4 py-2 rounded-xl bg-slate-100 text-slate-700 font-bold text-sm">پاشگەزبوونەوە</button>
                        <button type="submit" class="px-5 py-2 rounded-xl bg-emerald-700 text-white font-bold text-sm">پاشەکەوتکردنی تێبینی</button>
                    </div>
                </form>
            `;

            document.getElementById('edit-record-note-form').onsubmit = function(e) {
                e.preventDefault();
                const updatedNote = document.getElementById('edit-record-note-input').value.trim();

                if (benDists.length > 0) {
                    benDists.forEach((d, idx) => {
                        d.note = idx === 0 ? updatedNote : '';
                    });
                } else {
                    appState.distributions.unshift({
                        id: 'dist_' + Date.now(),
                        beneficiaryId: ben.id,
                        beneficiaryName: ben.name,
                        phone: ben.phone,
                        members: ben.members,
                        items: [],
                        totalFee: 0,
                        paymentStatus: 'unpaid',
                        note: updatedNote,
                        date: new Date().toLocaleDateString('en-CA') + ' ' + new Date().toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' })
                    });
                }

                saveState();
                closeUniversalModal();
                showToast('تێبینییەکە بە سەرکەوتوویی چاککرا', 'success');
            };

            openUniversalModal();
        }

        function goToDistributeFor(beneficiaryId) {
            selectedBeneficiaryId = beneficiaryId;
            switchTab('distribution');
            showToast('خێزانەکە هەڵبژێردرا بۆ پێدانی بەشە خۆراکە ماوەکان', 'info');
        }

        // --- 9. UNIVERSAL MODAL & ONLINE GUIDE ---
        function openUniversalModal() {
            const modal = document.getElementById('universal-modal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
        }

        function closeUniversalModal() {
            const modal = document.getElementById('universal-modal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        function openOnlineModal() {
            document.getElementById('modal-title').textContent = 'چۆنیەتی کردنی سیستەمەکە بە سایت لەسەر ئۆنلاین';
            document.getElementById('modal-body').innerHTML = `
                <div class="space-y-3 text-sm text-slate-700 leading-relaxed">
                    <p class="bg-sky-50 border border-sky-200 p-3 rounded-xl text-sky-900 font-semibold">
                        ئەم سیستەمە بە شێوەی یەک فایلی HTML دروستکراوە و بە پاسۆرد پارێزراوە (پاسۆردی بنەڕەتی: <strong class="font-mono">009988</strong>).
                    </p>
                    <ol class="list-decimal list-inside space-y-2 pr-2">
                        <li>فایلەکە لە سەرەوەی ئەم پەڕەیە دابەزێنە بە ناوی <code class="bg-slate-100 px-1.5 py-0.5 rounded font-mono text-xs">index.html</code>.</li>
                        <li>بچۆرە سەر یەکێک لە سایتە خۆڕاییەکانی وەک <strong>Netlify Drop</strong> یان <strong>GitHub Pages</strong> یان <strong>Vercel</strong>.</li>
                        <li>فایلی <code class="bg-slate-100 px-1.5 py-0.5 rounded font-mono text-xs">index.html</code> بخەرە ناوی و ڕاستەوخۆ لینکێکی ئۆنلاینت پێدەدات کە لە هەموو مۆبایل و کۆمپیوتەرێکەوە دەکرێتەوە.</li>
                    </ol>
                    <div class="flex justify-end pt-3 border-t border-slate-100">
                        <button type="button" onclick="closeUniversalModal()" class="px-5 py-2 rounded-xl bg-slate-800 text-white font-bold text-sm">تێگەیشتم</button>
                    </div>
                </div>
            `;
            openUniversalModal();
        }

        function viewArchiveDetails(archiveId) {
            const arch = appState.archives.find(a => a.id === archiveId);
            if (!arch) return;

            document.getElementById('modal-title').textContent = `ناوەڕۆکی فایل: ${arch.name}`;
            document.getElementById('modal-body').innerHTML = `
                <div class="space-y-4">
                    <div class="grid grid-cols-2 sm:grid-cols-4 gap-2 bg-wheat-50 p-3 rounded-xl border border-wheat-200 text-xs">
                        <div><span class="text-slate-500 block">بەروار:</span><strong dir="ltr">${arch.date}</strong></div>
                        <div><span class="text-slate-500 block">کۆی نەفەر:</span><strong>${formatNumber(arch.totalMembers)} نەفەر</strong></div>
                        <div><span class="text-slate-500 block">حساب وصل:</span><strong class="text-emerald-700">${formatNumber(arch.totalPaid)} د.ع</strong></div>
                        <div><span class="text-slate-500 block">باقی حساب:</span><strong class="text-amber-700">${formatNumber(arch.totalUnpaid)} د.ع</strong></div>
                    </div>
                    <div class="max-h-72 overflow-y-auto border border-slate-200 rounded-xl">
                        <table class="w-full text-right text-xs">
                            <thead class="bg-slate-100 text-slate-700 font-bold sticky top-0">
                                <tr>
                                    <th class="p-2.5">#</th>
                                    <th class="p-2.5">ناو</th>
                                    <th class="p-2.5">نەفەر</th>
                                    <th class="p-2.5">خۆراکەکان</th>
                                    <th class="p-2.5">حساب</th>
                                    <th class="p-2.5">تێبینی</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-slate-100">
                                ${arch.records.map((r, i) => `
                                    <tr>
                                        <td class="p-2.5 font-bold text-slate-400">${i + 1}</td>
                                        <td class="p-2.5 font-bold">${r.beneficiaryName}</td>
                                        <td class="p-2.5">${r.members}</td>
                                        <td class="p-2.5">${r.items.map(it => `${it.name} (${it.quantity} ${it.unit})`).join('، ')}</td>
                                        <td class="p-2.5 font-bold ${r.paymentStatus === 'paid' ? 'text-emerald-700' : 'text-amber-700'}">${r.paymentStatus === 'paid' ? 'حساب وصل' : 'باقی حساب'}</td>
                                        <td class="p-2.5 text-slate-500">${r.note || '-'}</td>
                                    </tr>
                                `).join('')}
                            </tbody>
                        </table>
                    </div>
                    <div class="flex flex-wrap justify-end gap-2 pt-2">
                        <button onclick="downloadArchiveCSV('${arch.id}')" class="px-4 py-2 rounded-xl bg-emerald-700 text-white font-bold text-sm flex items-center gap-1.5">
                            <i class="fa-solid fa-file-excel"></i> داگرتنی Excel
                        </button>
                        <button onclick="downloadArchiveHTML('${arch.id}')" class="px-4 py-2 rounded-xl bg-wheat-600 text-white font-bold text-sm flex items-center gap-1.5">
                            <i class="fa-solid fa-floppy-disk"></i> خەزنکردنی فایل
                        </button>
                        <button onclick="shareArchiveFile('${arch.id}')" class="px-4 py-2 rounded-xl bg-sky-600 text-white font-bold text-sm flex items-center gap-1.5">
                            <i class="fa-solid fa-share-nodes"></i> ناردن
                        </button>
                        <button onclick="window.print()" class="px-4 py-2 rounded-xl bg-slate-800 text-white font-bold text-sm flex items-center gap-1.5">
                            <i class="fa-solid fa-print"></i> چاپکردن
                        </button>
                        <button onclick="closeUniversalModal()" class="px-4 py-2 rounded-xl bg-slate-100 text-slate-700 font-bold text-sm">داخستن</button>
                    </div>
                </div>
            `;
            openUniversalModal();
        }

        // --- 10. INITIALIZE & UPDATE UI ---
        function updateAllUI() {
            const now = new Date();
            const kurdishWeekDays = ['یەکشەممە', 'دووشەممە', 'سێشەممە', 'چوارشەممە', 'پێنجشەممە', 'هەینی', 'شەممە'];
            const dayName = kurdishWeekDays[now.getDay()];
            const day = String(now.getDate()).padStart(2, '0');
            const month = String(now.getMonth() + 1).padStart(2, '0');
            const year = now.getFullYear();
            document.getElementById('header-current-day').textContent = dayName;
            document.getElementById('header-current-date').textContent = `${year}/${month}/${day}`;
            document.getElementById('current-sheet-label').textContent = appState.isMonthlyFileOpen && appState.currentSheetName ? appState.currentSheetName : 'هیچ فایلێک نەکراوەتەوە';
            document.getElementById('badge-beneficiaries-count').textContent = appState.beneficiaries.length;
            document.getElementById('badge-archive-count').textContent = appState.archives.length;

            // Toggle between Locked Main Page and Active Monthly File Workspace
            const lockedBox = document.getElementById('monthly-file-locked-box');
            const activeWorkspace = document.getElementById('monthly-file-active-workspace');
            if (lockedBox && activeWorkspace) {
                if (appState.isMonthlyFileOpen && appState.currentSheetName) {
                    lockedBox.classList.add('hidden');
                    activeWorkspace.classList.remove('hidden');
                    const titleEl = document.getElementById('active-monthly-file-title');
                    if (titleEl) titleEl.textContent = appState.currentSheetName;
                    const progEl = document.getElementById('monthly-progress-badge');
                    if (progEl) progEl.textContent = `${getCompletedBeneficiariesCount()} / ${appState.beneficiaries.length} خێزان تەواوبوون`;
                } else {
                    lockedBox.classList.remove('hidden');
                    activeWorkspace.classList.add('hidden');
                }
            }

            const completedBanner = document.getElementById('all-completed-banner');
            if (completedBanner) {
                if (appState.isMonthlyFileOpen && isAllBeneficiariesCompleted()) {
                    completedBanner.classList.remove('hidden');
                } else {
                    completedBanner.classList.add('hidden');
                }
            }

            renderDistBeneficiarySearch();
            renderSelectedBeneficiaryPanel();
            renderDistributionsTable();
            renderBeneficiariesTable();
            renderWarehouse();
            renderMonitoringTable();
            renderArchiveList();
        }

        window.addEventListener('DOMContentLoaded', () => {
            loadState();
            updateAllUI();
        });
    </script>
</body>
</html>

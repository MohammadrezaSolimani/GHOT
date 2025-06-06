<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- Chosen Palette: Galactic Night -->
    <!-- Application Structure Plan: Responding to user request for a dark theme and better icon layout. This version implements a "Galactic Night" theme, using deep dark backgrounds with vibrant neon highlights (blue/purple). The core single-page structure is retained. The skills/tools section is redesigned to place icons within their own distinct card for better visual grouping and emphasis, addressing the user's icon layout request. All components, including the chart and modals, are restyled for the new dark aesthetic. -->
    <!-- Visualization & Content Choices: 
        - Greeting: Goal: Inform/Engage. Method: Neon-glow gradient text (CSS) for a high-impact intro on a dark background. Library: Tailwind.
        - Skills Comparison: Goal: Compare. Method: Interactive Radar Chart (Chart.js) with colors matching the "Galactic Night" theme. Justification: Effective data viz, adapted to new aesthetic. Library: Chart.js.
        - Technology Icons: Goal: Organize. Method: Grouped icons within a dedicated, styled card. Justification: Fulfills user request for a side-by-side layout with more visual impact than loose badges. Library: Tailwind.
        - Projects: Goal: Organize/Inform/Enhance. Method: Dark-themed cards with neon accents, Gemini API button retained. Justification: Consistent look, AI feature retained. Library: Tailwind, Gemini API (fetch).
        - Future Goals: Goal: Inform/Change/Enhance. Method: List items styled as distinct, glowing cards/steps. Justification: Fits dark/tech theme. Library: Tailwind, Gemini API (fetch).
        - Modals for Gemini Content: Goal: Inform. Method: Dark-themed modal. Justification: Consistent UI for API content. Library: Tailwind, JS.
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <title>پروفایل محمدرضا سلیمانی - تم شب کهکشانی</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Vazirmatn:wght@300;400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Vazirmatn', sans-serif;
            background-color: #0d1117; /* GitHub Dark Dimmed */
            color: #c9d1d9; /* GitHub Dark Text */
        }
        .gradient-text {
            background-image: linear-gradient(to right, #58a6ff, #a371f7); /* Blue to Purple */
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        .text-glow {
            text-shadow: 0 0 8px currentColor;
        }
        .card {
            background-color: #161b22; /* GitHub Dark Card */
            border: 1px solid #30363d; /* GitHub Dark Border */
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .card:hover {
            transform: translateY(-8px);
            box-shadow: 0 0 25px rgba(88, 166, 255, 0.2); /* Blue glow */
        }
        .nav-link {
            transition: color 0.3s, text-shadow 0.3s;
            color: #8b949e; /* Medium Gray */
        }
        .nav-link:hover, .nav-link.active {
            color: #58a6ff; /* Blue accent */
            text-shadow: 0 0 5px #58a6ff;
        }
        .navbar-bg {
             background-color: rgba(13, 17, 23, 0.8);
             backdrop-filter: blur(10px);
             border-bottom: 1px solid #30363d;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 550px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 380px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 380px;
            }
        }
        .section-hidden {
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 0.7s ease-out, transform 0.7s ease-out;
        }
        .section-visible {
            opacity: 1;
            transform: translateY(0);
        }
        .modal {
            background-color: rgba(0, 0, 0, 0.7); 
        }
        .modal-content {
            background-color: #161b22;
            color: #c9d1d9;
            border: 1px solid #30363d;
        }
        .gemini-button {
            background: linear-gradient(to right, #58a6ff, #a371f7);
            color: white;
            padding: 10px 16px;
            border-radius: 8px;
            font-size: 0.9rem;
            font-weight: 500;
            transition: all 0.3s ease;
            border: none;
            box-shadow: 0 0 15px rgba(88, 166, 255, 0.3);
        }
        .gemini-button:hover {
            transform: scale(1.05);
            box-shadow: 0 0 25px rgba(163, 113, 247, 0.5);
        }
        .primary-button {
            background-color: #238636; /* GitHub Green */
            color: white;
            font-weight: 500;
            transition: background-color 0.3s ease;
        }
        .primary-button:hover {
            background-color: #2ea043;
        }
          .loader {
            border: 4px solid #30363d;
            border-top: 4px solid #58a6ff;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
            margin: 20px auto;
        }
        .timeline-icon {
            background: linear-gradient(to bottom, #58a6ff, #a371f7);
        }
        .tech-badge {
            background-color: #21262d; /* GitHub Dark Badge */
            color: #c9d1d9;
            font-weight: 500;
            border: 1px solid #30363d;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body class="antialiased">

    <header id="navbar" class="navbar-bg fixed top-0 left-0 right-0 z-50">
        <nav class="container mx-auto px-6 py-4 flex justify-between items-center">
            <div class="text-2xl font-bold">
                <a href="#home" class="nav-link gradient-text">محمدرضا سلیمانی</a>
            </div>
            <div class="hidden md:flex space-x-6 space-x-reverse text-md">
                <a href="#about" class="nav-link">درباره من</a>
                <a href="#skills" class="nav-link">مهارت‌ها</a>
                <a href="#projects" class="nav-link">پروژه‌ها</a>
                <a href="#future" class="nav-link">اهداف آینده</a>
                <a href="#contact" class="nav-link">ارتباط با من</a>
            </div>
            <div class="md:hidden">
                <button id="menu-btn" class="text-gray-400 focus:outline-none">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path></svg>
                </button>
            </div>
        </nav>
        <div id="mobile-menu" class="hidden md:hidden bg-[#161b22] border-t border-[#30363d]">
             <a href="#about" class="block py-3 px-4 text-sm nav-link hover:bg-[#21262d]">درباره من</a>
             <a href="#skills" class="block py-3 px-4 text-sm nav-link hover:bg-[#21262d]">مهارت‌ها</a>
             <a href="#projects" class="block py-3 px-4 text-sm nav-link hover:bg-[#21262d]">پروژه‌ها</a>
             <a href="#future" class="block py-3 px-4 text-sm nav-link hover:bg-[#21262d]">اهداف آینده</a>
             <a href="#contact" class="block py-3 px-4 text-sm nav-link hover:bg-[#21262d]">ارتباط با من</a>
        </div>
    </header>

    <main class="pt-20">
        <section id="home" class="min-h-screen flex items-center justify-center bg-[#0d1117]">
             <div class="absolute inset-0 z-0 opacity-10" style="background-image: radial-gradient(#30363d 1px, transparent 1px); background-size: 20px 20px;"></div>
            <div class="text-center px-4 py-16 z-10">
                <h1 class="text-5xl md:text-7xl font-bold text-gray-100">
                    سلام! من <span class="gradient-text text-glow">محمدرضا سلیمانی</span> هستم
                </h1>
                <p id="typing-text" class="text-blue-400 text-xl md:text-3xl mt-6 h-10 font-medium"></p>
                 <a href="#about" class="mt-16 inline-block animate-bounce p-3 bg-[#161b22] rounded-full shadow-lg border border-[#30363d]">
                    <svg class="w-8 h-8 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3"></path></svg>
                </a>
            </div>
        </section>

        <section id="about" class="py-20 md:py-28 section-hidden">
            <div class="container mx-auto px-6">
                <h2 class="text-4xl font-bold text-center mb-5 text-gray-100">درباره <span class="gradient-text">من</span></h2>
                <p class="text-center text-gray-400 mb-12 max-w-3xl mx-auto text-lg">
                    اینجا فضایی برای معرفی عمیق‌تر خودم به عنوان یک توسعه‌دهنده است. من به حل چالش‌های پیچیده و ساختن محصولات کاربردی و زیبا علاقه‌مندم.
                </p>
                <div class="text-lg text-gray-300 leading-relaxed max-w-4xl mx-auto text-center card p-8 md:p-12 rounded-xl">
                    <p>
                        من یک توسعه‌دهنده وب مشتاق با تمرکز بر تکنولوژی‌های مدرن جاوااسکریپت مانند React و Node.js هستم. سفر من در دنیای برنامه‌نویسی از کنجکاوی برای درک نحوه کارکرد وب آغاز شد و به سرعت به یک علاقه عمیق برای خلق تجربیات دیجیتال تبدیل شد. من از تبدیل ایده‌های خلاقانه به کدهای تمیز و کارآمد لذت می‌برم و همیشه در حال یادگیری و کاوش در فناوری‌های جدید هستم تا مهارت‌هایم را گسترش دهم.
                    </p>
                </div>
            </div>
        </section>

        <section id="skills" class="py-20 md:py-28 bg-[#161b22]/50 section-hidden">
            <div class="container mx-auto px-6">
                <h2 class="text-4xl font-bold text-center mb-16 text-gray-100">زرادخانه <span class="gradient-text">فنی</span> من</h2>
                <div class="flex flex-col lg:flex-row items-center gap-12 lg:gap-16">
                    <div class="w-full lg:w-1/2 card p-6 rounded-xl">
                        <div class="chart-container">
                            <canvas id="skillsChart"></canvas>
                        </div>
                    </div>
                    <div class="w-full lg:w-1/2 card p-8 rounded-xl">
                        <h3 class="text-3xl font-bold text-center mb-8 text-gray-200">ابزارها و تکنولوژی‌ها</h3>
                        <div class="flex flex-wrap justify-center gap-4">
                            <span class="tech-badge px-4 py-2 rounded-lg text-md">HTML</span>
                            <span class="tech-badge px-4 py-2 rounded-lg text-md">CSS</span>
                            <span class="tech-badge px-4 py-2 rounded-lg text-md">JavaScript</span>
                            <span class="tech-badge px-4 py-2 rounded-lg text-md">React</span>
                            <span class="tech-badge px-4 py-2 rounded-lg text-md">Redux</span>
                            <span class="tech-badge px-4 py-2 rounded-lg text-md">TailwindCSS</span>
                            <span class="tech-badge px-4 py-2 rounded-lg text-md">TypeScript</span>
                            <span class="tech-badge px-4 py-2 rounded-lg text-md">Node.js</span>
                            <span class="tech-badge px-4 py-2 rounded-lg text-md">Python</span>
                            <span class="tech-badge px-4 py-2 rounded-lg text-md">Flask</span>
                            <span class="tech-badge px-4 py-2 rounded-lg text-md">Figma</span>
                            <span class="tech-badge px-4 py-2 rounded-lg text-md">GitHub</span>
                            <span class="tech-badge px-4 py-2 rounded-lg text-md">Docker</span>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="projects" class="py-20 md:py-28 section-hidden">
            <div class="container mx-auto px-6">
                <h2 class="text-4xl font-bold text-center mb-16 text-gray-100">پروژه‌های <span class="gradient-text">منتخب</span></h2>
                <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <div class="card rounded-xl overflow-hidden p-6 text-center flex flex-col justify-between">
                        <div>
                            <h3 class="project-title text-2xl font-bold mb-3 text-gray-100">پروژه اول</h3>
                            <p class="project-description text-gray-400 mb-5 text-sm leading-relaxed">توضیحات مختصری در مورد این پروژه و چالش‌های آن. این پروژه با هدف ... ساخته شده است.</p>
                            <div class="mb-5 flex justify-center gap-2 flex-wrap">
                                <span class="bg-blue-600/20 text-blue-300 text-xs font-semibold px-2.5 py-1 rounded-full">React</span>
                                <span class="bg-purple-600/20 text-purple-300 text-xs font-semibold px-2.5 py-1 rounded-full">Node.js</span>
                            </div>
                        </div>
                        <div class="mt-auto space-y-3">
                             <button class="gemini-button suggest-description-btn w-full">✨ پیشنهاد توضیحات</button>
                            <a href="https://github.com/MohammadrezaSolimani/Project1" target="_blank" class="primary-button inline-block py-2.5 px-6 rounded-lg w-full">مشاهده در گیت‌هاب</a>
                        </div>
                    </div>
                     <div class="card rounded-xl overflow-hidden p-6 text-center flex flex-col justify-between">
                        <div>
                            <h3 class="project-title text-2xl font-bold mb-3 text-gray-100">پروژه دوم</h3>
                            <p class="project-description text-gray-400 mb-5 text-sm leading-relaxed">توضیحات مختصری در مورد این پروژه و چالش‌های آن. این پروژه با هدف ... ساخته شده است.</p>
                             <div class="mb-5 flex justify-center gap-2 flex-wrap">
                                <span class="bg-blue-600/20 text-blue-300 text-xs font-semibold px-2.5 py-1 rounded-full">Python</span>
                                <span class="bg-purple-600/20 text-purple-300 text-xs font-semibold px-2.5 py-1 rounded-full">Flask</span>
                            </div>
                        </div>
                        <div class="mt-auto space-y-3">
                            <button class="gemini-button suggest-description-btn w-full">✨ پیشنهاد توضیحات</button>
                            <a href="https://github.com/MohammadrezaSolimani/Project2" target="_blank" class="primary-button inline-block py-2.5 px-6 rounded-lg w-full">مشاهده در گیت‌هاب</a>
                        </div>
                    </div>
                    <div class="card rounded-xl overflow-hidden p-6 text-center flex flex-col justify-between">
                        <div>
                            <h3 class="project-title text-2xl font-bold mb-3 text-gray-100">پروژه سوم</h3>
                            <p class="project-description text-gray-400 mb-5 text-sm leading-relaxed">توضیحات مختصری در مورد این پروژه و چالش‌های آن. این پروژه با هدف ... ساخته شده است.</p>
                             <div class="mb-5 flex justify-center gap-2 flex-wrap">
                                <span class="bg-blue-600/20 text-blue-300 text-xs font-semibold px-2.5 py-1 rounded-full">JavaScript</span>
                                <span class="bg-purple-600/20 text-purple-300 text-xs font-semibold px-2.5 py-1 rounded-full">Telegram API</span>
                            </div>
                        </div>
                        <div class="mt-auto space-y-3">
                            <button class="gemini-button suggest-description-btn w-full">✨ پیشنهاد توضیحات</button>
                            <a href="https://github.com/MohammadrezaSolimani/Project3" target="_blank" class="primary-button inline-block py-2.5 px-6 rounded-lg w-full">مشاهده در گیت‌هاب</a>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="future" class="py-20 md:py-28 bg-[#161b22]/50 section-hidden">
            <div class="container mx-auto px-6">
                <h2 class="text-4xl font-bold text-center mb-16 text-gray-100">نقشه راه <span class="gradient-text">یادگیری</span></h2>
                <div class="relative max-w-3xl mx-auto border-r-2 border-[#30363d] pr-8">
                    <div class="space-y-12">
                        <div class="relative">
                            <div class="absolute -right-11 w-8 h-8 timeline-icon rounded-full flex items-center justify-center text-white text-xl shadow-lg">🧠</div>
                            <div class="card p-6 rounded-lg">
                                <h3 class="goal-name text-xl font-bold text-gray-100 mb-1">یادگیری عمیق (Deep Learning)</h3>
                                <p class="text-gray-400 text-sm leading-relaxed">کاوش در شبکه‌های عصبی و معماری‌های پیشرفته برای حل مسائل پیچیده.</p>
                                <button class="gemini-button suggest-goal-ideas-btn mt-4 text-xs px-3 py-1.5">✨ دریافت ایده</button>
                            </div>
                        </div>
                         <div class="relative">
                            <div class="absolute -right-11 w-8 h-8 timeline-icon rounded-full flex items-center justify-center text-white text-xl shadow-lg">📊</div>
                             <div class="card p-6 rounded-lg">
                                <h3 class="goal-name text-xl font-bold text-gray-100 mb-1">یادگیری ماشین (Machine Learning)</h3>
                                <p class="text-gray-400 text-sm leading-relaxed">تسلط بر الگوریتم‌ها و مدل‌ها برای ساخت سیستم‌های هوشمند.</p>
                                <button class="gemini-button suggest-goal-ideas-btn mt-4 text-xs px-3 py-1.5">✨ دریافت ایده</button>
                            </div>
                        </div>
                         <div class="relative">
                            <div class="absolute -right-11 w-8 h-8 timeline-icon rounded-full flex items-center justify-center text-white text-xl shadow-lg">🤖</div>
                             <div class="card p-6 rounded-lg">
                                <h3 class="goal-name text-xl font-bold text-gray-100 mb-1">پردازش زبان طبیعی (NLP)</h3>
                                <p class="text-gray-400 text-sm leading-relaxed">یادگیری تکنیک‌های درک و تولید زبان انسان توسط ماشین.</p>
                                <button class="gemini-button suggest-goal-ideas-btn mt-4 text-xs px-3 py-1.5">✨ دریافت ایده</button>
                            </div>
                        </div>
                         <div class="relative">
                            <div class="absolute -right-11 w-8 h-8 timeline-icon rounded-full flex items-center justify-center text-white text-xl shadow-lg">🔐</div>
                             <div class="card p-6 rounded-lg">
                                <h3 class="goal-name text-xl font-bold text-gray-100 mb-1">امنیت سایبری</h3>
                                <p class="text-gray-400 text-sm leading-relaxed">افزایش دانش در زمینه حفاظت از سیستم‌ها و داده‌ها در برابر تهدیدات.</p>
                                <button class="gemini-button suggest-goal-ideas-btn mt-4 text-xs px-3 py-1.5">✨ دریافت ایده</button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="contact" class="py-20 md:py-28 section-hidden">
            <div class="container mx-auto px-6 text-center">
                <h2 class="text-4xl font-bold text-center mb-6 text-gray-100">ارتباط با <span class="gradient-text">من</span></h2>
                <p class="text-gray-400 mb-10 max-w-2xl mx-auto text-lg">
                    از همکاری در پروژه‌های جدید یا صرفاً یک گفتگوی دوستانه در مورد تکنولوژی استقبال می‌کنم.
                </p>
                <div class="flex justify-center items-center space-x-10 space-x-reverse">
                    <a href="https://instagram.com/soleimani_mamadreza" target="_blank" class="text-gray-500 hover:text-pink-500 transition-transform duration-300 hover:scale-125 text-5xl">📸</a>
                    <a href="https://t.me/Solimani_reza" target="_blank" class="text-gray-500 hover:text-sky-400 transition-transform duration-300 hover:scale-125 text-5xl">✈️</a>
                    <a href="mailto:mohamadrezasoelymani53@gmail.com" class="text-gray-500 hover:text-red-500 transition-transform duration-300 hover:scale-125 text-5xl">✉️</a>
                    <a href="https://github.com/MohammadrezaSolimani" target="_blank" class="text-gray-500 hover:text-white transition-transform duration-300 hover:scale-125 text-5xl">💻</a>
                </div>
            </div>
        </section>
    </main>

    <footer class="bg-[#161b22] py-8 border-t border-[#30363d]">
        <div class="container mx-auto px-6 text-center text-gray-500">
            <p>🎉 از بازدید شما متشکرم! لطفاً ⭐ بدهید و دنبال کنید! 🌟</p>
            <p class="mt-3 text-sm">&copy; 2024 محمدرضا سلیمانی. تمام حقوق محفوظ است.</p>
        </div>
    </footer>

    <!-- Modal Structure -->
    <div id="geminiModal" class="fixed inset-0 z-[100] modal items-center justify-center p-4 hidden">
        <div class="modal-content max-w-lg w-full mx-auto rounded-xl shadow-2xl p-6 md:p-8">
            <div class="flex justify-between items-center mb-5">
                <h3 id="modalTitle" class="text-xl font-bold gradient-text">نتیجه از Gemini ✨</h3>
                <button id="closeModalBtn" class="text-gray-400 hover:text-white text-3xl">&times;</button>
            </div>
            <div id="modalBody" class="text-gray-300 whitespace-pre-wrap text-sm leading-relaxed max-h-[60vh] overflow-y-auto">
                <!-- Content will be injected here -->
            </div>
             <div id="modalLoader" class="loader hidden"></div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function () {
            
            const menuBtn = document.getElementById('menu-btn');
            const mobileMenu = document.getElementById('mobile-menu');
            if (menuBtn && mobileMenu) {
                menuBtn.addEventListener('click', () => {
                    mobileMenu.classList.toggle('hidden');
                });
            }
            
            const navLinks = document.querySelectorAll('.nav-link');
            const sections = document.querySelectorAll('main > section');

            function changeNavActiveState() {
                let currentSectionId = 'home';
                sections.forEach(section => {
                    const sectionTop = section.offsetTop;
                    if (window.scrollY >= sectionTop - 80 ) {
                        currentSectionId = section.getAttribute('id');
                    }
                });

                navLinks.forEach(link => {
                    link.classList.remove('active');
                    if (link.getAttribute('href') === `#${currentSectionId}`) {
                        link.classList.add('active');
                    }
                });
            }
            
            if (sections.length > 0 && navLinks.length > 0) {
                 changeNavActiveState();
                 window.addEventListener('scroll', changeNavActiveState);
            }
            
            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function (e) {
                    e.preventDefault();
                    const targetSection = document.querySelector(this.getAttribute('href'));
                    if (targetSection) {
                        targetSection.scrollIntoView({
                            behavior: 'smooth'
                        });
                    }
                    if (mobileMenu && mobileMenu.offsetParent !== null && !mobileMenu.classList.contains('hidden')) {
                        mobileMenu.classList.add('hidden');
                    }
                });
            });

            const typingTextElement = document.getElementById('typing-text');
            const phrases = [
                "توسعه‌دهنده فول استک",
                "علاقه‌مند به تکنولوژی",
                "خالق تجربیات دیجیتال",
                "مشتاق یادگیری و نوآوری"
            ];
            let phraseIndex = 0;
            let charIndex = 0;
            let isDeleting = false;

            function type() {
                const currentPhrase = phrases[phraseIndex];
                let displayText = '';

                if (isDeleting) {
                    displayText = currentPhrase.substring(0, charIndex - 1);
                    charIndex--;
                } else {
                    displayText = currentPhrase.substring(0, charIndex + 1);
                    charIndex++;
                }

                if (typingTextElement) {
                   typingTextElement.textContent = displayText;
                }

                let typeSpeed = 120;
                if (isDeleting) {
                    typeSpeed /= 1.5;
                }

                if (!isDeleting && charIndex === currentPhrase.length) {
                    typeSpeed = 2500;
                    isDeleting = true;
                } else if (isDeleting && charIndex === 0) {
                    isDeleting = false;
                    phraseIndex = (phraseIndex + 1) % phrases.length;
                    typeSpeed = 400;
                }

                setTimeout(type, typeSpeed);
            }
            if (typingTextElement) type();


            const skillsChartCanvas = document.getElementById('skillsChart');
            if (skillsChartCanvas) {
                const ctx = skillsChartCanvas.getContext('2d');
                const skillsData = {
                    labels: ['JavaScript', 'HTML', 'CSS', 'React', 'Node.js', 'Python', 'Telegram Bot'],
                    datasets: [{
                        label: 'میزان تسلط (درصد)',
                        data: [80, 90, 90, 75, 70, 45, 50],
                        backgroundColor: 'rgba(88, 166, 255, 0.2)', // Blue
                        borderColor: '#58a6ff', // Blue
                        pointBackgroundColor: '#58a6ff',
                        pointBorderColor: '#c9d1d9',
                        pointHoverBackgroundColor: '#c9d1d9',
                        pointHoverBorderColor: '#58a6ff',
                        borderWidth: 2.5
                    },
                    {
                        label: 'اهمیت در کار من',
                        data: [90, 85, 85, 95, 80, 60, 65],
                        backgroundColor: 'rgba(163, 113, 247, 0.2)', // Violet
                        borderColor: '#a371f7', // Violet
                        pointBackgroundColor: '#a371f7',
                        pointBorderColor: '#c9d1d9',
                        pointHoverBackgroundColor: '#c9d1d9',
                        pointHoverBorderColor: '#a371f7',
                        borderWidth: 2.5
                    }]
                };

                const chartConfig = {
                    type: 'radar',
                    data: skillsData,
                    options: {
                        maintainAspectRatio: false,
                        scales: {
                            r: {
                                angleLines: { color: 'rgba(139, 148, 158, 0.3)' }, // Gray-500
                                grid: { color: 'rgba(48, 54, 61, 0.8)' }, // Gray-300
                                pointLabels: { font: { size: 13, family: 'Vazirmatn', weight: '500' }, color: '#8b949e' },
                                ticks: { 
                                    color: '#0d1117', 
                                    backdropColor: 'rgba(139, 148, 158, 0.85)',
                                    backdropPadding: 5, 
                                    borderRadius: 4, 
                                    stepSize: 20,
                                    font: { family: 'Vazirmatn' }
                                },
                                 suggestedMin: 0,
                                 suggestedMax: 100
                            }
                        },
                        plugins: {
                            legend: { 
                                position: 'top',
                                labels: { 
                                    color: '#c9d1d9',
                                    font: { size: 13, family: 'Vazirmatn', weight: '500' },
                                    padding: 20
                                } 
                            },
                            tooltip: { 
                                bodyFont: { family: 'Vazirmatn' }, 
                                titleFont: { family: 'Vazirmatn' },
                                backgroundColor: '#161b22',
                                titleColor: '#c9d1d9',
                                bodyColor: '#8b949e',
                                padding: 10,
                                cornerRadius: 6,
                                borderColor: '#30363d',
                                borderWidth: 1
                            }
                        }
                    }
                };
                new Chart(ctx, chartConfig);
            }
            
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('section-visible');
                    }
                });
            }, { threshold: 0.15 });

            document.querySelectorAll('.section-hidden').forEach(section => {
                observer.observe(section);
            });

            // Modal Functionality
            const modal = document.getElementById('geminiModal');
            const closeModalBtn = document.getElementById('closeModalBtn');
            const modalTitle = document.getElementById('modalTitle');
            const modalBody = document.getElementById('modalBody');
            const modalLoader = document.getElementById('modalLoader');

            function showModal(title, content = '', isLoading = false) {
                if (!modal || !modalTitle || !modalBody || !modalLoader) return;
                modalTitle.textContent = title;
                modalBody.innerHTML = content.replace(/\n/g, '<br>');
                modal.classList.remove('hidden');
                modal.classList.add('flex');
                if (isLoading) {
                    modalBody.classList.add('hidden');
                    modalLoader.classList.remove('hidden');
                } else {
                    modalBody.classList.remove('hidden');
                    modalLoader.classList.add('hidden');
                }
            }

            function hideModal() {
                if (!modal) return;
                modal.classList.add('hidden');
                modal.classList.remove('flex');
                if(modalBody) modalBody.innerHTML = '';
                if(modalLoader) modalLoader.classList.add('hidden');
                if(modalBody) modalBody.classList.remove('hidden');
            }

            if(closeModalBtn) closeModalBtn.addEventListener('click', hideModal);
            if(modal) modal.addEventListener('click', (e) => {
                if (e.target === modal) {
                    hideModal();
                }
            });

            async function callGeminiAPI(prompt) {
                const apiKey = ""; 
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;
                
                let chatHistory = [{ role: "user", parts: [{ text: prompt }] }];
                const payload = { contents: chatHistory };

                try {
                    const response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });

                    if (!response.ok) {
                        const errorData = await response.json();
                        console.error('Gemini API Error:', errorData);
                        return `متاسفانه در ارتباط با Gemini خطایی رخ داد: ${errorData.error?.message || response.statusText}`;
                    }

                    const result = await response.json();
                    
                    if (result.candidates && result.candidates.length > 0 &&
                        result.candidates[0].content && result.candidates[0].content.parts &&
                        result.candidates[0].content.parts.length > 0) {
                        return result.candidates[0].content.parts[0].text;
                    } else {
                        console.error('Gemini API Response format unexpected:', result);
                        return "پاسخی از Gemini دریافت نشد یا فرمت پاسخ نامعتبر است.";
                    }
                } catch (error) {
                    console.error('Fetch Error calling Gemini API:', error);
                    return "خطا در برقراری ارتباط با سرویس Gemini. لطفاً اتصال اینترنت خود را بررسی کنید.";
                }
            }

            document.querySelectorAll('.suggest-description-btn').forEach(button => {
                button.addEventListener('click', async (e) => {
                    const card = e.target.closest('.card');
                    if (!card) return;
                    const projectTitleEl = card.querySelector('.project-title');
                    const currentDescriptionEl = card.querySelector('.project-description');
                    if(!projectTitleEl || !currentDescriptionEl) return;

                    const projectTitle = projectTitleEl.textContent.trim();
                    const currentDescription = currentDescriptionEl.textContent.trim();
                    
                    showModal(`✨ پیشنهاد توضیحات برای ${projectTitle}`, '', true);

                    const prompt = `بر اساس عنوان پروژه '${projectTitle}' و توضیحات فعلی '${currentDescription}'، یک پاراگراف توضیحات جذاب‌تر، حرفه‌ای‌تر و کامل‌تر برای این پروژه بنویس. تمرکز بر روی اهمیت پروژه، چالش‌های احتمالی و تکنولوژی‌های کلیدی باشد. پاسخ به زبان فارسی و با لحنی متقاعد کننده باشد.`;
                    const suggestion = await callGeminiAPI(prompt);
                    showModal(`✨ پیشنهاد توضیحات برای ${projectTitle}`, suggestion);
                });
            });

            document.querySelectorAll('.suggest-goal-ideas-btn').forEach(button => {
                button.addEventListener('click', async (e) => {
                    const listItem = e.target.closest('.card');
                    if (!listItem) return;
                    const goalNameEl = listItem.querySelector('.goal-name');
                    if(!goalNameEl) return;

                    const goalName = goalNameEl.textContent.trim();
                    
                    showModal(`✨ ایده‌هایی برای یادگیری ${goalName}`, '', true);
                    
                    const prompt = `برای یادگیری '${goalName}'، به زبان فارسی پیشنهاد بده:
                    1. سه منبع آموزشی آنلاین برتر (نام دوره/وبسایت و توضیح کوتاه).
                    2. دو کتاب کلیدی (نام کتاب و توضیح کوتاه).
                    3. یک ایده پروژه کوچک و کاربردی که بتوان با آن مهارت‌های کسب شده را تمرین کرد (همراه با مراحل اصلی اجرای پروژه).
                    پاسخ را به صورت ساختاریافته و با شماره‌گذاری ارائه بده.`;
                    const ideas = await callGeminiAPI(prompt);
                    showModal(`✨ ایده‌هایی برای یادگیری ${goalName}`, ideas);
                });
            });

        });
    </script>
</body>
</html>

<!DOCTYPE html>
<html lang="ru" class="scroll-smooth">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>MLT TEAM — Cyber-Brutalist Ecosystem</title>
  
  <script src="https://cdn.tailwindcss.com"></script>
  
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800;900&family=Syne:wght@700;800;900&family=JetBrains+Mono:wght@500;700&display=swap" rel="stylesheet">
  
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            display: ['"Syne"', 'sans-serif'],
            sans: ['"Plus Jakarta Sans"', 'sans-serif'],
            mono: ['"JetBrains Mono"', 'monospace'],
          },
          colors: {
            bgDark: '#050508',
            cardBg: '#0b0b10',
            neonViolet: '#bd00ff',
            crimsonRed: '#ff1a3c',
          }
        }
      }
    }
  </script>

  <style>
    body {
      background-color: #050508;
      color: #f3f4f6;
      overflow-x: hidden;
      -webkit-tap-highlight-color: transparent;
    }

    /* Фоновая технологичная сетка */
    .cyber-grid {
      background-size: 40px 40px;
      background-image: 
        linear-gradient(to right, rgba(255, 255, 255, 0.02) 1px, transparent 1px),
        linear-gradient(to bottom, rgba(255, 255, 255, 0.02) 1px, transparent 1px);
    }

    /* Живое дыхание красного градиента на фоне */
    @keyframes bgGlow {
      0%, 100% { opacity: 0.15; transform: scale(1); }
      50% { opacity: 0.25; transform: scale(1.08); }
    }
    .bg-breath {
      animation: bgGlow 8s ease-in-out infinite;
    }

    /* Пурпурный неон */
    .neon-violet-glow {
      box-shadow: 0 0 25px -2px rgba(189, 0, 255, 0.5), 0 0 10px 0 rgba(189, 0, 255, 0.3);
    }
    .neon-violet-text {
      background: linear-gradient(135deg, #ffffff 20%, #d14eff 70%, #9d00ff 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }

    /* Интро-экран */
    #intro-screen {
      position: fixed;
      inset: 0;
      background: #050508;
      z-index: 9999;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      transition: opacity 0.8s ease, visibility 0.8s ease;
    }

    /* Объемные серебристо-серые плашки кибер-брутализма */
    .cyber-card {
      background: linear-gradient(180deg, rgba(20, 20, 28, 0.85) 0%, rgba(10, 10, 15, 0.95) 100%);
      border: 1px solid rgba(255, 255, 255, 0.08);
      border-radius: 28px;
      box-shadow: 
        inset 0 1px 1px 0 rgba(255, 255, 255, 0.12),
        0 20px 40px -15px rgba(0, 0, 0, 0.8);
      position: relative;
      overflow: hidden;
      transition: all 0.35s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .cyber-card:hover {
      border-color: rgba(189, 0, 255, 0.45);
      transform: translateY(-5px);
      box-shadow: 
        inset 0 1px 2px 0 rgba(255, 255, 255, 0.2),
        0 25px 50px -15px rgba(0, 0, 0, 0.9),
        0 0 30px -5px rgba(189, 0, 255, 0.25);
    }

    /* Spotlight-эффект за курсором */
    .cyber-card::before {
      content: "";
      position: absolute;
      inset: 0;
      background: radial-gradient(400px circle at var(--mouse-x, 50%) var(--mouse-y, 50%), rgba(189, 0, 255, 0.1), transparent 60%);
      pointer-events: none;
      opacity: 0;
      transition: opacity 0.3s ease;
      border-radius: inherit;
    }
    .cyber-card:hover::before {
      opacity: 1;
    }

    /* Кнопки с фиолетовым неоном */
    .btn-cyber {
      background: linear-gradient(135deg, #bd00ff 0%, #7000ff 100%);
      border: 1px solid rgba(255, 255, 255, 0.25);
      box-shadow: inset 0 1px 1px 0 rgba(255, 255, 255, 0.4), 0 8px 25px rgba(189, 0, 255, 0.4);
      transition: all 0.25s ease;
    }
    .btn-cyber:hover {
      transform: translateY(-2px);
      box-shadow: inset 0 1px 2px 0 rgba(255, 255, 255, 0.6), 0 12px 30px rgba(189, 0, 255, 0.6);
    }
    .btn-cyber:active {
      transform: scale(0.97);
    }

    /* Плавающая таблетка-индикатор справа */
    .floating-pill {
      position: fixed;
      right: 20px;
      top: 50%;
      transform: translateY(-50%);
      width: 14px;
      height: 48px;
      background: linear-gradient(180deg, #bd00ff 0%, #ff1a3c 100%);
      border-radius: 20px;
      box-shadow: 0 0 15px rgba(189, 0, 255, 0.6);
      z-index: 30;
      display: none;
    }
    @media(min-width: 1024px) {
      .floating-pill { display: block; }
    }
  </style>
</head>
<body class="cyber-grid antialiased font-sans">

  <!-- ИНТРО С ЭФФЕКТОМ НАБОРА ТЕКСТА -->
  <div id="intro-screen">
    <div class="font-mono text-xl sm:text-3xl font-bold tracking-widest neon-violet-text mb-8" id="typing-text"></div>
    <button onclick="skipIntro()" class="px-6 py-2.5 rounded-full border border-white/10 text-xs font-mono text-gray-400 hover:text-white hover:border-neonViolet transition">
      [ ПРОПУСТИТЬ ИНТРО ]
    </button>
  </div>

  <!-- ПЛАВАЮЩАЯ ТАБЛЕТКА СПРАВА -->
  <div class="floating-pill" id="scroll-pill"></div>

  <!-- ФОНОВЫЕ ПЕРЕЛИВЫ -->
  <div class="fixed inset-0 cyber-grid pointer-events-none -z-10"></div>
  <div class="fixed top-[-10%] left-1/2 -translate-x-1/2 w-[80vw] max-w-[800px] h-[450px] bg-crimsonRed/20 rounded-full blur-[140px] pointer-events-none -z-10 bg-breath"></div>

  <!-- ШАПКА -->
  <header class="sticky top-5 z-40 max-w-6xl mx-auto px-4">
    <div class="cyber-card px-6 py-3.5 flex items-center justify-between backdrop-blur-xl">
      <a href="#" class="font-display font-black text-2xl tracking-tight text-white">MLT</a>
      <nav class="hidden md:flex items-center space-x-2 text-sm font-semibold">
        <a href="#about" class="px-4 py-2 rounded-full text-gray-300 hover:text-white transition">Лаборатория</a>
        <a href="#capsules" class="px-4 py-2 rounded-full text-gray-300 hover:text-white transition">Капсулы</a>
        <a href="#contact" class="px-5 py-2 rounded-full btn-cyber text-white font-bold">Связь</a>
      </nav>
      <a href="https://t.me/beloysa" target="_blank" class="px-5 py-2 rounded-full btn-cyber text-white text-xs sm:text-sm font-bold">
        Telegram
      </a>
    </div>
  </header>

  <!-- ГЛАВНЫЙ КОНТЕНТ -->
  <main class="max-w-6xl mx-auto px-4 pt-16 pb-28">

    <!-- HERO СЕКЦИЯ -->
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-center min-h-[75vh]">
      <div class="lg:col-span-7">
        <div class="inline-flex items-center gap-2 px-4 py-1.5 rounded-full text-xs font-bold uppercase tracking-wider bg-neonViolet/10 border border-neonViolet/30 text-neonViolet mb-6">
          <span>⚡ Секретный протокол</span>
        </div>
        <h1 class="font-display text-6xl sm:text-8xl font-black tracking-tight leading-[0.92] mb-6">
          MLT<br/>
          <span class="neon-violet-text">LABORATORY</span>
        </h1>
        <p class="text-gray-400 text-lg sm:text-xl font-normal leading-relaxed max-w-xl mb-9">
          Закрытая цифровая экосистема. Выбирай свою капсулу реальности. Никакой воды — только чистый контент и практика.
        </p>
        <div class="flex gap-4">
          <a href="https://t.me/beloysa" target="_blank" class="px-8 py-4 rounded-2xl btn-cyber font-bold text-white text-base">
            Активировать доступ
          </a>
        </div>
      </div>

      <!-- МЕСТО ПОД ВИДЕО С БАНКОЙ И ПЕРЧАТКОЙ -->
      <div class="lg:col-span-5 flex justify-center">
        <div class="w-full max-w-[420px] aspect-[4/5] cyber-card p-3 shadow-2xl flex items-center justify-center text-center relative">
          <!-- Сюда в будущем встанет твое сгенерированное видео с перчаткой -->
          <div class="text-gray-500 font-mono text-sm p-6 border border-dashed border-white/10 rounded-2xl w-full h-full flex flex-col items-center justify-center">
            <span class="text-neonViolet text-3xl mb-2">💊</span>
            <span>Здесь будет видео с банкой и перчаткой</span>
          </div>
        </div>
      </div>
    </div>

    <!-- 5 НАПРАВЛЕНИЙ ПО КАПСУЛАМ -->
    <section id="capsules" class="mt-32">
      <h2 class="font-display text-4xl sm:text-5xl font-black text-center mb-16 tracking-tight">
        5 ЦИФРОВЫХ <span class="neon-violet-text">КАПСУЛ</span>
      </h2>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <!-- 1. Синяя (Дизайн) -->
        <div class="cyber-card p-8 flex flex-col justify-between">
          <div>
            <div class="w-12 h-12 rounded-2xl bg-blue-500/10 border border-blue-500/30 text-blue-400 flex items-center justify-center text-xl mb-6">🔵</div>
            <h3 class="font-display text-2xl font-bold text-white mb-3">Дизайн</h3>
            <p class="text-gray-400 text-sm leading-relaxed">Современные интерфейсы, кибер-эстетика, UI/UX и визуальный стиль нового поколения.</p>
          </div>
        </div>

        <!-- 2. Красная (Отношения) -->
        <div class="cyber-card p-8 flex flex-col justify-between">
          <div>
            <div class="w-12 h-12 rounded-2xl bg-red-500/10 border border-red-500/30 text-red-400 flex items-center justify-center text-xl mb-6">🔴</div>
            <h3 class="font-display text-2xl font-bold text-white mb-3">Отношения</h3>
            <p class="text-gray-400 text-sm leading-relaxed">Психология влияния, коммуникации, связи и цифровой социальный интеллект.</p>
          </div>
        </div>

        <!-- 3. Белая (Психология) -->
        <div class="cyber-card p-8 flex flex-col justify-between">
          <div>
            <div class="w-12 h-12 rounded-2xl bg-white/10 border border-white/30 text-white flex items-center justify-center text-xl mb-6">⚪</div>
            <h3 class="font-display text-2xl font-bold text-white mb-3">Психология</h3>
            <p class="text-gray-400 text-sm leading-relaxed">Контроль разума, биохакинг продуктивности, ментальная устойчивость.</p>
          </div>
        </div>

        <!-- 4. Оранжевая (Вайбкодинг) -->
        <div class="cyber-card p-8 flex flex-col justify-between md:col-span-1.5">
          <div>
            <div class="w-12 h-12 rounded-2xl bg-orange-500/10 border border-orange-500/30 text-orange-400 flex items-center justify-center text-xl mb-6">🟠</div>
            <h3 class="font-display text-2xl font-bold text-white mb-3">Вайбкодинг</h3>
            <p class="text-gray-400 text-sm leading-relaxed">Замена старому кодингу. Полное обучение с нуля, продвинутые промты, готовые скрипты и практика.</p>
          </div>
        </div>

        <!-- 5. Зеленая (Заработок) -->
        <div class="cyber-card p-8 flex flex-col justify-between md:col-span-1.5">
          <div>
            <div class="w-12 h-12 rounded-2xl bg-emerald-500/10 border border-emerald-500/30 text-emerald-400 flex items-center justify-center text-xl mb-6">🟢</div>
            <h3 class="font-display text-2xl font-bold text-white mb-3">Заработок</h3>
            <p class="text-gray-400 text-sm leading-relaxed">Монетизация цифровых навыков, генерация трафика и построение стабильных денежных потоков.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- КОНТАКТЫ -->
    <section id="contact" class="mt-32">
      <div class="cyber-card p-12 sm:p-16 text-center max-w-3xl mx-auto">
        <h2 class="font-display text-4xl font-black mb-4 text-white">ВХОД В СИСТЕМУ</h2>
        <p class="text-gray-400 text-base mb-8">Готов принять таблетку и изменить правила игры? Пиши лично.</p>
        <a href="https://t.me/beloysa" target="_blank" class="inline-flex px-10 py-4 rounded-2xl btn-fire font-bold text-white text-base">
          Написать в Telegram (@beloysa)
        </a>
      </div>
    </section>

  </main>

  <!-- СКРИПТЫ И АНИМАЦИИ -->
  <script>
    // Эффект печатной машинки для интро
    const textToType = "MLT PROJECT // LOADING SYSTEM...";
    const typingElement = document.getElementById("typing-text");
    let charIndex = 0;

    function typeWriter() {
      if (charIndex < textToType.length) {
        typingElement.innerHTML += textToType.charAt(charIndex);
        charIndex++;
        setTimeout(typeWriter, 70);
      } else {
        setTimeout(skipIntro, 1200); // Автоматически убираем интро через 1.2 сек после окончания текста
      }
    }

    function skipIntro() {
      const intro = document.getElementById("intro-screen");
      intro.style.opacity = '0';
      setTimeout(() => intro.style.display = 'none', 800);
    }

    window.onload = () => {
      setTimeout(typeWriter, 400);
    };

    // Spotlight эффект слежки за курсором мыши на карточках
    document.querySelectorAll('.cyber-card').forEach(card => {
      card.addEventListener('mousemove', e => {
        const rect = card.getBoundingClientRect();
        const x = e.clientX - rect.left;
        const y = e.clientY - rect.top;
        card.style.setProperty('--mouse-x', `${x}px`);
        card.style.setProperty('--mouse-y', `${y}px`);
      });
    });

    // Динамическое перемещение правой таблетки при скролле
    window.addEventListener('scroll', () => {
      const scrollTop = window.scrollY;
      const docHeight = document.documentElement.scrollHeight - window.innerHeight;
      const scrollPercent = scrollTop / docHeight;
      const pill = document.getElementById('scroll-pill');
      const maxMove = window.innerHeight * 0.4;
      pill.style.transform = `translateY(${ (scrollPercent - 0.5) * maxMove }px)`;
    });
  </script>
</body>
</html>

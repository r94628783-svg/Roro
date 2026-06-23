<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <title>ورشة البشمهندس أمجد - بطل نكد</title>

    <!-- ===== GSAP ===== -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js">
    </script>

    <style>
        /* ============================================================
                   RESET & BASE
                   ============================================================ */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', 'Tahoma', system-ui, sans-serif;
            background: #fcf9f0;
            /* كريمي فاتح */
            min-height: 100vh;
            overflow-x: hidden;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        /* ============================================================
                   LOADER (شاشة التحميل)
                   ============================================================ */
        #loader {
            position: fixed;
            inset: 0;
            z-index: 9999;
            background: #fcf9f0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            transition: opacity 0.9s ease, transform 0.9s ease;
        }
        #loader.hide {
            opacity: 0;
            transform: scale(1.1);
            pointer-events: none;
        }

        /* العربية الكرتونية المتعطلة */
        .loader-car {
            font-size: 5.5rem;
            line-height: 1;
            position: relative;
            animation: carShake 0.35s infinite alternate ease-in-out;
        }
        .loader-car .smoke {
            position: absolute;
            top: -20px;
            right: -10px;
            font-size: 2.8rem;
            opacity: 0.7;
            animation: smokePuff 0.9s infinite alternate ease-in-out;
        }
        .loader-car .girl {
            position: absolute;
            bottom: -10px;
            left: -35px;
            font-size: 2.8rem;
            animation: girlPush 0.5s infinite alternate ease-in-out;
        }

        @keyframes carShake {
            0% {
                transform: rotate(-2deg) translateX(-3px);
            }
            100% {
                transform: rotate(2deg) translateX(3px);
            }
        }
        @keyframes smokePuff {
            0% {
                opacity: 0.3;
                transform: scale(0.9) translateY(0);
            }
            100% {
                opacity: 1;
                transform: scale(1.3) translateY(-12px);
            }
        }
        @keyframes girlPush {
            0% {
                transform: translateX(-6px) rotate(-5deg);
            }
            100% {
                transform: translateX(6px) rotate(5deg);
            }
        }

        /* شريط التحميل على شكل مفتاح إنجليزي */
        .loader-bar-wrap {
            width: 280px;
            max-width: 80vw;
            margin-top: 2rem;
            background: #e8e0d0;
            border-radius: 40px;
            padding: 5px;
            box-shadow: inset 0 2px 6px rgba(0, 0, 0, 0.1);
            position: relative;
        }
        .loader-bar {
            height: 22px;
            border-radius: 40px;
            width: 0%;
            background: linear-gradient(90deg, #f9d56e, #f8b042, #f9d56e);
            background-size: 200% 100%;
            animation: shimmer 1.2s infinite linear;
            transition: width 0.15s linear;
            box-shadow: 0 0 14px #f9d56e88;
        }
        @keyframes shimmer {
            0% {
                background-position: 200% 0;
            }
            100% {
                background-position: -200% 0;
            }
        }

        .loader-label {
            margin-top: 1rem;
            font-size: 1rem;
            font-weight: 600;
            color: #4a3f35;
            letter-spacing: 0.5px;
            background: #f5efe4;
            padding: 0.4rem 1.6rem;
            border-radius: 40px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
        }

        /* ============================================================
                   MAIN WRAPPER
                   ============================================================ */
        .app {
            width: 100%;
            max-width: 480px;
            /* عرض طولي للموبايل */
            padding: 1.2rem 1rem 2.5rem;
            display: none;
            /* يظهر بعد اختفاء loader */
            flex-direction: column;
            align-items: center;
            gap: 1.6rem;
            background: #fcf9f0;
            min-height: 100vh;
        }
        .app.show {
            display: flex;
        }

        /* ============================================================
                   HEADER – يافطة "بطل نكد" بخشب وسلاسل
                   ============================================================ */
        .header {
            width: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            padding: 0.6rem 0.8rem;
            background: #f5efe4;
            border-radius: 60px;
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.06);
            position: relative;
            border: 2px solid #dacfbc;
        }

        /* اليافطة الخشبية المتحركة */
        .sign {
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.3rem;
            padding: 0.3rem 1.4rem 0.3rem 1rem;
            background: #c8a87c;
            /* خشب */
            border-radius: 14px 4px 14px 4px;
            box-shadow: 0 4px 0 #a8885e, inset 0 -2px 0 #b4946a;
            transform-origin: top center;
            animation: signSwing 3.5s infinite alternate ease-in-out;
            border: 1px solid #b0885a;
        }
        /* السلاسل الحديد */
        .sign::before,
        .sign::after {
            content: "⛓️";
            font-size: 1.2rem;
            position: absolute;
            top: -22px;
            filter: grayscale(0.4);
        }
        .sign::before {
            left: 8px;
            transform: rotate(-12deg);
        }
        .sign::after {
            right: 8px;
            transform: rotate(12deg);
        }

        @keyframes signSwing {
            0% {
                transform: rotate(-3deg);
            }
            100% {
                transform: rotate(3deg);
            }
        }

        .sign-text {
            font-size: 1.5rem;
            font-weight: 900;
            color: #fff6e0;
            text-shadow: 2px 2px 0 #7a5f3e, 4px 4px 0 #5a4a2e;
            letter-spacing: 1px;
            font-family: 'Comic Sans MS', 'Segoe UI', cursive;
        }

        /* لوجو القلب + مفتاح */
        .logo-icon {
            font-size: 2.2rem;
            animation: heartBeat 1.2s infinite ease-in-out;
            display: inline-block;
            filter: drop-shadow(0 2px 6px rgba(200, 50, 50, 0.3));
        }
        @keyframes heartBeat {
            0%,
            100% {
                transform: scale(1);
            }
            15% {
                transform: scale(1.25);
            }
            30% {
                transform: scale(1);
            }
            45% {
                transform: scale(1.15);
            }
            60% {
                transform: scale(1);
            }
        }

        /* ============================================================
                   COUNTER – عداد الأعطال
                   ============================================================ */
        .counter-box {
            width: 100%;
            background: #f5efe4;
            border-radius: 40px;
            padding: 1.4rem 1rem 1.2rem;
            box-shadow: inset 0 -4px 0 #dacfbc, 0 8px 24px rgba(0, 0, 0, 0.04);
            border: 2px solid #e4d9c6;
            text-align: center;
        }

        .counter-label {
            font-size: 0.85rem;
            font-weight: 700;
            color: #6a5e4e;
            letter-spacing: 1px;
            text-transform: uppercase;
            margin-bottom: 0.5rem;
        }

        .gauge-wrap {
            position: relative;
            width: 100%;
            max-width: 300px;
            margin: 0 auto;
        }

        .gauge-track {
            width: 100%;
            height: 18px;
            background: #e8e0d0;
            border-radius: 40px;
            overflow: hidden;
            box-shadow: inset 0 2px 6px rgba(0, 0, 0, 0.08);
            position: relative;
        }

        .gauge-fill {
            height: 100%;
            width: 18%;
            /* يبدأ في المنطقة الحمراء */
            background: linear-gradient(90deg, #e74c3c, #f1948a);
            border-radius: 40px;
            transition: width 1.2s cubic-bezier(0.34, 1.56, 0.64, 1);
            box-shadow: 0 0 18px #e74c3c66;
        }

        .gauge-labels {
            display: flex;
            justify-content: space-between;
            font-size: 0.7rem;
            font-weight: 700;
            color: #5a4f40;
            margin-top: 4px;
            padding: 0 4px;
        }
        .gauge-labels span:last-child {
            color: #27ae60;
        }

        .warning-light {
            display: inline-block;
            margin-top: 0.6rem;
            padding: 0.2rem 1rem;
            border-radius: 40px;
            background: #e74c3c;
            color: #fff;
            font-weight: 700;
            font-size: 0.75rem;
            letter-spacing: 0.5px;
            box-shadow: 0 0 16px #e74c3c88;
            animation: blinkLight 1s infinite alternate;
            transition: background 0.6s, box-shadow 0.6s;
        }
        .warning-light.green {
            background: #27ae60;
            box-shadow: 0 0 20px #27ae6088;
            animation: none;
        }
        @keyframes blinkLight {
            0% {
                opacity: 0.6;
            }
            100% {
                opacity: 1;
            }
        }

        /* ============================================================
                   IMAGE FRAME – الصورة المرفقة
                   ============================================================ */
        .image-frame {
            width: 100%;
            border-radius: 32px;
            background: #f5efe4;
            padding: 0.8rem;
            border: 3px solid #e4d9c6;
            box-shadow: 0 8px 28px rgba(0, 0, 0, 0.04);
            transition: transform 0.3s ease;
        }
        .image-frame:hover {
            transform: scale(1.005);
        }

        .image-frame-title {
            font-size: 0.75rem;
            font-weight: 700;
            color: #6a5e4e;
            text-align: center;
            letter-spacing: 0.5px;
            margin-bottom: 0.5rem;
            background: #e8e0d0;
            padding: 0.2rem 0;
            border-radius: 40px;
        }

        .image-frame img {
            width: 100%;
            height: auto;
            border-radius: 20px;
            display: block;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.04);
            background: #f0ebe0;
            /* fallback */
        }

        /* ============================================================
                   TRIGGER BUTTON – الزر الأحمر الضخم
                   ============================================================ */
        .trigger-btn {
            width: 100%;
            padding: 1.3rem 0.5rem;
            font-size: 1.6rem;
            font-weight: 900;
            color: #fff;
            background: linear-gradient(145deg, #e74c3c, #c0392b);
            border: none;
            border-radius: 60px;
            box-shadow: 0 10px 0 #922b21, 0 12px 32px rgba(231, 76, 60, 0.35);
            cursor: pointer;
            transition: all 0.08s linear;
            text-shadow: 2px 2px 0 #922b21;
            letter-spacing: 0.5px;
            transform: translateY(-4px);
            font-family: 'Comic Sans MS', 'Segoe UI', cursive;
        }
        .trigger-btn:active {
            transform: translateY(4px);
            box-shadow: 0 4px 0 #922b21, 0 8px 24px rgba(231, 76, 60, 0.3);
        }

        /* ============================================================
                   MODAL – نافذة الرسالة الكرتونية
                   ============================================================ */
        .modal-overlay {
            position: fixed;
            inset: 0;
            z-index: 9998;
            background: rgba(0, 0, 0, 0.35);
            backdrop-filter: blur(6px);
            display: none;
            align-items: center;
            justify-content: center;
            padding: 1.2rem;
            animation: modalFadeIn 0.5s ease;
        }
        .modal-overlay.open {
            display: flex;
        }

        @keyframes modalFadeIn {
            0% {
                opacity: 0;
                transform: scale(0.92);
            }
            100% {
                opacity: 1;
                transform: scale(1);
            }
        }

        .modal-card {
            max-width: 420px;
            width: 100%;
            background: #fcf9f0;
            border-radius: 48px 48px 32px 32px;
            padding: 2rem 1.4rem 1.8rem;
            box-shadow: 0 30px 60px rgba(0, 0, 0, 0.2);
            border: 4px solid #f5efe4;
            position: relative;
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-card h2 {
            font-size: 1.6rem;
            font-weight: 900;
            color: #c0392b;
            text-align: center;
            margin-bottom: 0.2rem;
            font-family: 'Comic Sans MS', 'Segoe UI', cursive;
        }
        .modal-card .subhead {
            text-align: center;
            font-size: 0.85rem;
            color: #7a6a5a;
            margin-bottom: 1rem;
            border-bottom: 2px dashed #e4d9c6;
            padding-bottom: 0.6rem;
        }

        .modal-message {
            font-size: 1.05rem;
            line-height: 1.8;
            color: #3d352a;
            background: #f5efe4;
            padding: 1rem 1.2rem;
            border-radius: 24px;
            white-space: pre-wrap;
            font-weight: 500;
            box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.02);
        }

        .modal-message .highlight {
            color: #c0392b;
            font-weight: 700;
        }

        .modal-close-btn {
            display: block;
            width: 100%;
            margin-top: 1.2rem;
            padding: 1rem;
            font-size: 1.3rem;
            font-weight: 800;
            background: linear-gradient(145deg, #f39c12, #e67e22);
            border: none;
            border-radius: 60px;
            color: #fff;
            box-shadow: 0 6px 0 #b86d1c, 0 8px 24px rgba(243, 156, 18, 0.3);
            cursor: pointer;
            transition: all 0.07s linear;
            transform: translateY(-3px);
            font-family: 'Comic Sans MS', 'Segoe UI', cursive;
            text-shadow: 1px 1px 0 #b86d1c;
        }
        .modal-close-btn:active {
            transform: translateY(4px);
            box-shadow: 0 2px 0 #b86d1c;
        }

        /* ============================================================
                   CONFETTI (تساقط القصاصات)
                   ============================================================ */
        .confetti-container {
            position: fixed;
            inset: 0;
            pointer-events: none;
            z-index: 9997;
            overflow: hidden;
        }
        .confetti-piece {
            position: absolute;
            width: 10px;
            height: 10px;
            opacity: 0.85;
            animation: confettiFall linear forwards;
        }
        @keyframes confettiFall {
            0% {
                transform: translateY(-20px) rotate(0deg) scale(0.6);
                opacity: 1;
            }
            100% {
                transform: translateY(110vh) rotate(720deg) scale(1);
                opacity: 0;
            }
        }

        /* ============================================================
                   FOOTER
                   ============================================================ */
        .footer {
            width: 100%;
            text-align: center;
            padding: 0.8rem 0 0.2rem;
            font-size: 0.7rem;
            color: #b5a692;
            border-top: 2px solid #ede5d6;
            margin-top: 0.6rem;
        }

        /* ============================================================
                   RESPONSIVE TWEAKS
                   ============================================================ */
        @media (max-width: 420px) {
            .sign-text {
                font-size: 1.2rem;
            }
            .logo-icon {
                font-size: 1.7rem;
            }
            .trigger-btn {
                font-size: 1.2rem;
                padding: 1rem 0.5rem;
            }
            .modal-message {
                font-size: 0.95rem;
                padding: 0.8rem 1rem;
            }
            .loader-car {
                font-size: 4.2rem;
            }
        }
    </style>
</head>

<body>

    <!-- ============================================================
    LOADER
    ============================================================ -->
    <div id="loader">
        <div class="loader-car">
            🚗
            <span class="smoke">💨</span>
            <span class="girl">👩🏻‍🔧</span>
        </div>

        <div class="loader-bar-wrap">
            <div class="loader-bar" id="loaderBar"></div>
        </div>
        <div class="loader-label">🔧 جاري فحص الموتور والبحث عن أسباب النكد... برجاء الانتظار</div>
    </div>

    <!-- ============================================================
    MAIN APP
    ============================================================ -->
    <div class="app" id="app">

        <!-- HEADER -->
        <header class="header">
            <div class="sign">
                <span class="sign-text">🏎️ بطل نكد</span>
            </div>
            <span class="logo-icon">❤️🔧</span>
        </header>

        <!-- COUNTER -->
        <section class="counter-box">
            <div class="counter-label">📊 عداد الأعطال</div>
            <div class="gauge-wrap">
                <div class="gauge-track">
                    <div class="gauge-fill" id="gaugeFill" style="width:18%;"></div>
                </div>
                <div class="gauge-labels">
                    <span>🔴 مَقموص / زعلان</span>
                    <span>🟢 رايق وبيقدم حب</span>
                </div>
            </div>
            <div class="warning-light" id="warningLight">⚠️ CHECK ENGINE</div>
        </section>

        <!-- IMAGE FRAME -->
        <div class="image-frame" id="imageFrame">
            <div class="image-frame-title">📸 تقرير الفحص الفني المصور لحالة الشد والجذب</div>
            <img
            src="https://files.catbox.moe/5ym3lp.png"
            alt="صورة البشمهندس أمجد"
            onerror="this.src='data:image/svg+xml,%3Csvg xmlns=%22http://www.w3.org/2000/svg%22 width=%22300%22 height=%22300%22%3E%3Crect fill=%22%23e8e0d0%22 width=%22300%22 height=%22300%22/%3E%3Ctext x=%2250%%22 y=%2250%%22 text-anchor=%22middle%22 dy=%22.3em%22 font-size=%2220%22 fill=%22%23908070%22%3E⚠️ الصورة غير متاحة%3C/text%3E%3C/svg%3E'"
            />
        </div>

        <!-- TRIGGER BUTTON -->
        <button class="trigger-btn" id="triggerBtn">🔧 اضغط هنا لفك العَمرة وتدوير الموتور</button>

        <!-- FOOTER -->
        <div class="footer">🚘 ورشة البشمهندس أمجد – صيانة العلاقات</div>
    </div>

    <!-- ============================================================
    MODAL
    ============================================================ -->
    <div class="modal-overlay" id="modalOverlay">
        <div class="modal-card">
            <h2>🛠️ رسالة فنية</h2>
            <div class="subhead">📋 تقرير الفحص النهائي</div>
            <div class="modal-message">
                بص يا بشمهندس أمجد.. مبدئيًا كده، الإنسان اللي معاه واحدة زيي مفروض ميزعلش أبدًا مهما اتنكد عليه، ده أنا نعمة! 😂

                بعدين أنت ميكانيكي, يعني مفروض أول ما تلاقيني عِطلت أو بلخبط، تدور على المشكلة وتحلها علطول.. ولا أنت طلعت ميكانيكي فاشل؟

                خلي بالك.. العربية اللي معاك دي موتورها غالي أوي ومش بيدور ولا بيليّن غير ليك أنت بس يا هندسة! 😉
                <span class="highlight">صالِحني بقى وبلاش قمص ميكانيكية.</span>
            </div>
            <button class="modal-close-btn" id="modalCloseBtn">✅ اضغط هنا للاعتراف بإن الموتور دار وبقيت تمام</button>
        </div>
    </div>

    <!-- ============================================================
    CONFETTI CONTAINER
    ============================================================ -->
    <div class="confetti-container" id="confettiContainer"></div>

    <!-- ============================================================
    SCRIPT
    ============================================================ -->
    <script>
        (function() {
            'use strict';

            // ---- elements ----
            const loader = document.getElementById('loader');
            const loaderBar = document.getElementById('loaderBar');
            const app = document.getElementById('app');
            const gaugeFill = document.getElementById('gaugeFill');
            const warningLight = document.getElementById('warningLight');
            const triggerBtn = document.getElementById('triggerBtn');
            const modalOverlay = document.getElementById('modalOverlay');
            const modalCloseBtn = document.getElementById('modalCloseBtn');
            const confettiContainer = document.getElementById('confettiContainer');

            // ---- 1) LOADER ----
            let progress = 0;
            const loadInterval = setInterval(function() {
                progress += Math.random() * 6 + 2;
                if (progress > 100) progress = 100;
                loaderBar.style.width = progress + '%';
                if (progress >= 100) {
                    clearInterval(loadInterval);
                    // hide loader after a tiny delay
                    setTimeout(function() {
                        loader.classList.add('hide');
                        app.classList.add('show');
                        // تشغيل الأغنية تلقائياً
                        playAudio();
                        // انيميشن دخول الصورة عند السكرول
                        animateImageOnScroll();
                    }, 400);
                }
            }, 120);

            // ---- 2) تشغيل الأغنية ----
            function playAudio() {
                try {
                    const audio = new Audio('https://files.catbox.moe/yyrr5o.mp3');
                    audio.loop = false;
                    audio.volume = 0.7;
                    audio.play().catch(function(e) {
                        // المستعرض قد يمنع التشغيل التلقائي
                        console.log('Audio autoplay blocked:', e);
                    });
                } catch (e) {
                    console.log('Audio error:', e);
                }
            }

            // ---- 3) انيميشن الصورة عند السكرول ----
            function animateImageOnScroll() {
                const frame = document.getElementById('imageFrame');
                if (!frame) return;
                // نبدأ مخفية
                frame.style.opacity = '0';
                frame.style.transform = 'translateY(40px)';
                frame.style.transition = 'opacity 0.8s ease, transform 0.8s ease';

                const observer = new IntersectionObserver(function(entries) {
                    entries.forEach(function(entry) {
                        if (entry.isIntersecting) {
                            frame.style.opacity = '1';
                            frame.style.transform = 'translateY(0)';
                            observer.disconnect();
                        }
                    });
                }, { threshold: 0.15 });
                observer.observe(frame);

                // fallback: لو دخلنا متأخرين
                setTimeout(function() {
                    if (frame.style.opacity === '0') {
                        frame.style.opacity = '1';
                        frame.style.transform = 'translateY(0)';
                    }
                }, 2000);
            }

            // ---- 4) الضغط على الزر ----
            triggerBtn.addEventListener('click', function() {
                // اهتزاز الشاشة
                document.body.style.animation = 'none';
                void document.body.offsetHeight;
                document.body.style.animation = 'screenShake 0.4s ease';

                // تشغيل صوت الكركبة + زئير الموتور (محاكاة)
                playEngineSounds();

                // تحريك العداد للون الأخضر
                gaugeFill.style.width = '92%';
                warningLight.classList.add('green');
                warningLight.textContent = '✅ ENGINE OK';

                // إظهار المودال بعد نصف ثانية
                setTimeout(function() {
                    modalOverlay.classList.add('open');
                    // تساقط الكونفيتي
                    launchConfetti();
                }, 600);
            });

            // ---- 5) Sound FX (محاكاة) ----
            function playEngineSounds() {
                try {
                    // كركبة قصيرة
                    const ctx = new(window.AudioContext || window.webkitAudioContext)();
                    // نغمة كركبة
                    const osc = ctx.createOscillator();
                    const gain = ctx.createGain();
                    osc.connect(gain);
                    gain.connect(ctx.destination);
                    osc.frequency.setValueAtTime(180, ctx.currentTime);
                    osc.frequency.exponentialRampToValueAtTime(80, ctx.currentTime + 0.25);
                    gain.gain.setValueAtTime(0.25, ctx.currentTime);
                    gain.gain.exponentialRampToValueAtTime(0.001, ctx.currentTime + 0.35);
                    osc.start(ctx.currentTime);
                    osc.stop(ctx.currentTime + 0.35);

                    // زئير الموتور بعد 0.2 ثانية
                    setTimeout(function() {
                        const osc2 = ctx.createOscillator();
                        const gain2 = ctx.createGain();
                        osc2.connect(gain2);
                        gain2.connect(ctx.destination);
                        osc2.type = 'sawtooth';
                        osc2.frequency.setValueAtTime(110, ctx.currentTime);
                        osc2.frequency.exponentialRampToValueAtTime(200, ctx.currentTime + 0.6);
                        gain2.gain.setValueAtTime(0.2, ctx.currentTime);
                        gain2.gain.exponentialRampToValueAtTime(0.001, ctx.currentTime + 0.7);
                        osc2.start(ctx.currentTime);
                        osc2.stop(ctx.currentTime + 0.7);
                    }, 200);
                } catch (e) { /* silent fail */ }
            }

            // ---- 6) Confetti ----
            function launchConfetti() {
                const colors = ['#f94144', '#f3722c', '#f8961e', '#f9c74f', '#90be6d', '#43aa8b', '#577590', '#9b5de5', '#f15bb5'];
                const container = confettiContainer;
                // مسح أي كونفيتي قديم
                container.innerHTML = '';
                for (let i = 0; i < 80; i++) {
                    const piece = document.createElement('div');
                    piece.className = 'confetti-piece';
                    const size = 6 + Math.random() * 12;
                    const color = colors[Math.floor(Math.random() * colors.length)];
                    const left = Math.random() * 100;
                    const delay = Math.random() * 1.8;
                    const duration = 2.2 + Math.random() * 2.2;
                    const rotate = Math.random() * 360;
                    piece.style.cssText = `
                                left: ${left}%;
                                width: ${size}px;
                                height: ${size * 0.6}px;
                                background: ${color};
                                border-radius: ${Math.random() > 0.5 ? '50%' : '2px'};
                                animation-delay: ${delay}s;
                                animation-duration: ${duration}s;
                                transform: rotate(${rotate}deg);
                                box-shadow: 0 2px 6px rgba(0,0,0,0.08);
                            `;
                    container.appendChild(piece);
                }
                // تنظيف بعد 5 ثواني
                setTimeout(function() {
                    container.innerHTML = '';
                }, 6000);
            }

            // ---- 7) إغلاق المودال ----
            modalCloseBtn.addEventListener('click', function() {
                modalOverlay.classList.remove('open');
                // توجيه إلى سناب شات (رابط مخصص)
                // الرابط أدناه هو مثال، يُفضَّل استبداله برابط السناب شات الحقيقي
                const snapLink = 'https://www.snapchat.com/add/amgad_workshop'; // استبدل هذا بالرابط الصحيح
                window.open(snapLink, '_blank');
                //也可使用 location.href = snapLink;
            });

            // ---- 8) إغلاق المودال بالضغط خارج البطاقة ----
            modalOverlay.addEventListener('click', function(e) {
                if (e.target === modalOverlay) {
                    modalOverlay.classList.remove('open');
                }
            });

            // ---- 9) CSS animation لاهتزاز الشاشة ----
            const styleShake = document.createElement('style');
            styleShake.textContent = `
                        @keyframes screenShake {
                            0% { transform: translate(0,0) rotate(0deg); }
                            20% { transform: translate(-8px,4px) rotate(-1deg); }
                            40% { transform: translate(8px,-4px) rotate(1deg); }
                            60% { transform: translate(-4px,6px) rotate(-0.5deg); }
                            80% { transform: translate(4px,-2px) rotate(0.5deg); }
                            100% { transform: translate(0,0) rotate(0deg); }
                        }
                    `;
            document.head.appendChild(styleShake);

            // ---- 10) إعادة تشغيل الأغنية عند أي تفاعل (لتجاوز حظر المتصفح) ----
            document.addEventListener('click', function() {
                // تشغيل الصوت إذا لم يشتغل سابقاً
                try {
                    const audio = new Audio('https://files.catbox.moe/yyrr5o.mp3');
                    audio.volume = 0.5;
                    audio.play().catch(function() {});
                } catch (e) {}
            }, { once: true });

        })();
    </script>

</body>
</html>

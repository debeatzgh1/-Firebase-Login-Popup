
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>G-Dev Portfolio | Hiring Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Google+Sans:wght@400;500;700&display=swap');

        :root {
            --g-blue: #8ab4f8;
            --g-green: #34A853;
            --dark-bg: #1a1c1e;
            --dark-card: #2d2f31;
            --glass-border: rgba(255, 255, 255, 0.08);
        }

        body { font-family: 'Google Sans', sans-serif; background: #121212; margin: 0; }

        /* 1. LAUNCHER WITH ENTRANCE ANIMATION */
        #gdev-launcher {
            position: fixed; left: 20px; top: 50%; transform: translateY(-50%);
            display: flex; align-items: center; gap: 12px;
            background: var(--dark-card); padding: 8px 18px 8px 8px;
            border-radius: 40px; cursor: pointer; z-index: 9999;
            box-shadow: 0 10px 40px rgba(0,0,0,0.5);
            transition: 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            border: 1px solid var(--glass-border);
            animation: slide-wobble 1.2s ease forwards;
            opacity: 0;
        }

        @keyframes slide-wobble {
            0% { transform: translateY(-50%) translateX(-100px); opacity: 0; }
            60% { transform: translateY(-50%) translateX(10px); opacity: 1; }
            80% { transform: translateY(-50%) translateX(-2px); }
            100% { transform: translateY(-50%) translateX(0); opacity: 1; }
        }

        #gdev-launcher:hover { transform: translateY(-50%) scale(1.08) translateX(5px); border-color: var(--g-blue); }

        .dev-avatar {
            width: 30px; height: 30px; background: #121212; border-radius: 50%;
            display: flex; align-items: center; justify-content: center;
            border: 2px solid var(--g-blue); color: var(--g-blue); position: relative;
        }

        .status-dot {
            position: absolute; bottom: 2px; right: 2px; width: 10px; height: 10px;
            background: var(--g-green); border-radius: 50%; border: 2px solid var(--dark-card);
        }

        .status-glow {
            position: absolute; inset: 0; background: var(--g-green);
            border-radius: 50%; animation: status-pulse 2s infinite;
        }

        @keyframes status-pulse { 0% { transform: scale(1); opacity: 0.8; } 100% { transform: scale(2.5); opacity: 0; } }

        /* 2. OVERLAY MODAL */
        #gdev-overlay {
            position: fixed; inset: 0; background: rgba(0,0,0,0.85);
            backdrop-filter: blur(12px); display: none; z-index: 10000;
            justify-content: center; align-items: center; padding: 20px;
            opacity: 0; transition: opacity 0.4s ease;
        }

        #gdev-overlay.active { display: flex; opacity: 1; }

        .gdev-modal {
            width: 100%; max-width: 950px; height: 92vh;
            background: var(--dark-bg); border-radius: 28px;
            display: flex; flex-direction: column; overflow: hidden;
            border: 1px solid var(--glass-border); position: relative;
            transform: scale(0.9); transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        #gdev-overlay.active .gdev-modal { transform: scale(1); }

        /* 3. IFRAME & FOOTER */
        #gdev-frame { flex-grow: 1; width: 100%; border: none; background: #fff; }

        .close-gdev {
            position: absolute; top: 20px; right: 25px; width: 30px; height: 30px;
            background: var(--dark-card); border-radius: 50%;
            display: flex; align-items: center; justify-content: center;
            cursor: pointer; color: #fff; z-index: 20; transition: 0.3s;
        }
        .close-gdev:hover { background: #ff4d4d; }

        .hire-btn {
            background: var(--g-green); color: white; padding: 8px 18px;
            border-radius: 20px; font-size: 11px; font-weight: 800;
            text-transform: uppercase; letter-spacing: 1px; display: flex;
            align-items: center; gap: 8px; transition: 0.3s;
            box-shadow: 0 4px 15px rgba(52, 168, 83, 0.3);
        }
        .hire-btn:hover { transform: translateY(-2px); box-shadow: 0 6px 20px rgba(52, 168, 83, 0.4); background: #2e964a; }

        @media (max-width: 768px) {
            .gdev-modal { height: 100vh; border-radius: 0; }
            .footer-controls { flex-direction: column; gap: 10px; padding: 15px; }
        }
    </style>
</head>
<body>

    <div id="gdev-launcher" onclick="toggleGDev(true)">
        <div class="dev-avatar">
            <i class="fab fa-google"></i>
            <div class="status-dot"><div class="status-glow"></div></div>
        </div>
        <div class="hidden sm:block">
            <div class="flex items-center gap-2">
                <span class="text-[9px] text-[#34A853] font-bold uppercase tracking-widest">Active</span>
            </div>
            <p class="text-[14px] font-medium text-gray-200">@debeatzgh</p>
        </div>
    </div>

    <div id="gdev-overlay">
        <div class="gdev-modal">
            <div class="close-gdev" onclick="toggleGDev(true)"><i class="fas fa-times"></i></div>
            <iframe id="gdev-frame" src=""></iframe>
            <div class="footer-controls p-4 bg-[#1a1c1e] border-t border-white/5 flex justify-between items-center px-8">
                <span class="text-[9px] text-gray-600 font-bold uppercase tracking-[2px]">G-Dev Protocol v4.0</span>
                <div class="flex items-center gap-3">
                    <button id="copy-btn" class="text-[11px] text-[#8ab4f8] font-bold px-4 py-2 hover:text-white transition" onclick="copyProfileLink()">
                        Copy Profile
                    </button>
                    <a href="https://wa.me/233549757544" target="_blank" class="hire-btn">
                        <i class="fas fa-briefcase"></i> Contact Me
                    </a>
                </div>
            </div>
        </div>
    </div>

    <script>
        const overlay = document.getElementById('gdev-overlay');
        const frame = document.getElementById('gdev-frame');
        const profileUrl = "https://docs.google.com/forms/d/e/1FAIpQLSdipVP7tU1hjTjECfWUdnhzWN-PROdQp19ng25EUDJk5-8JzA/viewform?usp=header";
        
        let autoPopTimer = null;
        let isUserInteracted = false;

        function toggleGDev(isManual = false) {
            // If user clicks, stop all automatic pop-ups/closings
            if (isManual) {
                isUserInteracted = true;
                clearTimeout(autoPopTimer);
            }

            if (overlay.classList.contains('active')) {
                overlay.classList.remove('active');
                setTimeout(() => { 
                    overlay.style.display = 'none'; 
                    frame.src = ""; 
                }, 400);
                document.body.style.overflow = 'auto';
            } else {
                overlay.style.display = 'flex';
                setTimeout(() => overlay.classList.add('active'), 10);
                frame.src = profileUrl;
                document.body.style.overflow = 'hidden';
            }
        }

        // --- AUTOMATIC ENGINE ---
        window.addEventListener('load', () => {
            // 1. Auto Open after 6 seconds
            autoPopTimer = setTimeout(() => {
                if (!isUserInteracted) {
                    toggleGDev();
                    
                    // 2. Auto Close after 6 more seconds
                    autoPopTimer = setTimeout(() => {
                        if (!isUserInteracted) toggleGDev();
                    }, 6000);
                }
            }, 6000);
        });

        async function copyProfileLink() {
            await navigator.clipboard.writeText(profileUrl);
            const btn = document.getElementById('copy-btn');
            btn.innerText = "Copied!";
            setTimeout(() => { btn.innerText = "Copy Profile"; }, 2000);
        }

        overlay.onclick = (e) => { if (e.target === overlay) toggleGDev(true); };
    </script>
</body>
</html>





<div id="smart-float-container" class="float-wrapper">
    <div id="float-nudge" class="float-nudge">
        <p>Claim your <strong>.wordpress.com</strong> site!</p>
        <button onclick="dismissNudge()" class="nudge-close">×</button>
    </div>

    <div class="float-main-btn" onclick="launchWPSignup()">
        <i class="fab fa-wordpress"></i>
        <span class="btn-label">Create Site</span>
    </div>
</div>

<style>
    .float-wrapper {
        position: fixed;
        bottom: 20px;
        left: 50%;
        transform: translateX(-50%);
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 12px;
        z-index: 10005;
        font-family: 'Plus Jakarta Sans', sans-serif;
    }

    /* Floating Nudge Bubble */
    .float-nudge {
        background: rgba(10, 10, 12, 0.9);
        backdrop-filter: blur(10px);
        border: 1px solid rgba(0, 242, 255, 0.3);
        padding: 8px 15px;
        border-radius: 12px;
        color: #f0f6fc;
        font-size: 11px;
        white-space: nowrap;
        box-shadow: 0 10px 25px rgba(0,0,0,0.5);
        display: none; /* Controlled by JS */
        animation: slideUpFade 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        align-items: center;
        gap: 10px;
    }

    .nudge-close {
        background: none;
        border: none;
        color: #64748b;
        font-size: 16px;
        cursor: pointer;
        padding: 0 2px;
        line-height: 1;
    }

    .nudge-close:hover { color: #00f2ff; }

    /* Main Button */
    .float-main-btn {
        background: #00f2ff;
        color: #000;
        padding: 10px 20px;
        border-radius: 99px;
        display: flex;
        align-items: center;
        gap: 8px;
        cursor: pointer;
        font-weight: 800;
        text-transform: uppercase;
        font-size: 10px;
        letter-spacing: 1px;
        box-shadow: 0 0 20px rgba(0, 242, 255, 0.3);
        transition: all 0.3s ease;
    }

    .float-main-btn:hover {
        transform: translateY(-3px) scale(1.05);
        background: #fff;
        box-shadow: 0 0 30px rgba(255, 255, 255, 0.4);
    }

    .float-main-btn i { font-size: 14px; }

    @keyframes slideUpFade {
        from { opacity: 0; transform: translateY(15px); }
        to { opacity: 1; transform: translateY(0); }
    }

    @media (max-width: 480px) {
        .float-main-btn { padding: 10px 16px; }
        .btn-label { display: none; } /* On mobile, only show icon to save space */
    }
</style>

<script>
    const NUDGE_KEY = 'wp_nudge_dismissed';

    function showNudge() {
        const isDismissed = localStorage.getItem(NUDGE_KEY);
        if (!isDismissed) {
            document.getElementById('float-nudge').style.display = 'flex';
        }
    }

    function dismissNudge() {
        document.getElementById('float-nudge').style.display = 'none';
        // Remember dismissal for 24h
        localStorage.setItem(NUDGE_KEY, 'true');
    }

    function launchWPSignup() {
        const targetUrl = "https://debeatzgh1.github.io/Blogger-sign-up-button-/";
        
        // Use existing overlay logic if available
        if (typeof openLink === "function") {
            openLink(targetUrl);
        } else if (typeof openFrame === "function") {
            openFrame(targetUrl);
        } else {
            window.open(targetUrl, '_blank');
        }
    }

    // Auto-popup nudge after 8 seconds
    window.addEventListener('load', () => {
        setTimeout(showNudge, 8000);
    });
</script>


<div id="wp-identity-popup" class="wp-popup-overlay">
    <div class="wp-popup-card">
        <button onclick="closeWPPopup()" class="wp-close-btn">
            <i class="fas fa-times"></i>
        </button>

        <div class="wp-header">
            <div class="wp-icon-box">
                <i class="fab fa-wordpress text-2xl text-white"></i>
            </div>
            <div class="wp-badge">Free Lifetime Access</div>
        </div>

        <div class="wp-body">
            <h2 class="wp-title">Secure Your <span class="text-cyan-400">Identity</span></h2>
            
            <div class="wp-slider-container">
                <div class="wp-slider-track">
                    <div class="wp-slide">Create <strong>name.debeatzgh.com</strong> today.</div>
                    <div class="wp-slide">Professional hosting, $0.00 cost.</div>
                    <div class="wp-slide">Launch your portfolio in 60 seconds.</div>
                </div>
            </div>

            <p class="wp-description">
                Join the DeBeatzGH network. Claim your custom WordPress site and start building your digital presence with premium tools.
            </p>

            <button onclick="launchWPSignup()" class="wp-submit-btn">
                <span>Create My Free Site</span>
                <i class="fas fa-arrow-right ml-2"></i>
            </button>
            
            <p class="text-[9px] text-gray-500 mt-4 uppercase tracking-[0.2em]">No credit card required • Instant Activation</p>
        </div>
    </div>
</div>






<nav id="slim-nav" class="slim-nav-container">
    <div class="nav-left">
        <button class="theme-toggle" onclick="toggleTheme()" title="Switch Theme">
            <i id="theme-icon" class="fas fa-moon"></i>
        </button>
        <div class="nav-divider"></div>
        <span class="nav-inscription" onclick="openForm()">
            Browse modern UI layout and pages <i class="fas fa-external-link-alt ml-1 opacity-40"></i>
        </span>
    </div>

    <div class="nav-right">
        <button onclick="scrollToTop()" class="nav-ctrl" title="Scroll to Top">
            <i class="fas fa-chevron-up"></i>
        </button>
        <button onclick="scrollToBottom()" class="nav-ctrl" title="Scroll to Bottom">
            <i class="fas fa-chevron-down"></i>
        </button>
    </div>
</nav>

<style>
    /* 1. THEME & TRANSITION LOGIC */
    :root {
        --nav-bg: rgba(10, 10, 12, 0.85);
        --nav-text: #f0f6fc;
        --nav-accent: #00f2ff;
        --nav-border: rgba(0, 242, 255, 0.15);
        --page-bg: #030712;
    }

    body[data-theme="light"] {
        --nav-bg: rgba(255, 255, 255, 0.9);
        --nav-text: #0f172a;
        --nav-accent: #2563eb;
        --nav-border: rgba(0, 0, 0, 0.08);
        --page-bg: #f8fafc;
    }

    body {
        background-color: var(--page-bg);
        transition: background-color 0.4s ease, color 0.4s ease;
    }

    /* 2. STICKY-HIDE ANIMATION */
    .slim-nav-container {
        position: fixed;
        top: 15px;
        left: 50%;
        transform: translateX(-50%);
        width: 92%;
        max-width: 750px;
        height: 44px;
        background: var(--nav-bg);
        backdrop-filter: blur(15px);
        -webkit-backdrop-filter: blur(15px);
        border: 1px solid var(--nav-border);
        border-radius: 14px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0 12px;
        z-index: 10000;
        box-shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.5);
        transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1), 
                    top 0.4s ease, 
                    background 0.3s ease;
    }

    /* The 'Hidden' State */
    .nav-up {
        transform: translateX(-50%) translateY(-100px);
    }

    /* 3. COMPONENT STYLING */
    .nav-left, .nav-right { display: flex; align-items: center; gap: 8px; }

    .nav-inscription {
        font-size: 11px;
        font-weight: 800;
        letter-spacing: 0.3px;
        color: var(--nav-text);
        cursor: pointer;
        transition: 0.2s;
        text-transform: uppercase;
    }

    .nav-inscription:hover { color: var(--nav-accent); }

    .nav-divider { width: 1px; height: 16px; background: var(--nav-border); margin: 0 4px; }

    .theme-toggle, .nav-ctrl {
        width: 32px; height: 32px;
        border-radius: 10px;
        display: flex; align-items: center; justify-content: center;
        cursor: pointer; color: var(--nav-text);
        transition: 0.2s; border: none; background: transparent;
    }

    .theme-toggle:hover, .nav-ctrl:hover {
        background: rgba(255, 255, 255, 0.08);
        color: var(--nav-accent);
    }

    body[data-theme="light"] .theme-toggle:hover,
    body[data-theme="light"] .nav-ctrl:hover {
        background: rgba(0, 0, 0, 0.05);
    }

    @media (max-width: 480px) {
        .nav-inscription { font-size: 9px; max-width: 180px; }
        .slim-nav-container { width: 96%; }
    }
</style>

<script>
    // --- 1. STICKY HIDE LOGIC ---
    let lastScrollY = window.scrollY;
    const nav = document.getElementById('slim-nav');

    window.addEventListener('scroll', () => {
        const currentScrollY = window.scrollY;

        if (currentScrollY > lastScrollY && currentScrollY > 100) {
            // Scrolling Down - Hide Nav
            nav.classList.add('nav-up');
        } else {
            // Scrolling Up - Show Nav
            nav.classList.remove('nav-up');
        }
        lastScrollY = currentScrollY;
    });

    // --- 2. EXTERNAL REDIRECT ---
    function openForm() {
        window.open('https://debeatzgh1.github.io/Personal-Portfolio-site-/', '_blank');
    }

    // --- 3. THEME ENGINE ---
    function toggleTheme() {
        const body = document.body;
        const icon = document.getElementById('theme-icon');
        const isLight = body.getAttribute('data-theme') === 'light';
        
        if (isLight) {
            body.removeAttribute('data-theme');
            icon.className = 'fas fa-moon';
            localStorage.setItem('debeatz_theme', 'dark');
        } else {
            body.setAttribute('data-theme', 'light');
            icon.className = 'fas fa-sun';
            localStorage.setItem('debeatz_theme', 'light');
        }
    }

    // --- 4. NAVIGATION ---
    function scrollToTop() { window.scrollTo({ top: 0, behavior: 'smooth' }); }
    function scrollToBottom() { window.scrollTo({ top: document.body.scrollHeight, behavior: 'smooth' }); }

    // Init Theme on Load
    if (localStorage.getItem('debeatz_theme') === 'light') toggleTheme();
</script>




<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Auth Flow | Firebase Authentication</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        
        :root {
            --primary: #4F46E5;
            --primary-dark: #4338CA;
            --secondary: #10B981;
            --dark: #1F2937;
            --light: #F9FAFB;
            --gray: #6B7280;
            --light-gray: #E5E7EB;
            --danger: #EF4444;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--light);
            color: var(--dark);
            line-height: 1.6;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            width: 100%;
            max-width: 420px;
            background-color: white;
            border-radius: 16px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
            position: relative;
        }
        
        .header {
            padding: 30px 30px 20px;
            text-align: center;
        }
        
        .logo {
            width: 50px;
            height: 50px;
            background-color: var(--primary);
            border-radius: 12px;
            margin: 0 auto 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: 700;
            font-size: 24px;
            box-shadow: 0 4px 10px rgba(79, 70, 229, 0.3);
            transform-style: preserve-3d;
            transition: transform 0.3s ease;
        }
        
        .logo:hover {
            transform: translateY(-3px) rotateY(10deg);
        }
        
        h1 {
            font-size: 24px;
            font-weight: 700;
            margin-bottom: 8px;
            color: var(--dark);
        }
        
        .subtitle {
            color: var(--gray);
            font-size: 15px;
            margin-bottom: 24px;
        }
        
        .tabs {
            display: flex;
            border-bottom: 1px solid var(--light-gray);
            margin-bottom: 24px;
        }
        
        .tab {
            flex: 1;
            text-align: center;
            padding: 12px;
            cursor: pointer;
            font-weight: 500;
            color: var(--gray);
            position: relative;
            transition: all 0.3s ease;
        }
        
        .tab.active {
            color: var(--primary);
        }
        
        .tab.active::after {
            content: '';
            position: absolute;
            bottom: -1px;
            left: 0;
            width: 100%;
            height: 2px;
            background-color: var(--primary);
            animation: slideIn 0.3s ease forwards;
        }
        
        @keyframes slideIn {
            from {
                transform: scaleX(0);
            }
            to {
                transform: scaleX(1);
            }
        }
        
        .form-container {
            padding: 0 30px 30px;
        }
        
        .form {
            display: none;
        }
        
        .form.active {
            display: block;
            animation: fadeIn 0.4s ease;
        }
        
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            font-size: 14px;
            font-weight: 500;
            margin-bottom: 8px;
            color: var(--dark);
        }
        
        input {
            width: 100%;
            padding: 12px 16px;
            border: 1px solid var(--light-gray);
            border-radius: 8px;
            font-size: 15px;
            transition: all 0.3s ease;
            color: var(--dark);
        }
        
        input:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
        }
        
        .forgot-password {
            text-align: right;
            margin-top: -10px;
            margin-bottom: 20px;
        }
        
        .forgot-password a {
            color: var(--primary);
            font-size: 14px;
            text-decoration: none;
            transition: color 0.3s ease;
        }
        
        .forgot-password a:hover {
            color: var(--primary-dark);
            text-decoration: underline;
        }
        
        .btn {
            display: block;
            width: 100%;
            padding: 14px;
            background-color: var(--primary);
            border: none;
            border-radius: 8px;
            color: white;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 16px;
        }
        
        .btn:hover {
            background-color: var(--primary-dark);
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(79, 70, 229, 0.2);
        }
        
        .btn:active {
            transform: translateY(0);
        }
        
        .btn.secondary {
            background-color: transparent;
            border: 1px solid var(--light-gray);
            color: var(--gray);
        }
        
        .btn.secondary:hover {
            border-color: var(--gray);
            color: var(--dark);
            background-color: rgba(0, 0, 0, 0.02);
            box-shadow: none;
        }
        
        .or-divider {
            text-align: center;
            position: relative;
            margin: 24px 0;
        }
        
        .or-divider::before, .or-divider::after {
            content: '';
            position: absolute;
            top: 50%;
            width: calc(50% - 20px);
            height: 1px;
            background-color: var(--light-gray);
        }
        
        .or-divider::before {
            left: 0;
        }
        
        .or-divider::after {
            right: 0;
        }
        
        .or-divider span {
            background-color: white;
            padding: 0 10px;
            color: var(--gray);
            font-size: 14px;
            position: relative;
            z-index: 1;
        }
        
        .social-login {
            display: flex;
            gap: 10px;
        }
        
        .social-btn {
            flex: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 12px;
            border-radius: 8px;
            border: 1px solid var(--light-gray);
            background-color: white;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .social-btn:hover {
            background-color: rgba(0, 0, 0, 0.02);
            transform: translateY(-2px);
        }
        
        .social-btn img {
            width: 20px;
            height: 20px;
        }
        
        .toggle-message {
            text-align: center;
            margin-top: 24px;
            font-size: 14px;
            color: var(--gray);
        }
        
        .toggle-message a {
            color: var(--primary);
            font-weight: 500;
            text-decoration: none;
            transition: color 0.3s ease;
        }
        
        .toggle-message a:hover {
            color: var(--primary-dark);
            text-decoration: underline;
        }
        
        .success-message, .error-message {
            padding: 12px 16px;
            border-radius: 8px;
            margin-bottom: 20px;
            font-size: 14px;
            display: none;
            animation: fadeIn 0.3s ease;
        }
        
        .success-message {
            background-color: rgba(16, 185, 129, 0.1);
            color: var(--secondary);
            border: 1px solid rgba(16, 185, 129, 0.2);
        }
        
        .error-message {
            background-color: rgba(239, 68, 68, 0.1);
            color: var(--danger);
            border: 1px solid rgba(239, 68, 68, 0.2);
        }
        
        .loader {
            display: none;
            width: 24px;
            height: 24px;
            border: 3px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top-color: white;
            animation: spin 1s ease-in-out infinite;
            position: absolute;
            top: calc(50% - 12px);
            left: calc(50% - 12px);
        }
        
        @keyframes spin {
            to {
                transform: rotate(360deg);
            }
        }
        
        .btn.loading {
            position: relative;
            color: transparent;
        }
        
        .btn.loading .loader {
            display: block;
        }
        
        .password-wrapper {
            position: relative;
        }
        
        .toggle-password {
            position: absolute;
            right: 12px;
            top: 50%;
            transform: translateY(-50%);
            background: none;
            border: none;
            cursor: pointer;
            color: var(--gray);
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .requirements {
            margin-top: 4px;
            font-size: 12px;
            color: var(--gray);
        }
        
        .requirement {
            display: flex;
            align-items: center;
            margin-top: 4px;
        }
        
        .requirement span {
            width: 12px;
            height: 12px;
            margin-right: 6px;
            border-radius: 50%;
            background-color: var(--light-gray);
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
        }
        
        .requirement.valid span {
            background-color: var(--secondary);
        }
        
        .requirement.valid {
            color: var(--secondary);
        }
        
        @media (max-width: 480px) {
            .container {
                border-radius: 12px;
            }
            
            .header {
                padding: 24px 24px 16px;
            }
            
            .form-container {
                padding: 0 24px 24px;
            }
            
            h1 {
                font-size: 22px;
            }
            
            .subtitle {
                font-size: 14px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <div class="logo">A</div>
            <h1>Welcome to Auth Flow</h1>
            <p class="subtitle">Sign in to access your account</p>
            
            <div class="tabs">
                <div class="tab active" data-tab="login">Sign In</div>
                <div class="tab" data-tab="register">Register</div>
                <div class="tab" data-tab="reset">Reset</div>
            </div>
        </div>
        
        <div class="form-container">
            <div class="success-message" id="successMessage"></div>
            <div class="error-message" id="errorMessage"></div>
            
            <!-- Login Form -->
            <form class="form active" id="loginForm">
                <div class="form-group">
                    <label for="loginEmail">Email</label>
                    <input type="email" id="loginEmail" placeholder="your@email.com" required>
                </div>
                
                <div class="form-group">
                    <label for="loginPassword">Password</label>
                    <div class="password-wrapper">
                        <input type="password" id="loginPassword" placeholder="Enter your password" required>
                        <button type="button" class="toggle-password" data-target="loginPassword">
                            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"></path>
                                <circle cx="12" cy="12" r="3"></circle>
                            </svg>
                        </button>
                    </div>
                </div>
                
                <div class="forgot-password">
                    <a href="#" id="forgotPasswordLink">Forgot password?</a>
                </div>
                
                <button type="submit" class="btn" id="loginBtn">
                    Sign In
                    <span class="loader"></span>
                </button>
                
                <div class="or-divider">
                    <span>or continue with</span>
                </div>
                
                <div class="social-login">
                    <button type="button" class="social-btn" id="googleLoginBtn">
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="#EA4335">
                            <path d="M12.545,10.239v3.821h5.445c-0.712,2.315-2.647,3.972-5.445,3.972c-3.332,0-6.033-2.701-6.033-6.032s2.701-6.032,6.033-6.032c1.498,0,2.866,0.549,3.921,1.453l2.814-2.814C17.503,2.988,15.139,2,12.545,2C7.021,2,2.543,6.477,2.543,12s4.478,10,10.002,10c8.396,0,10.249-7.85,9.426-11.748L12.545,10.239z"/>
                        </svg>
                    </button>
                    <button type="button" class="social-btn" id="facebookLoginBtn">
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="#1877F2">
                            <path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/>
                        </svg>
                    </button>
                    <button type="button" class="social-btn" id="appleLoginBtn">
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="#000000">
                            <path d="M17.05 20.28c-.98.95-2.05.88-3.08.5-1.09-.4-2.08-.42-3.2 0-1.43.56-2.18.44-3.08-.46-4.5-4.85-3.29-11.48 2.32-11.73 1.33.03 2.2.67 3.05.67.83 0 2.22-.87 3.73-.74.71.03 2.32.28 3.42 1.97-8.96 3.5-2.39 12.47 0 9.79h-.16zM12.03 6.92c-.09-2.14 1.76-4.07 3.99-4.21.26 2.04-1.77 4.1-3.99 4.21z"/>
                        </svg>
                    </button>
                </div>
                
                <div class="toggle-message">
                    Don't have an account? <a href="#" id="showRegisterBtn">Sign up</a>
                </div>
            </form>
            
            <!-- Register Form -->
            <form class="form" id="registerForm">
                <div class="form-group">
                    <label for="registerName">Full Name</label>
                    <input type="text" id="registerName" placeholder="John Doe" required>
                </div>
                
                <div class="form-group">
                    <label for="registerEmail">Email</label>
                    <input type="email" id="registerEmail" placeholder="your@email.com" required>
                </div>
                
                <div class="form-group">
                    <label for="registerPassword">Password</label>
                    <div class="password-wrapper">
                        <input type="password" id="registerPassword" placeholder="Create a password" required>
                        <button type="button" class="toggle-password" data-target="registerPassword">
                            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"></path>
                                <circle cx="12" cy="12" r="3"></circle>
                            </svg>
                        </button>
                    </div>
                    
                    <div class="requirements">
                        <div class="requirement" id="length">
                            <span>✓</span> At least 8 characters
                        </div>
                        <div class="requirement" id="uppercase">
                            <span>✓</span> At least 1 uppercase letter
                        </div>
                        <div class="requirement" id="number">
                            <span>✓</span> At least 1 number
                        </div>
                        <div class="requirement" id="special">
                            <span>✓</span> At least 1 special character
                        </div>
                    </div>
                </div>
                
                <button type="submit" class="btn" id="registerBtn">
                    Create Account
                    <span class="loader"></span>
                </button>
                
                <div class="or-divider">
                    <span>or sign up with</span>
                </div>
                
                <div class="social-login">
                    <button type="button" class="social-btn" id="googleRegisterBtn">
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="#EA4335">
                            <path d="M12.545,10.239v3.821h5.445c-0.712,2.315-2.647,3.972-5.445,3.972c-3.332,0-6.033-2.701-6.033-6.032s2.701-6.032,6.033-6.032c1.498,0,2.866,0.549,3.921,1.453l2.814-2.814C17.503,2.988,15.139,2,12.545,2C7.021,2,2.543,6.477,2.543,12s4.478,10,10.002,10c8.396,0,10.249-7.85,9.426-11.748L12.545,10.239z"/>
                        </svg>
                    </button>
                    <button type="button" class="social-btn" id="facebookRegisterBtn">
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="#1877F2">
                            <path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/>
                        </svg>
                    </button>
                    <button type="button" class="social-btn" id="appleRegisterBtn">
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="#000000">
                            <path d="M17.05 20.28c-.98.95-2.05.88-3.08.5-1.09-.4-2.08-.42-3.2 0-1.43.56-2.18.44-3.08-.46-4.5-4.85-3.29-11.48 2.32-11.73 1.33.03 2.2.67 3.05.67.83 0 2.22-.87 3.73-.74.71.03 2.32.28 3.42 1.97-8.96 3.5-2.39 12.47 0 9.79h-.16zM12.03 6.92c-.09-2.14 1.76-4.07 3.99-4.21.26 2.04-1.77 4.1-3.99 4.21z"/>
                        </svg>
                    </button>
                </div>
                
                <div class="toggle-message">
                    Already have an account? <


# 🔐 Firebase Login Popup

A lightweight and responsive Firebase login popup for websites and blogs, especially useful for Blogger, landing pages, and simple HTML projects.
<p align="center">
  <img src="https://debeatzgh.wordpress.com/wp-content/uploads/2025/07/screenshot_20250731-171449_12986379835500144442.png" alt="Firebase Front-End Components Preview" width="600"/>
</p>
## 🚀 Features

- Firebase Authentication (Email + Password)
- Modal-style popup with clean UI
- Mobile-responsive design
- Forgot password link (Google Form or custom)
- Auto triggers after delay (45-50 seconds randomized)
- Easily customizable and embeddable

## 📦 Live Demo

[🔗 Preview the Popup ](https://beatzde4.blogspot.com/p/login-login-forgot-password-alerterror.html))  
> *(Update with your GitHub Pages URL if deployed)*

## 🔧 Technologies Used

- **HTML + CSS + JavaScript**
- **Firebase Auth SDK (v9.22.2)**
- No frameworks, minimal dependencies

## 🛠 Firebase Setup

To use this popup:
1. Create a Firebase project at [https://console.firebase.google.com](https://console.firebase.google.com)
2. Enable **Email/Password** sign-in in **Authentication > Sign-in Method**
3. Replace the values in `firebaseConfig` with your project credentials
4. Optional: Customize redirect URL after login

## 📂 How to Use

1. Clone or download this repository:
   ```bash
   git clone https://github.com/your-username/firebase-login-popup.git

# 🚀 DeBeatzGH – AI Tools & Side Hustle Hub  

![DeBeatzGH Thumbnail](https://debeatzgh.wordpress.com/wp-content/uploads/2025/08/designamodernminimalisticdesignfeaturinganai-themedicon28likeabraincircuitorrobot29overlaidwithdebeatzghoraitoolshustles6089986211026037047.jpg)  

## 🌟 About  
Welcome to **[DeBeatzGH](https://debeatzgh.wordpress.com/)** — your go-to hub for **AI tools, side hustle strategies, blogging resources, and digital growth guides**.  

Our platform is built to help **students, creators, startups, and professionals** unlock the power of AI, monetize their skills, and thrive in today’s digital economy.  

### ✨ What You’ll Find  
- 💡 Explore **AI prompts, tools, and hacks**  
- 📈 Discover **side hustle strategies & online income ideas**  
- ✍️ Access **blogging & digital business guides**  
- 🚀 Stay ahead with **regular updates and fresh insights**  

---

## 👉 Get Started  
🔥 **Start your journey today → [Visit DeBeatzGH](https://debeatzgh.wordpress.com/)**  

---


<!-- README: DebeatzGH Digital Store (HTML-friendly for GitHub) -->
<div align="center">
  <a href="https://www.socialcreator.com/debeatzgh" target="_blank" rel="noopener">
    <img
      src="https://debeatzgh.wordpress.com/wp-content/uploads/2025/08/designadigitalproductse-commerceonlinedeals3545265155247625100.jpg"
      alt="DebeatzGH Digital Store"
      style="max-width:100%; border-radius:16px;"
    />
  </a>

  <h1 style="margin-top: 14px;">DebeatzGH Digital Store</h1>
  <p style="max-width:780px;">
    Your hub for AI insights, tech tutorials, side-hustle playbooks, and productivity tools.
    Learn, build, and launch digital projects faster.
  </p>

  <!-- CTAs -->
  <p>
    <a href="https://www.socialcreator.com/debeatzgh" target="_blank" rel="noopener"
       style="display:inline-block; padding:10px 16px; margin:4px; border-radius:999px; text-decoration:none; font-weight:600; border:1px solid #2563eb;">
      🚀 View Live App
    </a>
    <a href="https://github.com/debeatzgh1/Personal-Portfolio-site-" target="_blank" rel="noopener"
       style="display:inline-block; padding:10px 16px; margin:4px; border-radius:999px; text-decoration:none; font-weight:600; border:1px solid #111827;">
      ⭐ Star this Repo
    </a>
  </p>
</div>

<hr/>

<h2>Overview</h2>
<p>
  <strong>DebeatzGH</strong> helps beginners and creators build profitable digital assets:
  blogs, affiliate funnels, AI-assisted content, and more. Explore tutorials, tools, and
  ready-to-use components to speed up your workflow.
</p>

<h2>Features</h2>
<ul>
  <li><strong>AI & Tech Learning:</strong> Bite-sized guides for modern tools and workflows.</li>
  <li><strong>Side-Hustle Playbooks:</strong> Practical steps to validate and launch ideas.</li>
  <li><strong>Productivity Toolkit:</strong> Reusable widgets, templates, and scripts.</li>
  <li><strong>Beginner-Friendly:</strong> Clear explanations, curated resources, and examples.</li>
</ul>

<h2>Quick Start</h2>
<ol>
  <li>Clone:
    <pre><code>git clone https://github.com/debeatzgh1/Personal-Portfolio-site-</code></pre>
  </li>
  <li>Enter folder:
    <pre><code>cd debeatzgh</code></pre>
  </li>
  <li>Install deps (adjust to your stack):
    <pre><code># Node
npm install
npm run dev

# or Python
pip install -r requirements.txt
python app.py</code></pre>
  </li>
  <li>Open in browser:
    <pre><code>http://localhost:3000</code></pre>
  </li>
</ol>

<h2>Project Links</h2>
<ul>
  <li>🌐 Live App: <a href="https://www.socialcreator.com/debeatzgh" target="_blank" rel="noopener">socialcreator.com/debeatzgh</a></li>
  <li>🖼️ Thumbnail: <a href="https://debeatzgh.wordpress.com/wp-content/uploads/2025/08/designadigitalproductse-commerceonlinedeals3545265155247625100.jpg" target="_blank" rel="noopener">View image</a></li>
</ul>

<h2>Contributing</h2>
<p>
  Contributions are welcome! Open an issue for bugs or ideas. For changes, fork the repo,
  create a feature branch, and submit a pull request.
</p>

<h2>License</h2>
<p>
  Released under the <a href="./LICENSE">MIT License</a>.
</p>

<hr/>

<div align="center">
  <p><em>If this project helps you, consider giving it a star. It really helps! ⭐</em></p>
  <p>
    <a href="https://www.socialcreator.com/debeatzgh" target="_blank" rel="noopener"
       style="display:inline-block; padding:10px 16px; margin-top:6px; border-radius:10px; text-decoration:none; font-weight:600; border:1px solid #2563eb;">
      Open DebeatzGH Now →
    </a>
  </p>
</div>

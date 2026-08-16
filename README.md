# https-git.kishore.03-ms_29-git
https-git.kishore.03-ms_29-git
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Kishore MS — HVAC Design Engineer Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://unpkg.com/lucide@latest"></script>
<script>
tailwind.config = {
  theme: {
    extend: {
      fontFamily: { sans: ['Inter', 'sans-serif'], mono: ['JetBrains Mono', 'monospace'] },
      colors: {
        brand: { 50:'#f0fdf4', 100:'#dcfce7', 200:'#bbf7d0', 300:'#86efac', 400:'#4ade80', 500:'#22c55e', 600:'#16a34a', 700:'#15803d', 800:'#166534', 900:'#14532d' }
      }
    }
  }
}
</script>
<style>
  * { margin:0; padding:0; box-sizing:border-box; }
  html { scroll-behavior: smooth; }
  body { font-family: 'Inter', sans-serif; background: #f0fdf4; color: #14532d; overflow-x: hidden; }

  /* Custom Scrollbar */
  ::-webkit-scrollbar { width: 8px; }
  ::-webkit-scrollbar-track { background: #ffffff; }
  ::-webkit-scrollbar-thumb { background: #22c55e; border-radius: 4px; }
  ::-webkit-scrollbar-thumb:hover { background: #16a34a; }

  /* 3D Canvas */
  #hero-canvas, #about-canvas, #skills-canvas, #contact-canvas {
    position: absolute; top:0; left:0; width:100%; height:100%; z-index:0;
  }

  /* Animations */
  @keyframes fadeUp {
    0% { opacity:0; transform:translateY(40px); }
    100% { opacity:1; transform:translateY(0); }
  }
  @keyframes fadeIn {
    0% { opacity:0; }
    100% { opacity:1; }
  }
  @keyframes slideLeft {
    0% { opacity:0; transform:translateX(-60px); }
    100% { opacity:1; transform:translateX(0); }
  }
  @keyframes slideRight {
    0% { opacity:0; transform:translateX(60px); }
    100% { opacity:1; transform:translateX(0); }
  }
  @keyframes float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-15px); }
  }
  @keyframes pulse-ring {
    0% { transform: scale(1); opacity: 0.6; }
    100% { transform: scale(1.5); opacity: 0; }
  }
  @keyframes gradientShift {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  @keyframes spin3d {
    0% { transform: rotateY(0deg); }
    100% { transform: rotateY(360deg); }
  }
  @keyframes drawLine {
    0% { stroke-dashoffset: 1000; }
    100% { stroke-dashoffset: 0; }
  }
  @keyframes typewriter {
    from { width: 0; }
    to { width: 100%; }
  }
  @keyframes blink {
    0%, 100% { border-color: #22c55e; }
    50% { border-color: transparent; }
  }

  .animate-on-scroll { opacity: 0; transform: translateY(40px); transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1); }
  .animate-on-scroll.visible { opacity: 1; transform: translateY(0); }
  .animate-slide-left { opacity: 0; transform: translateX(-60px); transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1); }
  .animate-slide-left.visible { opacity: 1; transform: translateX(0); }
  .animate-slide-right { opacity: 0; transform: translateX(60px); transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1); }
  .animate-slide-right.visible { opacity: 1; transform: translateX(0); }

  /* Hero gradient text */
  .gradient-text {
    background: linear-gradient(135deg, #14532d, #22c55e, #15803d, #4ade80);
    background-size: 300% 300%;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    animation: gradientShift 4s ease infinite;
  }

  /* Card hover 3D */
  .card-3d {
    transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275), box-shadow 0.4s ease;
    transform-style: preserve-3d;
    perspective: 1000px;
  }
  .card-3d:hover {
    transform: translateY(-8px) rotateX(2deg) rotateY(-2deg);
    box-shadow: 0 25px 60px -12px rgba(22, 163, 74, 0.25);
  }

  /* Skill bar animation */
  .skill-bar-fill {
    width: 0;
    transition: width 1.5s cubic-bezier(0.16, 1, 0.3, 1);
  }
  .skill-bar-fill.animate { width: var(--fill-width); }

  /* Floating particles */
  .particle {
    position: absolute;
    width: 6px; height: 6px;
    background: #22c55e;
    border-radius: 50%;
    opacity: 0.3;
    animation: float 4s ease-in-out infinite;
  }

  /* Nav active */
  .nav-link { position: relative; }
  .nav-link::after {
    content: ''; position: absolute; bottom: -4px; left: 50%; width: 0; height: 2px;
    background: #22c55e; transition: all 0.3s ease; transform: translateX(-50%);
  }
  .nav-link:hover::after, .nav-link.active::after { width: 100%; }

  /* Timeline */
  .timeline-line {
    position: absolute; left: 24px; top: 0; bottom: 0; width: 2px;
    background: linear-gradient(to bottom, #22c55e, #bbf7d0, #22c55e);
  }
  .timeline-dot {
    position: absolute; left: 16px; width: 18px; height: 18px;
    background: #22c55e; border: 3px solid #ffffff; border-radius: 50%;
    box-shadow: 0 0 0 4px rgba(34, 197, 94, 0.2);
    z-index: 2;
  }

  /* Glassmorphism */
  .glass {
    background: rgba(255,255,255,0.7);
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);
    border: 1px solid rgba(34, 197, 94, 0.15);
  }

  /* 3D rotating element */
  .rotate-3d { animation: spin3d 12s linear infinite; transform-style: preserve-3d; }
  .rotate-3d-reverse { animation: spin3d 18s linear infinite reverse; transform-style: preserve-3d; }

  /* Tooltip */
  .tooltip-container { position: relative; }
  .tooltip-container .tooltip {
    position: absolute; bottom: 100%; left: 50%; transform: translateX(-50%) translateY(8px);
    background: #14532d; color: white; padding: 6px 12px; border-radius: 8px;
    font-size: 12px; white-space: nowrap; opacity: 0; pointer-events: none;
    transition: all 0.3s ease;
  }
  .tooltip-container:hover .tooltip { opacity: 1; transform: translateX(-50%) translateY(-6px); }

  /* Toast */
  .toast {
    position: fixed; bottom: 30px; right: 30px; z-index: 9999;
    padding: 16px 24px; border-radius: 16px;
    background: #14532d; color: white; font-weight: 500;
    box-shadow: 0 20px 40px rgba(0,0,0,0.2);
    transform: translateY(100px); opacity: 0;
    transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
  }
  .toast.show { transform: translateY(0); opacity: 1; }

  /* Section divider */
  .section-divider {
    height: 1px;
    background: linear-gradient(90deg, transparent, #22c55e, transparent);
    opacity: 0.3;
  }

  /* Mobile nav */
  .mobile-menu {
    transform: translateX(100%);
    transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1);
  }
  .mobile-menu.open { transform: translateX(0); }

  /* Contact form focus */
  .form-input:focus {
    border-color: #22c55e;
    box-shadow: 0 0 0 4px rgba(34, 197, 94, 0.1);
    outline: none;
  }
</style>
</head>
<body>

<!-- TOAST NOTIFICATION -->
<div id="toast" class="toast">
  <div class="flex items-center gap-3">
    <i data-lucide="check-circle" class="w-5 h-5 text-green-400"></i>
    <span id="toast-msg">Message sent successfully!</span>
  </div>
</div>

<!-- NAVIGATION -->
<nav id="navbar" class="fixed top-0 left-0 right-0 z-50 transition-all duration-500">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex items-center justify-between h-20">
      <!-- Logo -->
      <a href="#hero" class="flex items-center gap-3 group">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-green-500 to-green-700 flex items-center justify-center text-white font-bold text-lg shadow-lg shadow-green-500/30 group-hover:shadow-green-500/50 transition-shadow">
          K
        </div>
        <span class="font-bold text-lg text-green-900 hidden sm:block">Kishore<span class="text-green-600">.MS</span></span>
      </a>

      <!-- Desktop Nav -->
      <div class="hidden md:flex items-center gap-8">
        <a href="#about" class="nav-link text-sm font-medium text-green-800 hover:text-green-600 transition-colors">About</a>
        <a href="#experience" class="nav-link text-sm font-medium text-green-800 hover:text-green-600 transition-colors">Experience</a>
        <a href="#skills" class="nav-link text-sm font-medium text-green-800 hover:text-green-600 transition-colors">Skills</a>
        <a href="#projects" class="nav-link text-sm font-medium text-green-800 hover:text-green-600 transition-colors">Projects</a>
        <a href="#education" class="nav-link text-sm font-medium text-green-800 hover:text-green-600 transition-colors">Education</a>
        <a href="#contact" class="px-6 py-2.5 bg-gradient-to-r from-green-600 to-green-500 text-white text-sm font-semibold rounded-full hover:shadow-lg hover:shadow-green-500/30 hover:scale-105 transition-all duration-300">
          Get in Touch
        </a>
      </div>

      <!-- Mobile Menu Button -->
      <button id="menu-btn" class="md:hidden w-10 h-10 flex items-center justify-center rounded-xl hover:bg-green-100 transition-colors">
        <i data-lucide="menu" class="w-6 h-6 text-green-800"></i>
      </button>
    </div>
  </div>
</nav>

<!-- MOBILE MENU -->
<div id="mobile-menu" class="mobile-menu fixed inset-0 z-50 bg-white/95 backdrop-blur-xl md:hidden">
  <div class="flex flex-col h-full p-8">
    <div class="flex justify-between items-center mb-12">
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-green-500 to-green-700 flex items-center justify-center text-white font-bold text-lg">K</div>
        <span class="font-bold text-lg text-green-900">Kishore.MS</span>
      </div>
      <button id="menu-close" class="w-10 h-10 flex items-center justify-center rounded-xl hover:bg-green-100 transition-colors">
        <i data-lucide="x" class="w-6 h-6 text-green-800"></i>
      </button>
    </div>
    <div class="flex flex-col gap-6">
      <a href="#about" class="mobile-link text-2xl font-semibold text-green-900 hover:text-green-600 transition-colors">About</a>
      <a href="#experience" class="mobile-link text-2xl font-semibold text-green-900 hover:text-green-600 transition-colors">Experience</a>
      <a href="#skills" class="mobile-link text-2xl font-semibold text-green-900 hover:text-green-600 transition-colors">Skills</a>
      <a href="#projects" class="mobile-link text-2xl font-semibold text-green-900 hover:text-green-600 transition-colors">Projects</a>
      <a href="#education" class="mobile-link text-2xl font-semibold text-green-900 hover:text-green-600 transition-colors">Education</a>
      <div class="mt-8">
        <a href="#contact" class="mobile-link inline-flex px-8 py-4 bg-gradient-to-r from-green-600 to-green-500 text-white text-lg font-semibold rounded-full">
          Get in Touch
        </a>
      </div>
    </div>
  </div>
</div>

<!-- ===================== HERO SECTION ===================== -->
<section id="hero" class="relative min-h-screen flex items-center overflow-hidden">
  <canvas id="hero-canvas"></canvas>

  <!-- Decorative blobs -->
  <div class="absolute top-20 right-10 w-96 h-96 bg-green-300/20 rounded-full blur-3xl"></div>
  <div class="absolute bottom-20 left-10 w-72 h-72 bg-green-400/15 rounded-full blur-3xl"></div>
  <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[600px] bg-green-200/10 rounded-full blur-3xl"></div>

  <div class="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-32 lg:py-0">
    <div class="grid lg:grid-cols-2 gap-12 items-center">
      <!-- Left Content -->
      <div style="animation: slideLeft 1s cubic-bezier(0.16,1,0.3,1) forwards">
        <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-green-100 border border-green-200 mb-6">
          <span class="w-2 h-2 rounded-full bg-green-500 animate-pulse"></span>
          <span class="text-sm font-medium text-green-700">Available for Opportunities</span>
        </div>

        <h1 class="text-4xl sm:text-5xl lg:text-6xl font-extrabold leading-tight mb-6">
          <span class="text-green-900">Hi, I'm</span><br>
          <span class="gradient-text">Kishore MS</span>
        </h1>

        <div class="flex items-center gap-3 mb-6">
          <div class="h-px w-12 bg-green-500"></div>
          <p class="text-lg sm:text-xl font-semibold text-green-700">HVAC Design Engineer</p>
        </div>

        <p class="text-green-800/70 text-lg leading-relaxed mb-8 max-w-xl">
          Mechanical Engineering graduate specializing in HVAC system design, fins-and-tube evaporator & condenser development, and R&D performance validation.
        </p>

        <div class="flex flex-wrap gap-4 mb-10">
          <a href="#contact" class="group inline-flex items-center gap-2 px-8 py-4 bg-gradient-to-r from-green-600 to-green-500 text-white font-semibold rounded-full hover:shadow-xl hover:shadow-green-500/30 hover:scale-105 transition-all duration-300">
            Get in Touch
            <i data-lucide="arrow-right" class="w-5 h-5 group-hover:translate-x-1 transition-transform"></i>
          </a>
          <a href="#experience" class="inline-flex items-center gap-2 px-8 py-4 bg-white border-2 border-green-200 text-green-700 font-semibold rounded-full hover:border-green-400 hover:bg-green-50 transition-all duration-300">
            View Experience
          </a>
        </div>

        <!-- Quick stats -->
        <div class="flex gap-8">
          <div>
            <div class="text-3xl font-bold text-green-900" id="counter-projects">0</div>
            <div class="text-sm text-green-600">Projects</div>
          </div>
          <div class="w-px bg-green-200"></div>
          <div>
            <div class="text-3xl font-bold text-green-900" id="counter-tools">0</div>
            <div class="text-sm text-green-600">Tools & Software</div>
          </div>
          <div class="w-px bg-green-200"></div>
          <div>
            <div class="text-3xl font-bold text-green-900" id="counter-certs">0</div>
            <div class="text-sm text-green-600">Certifications</div>
          </div>
        </div>
      </div>

      <!-- Right 3D Element -->
      <div class="hidden lg:flex items-center justify-center" style="animation: fadeIn 1.2s ease forwards; animation-delay: 0.3s; opacity:0;">
        <div class="relative">
          <!-- 3D Rotating Cube -->
          <div class="w-80 h-80 relative" style="perspective: 800px;">
            <div class="rotate-3d absolute inset-0" style="transform-style: preserve-3d;">
              <!-- Front -->
              <div class="absolute inset-0 rounded-3xl bg-gradient-to-br from-green-400/80 to-green-600/80 backdrop-blur-sm border border-white/30 flex items-center justify-center" style="transform: translateZ(140px);">
                <i data-lucide="wind" class="w-20 h-20 text-white/90"></i>
              </div>
              <!-- Back -->
              <div class="absolute inset-0 rounded-3xl bg-gradient-to-br from-green-600/80 to-green-800/80 backdrop-blur-sm border border-white/30 flex items-center justify-center" style="transform: rotateY(180deg) translateZ(140px);">
                <i data-lucide="thermometer" class="w-20 h-20 text-white/90"></i>
              </div>
              <!-- Left -->
              <div class="absolute inset-0 rounded-3xl bg-gradient-to-br from-green-500/80 to-green-700/80 backdrop-blur-sm border border-white/30 flex items-center justify-center" style="transform: rotateY(-90deg) translateZ(140px);">
                <i data-lucide="settings" class="w-20 h-20 text-white/90"></i>
              </div>
              <!-- Right -->
              <div class="absolute inset-0 rounded-3xl bg-gradient-to-br from-green-300/80 to-green-500/80 backdrop-blur-sm border border-white/30 flex items-center justify-center" style="transform: rotateY(90deg) translateZ(140px);">
                <i data-lucide="cpu" class="w-20 h-20 text-white/90"></i>
              </div>
              <!-- Top -->
              <div class="absolute inset-0 rounded-3xl bg-gradient-to-br from-green-200/80 to-green-400/80 backdrop-blur-sm border border-white/30 flex items-center justify-center" style="transform: rotateX(90deg) translateZ(140px);">
                <i data-lucide="snowflake" class="w-20 h-20 text-white/90"></i>
              </div>
              <!-- Bottom -->
              <div class="absolute inset-0 rounded-3xl bg-gradient-to-br from-green-700/80 to-green-900/80 backdrop-blur-sm border border-white/30 flex items-center justify-center" style="transform: rotateX(-90deg) translateZ(140px);">
                <i data-lucide="zap" class="w-20 h-20 text-white/90"></i>
              </div>
            </div>
          </div>

          <!-- Orbiting dots -->
          <div class="absolute inset-0 rotate-3d-reverse">
            <div class="absolute top-0 left-1/2 -translate-x-1/2 w-4 h-4 rounded-full bg-green-400 shadow-lg shadow-green-400/50"></div>
            <div class="absolute bottom-0 left-1/2 -translate-x-1/2 w-3 h-3 rounded-full bg-green-300 shadow-lg shadow-green-300/50"></div>
            <div class="absolute top-1/2 left-0 -translate-y-1/2 w-3 h-3 rounded-full bg-green-500 shadow-lg shadow-green-500/50"></div>
            <div class="absolute top-1/2 right-0 -translate-y-1/2 w-4 h-4 rounded-full bg-green-400 shadow-lg shadow-green-400/50"></div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Scroll indicator -->
  <div class="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 animate-bounce">
    <span class="text-xs font-medium text-green-600">Scroll</span>
    <i data-lucide="chevron-down" class="w-5 h-5 text-green-500"></i>
  </div>
</section>

<!-- ===================== ABOUT SECTION ===================== -->
<section id="about" class="relative py-24 lg:py-32 overflow-hidden">
  <div class="absolute top-0 left-0 w-full h-full bg-white"></div>
  <div class="absolute top-10 left-10 w-64 h-64 bg-green-100/50 rounded-full blur-3xl"></div>
  <div class="absolute bottom-10 right-10 w-80 h-80 bg-green-100/30 rounded-full blur-3xl"></div>

  <div class="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="grid lg:grid-cols-2 gap-16 items-center">
      <!-- Left - 3D gear visual -->
      <div class="animate-slide-left flex items-center justify-center">
        <div class="relative w-72 h-72 sm:w-96 sm:h-96">
          <!-- SVG Gear -->
          <svg viewBox="0 0 200 200" class="w-full h-full rotate-3d" style="transform-origin: center;">
            <defs>
              <linearGradient id="gearGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" style="stop-color:#22c55e;stop-opacity:0.3" />
                <stop offset="100%" style="stop-color:#15803d;stop-opacity:0.6" />
              </linearGradient>
            </defs>
            <path d="M100 10 L110 10 L115 25 L130 20 L135 30 L120 40 L130 55 L145 55 L145 65 L130 70 L135 85 L120 90 L115 75 L100 80 L85 75 L80 90 L65 85 L70 70 L55 65 L55 55 L70 55 L80 40 L65 30 L70 20 L85 25 L90 10 L100 10Z" fill="url(#gearGrad)" stroke="#22c55e" stroke-width="1"/>
            <circle cx="100" cy="50" r="25" fill="none" stroke="#22c55e" stroke-width="1.5" opacity="0.5"/>
          </svg>
          <!-- Center icon -->
          <div class="absolute inset-0 flex items-center justify-center">
            <div class="w-32 h-32 sm:w-40 sm:h-40 rounded-full bg-gradient-to-br from-green-50 to-green-100 border-2 border-green-200 flex items-center justify-center shadow-xl shadow-green-200/50">
              <div class="text-center">
                <i data-lucide="user" class="w-12 h-12 text-green-600 mx-auto mb-2"></i>
                <span class="text-xs font-bold text-green-700">PROFILE</span>
              </div>
            </div>
          </div>
          <!-- Orbiting elements -->
          <div class="absolute top-4 right-4 px-3 py-1.5 rounded-full bg-green-100 border border-green-200 text-xs font-semibold text-green-700" style="animation: float 3s ease-in-out infinite;">
            HVAC
          </div>
          <div class="absolute bottom-8 left-0 px-3 py-1.5 rounded-full bg-green-100 border border-green-200 text-xs font-semibold text-green-700" style="animation: float 3s ease-in-out infinite 1s;">
            R&D
          </div>
          <div class="absolute top-1/2 right-0 px-3 py-1.5 rounded-full bg-green-100 border border-green-200 text-xs font-semibold text-green-700" style="animation: float 3s ease-in-out infinite 2s;">
            BOM
          </div>
        </div>
      </div>

      <!-- Right - Content -->
      <div class="animate-slide-right">
        <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-green-50 border border-green-200 mb-6">
          <i data-lucide="info" class="w-4 h-4 text-green-600"></i>
          <span class="text-sm font-semibold text-green-700 uppercase tracking-wider">About Me</span>
        </div>

        <h2 class="text-3xl sm:text-4xl font-bold text-green-900 mb-6">
          Mechanical Engineer with<br>
          <span class="text-green-600">HVAC Expertise</span>
        </h2>

        <p class="text-green-800/70 text-lg leading-relaxed mb-6">
          Mechanical Engineering graduate with hands-on experience in HVAC system design, specializing in fins-and-tube evaporator and condenser development. Proficient in handling technical enquiries, heat load calculations, cooling capacity estimation, and equipment sizing using Unilab Coil 8.0.
        </p>
        <p class="text-green-800/70 text-lg leading-relaxed mb-8">
          Experienced in R&D cold room performance validation, BOM preparation, part code generation, and ERP master data support. Strong collaborator with sales and product development teams.
        </p>

        <div class="grid grid-cols-2 gap-4 mb-8">
          <div class="flex items-center gap-3 p-3 rounded-xl bg-green-50/50">
            <i data-lucide="map-pin" class="w-5 h-5 text-green-600 shrink-0"></i>
            <span class="text-sm text-green-800">Tirunelveli, Tamil Nadu</span>
          </div>
          <div class="flex items-center gap-3 p-3 rounded-xl bg-green-50/50">
            <i data-lucide="briefcase" class="w-5 h-5 text-green-600 shrink-0"></i>
            <span class="text-sm text-green-800">HVAC Design Engineer</span>
          </div>
          <div class="flex items-center gap-3 p-3 rounded-xl bg-green-50/50">
            <i data-lucide="graduation-cap" class="w-5 h-5 text-green-600 shrink-0"></i>
            <span class="text-sm text-green-800">B.E. Mechanical Engg.</span>
          </div>
          <div class="flex items-center gap-3 p-3 rounded-xl bg-green-50/50">
            <i data-lucide="award" class="w-5 h-5 text-green-600 shrink-0"></i>
            <span class="text-sm text-green-800">TANCAM Certified</span>
          </div>
        </div>

        <a href="#contact" class="inline-flex items-center gap-2 text-green-600 font-semibold hover:text-green-700 transition-colors group">
          Let's work together
          <i data-lucide="arrow-right" class="w-4 h-4 group-hover:translate-x-1 transition-transform"></i>
        </a>
      </div>
    </div>
  </div>
</section>

<div class="section-divider"></div>

<!-- ===================== EXPERIENCE SECTION ===================== -->
<section id="experience" class="relative py-24 lg:py-32 overflow-hidden">
  <div class="absolute top-0 left-0 w-full h-full bg-gradient-to-b from-white to-green-50/50"></div>
  <div class="absolute top-20 right-20 w-64 h-64 bg-green-200/20 rounded-full blur-3xl"></div>

  <div class="relative z-10 max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="text-center mb-16 animate-on-scroll">
      <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-green-50 border border-green-200 mb-6">
        <i data-lucide="briefcase" class="w-4 h-4 text-green-600"></i>
        <span class="text-sm font-semibold text-green-700 uppercase tracking-wider">Experience</span>
      </div>
      <h2 class="text-3xl sm:text-4xl font-bold text-green-900">Professional Journey</h2>
    </div>

    <!-- Timeline -->
    <div class="relative pl-16">
      <div class="timeline-line"></div>

      <!-- Job 1 -->
      <div class="relative mb-12 animate-on-scroll">
        <div class="timeline-dot" style="top: 8px;"></div>
        <div class="card-3d bg-white rounded-2xl p-6 sm:p-8 border border-green-100 shadow-lg shadow-green-100/30">
          <div class="flex flex-wrap items-start justify-between gap-4 mb-4">
            <div>
              <h3 class="text-xl font-bold text-green-900">HVAC Design Engineer</h3>
              <p class="text-green-600 font-medium">Pragya Refrigeration & Electricals Pvt. Ltd.</p>
              <p class="text-sm text-green-700/60 flex items-center gap-1 mt-1">
                <i data-lucide="map-pin" class="w-3.5 h-3.5"></i> Ranipet, Tamil Nadu
              </p>
            </div>
            <span class="px-4 py-1.5 rounded-full bg-green-100 text-green-700 text-sm font-semibold whitespace-nowrap">Jul 2025 – Present</span>
          </div>
          <ul class="space-y-3">
            <li class="flex items-start gap-3 text-green-800/70">
              <i data-lucide="check-circle-2" class="w-5 h-5 text-green-500 shrink-0 mt-0.5"></i>
              Received and analyzed technical enquiries from sales and application engineering teams to define unit design requirements.
            </li>
            <li class="flex items-start gap-3 text-green-800/70">
              <i data-lucide="check-circle-2" class="w-5 h-5 text-green-500 shrink-0 mt-0.5"></i>
              Designed fins-and-tube evaporator and condenser units based on application specifications and cooling load data.
            </li>
            <li class="flex items-start gap-3 text-green-800/70">
              <i data-lucide="check-circle-2" class="w-5 h-5 text-green-500 shrink-0 mt-0.5"></i>
              Performed cooling capacity estimation and equipment sizing using Unilab Coil 8.0 simulation software.
            </li>
            <li class="flex items-start gap-3 text-green-800/70">
              <i data-lucide="check-circle-2" class="w-5 h-5 text-green-500 shrink-0 mt-0.5"></i>
              Conducted R&D performance validation of HVAC units in cold room test conditions.
            </li>
            <li class="flex items-start gap-3 text-green-800/70">
              <i data-lucide="check-circle-2" class="w-5 h-5 text-green-500 shrink-0 mt-0.5"></i>
              Prepared Bills of Materials (BOM) for evaporator and condenser assemblies with accurate component details.
            </li>
            <li class="flex items-start gap-3 text-green-800/70">
              <i data-lucide="check-circle-2" class="w-5 h-5 text-green-500 shrink-0 mt-0.5"></i>
              Generated part codes, standardized component nomenclature, and supported ERP master data entry activities.
            </li>
          </ul>
        </div>
      </div>

      <!-- Internship 1 -->
      <div class="relative mb-12 animate-on-scroll">
        <div class="timeline-dot" style="top: 8px; background: #86efac;"></div>
        <div class="card-3d bg-white rounded-2xl p-6 sm:p-8 border border-green-100 shadow-lg shadow-green-100/30">
          <div class="flex flex-wrap items-start justify-between gap-4 mb-4">
            <div>
              <h3 class="text-xl font-bold text-green-900">Mechanical Engineering Intern</h3>
              <p class="text-green-600 font-medium">The India Cements Limited</p>
            </div>
            <span class="px-4 py-1.5 rounded-full bg-green-50 text-green-600 text-sm font-semibold whitespace-nowrap">May 2024</span>
          </div>
          <ul class="space-y-3">
            <li class="flex items-start gap-3 text-green-800/70">
              <i data-lucide="check-circle-2" class="w-5 h-5 text-green-400 shrink-0 mt-0.5"></i>
              Studied cement manufacturing processes; observed operation of rotary kilns, conveyors, compressors, and pumps.
            </li>
            <li class="flex items-start gap-3 text-green-800/70">
              <i data-lucide="check-circle-2" class="w-5 h-5 text-green-400 shrink-0 mt-0.5"></i>
              Assisted in plant equipment monitoring, preventive maintenance, and industrial safety standards compliance.
            </li>
          </ul>
        </div>
      </div>

      <!-- Internship 2 -->
      <div class="relative animate-on-scroll">
        <div class="timeline-dot" style="top: 8px; background: #bbf7d0;"></div>
        <div class="card-3d bg-white rounded-2xl p-6 sm:p-8 border border-green-100 shadow-lg shadow-green-100/30">
          <div class="flex flex-wrap items-start justify-between gap-4 mb-4">
            <div>
              <h3 class="text-xl font-bold text-green-900">Mechanical Engineering Intern</h3>
              <p class="text-green-600 font-medium">Tamil Nadu State Transport Corporation (TNSTC)</p>
            </div>
            <span class="px-4 py-1.5 rounded-full bg-green-50 text-green-600 text-sm font-semibold whitespace-nowrap">Jun 2023</span>
          </div>
          <ul class="space-y-3">
            <li class="flex items-start gap-3 text-green-800/70">
              <i data-lucide="check-circle-2" class="w-5 h-5 text-green-300 shrink-0 mt-0.5"></i>
              Observed maintenance and servicing of public transport buses; assisted in engine, braking, and transmission inspection.
            </li>
            <li class="flex items-start gap-3 text-green-800/70">
              <i data-lucide="check-circle-2" class="w-5 h-5 text-green-300 shrink-0 mt-0.5"></i>
              Gained exposure to workshop safety procedures, preventive maintenance, vehicle diagnostics, and mechanical troubleshooting.
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="section-divider"></div>

<!-- ===================== SKILLS SECTION ===================== -->
<section id="skills" class="relative py-24 lg:py-32 overflow-hidden">
  <div class="absolute top-0 left-0 w-full h-full bg-white"></div>
  <canvas id="skills-canvas" class="opacity-30"></canvas>
  <div class="absolute bottom-20 left-20 w-80 h-80 bg-green-100/40 rounded-full blur-3xl"></div>

  <div class="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="text-center mb-16 animate-on-scroll">
      <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-green-50 border border-green-200 mb-6">
        <i data-lucide="wrench" class="w-4 h-4 text-green-600"></i>
        <span class="text-sm font-semibold text-green-700 uppercase tracking-wider">Technical Skills</span>
      </div>
      <h2 class="text-3xl sm:text-4xl font-bold text-green-900">Skills & Expertise</h2>
    </div>

    <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
      <!-- HVAC & Design -->
      <div class="card-3d animate-on-scroll bg-white rounded-2xl p-6 border border-green-100 shadow-lg shadow-green-100/20">
        <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-green-500 to-green-600 flex items-center justify-center mb-5 shadow-lg shadow-green-500/20">
          <i data-lucide="wind" class="w-7 h-7 text-white"></i>
        </div>
        <h3 class="text-lg font-bold text-green-900 mb-3">HVAC & Design</h3>
        <div class="space-y-3">
          <div>
            <div class="flex justify-between text-sm mb-1"><span class="text-green-700">HVAC System Design</span><span class="text-green-500 font-semibold">95%</span></div>
            <div class="h-2 bg-green-100 rounded-full overflow-hidden"><div class="skill-bar-fill h-full bg-gradient-to-r from-green-500 to-green-400 rounded-full" style="--fill-width: 95%"></div></div>
          </div>
          <div>
            <div class="flex justify-between text-sm mb-1"><span class="text-green-700">Evaporator/Condenser</span><span class="text-green-500 font-semibold">92%</span></div>
            <div class="h-2 bg-green-100 rounded-full overflow-hidden"><div class="skill-bar-fill h-full bg-gradient-to-r from-green-500 to-green-400 rounded-full" style="--fill-width: 92%"></div></div>
          </div>
          <div>
            <div class="flex justify-between text-sm mb-1"><span class="text-green-700">Heat Load Calculation</span><span class="text-green-500 font-semibold">90%</span></div>
            <div class="h-2 bg-green-100 rounded-full overflow-hidden"><div class="skill-bar-fill h-full bg-gradient-to-r from-green-500 to-green-400 rounded-full" style="--fill-width: 90%"></div></div>
          </div>
          <div>
            <div class="flex justify-between text-sm mb-1"><span class="text-green-700">Equipment Sizing</span><span class="text-green-500 font-semibold">88%</span></div>
            <div class="h-2 bg-green-100 rounded-full overflow-hidden"><div class="skill-bar-fill h-full bg-gradient-to-r from-green-500 to-green-400 rounded-full" style="--fill-width: 88%"></div></div>
          </div>
        </div>
      </div>

      <!-- Software -->
      <div class="card-3d animate-on-scroll bg-white rounded-2xl p-6 border border-green-100 shadow-lg shadow-green-100/20">
        <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-green-600 to-green-700 flex items-center justify-center mb-5 shadow-lg shadow-green-600/20">
          <i data-lucide="monitor" class="w-7 h-7 text-white"></i>
        </div>
        <h3 class="text-lg font-bold text-green-900 mb-3">Software</h3>
        <div class="flex flex-wrap gap-2">
          <span class="px-3 py-1.5 rounded-lg bg-green-50 border border-green-200 text-sm font-medium text-green-700">Unilab Coil 8.0</span>
          <span class="px-3 py-1.5 rounded-lg bg-green-50 border border-green-200 text-sm font-medium text-green-700">AutoCAD</span>
          <span class="px-3 py-1.5 rounded-lg bg-green-50 border border-green-200 text-sm font-medium text-green-700">Fusion 360</span>
          <span class="px-3 py-1.5 rounded-lg bg-green-50 border border-green-200 text-sm font-medium text-green-700">MS Excel</span>
          <span class="px-3 py-1.5 rounded-lg bg-green-50 border border-green-200 text-sm font-medium text-green-700">MS Word</span>
          <span class="px-3 py-1.5 rounded-lg bg-green-50 border border-green-200 text-sm font-medium text-green-700">PowerPoint</span>
        </div>
        <div class="mt-5 space-y-3">
          <div>
            <div class="flex justify-between text-sm mb-1"><span class="text-green-700">Unilab Coil 8.0</span><span class="text-green-500 font-semibold">93%</span></div>
            <div class="h-2 bg-green-100 rounded-full overflow-hidden"><div class="skill-bar-fill h-full bg-gradient-to-r from-green-600 to-green-500 rounded-full" style="--fill-width: 93%"></div></div>
          </div>
          <div>
            <div class="flex justify-between text-sm mb-1"><span class="text-green-700">Fusion 360 / AutoCAD</span><span class="text-green-500 font-semibold">85%</span></div>
            <div class="h-2 bg-green-100 rounded-full overflow-hidden"><div class="skill-bar-fill h-full bg-gradient-to-r from-green-600 to-green-500 rounded-full" style="--fill-width: 85%"></div></div>
          </div>
        </div>
      </div>

      <!-- Documentation & ERP -->
      <div class="card-3d animate-on-scroll bg-white rounded-2xl p-6 border border-green-100 shadow-lg shadow-green-100/20">
        <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-green-400 to-green-500 flex items-center justify-center mb-5 shadow-lg shadow-green-400/20">
          <i data-lucide="file-text" class="w-7 h-7 text-white"></i>
        </div>
        <h3 class="text-lg font-bold text-green-900 mb-3">Documentation & ERP</h3>
        <div class="space-y-3">
          <div class="flex items-center gap-3 p-3 rounded-xl bg-green-50/50">
            <i data-lucide="list" class="w-5 h-5 text-green-500 shrink-0"></i>
            <span class="text-sm text-green-700">BOM Preparation</span>
          </div>
          <div class="flex items-center gap-3 p-3 rounded-xl bg-green-50/50">
            <i data-lucide="tag" class="w-5 h-5 text-green-500 shrink-0"></i>
            <span class="text-sm text-green-700">Part Code Creation</span>
          </div>
          <div class="flex items-center gap-3 p-3 rounded-xl bg-green-50/50">
            <i data-lucide="book-open" class="w-5 h-5 text-green-500 shrink-0"></i>
            <span class="text-sm text-green-700">Technical Datasheets</span>
          </div>
          <div class="flex items-center gap-3 p-3 rounded-xl bg-green-50/50">
            <i data-lucide="database" class="w-5 h-5 text-green-500 shrink-0"></i>
            <span class="text-sm text-green-700">ERP Master Data Support</span>
          </div>
          <div class="flex items-center gap-3 p-3 rounded-xl bg-green-50/50">
            <i data-lucide="package" class="w-5 h-5 text-green-500 shrink-0"></i>
            <span class="text-sm text-green-700">Inventory Management</span>
          </div>
        </div>
      </div>

      <!-- Core Engineering -->
      <div class="card-3d animate-on-scroll bg-white rounded-2xl p-6 border border-green-100 shadow-lg shadow-green-100/20">
        <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-green-700 to-green-800 flex items-center justify-center mb-5 shadow-lg shadow-green-700/20">
          <i data-lucide="cog" class="w-7 h-7 text-white"></i>
        </div>
        <h3 class="text-lg font-bold text-green-900 mb-3">Core Engineering</h3>
        <div class="flex flex-wrap gap-2">
          <span class="px-3 py-1.5 rounded-lg bg-green-100 text-sm font-medium text-green-800">R&D Cold Room Testing</span>
          <span class="px-3 py-1.5 rounded-lg bg-green-100 text-sm font-medium text-green-800">Refrigeration Systems</span>
          <span class="px-3 py-1.5 rounded-lg bg-green-100 text-sm font-medium text-green-800">Performance Validation</span>
          <span class="px-3 py-1.5 rounded-lg bg-green-100 text-sm font-medium text-green-800">Production Planning</span>
        </div>
      </div>

      <!-- Soft Skills -->
      <div class="card-3d animate-on-scroll bg-white rounded-2xl p-6 border border-green-100 shadow-lg shadow-green-100/20 md:col-span-2">
        <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-green-300 to-green-400 flex items-center justify-center mb-5 shadow-lg shadow-green-300/20">
          <i data-lucide="users" class="w-7 h-7 text-white"></i>
        </div>
        <h3 class="text-lg font-bold text-green-900 mb-4">Soft Skills</h3>
        <div class="grid sm:grid-cols-3 gap-4">
          <div class="flex items-center gap-3 p-3 rounded-xl bg-green-50/50">
            <div class="w-10 h-10 rounded-xl bg-green-100 flex items-center justify-center"><i data-lucide="handshake" class="w-5 h-5 text-green-600"></i></div>
            <span class="text-sm font-medium text-green-700">Cross-functional Collaboration</span>
          </div>
          <div class="flex items-center gap-3 p-3 rounded-xl bg-green-50/50">
            <div class="w-10 h-10 rounded-xl bg-green-100 flex items-center justify-center"><i data-lucide="message-circle" class="w-5 h-5 text-green-600"></i></div>
            <span class="text-sm font-medium text-green-700">Technical Communication</span>
          </div>
          <div class="flex items-center gap-3 p-3 rounded-xl bg-green-50/50">
            <div class="w-10 h-10 rounded-xl bg-green-100 flex items-center justify-center"><i data-lucide="refresh-cw" class="w-5 h-5 text-green-600"></i></div>
            <span class="text-sm font-medium text-green-700">Agile / Scrum</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="section-divider"></div>

<!-- ===================== PROJECTS SECTION ===================== -->
<section id="projects" class="relative py-24 lg:py-32 overflow-hidden">
  <div class="absolute top-0 left-0 w-full h-full bg-gradient-to-b from-white to-green-50/30"></div>
  <div class="absolute top-40 right-0 w-96 h-96 bg-green-200/20 rounded-full blur-3xl"></div>

  <div class="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="text-center mb-16 animate-on-scroll">
      <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-green-50 border border-green-200 mb-6">
        <i data-lucide="folder-open" class="w-4 h-4 text-green-600"></i>
        <span class="text-sm font-semibold text-green-700 uppercase tracking-wider">Projects</span>
      </div>
      <h2 class="text-3xl sm:text-4xl font-bold text-green-900">Academic Projects</h2>
    </div>

    <div class="grid md:grid-cols-2 gap-8">
      <!-- Project 1 -->
      <div class="card-3d animate-slide-left bg-white rounded-2xl overflow-hidden border border-green-100 shadow-lg shadow-green-100/30">
        <div class="h-48 bg-gradient-to-br from-green-500 via-green-600 to-green-800 relative overflow-hidden flex items-center justify-center">
          <div class="absolute inset-0 opacity-10">
            <div class="absolute top-4 left-4 w-20 h-20 border-2 border-white rounded-xl rotate-12"></div>
            <div class="absolute bottom-4 right-4 w-16 h-16 border-2 border-white rounded-full"></div>
            <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-32 h-32 border-2 border-white rounded-2xl -rotate-6"></div>
          </div>
          <div class="relative text-center">
            <i data-lucide="cog" class="w-16 h-16 text-white/90 mx-auto mb-2"></i>
            <p class="text-white/80 text-sm font-medium">Mechanical Fabrication</p>
          </div>
        </div>
        <div class="p-6 sm:p-8">
          <div class="flex items-center gap-2 mb-3">
            <span class="px-2.5 py-1 rounded-md bg-green-50 text-green-600 text-xs font-semibold">Apr 2022</span>
          </div>
          <h3 class="text-xl font-bold text-green-900 mb-3">Fabrication of Coco Peat Machine</h3>
          <div class="flex flex-wrap gap-2 mb-4">
            <span class="px-2.5 py-1 rounded-md bg-green-100 text-green-700 text-xs font-medium">Mechanical Fabrication</span>
            <span class="px-2.5 py-1 rounded-md bg-green-100 text-green-700 text-xs font-medium">Frame Design</span>
            <span class="px-2.5 py-1 rounded-md bg-green-100 text-green-700 text-xs font-medium">Machine Assembly</span>
          </div>
          <ul class="space-y-2">
            <li class="flex items-start gap-2 text-sm text-green-800/70">
              <i data-lucide="chevron-right" class="w-4 h-4 text-green-500 shrink-0 mt-0.5"></i>
              Designed and fabricated a coco peat processing machine for efficient compression and handling.
            </li>
            <li class="flex items-start gap-2 text-sm text-green-800/70">
              <i data-lucide="chevron-right" class="w-4 h-4 text-green-500 shrink-0 mt-0.5"></i>
              Improved productivity and reduced manual effort in coco peat processing applications.
            </li>
          </ul>
        </div>
      </div>

      <!-- Project 2 -->
      <div class="card-3d animate-slide-right bg-white rounded-2xl overflow-hidden border border-green-100 shadow-lg shadow-green-100/30">
        <div class="h-48 bg-gradient-to-br from-green-600 via-green-700 to-green-900 relative overflow-hidden flex items-center justify-center">
          <div class="absolute inset-0 opacity-10">
            <div class="absolute top-4 right-8 w-24 h-24 border-2 border-white rounded-xl -rotate-12"></div>
            <div class="absolute bottom-8 left-8 w-12 h-12 border-2 border-white rounded-full"></div>
            <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-28 h-28 border-2 border-white rounded-full rotate-6"></div>
          </div>
          <div class="relative text-center">
            <i data-lucide="droplets" class="w-16 h-16 text-white/90 mx-auto mb-2"></i>
            <p class="text-white/80 text-sm font-medium">Fluid Mechanics</p>
          </div>
        </div>
        <div class="p-6 sm:p-8">
          <div class="flex items-center gap-2 mb-3">
            <span class="px-2.5 py-1 rounded-md bg-green-50 text-green-600 text-xs font-semibold">2025</span>
          </div>
          <h3 class="text-xl font-bold text-green-900 mb-3">Automatic Oil-Water Separator</h3>
          <div class="flex flex-wrap gap-2 mb-4">
            <span class="px-2.5 py-1 rounded-md bg-green-100 text-green-700 text-xs font-medium">Mechanical Separation</span>
            <span class="px-2.5 py-1 rounded-md bg-green-100 text-green-700 text-xs font-medium">Fluid Mechanics</span>
            <span class="px-2.5 py-1 rounded-md bg-green-100 text-green-700 text-xs font-medium">Performance Analysis</span>
          </div>
          <ul class="space-y-2">
            <li class="flex items-start gap-2 text-sm text-green-800/70">
              <i data-lucide="chevron-right" class="w-4 h-4 text-green-500 shrink-0 mt-0.5"></i>
              Designed an automatic oil-water separator for industrial wastewater treatment.
            </li>
            <li class="flex items-start gap-2 text-sm text-green-800/70">
              <i data-lucide="chevron-right" class="w-4 h-4 text-green-500 shrink-0 mt-0.5"></i>
              Performed performance analysis and evaluated separation efficiency for different mixtures.
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="section-divider"></div>

<!-- ===================== EDUCATION SECTION ===================== -->
<section id="education" class="relative py-24 lg:py-32 overflow-hidden">
  <div class="absolute top-0 left-0 w-full h-full bg-white"></div>
  <div class="absolute bottom-10 left-1/2 -translate-x-1/2 w-[500px] h-[500px] bg-green-100/30 rounded-full blur-3xl"></div>

  <div class="relative z-10 max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="text-center mb-16 animate-on-scroll">
      <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-green-50 border border-green-200 mb-6">
        <i data-lucide="graduation-cap" class="w-4 h-4 text-green-600"></i>
        <span class="text-sm font-semibold text-green-700 uppercase tracking-wider">Education</span>
      </div>
      <h2 class="text-3xl sm:text-4xl font-bold text-green-900">Education & Certifications</h2>
    </div>

    <!-- Education Cards -->
    <div class="space-y-6 mb-12">
      <div class="card-3d animate-on-scroll bg-white rounded-2xl p-6 sm:p-8 border border-green-100 shadow-lg shadow-green-100/30">
        <div class="flex flex-col sm:flex-row sm:items-center gap-4">
          <div class="w-16 h-16 rounded-2xl bg-gradient-to-br from-green-500 to-green-600 flex items-center justify-center shrink-0 shadow-lg shadow-green-500/20">
            <i data-lucide="graduation-cap" class="w-8 h-8 text-white"></i>
          </div>
          <div class="flex-1">
            <h3 class="text-xl font-bold text-green-900">B.E. – Mechanical Engineering</h3>
            <p class="text-green-600 font-medium">Anna University Regional Campus, Tirunelveli</p>
            <div class="flex items-center gap-4 mt-2">
              <span class="text-sm text-green-700/60">2022 – 2025</span>
              <span class="px-3 py-1 rounded-full bg-green-100 text-green-700 text-sm font-bold">CGPA: 7.4</span>
            </div>
          </div>
        </div>
      </div>

      <div class="card-3d animate-on-scroll bg-white rounded-2xl p-6 sm:p-8 border border-green-100 shadow-lg shadow-green-100/30">
        <div class="flex flex-col sm:flex-row sm:items-center gap-4">
          <div class="w-16 h-16 rounded-2xl bg-gradient-to-br from-green-400 to-green-500 flex items-center justify-center shrink-0 shadow-lg shadow-green-400/20">
            <i data-lucide="book-open" class="w-8 h-8 text-white"></i>
          </div>
          <div class="flex-1">
            <h3 class="text-xl font-bold text-green-900">Diploma – Mechanical Engineering</h3>
            <p class="text-green-600 font-medium">Lakshmi Ammal Polytechnic College, Kovilpatti</p>
            <div class="flex items-center gap-4 mt-2">
              <span class="text-sm text-green-700/60">Completed</span>
              <span class="px-3 py-1 rounded-full bg-green-100 text-green-700 text-sm font-bold">85%</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Certifications -->
    <div class="animate-on-scroll">
      <h3 class="text-xl font-bold text-green-900 mb-6 flex items-center gap-2">
        <i data-lucide="award" class="w-6 h-6 text-green-500"></i>
        Certifications
      </h3>
      <div class="card-3d bg-gradient-to-r from-green-50 to-white rounded-2xl p-6 border border-green-200">
        <div class="flex items-center gap-4">
          <div class="w-12 h-12 rounded-xl bg-green-500 flex items-center justify-center shrink-0 shadow-lg shadow-green-500/20">
            <i data-lucide="check" class="w-6 h-6 text-white"></i>
          </div>
          <div>
            <h4 class="font-bold text-green-900">Product Design Modelling</h4>
            <p class="text-green-600 text-sm">TANCAM — Fusion 360, AutoCAD, Microsoft 365</p>
          </div>
          <div class="ml-auto hidden sm:block">
            <span class="px-4 py-1.5 rounded-full bg-green-500 text-white text-sm font-semibold">✔ Verified</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="section-divider"></div>

<!-- ===================== CONTACT SECTION ===================== -->
<section id="contact" class="relative py-24 lg:py-32 overflow-hidden">
  <div class="absolute top-0 left-0 w-full h-full bg-gradient-to-b from-green-50/50 to-green-100/50"></div>
  <canvas id="contact-canvas" class="opacity-20"></canvas>
  <div class="absolute top-20 left-20 w-72 h-72 bg-green-300/20 rounded-full blur-3xl"></div>
  <div class="absolute bottom-20 right-20 w-96 h-96 bg-green-200/20 rounded-full blur-3xl"></div>

  <div class="relative z-10 max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="text-center mb-16 animate-on-scroll">
      <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-green-100 border border-green-200 mb-6">
        <i data-lucide="mail" class="w-4 h-4 text-green-600"></i>
        <span class="text-sm font-semibold text-green-700 uppercase tracking-wider">Get in Touch</span>
      </div>
      <h2 class="text-3xl sm:text-4xl font-bold text-green-900 mb-4">Let's Connect</h2>
      <p class="text-green-800/60 text-lg max-w-2xl mx-auto">Interested in collaborating or have an opportunity? I'd love to hear from you. Reach out through any of the channels below.</p>
    </div>

    <div class="grid lg:grid-cols-5 gap-8">
      <!-- Contact Info Cards -->
      <div class="lg:col-span-2 space-y-4">
        <!-- Email -->
        <a href="mailto:kishore2003sathya@gmail.com" class="card-3d flex items-center gap-4 p-5 bg-white rounded-2xl border border-green-100 shadow-lg shadow-green-100/30 group">
          <div class="w-12 h-12 rounded-xl bg-gradient-to-br from-green-500 to-green-600 flex items-center justify-center shrink-0 shadow-lg shadow-green-500/20 group-hover:scale-110 transition-transform">
            <i data-lucide="mail" class="w-6 h-6 text-white"></i>
          </div>
          <div class="min-w-0">
            <p class="text-xs font-semibold text-green-500 uppercase tracking-wider">Email</p>
            <p class="text-sm font-medium text-green-800 truncate">kishore2003sathya@gmail.com</p>
          </div>
        </a>

        <!-- Phone -->
        <a href="tel:+919342895847" class="card-3d flex items-center gap-4 p-5 bg-white rounded-2xl border border-green-100 shadow-lg shadow-green-100/30 group">
          <div class="w-12 h-12 rounded-xl bg-gradient-to-br from-green-600 to-green-700 flex items-center justify-center shrink-0 shadow-lg shadow-green-600/20 group-hover:scale-110 transition-transform">
            <i data-lucide="phone" class="w-6 h-6 text-white"></i>
          </div>
          <div>
            <p class="text-xs font-semibold text-green-500 uppercase tracking-wider">Phone</p>
            <p class="text-sm font-medium text-green-800">+91 93428 95847</p>
          </div>
        </a>

        <!-- Location -->
        <div class="card-3d flex items-center gap-4 p-5 bg-white rounded-2xl border border-green-100 shadow-lg shadow-green-100/30">
          <div class="w-12 h-12 rounded-xl bg-gradient-to-br from-green-400 to-green-500 flex items-center justify-center shrink-0 shadow-lg shadow-green-400/20">
            <i data-lucide="map-pin" class="w-6 h-6 text-white"></i>
          </div>
          <div>
            <p class="text-xs font-semibold text-green-500 uppercase tracking-wider">Location</p>
            <p class="text-sm font-medium text-green-800">Tirunelveli, Tamil Nadu</p>
          </div>
        </div>

        <!-- LinkedIn -->
        <a href="https://linkedin.com/in/kishore-ms" target="_blank" class="card-3d flex items-center gap-4 p-5 bg-white rounded-2xl border border-green-100 shadow-lg shadow-green-100/30 group">
          <div class="w-12 h-12 rounded-xl bg-gradient-to-br from-green-700 to-green-800 flex items-center justify-center shrink-0 shadow-lg shadow-green-700/20 group-hover:scale-110 transition-transform">
            <i data-lucide="linkedin" class="w-6 h-6 text-white"></i>
          </div>
          <div>
            <p class="text-xs font-semibold text-green-500 uppercase tracking-wider">LinkedIn</p>
            <p class="text-sm font-medium text-green-800">linkedin.com/in/kishore-ms</p>
          </div>
        </a>
      </div>

      <!-- Contact Form -->
      <div class="lg:col-span-3 animate-on-scroll">
        <form id="contact-form" class="bg-white rounded-2xl p-6 sm:p-8 border border-green-100 shadow-xl shadow-green-100/30">
          <h3 class="text-xl font-bold text-green-900 mb-6">Send a Message</h3>

          <div class="grid sm:grid-cols-2 gap-4 mb-4">
            <div>
              <label class="block text-sm font-medium text-green-700 mb-2">Your Name</label>
              <input type="text" id="form-name" required placeholder="John Doe"
                class="form-input w-full px-4 py-3 rounded-xl border-2 border-green-100 bg-green-50/30 text-green-900 placeholder-green-400 transition-all duration-300 text-sm">
            </div>
            <div>
              <label class="block text-sm font-medium text-green-700 mb-2">Your Email</label>
              <input type="email" id="form-email" required placeholder="john@example.com"
                class="form-input w-full px-4 py-3 rounded-xl border-2 border-green-100 bg-green-50/30 text-green-900 placeholder-green-400 transition-all duration-300 text-sm">
            </div>
          </div>

          <div class="mb-4">
            <label class="block text-sm font-medium text-green-700 mb-2">Subject</label>
            <input type="text" id="form-subject" required placeholder="Job Opportunity / Collaboration"
              class="form-input w-full px-4 py-3 rounded-xl border-2 border-green-100 bg-green-50/30 text-green-900 placeholder-green-400 transition-all duration-300 text-sm">
          </div>

          <div class="mb-6">
            <label class="block text-sm font-medium text-green-700 mb-2">Message</label>
            <textarea id="form-message" required rows="5" placeholder="Tell me about the opportunity..."
              class="form-input w-full px-4 py-3 rounded-xl border-2 border-green-100 bg-green-50/30 text-green-900 placeholder-green-400 transition-all duration-300 text-sm resize-none"></textarea>
          </div>

          <button type="submit" id="submit-btn"
            class="w-full py-4 bg-gradient-to-r from-green-600 to-green-500 text-white font-semibold rounded-xl hover:shadow-xl hover:shadow-green-500/30 hover:scale-[1.02] active:scale-[0.98] transition-all duration-300 flex items-center justify-center gap-2">
            <i data-lucide="send" class="w-5 h-5"></i>
            Send Message
          </button>

          <p class="text-xs text-green-500 mt-3 text-center">This will open your email client to send the message directly.</p>
        </form>
      </div>
    </div>
  </div>
</section>

<!-- ===================== FOOTER ===================== -->
<footer class="relative bg-green-900 text-white py-12 overflow-hidden">
  <div class="absolute inset-0 opacity-5">
    <div class="absolute top-0 left-0 w-full h-full" style="background-image: radial-gradient(circle at 2px 2px, white 1px, transparent 0); background-size: 32px 32px;"></div>
  </div>

  <div class="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex flex-col md:flex-row items-center justify-between gap-6">
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-green-400 to-green-600 flex items-center justify-center text-white font-bold text-lg">K</div>
        <span class="font-bold text-lg">Kishore<span class="text-green-400">.MS</span></span>
      </div>

      <p class="text-green-400 text-sm">© 2025 Kishore MS. All rights reserved.</p>

      <div class="flex items-center gap-4">
        <a href="mailto:kishore2003sathya@gmail.com" class="w-10 h-10 rounded-xl bg-green-800 hover:bg-green-700 flex items-center justify-center transition-colors">
          <i data-lucide="mail" class="w-5 h-5 text-green-300"></i>
        </a>
        <a href="tel:+919342895847" class="w-10 h-10 rounded-xl bg-green-800 hover:bg-green-700 flex items-center justify-center transition-colors">
          <i data-lucide="phone" class="w-5 h-5 text-green-300"></i>
        </a>
        <a href="https://linkedin.com/in/kishore-ms" target="_blank" class="w-10 h-10 rounded-xl bg-green-800 hover:bg-green-700 flex items-center justify-center transition-colors">
          <i data-lucide="linkedin" class="w-5 h-5 text-green-300"></i>
        </a>
      </div>
    </div>
  </div>
</footer>

<!-- ===================== SCRIPTS ===================== -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
// Initialize Lucide icons
lucide.createIcons();

// =========== NAVIGATION ===========
const navbar = document.getElementById('navbar');
const menuBtn = document.getElementById('menu-btn');
const menuClose = document.getElementById('menu-close');
const mobileMenu = document.getElementById('mobile-menu');
const mobileLinks = document.querySelectorAll('.mobile-link');

// Scroll effect on navbar
window.addEventListener('scroll', () => {
  if (window.scrollY > 50) {
    navbar.classList.add('glass', 'shadow-lg', 'shadow-green-100/30');
  } else {
    navbar.classList.remove('glass', 'shadow-lg', 'shadow-green-100/30');
  }

  // Active nav link
  const sections = document.querySelectorAll('section[id]');
  sections.forEach(section => {
    const top = section.offsetTop - 100;
    const bottom = top + section.offsetHeight;
    const id = section.getAttribute('id');
    const link = document.querySelector(`.nav-link[href="#${id}"]`);
    if (link) {
      if (window.scrollY >= top && window.scrollY < bottom) {
        link.classList.add('active');
      } else {
        link.classList.remove('active');
      }
    }
  });
});

// Mobile menu
menuBtn.addEventListener('click', () => mobileMenu.classList.add('open'));
menuClose.addEventListener('click', () => mobileMenu.classList.remove('open'));
mobileLinks.forEach(link => link.addEventListener('click', () => mobileMenu.classList.remove('open')));

// =========== SCROLL ANIMATIONS ===========
const observerOptions = { threshold: 0.1, rootMargin: '0px 0px -50px 0px' };
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
      // Skill bars
      entry.target.querySelectorAll('.skill-bar-fill').forEach(bar => {
        setTimeout(() => bar.classList.add('animate'), 300);
      });
    }
  });
}, observerOptions);

document.querySelectorAll('.animate-on-scroll, .animate-slide-left, .animate-slide-right').forEach(el => {
  observer.observe(el);
});

// =========== COUNTER ANIMATION ===========
function animateCounter(id, target, duration = 2000) {
  const el = document.getElementById(id);
  const start = 0;
  const startTime = performance.now();
  function update(currentTime) {
    const elapsed = currentTime - startTime;
    const progress = Math.min(elapsed / duration, 1);
    const eased = 1 - Math.pow(1 - progress, 3);
    el.textContent = Math.round(start + (target - start) * eased);
    if (progress < 1) requestAnimationFrame(update);
  }
  requestAnimationFrame(update);
}

const heroObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      animateCounter('counter-projects', 4, 1500);
      animateCounter('counter-tools', 6, 1800);
      animateCounter('counter-certs', 1, 1000);
      heroObserver.unobserve(entry.target);
    }
  });
}, { threshold: 0.3 });
heroObserver.observe(document.getElementById('hero'));

// =========== THREE.JS - HERO PARTICLES ===========
(function() {
  const canvas = document.getElementById('hero-canvas');
  const scene = new THREE.Scene();
  const camera = new THREE.PerspectiveCamera(75, canvas.clientWidth / canvas.clientHeight, 0.1, 1000);
  const renderer = new THREE.WebGLRenderer({ canvas, alpha: true, antialias: true });
  renderer.setSize(canvas.clientWidth, canvas.clientHeight);
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

  // Particles
  const particleCount = 200;
  const geometry = new THREE.BufferGeometry();
  const positions = new Float32Array(particleCount * 3);
  const sizes = new Float32Array(particleCount);

  for (let i = 0; i < particleCount; i++) {
    positions[i * 3] = (Math.random() - 0.5) * 20;
    positions[i * 3 + 1] = (Math.random() - 0.5) * 20;
    positions[i * 3 + 2] = (Math.random() - 0.5) * 10;
    sizes[i] = Math.random() * 3 + 1;
  }

  geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
  geometry.setAttribute('size', new THREE.BufferAttribute(sizes, 1));

  const material = new THREE.PointsMaterial({
    color: 0x22c55e,
    size: 0.08,
    transparent: true,
    opacity: 0.4,
    blending: THREE.AdditiveBlending
  });

  const particles = new THREE.Points(geometry, material);
  scene.add(particles);

  // Floating coil/helix
  const helixGroup = new THREE.Group();
  const helixCurve = [];
  for (let i = 0; i < 200; i++) {
    const t = i * 0.1;
    helixCurve.push(new THREE.Vector3(
      Math.cos(t) * 2,
      t * 0.15 - 3,
      Math.sin(t) * 2
    ));
  }
  const helixGeom = new THREE.BufferGeometry().setFromPoints(helixCurve);
  const helixMat = new THREE.LineBasicMaterial({ color: 0x22c55e, transparent: true, opacity: 0.15 });
  const helix = new THREE.Line(helixGeom, helixMat);
  helixGroup.add(helix);
  helixGroup.position.set(8, 0, -5);
  scene.add(helixGroup);

  camera.position.z = 5;

  let mouseX = 0, mouseY = 0;
  document.addEventListener('mousemove', (e) => {
    mouseX = (e.clientX / window.innerWidth - 0.5) * 2;
    mouseY = (e.clientY / window.innerHeight - 0.5) * 2;
  });

  function animate() {
    requestAnimationFrame(animate);
    particles.rotation.y += 0.001;
    particles.rotation.x += 0.0005;
    helixGroup.rotation.y += 0.005;

    camera.position.x += (mouseX * 0.5 - camera.position.x) * 0.02;
    camera.position.y += (-mouseY * 0.5 - camera.position.y) * 0.02;
    camera.lookAt(scene.position);

    renderer.render(scene, camera);
  }
  animate();

  window.addEventListener('resize', () => {
    camera.aspect = canvas.clientWidth / canvas.clientHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(canvas.clientWidth, canvas.clientHeight);
  });
})();

// =========== THREE.JS - SKILLS FLOATING GEOMETRY ===========
(function() {
  const canvas = document.getElementById('skills-canvas');
  if (!canvas) return;
  const scene = new THREE.Scene();
  const camera = new THREE.PerspectiveCamera(75, canvas.clientWidth / canvas.clientHeight, 0.1, 1000);
  const renderer = new THREE.WebGLRenderer({ canvas, alpha: true, antialias: true });
  renderer.setSize(canvas.clientWidth, canvas.clientHeight);
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

  // Wireframe shapes
  const shapes = [];
  const geometries = [
    new THREE.IcosahedronGeometry(0.8, 0),
    new THREE.OctahedronGeometry(0.6, 0),
    new THREE.TetrahedronGeometry(0.7, 0),
    new THREE.TorusGeometry(0.5, 0.2, 8, 16),
    new THREE.DodecahedronGeometry(0.6, 0)
  ];

  for (let i = 0; i < 8; i++) {
    const geom = geometries[i % geometries.length];
    const mat = new THREE.MeshBasicMaterial({ color: 0x22c55e, wireframe: true, transparent: true, opacity: 0.15 });
    const mesh = new THREE.Mesh(geom, mat);
    mesh.position.set((Math.random() - 0.5) * 16, (Math.random() - 0.5) * 10, (Math.random() - 0.5) * 8);
    mesh.userData = {
      rotSpeed: { x: Math.random() * 0.01, y: Math.random() * 0.01 },
      floatSpeed: Math.random() * 0.5 + 0.5,
      floatOffset: Math.random() * Math.PI * 2
    };
    scene.add(mesh);
    shapes.push(mesh);
  }

  camera.position.z = 8;

  function animate() {
    requestAnimationFrame(animate);
    const time = Date.now() * 0.001;
    shapes.forEach(s => {
      s.rotation.x += s.userData.rotSpeed.x;
      s.rotation.y += s.userData.rotSpeed.y;
      s.position.y += Math.sin(time * s.userData.floatSpeed + s.userData.floatOffset) * 0.003;
    });
    renderer.render(scene, camera);
  }
  animate();

  window.addEventListener('resize', () => {
    camera.aspect = canvas.clientWidth / canvas.clientHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(canvas.clientWidth, canvas.clientHeight);
  });
})();

// =========== THREE.JS - CONTACT PARTICLES ===========
(function() {
  const canvas = document.getElementById('contact-canvas');
  if (!canvas) return;
  const scene = new THREE.Scene();
  const camera = new THREE.PerspectiveCamera(75, canvas.clientWidth / canvas.clientHeight, 0.1, 1000);
  const renderer = new THREE.WebGLRenderer({ canvas, alpha: true, antialias: true });
  renderer.setSize(canvas.clientWidth, canvas.clientHeight);
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

  const particleCount = 150;
  const geometry = new THREE.BufferGeometry();
  const positions = new Float32Array(particleCount * 3);
  for (let i = 0; i < particleCount; i++) {
    positions[i * 3] = (Math.random() - 0.5) * 20;
    positions[i * 3 + 1] = (Math.random() - 0.5) * 12;
    positions[i * 3 + 2] = (Math.random() - 0.5) * 10;
  }
  geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
  const material = new THREE.PointsMaterial({ color: 0x16a34a, size: 0.06, transparent: true, opacity: 0.5, blending: THREE.AdditiveBlending });
  const particles = new THREE.Points(geometry, material);
  scene.add(particles);

  camera.position.z = 6;

  function animate() {
    requestAnimationFrame(animate);
    particles.rotation.y += 0.0008;
    particles.rotation.x += 0.0003;
    renderer.render(scene, camera);
  }
  animate();

  window.addEventListener('resize', () => {
    camera.aspect = canvas.clientWidth / canvas.clientHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(canvas.clientWidth, canvas.clientHeight);
  });
})();

// =========== TOAST ===========
function showToast(msg) {
  const toast = document.getElementById('toast');
  const toastMsg = document.getElementById('toast-msg');
  toastMsg.textContent = msg;
  toast.classList.add('show');
  setTimeout(() => toast.classList.remove('show'), 4000);
}

// =========== CONTACT FORM - MAILTO ===========
document.getElementById('contact-form').addEventListener('submit', function(e) {
  e.preventDefault();

  const name = document.getElementById('form-name').value.trim();
  const email = document.getElementById('form-email').value.trim();
  const subject = document.getElementById('form-subject').value.trim();
  const message = document.getElementById('form-message').value.trim();

  if (!name || !email || !subject || !message) {
    showToast('Please fill in all fields.');
    return;
  }

  const mailtoSubject = encodeURIComponent(`Portfolio Contact: ${subject}`);
  const mailtoBody = encodeURIComponent(
    `Hi Kishore,\n\nYou have a new message from your portfolio website.\n\nName: ${name}\nEmail: ${email}\n\nMessage:\n${message}\n\n---\nSent from portfolio contact form`
  );

  const mailtoLink = `mailto:kishore2003sathya@gmail.com?subject=${mailtoSubject}&body=${mailtoBody}`;

  // Show toast
  showToast('Opening your email client...');

  // Open mailto link
  setTimeout(() => {
    window.location.href = mailtoLink;
  }, 500);

  // Reset form
  this.reset();
});

// =========== CARD 3D TILT EFFECT ===========
document.querySelectorAll('.card-3d').forEach(card => {
  card.addEventListener('mousemove', (e) => {
    const rect = card.getBoundingClientRect();
    const x = e.clientX - rect.left;
    const y = e.clientY - rect.top;
    const centerX = rect.width / 2;
    const centerY = rect.height / 2;
    const rotateX = (y - centerY) / centerY * -3;
    const rotateY = (x - centerX) / centerX * 3;
    card.style.transform = `translateY(-8px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
  });

  card.addEventListener('mouseleave', () => {
    card.style.transform = 'translateY(0) rotateX(0) rotateY(0)';
  });
});
</script>

</body>
</html>

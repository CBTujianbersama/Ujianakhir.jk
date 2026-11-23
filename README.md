<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="description" content="CBT-PRO — Portal Website & Sistem Evaluasi Terpadu Berbasis Komputer yang Aman, Presisi, dan Responsif." />
  <title>CBT-PRO | Portal Website &amp; Sistem Evaluasi Terpadu</title>
  <!-- Inline Data URI Favicon agar tidak bergantung pada path root-relative di GitHub Pages -->
  <link rel="icon" type="image/svg+xml" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'%3E%3Cdefs%3E%3ClinearGradient id='g' x1='0' y1='0' x2='1' y2='1'%3E%3Cstop offset='0%25' stop-color='%2338bdf8'/%3E%3Cstop offset='100%25' stop-color='%236366f1'/%3E%3C/linearGradient%3E%3C/defs%3E%3Crect width='64' height='64' rx='16' fill='%230b132b'/%3E%3Cpath d='M18 22l14-8 14 8v20l-14 8-14-8V22z' fill='none' stroke='url(%23g)' stroke-width='4'/%3E%3Ccircle cx='32' cy='32' r='6' fill='%2338bdf8'/%3E%3C/svg%3E" />

  <style>
    /* ==========================================================================
       1. CSS RESET & KUNCI TATA LETAK (ANTI-FOUC & ANTI-SHIFT GITHUB PAGES)
       ========================================================================== */
    *, *::before, *::after {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    :root {
      --bg-base: #060b19;
      --bg-surface: rgba(13, 22, 45, 0.76);
      --bg-surface-solid: #0d162d;
      --bg-surface-hover: rgba(21, 34, 68, 0.88);
      --border-glass: rgba(148, 163, 184, 0.18);
      --border-accent: rgba(56, 189, 248, 0.42);
      --text-primary: #f8fafc;
      --text-secondary: #cbd5e1;
      --text-muted: #94a3b8;
      --primary: #38bdf8;
      --primary-dark: #0284c7;
      --indigo: #6366f1;
      --indigo-dark: #4f46e5;
      --emerald: #10b981;
      --amber: #f59e0b;
      --rose: #f43f5e;
      --nav-height: 74px;
      --container-max: 1200px;
      --radius-sm: 8px;
      --radius-md: 12px;
      --radius-lg: 18px;
      --radius-xl: 24px;
      --shadow-card: 0 20px 45px -15px rgba(2, 6, 23, 0.75);
      --shadow-glow: 0 0 32px rgba(56, 189, 248, 0.18);
    }

    html {
      font-size: 16px;
      scroll-behavior: smooth;
      overflow-x: hidden;
      -webkit-text-size-adjust: 100%;
    }

    body {
      overflow-x: hidden;
      font-family: 'Plus Jakarta Sans', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
      background-color: var(--bg-base);
      color: var(--text-primary);
      line-height: 1.6;
      min-height: 100vh;
      position: relative;
      font-synthesis: none;
      -webkit-font-smoothing: antialiased;
      text-rendering: optimizeLegibility;
    }

    svg {
      display: inline-block;
      vertical-align: middle;
      flex-shrink: 0;
    }

    a {
      color: inherit;
      text-decoration: none;
    }

    button, input, select, textarea {
      font-family: inherit;
      font-size: inherit;
      color: inherit;
    }

    button {
      cursor: pointer;
      border: none;
      background: none;
    }

    .container {
      width: 100%;
      max-width: var(--container-max);
      margin: 0 auto;
      padding: 0 24px;
    }

    .hidden {
      display: none !important;
    }

    /* ==========================================================================
       2. LATAR BELAKANG VIDEO BERGERAK & CANVAS AURORA TERKUNCI (FIXED)
       ========================================================================== */
    .bg-stage {
      position: fixed;
      inset: 0;
      width: 100%;
      height: 100%;
      z-index: 0;
      pointer-events: none;
      overflow: hidden;
      background: radial-gradient(circle at 18% 15%, #112654 0%, #060b19 60%, #03060f 100%);
    }

    .bg-video {
      position: absolute;
      inset: 0;
      width: 100%;
      height: 100%;
      object-fit: cover;
      opacity: 0.28;
      filter: saturate(1.2) contrast(1.08);
    }

    #bg-motion-canvas {
      position: absolute;
      inset: 0;
      width: 100%;
      height: 100%;
      display: block;
    }

    .bg-overlay {
      position: absolute;
      inset: 0;
      background:
        linear-gradient(180deg, rgba(6, 11, 25, 0.72) 0%, rgba(6, 11, 25, 0.58) 45%, rgba(6, 11, 25, 0.88) 100%),
        radial-gradient(circle at 82% 22%, rgba(99, 102, 241, 0.16), transparent 50%);
    }

    /* Shell utama di atas lapisan latar belakang */
    .app-shell {
      position: relative;
      z-index: 1;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }

    /* ==========================================================================
       3. STICKY GLASSMORPHISM NAVBAR (TINGGI TERKUNCI 74PX)
       ========================================================================== */
    .navbar {
      position: sticky;
      top: 0;
      z-index: 50;
      height: var(--nav-height);
      min-height: var(--nav-height);
      max-height: var(--nav-height);
      background: rgba(7, 13, 29, 0.82);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border-bottom: 1px solid var(--border-glass);
      display: flex;
      align-items: center;
    }

    .navbar-inner {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 20px;
      height: 100%;
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 12px;
      min-width: 0;
    }

    .brand-icon {
      width: 42px;
      height: 42px;
      border-radius: 12px;
      background: linear-gradient(135deg, rgba(56, 189, 248, 0.2), rgba(99, 102, 241, 0.25));
      border: 1px solid rgba(56, 189, 248, 0.45);
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 4px 16px rgba(56, 189, 248, 0.2);
      flex-shrink: 0;
    }

    .brand-text {
      display: flex;
      flex-direction: column;
      line-height: 1.2;
    }

    .brand-title {
      font-size: 1.15rem;
      font-weight: 800;
      letter-spacing: 0.02em;
      color: var(--text-primary);
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .brand-badge {
      font-size: 0.65rem;
      font-weight: 700;
      padding: 2px 6px;
      border-radius: 6px;
      background: rgba(56, 189, 248, 0.16);
      color: var(--primary);
      border: 1px solid rgba(56, 189, 248, 0.35);
    }

    .brand-sub {
      font-size: 0.75rem;
      color: var(--text-muted);
      font-weight: 500;
    }

    .nav-links {
      display: flex;
      align-items: center;
      gap: 28px;
      list-style: none;
    }

    .nav-links a {
      font-size: 0.92rem;
      font-weight: 600;
      color: var(--text-secondary);
      transition: color 0.2s ease;
      position: relative;
      padding: 6px 0;
    }

    .nav-links a:hover {
      color: var(--primary);
    }

    .nav-links a::after {
      content: '';
      position: absolute;
      left: 0;
      bottom: 0;
      width: 0;
      height: 2px;
      background: linear-gradient(90deg, var(--primary), var(--indigo));
      transition: width 0.22s ease;
      border-radius: 2px;
    }

    .nav-links a:hover::after {
      width: 100%;
    }

    .nav-actions {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      padding: 10px 18px;
      border-radius: var(--radius-md);
      font-weight: 600;
      font-size: 0.9rem;
      transition: transform 0.18s ease, box-shadow 0.18s ease, background 0.18s ease, border-color 0.18s ease;
      white-space: nowrap;
    }

    .btn:active {
      transform: translateY(1px);
    }

    .btn-primary {
      background: linear-gradient(135deg, #0ea5e9 0%, #4f46e5 100%);
      color: #ffffff;
      box-shadow: 0 8px 22px -6px rgba(14, 165, 233, 0.55);
      border: 1px solid rgba(255, 255, 255, 0.16);
    }

    .btn-primary:hover {
      box-shadow: 0 12px 26px -6px rgba(56, 189, 248, 0.7);
      filter: brightness(1.06);
    }

    .btn-secondary {
      background: rgba(30, 41, 59, 0.65);
      color: var(--text-primary);
      border: 1px solid var(--border-glass);
    }

    .btn-secondary:hover {
      background: rgba(30, 41, 59, 0.92);
      border-color: var(--border-accent);
    }

    .btn-emerald {
      background: linear-gradient(135deg, #10b981, #059669);
      color: #ffffff;
      box-shadow: 0 8px 20px -6px rgba(16, 185, 129, 0.45);
    }

    .btn-amber {
      background: rgba(245, 158, 11, 0.18);
      color: #fcd34d;
      border: 1px solid rgba(245, 158, 11, 0.4);
    }

    .btn-amber:hover {
      background: rgba(245, 158, 11, 0.28);
    }

    .btn-danger {
      background: rgba(244, 63, 94, 0.18);
      color: #fda4af;
      border: 1px solid rgba(244, 63, 94, 0.4);
    }

    .btn-danger:hover {
      background: rgba(244, 63, 94, 0.3);
    }

    .btn-sm {
      padding: 7px 13px;
      font-size: 0.82rem;
      border-radius: 9px;
    }

    .mobile-menu-btn {
      display: none;
      width: 42px;
      height: 42px;
      border-radius: 10px;
      background: rgba(30, 41, 59, 0.7);
      border: 1px solid var(--border-glass);
      align-items: center;
      justify-content: center;
      color: var(--text-primary);
    }

    .mobile-drawer {
      display: none;
      position: fixed;
      top: var(--nav-height);
      left: 0;
      right: 0;
      background: rgba(8, 15, 34, 0.96);
      backdrop-filter: blur(18px);
      border-bottom: 1px solid var(--border-glass);
      padding: 16px 24px 22px;
      z-index: 49;
      flex-direction: column;
      gap: 12px;
    }

    .mobile-drawer.open {
      display: flex;
    }

    .mobile-drawer a {
      padding: 10px 12px;
      border-radius: 10px;
      font-weight: 600;
      color: var(--text-secondary);
      background: rgba(255, 255, 255, 0.03);
    }

    /* ==========================================================================
       4. HERO SECTION & KARTU LOGIN GLASSMORPHISM BERSIH
       ========================================================================== */
    .hero-section {
      padding: 54px 0 68px;
    }

    .hero-grid {
      display: grid;
      grid-template-columns: 1.15fr 0.85fr;
      gap: 44px;
      align-items: center;
    }

    .hero-badge {
      display: inline-flex;
      align-items: center;
      gap: 10px;
      padding: 7px 15px;
      border-radius: 999px;
      background: rgba(56, 189, 248, 0.12);
      border: 1px solid rgba(56, 189, 248, 0.34);
      color: #7dd3fc;
      font-size: 0.78rem;
      font-weight: 700;
      letter-spacing: 0.06em;
      margin-bottom: 20px;
    }

    .pulse-dot {
      width: 8px;
      height: 8px;
      border-radius: 50%;
      background: #38bdf8;
      box-shadow: 0 0 0 0 rgba(56, 189, 248, 0.7);
      animation: pulseRing 2s infinite;
    }

    @keyframes pulseRing {
      0% { box-shadow: 0 0 0 0 rgba(56, 189, 248, 0.7); }
      70% { box-shadow: 0 0 0 8px rgba(56, 189, 248, 0); }
      100% { box-shadow: 0 0 0 0 rgba(56, 189, 248, 0); }
    }

    .hero-title {
      font-size: clamp(2rem, 3.6vw, 3.05rem);
      font-weight: 800;
      line-height: 1.16;
      letter-spacing: -0.02em;
      color: #ffffff;
      margin-bottom: 18px;
    }

    .hero-title span {
      background: linear-gradient(135deg, #38bdf8 0%, #818cf8 55%, #c084fc 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .hero-desc {
      font-size: 1.04rem;
      color: var(--text-secondary);
      line-height: 1.7;
      margin-bottom: 26px;
      max-width: 600px;
    }

    .hero-pills {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-bottom: 30px;
    }

    .pill-item {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 8px 14px;
      border-radius: 999px;
      background: rgba(15, 23, 42, 0.72);
      border: 1px solid var(--border-glass);
      font-size: 0.84rem;
      font-weight: 600;
      color: #e2e8f0;
    }

    .hero-cta {
      display: flex;
      flex-wrap: wrap;
      gap: 14px;
      align-items: center;
    }

    .hero-cta .btn {
      padding: 13px 22px;
      font-size: 0.95rem;
    }

    /* Kartu Login Glassmorphism */
    .login-card {
      background: rgba(11, 20, 42, 0.82);
      backdrop-filter: blur(20px);
      -webkit-backdrop-filter: blur(20px);
      border: 1px solid rgba(148, 163, 184, 0.22);
      border-radius: var(--radius-xl);
      padding: 30px 28px;
      box-shadow: var(--shadow-card), var(--shadow-glow);
      position: relative;
      overflow: hidden;
    }

    .login-card::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      height: 3px;
      background: linear-gradient(90deg, #38bdf8, #6366f1, #a855f7);
    }

    .login-header {
      margin-bottom: 20px;
    }

    .login-title {
      font-size: 1.32rem;
      font-weight: 800;
      color: #ffffff;
      margin-bottom: 4px;
    }

    .login-subtitle {
      font-size: 0.86rem;
      color: var(--text-muted);
    }

    .role-tabs {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 6px;
      padding: 5px;
      background: rgba(6, 11, 25, 0.75);
      border: 1px solid var(--border-glass);
      border-radius: 12px;
      margin-bottom: 20px;
    }

    .role-tab {
      padding: 9px 6px;
      border-radius: 9px;
      font-size: 0.8rem;
      font-weight: 700;
      color: var(--text-muted);
      text-align: center;
      transition: all 0.2s ease;
    }

    .role-tab:hover {
      color: var(--text-primary);
    }

    .role-tab.active {
      background: linear-gradient(135deg, rgba(14, 165, 233, 0.25), rgba(99, 102, 241, 0.32));
      color: #ffffff;
      border: 1px solid rgba(56, 189, 248, 0.45);
      box-shadow: 0 4px 12px rgba(2, 6, 23, 0.4);
    }

    .form-group {
      margin-bottom: 16px;
    }

    .form-label {
      display: block;
      font-size: 0.83rem;
      font-weight: 600;
      color: var(--text-secondary);
      margin-bottom: 7px;
    }

    .input-wrap {
      position: relative;
      display: flex;
      align-items: center;
    }

    .input-icon {
      position: absolute;
      left: 14px;
      color: var(--text-muted);
      pointer-events: none;
      display: flex;
      align-items: center;
    }

    .form-control {
      width: 100%;
      height: 46px;
      padding: 0 42px 0 42px;
      background: rgba(6, 11, 25, 0.78);
      border: 1px solid rgba(148, 163, 184, 0.25);
      border-radius: 11px;
      color: #ffffff;
      font-size: 0.92rem;
      transition: border-color 0.2s ease, box-shadow 0.2s ease;
    }

    .form-control::placeholder {
      color: #64748b;
    }

    .form-control:focus {
      outline: none;
      border-color: var(--primary);
      box-shadow: 0 0 0 3px rgba(56, 189, 248, 0.18);
    }

    .toggle-pwd-btn {
      position: absolute;
      right: 12px;
      width: 32px;
      height: 32px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: var(--text-muted);
      border-radius: 8px;
    }

    .toggle-pwd-btn:hover {
      color: var(--text-primary);
      background: rgba(255, 255, 255, 0.06);
    }

    .login-options {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      margin-bottom: 18px;
      font-size: 0.83rem;
    }

    .checkbox-label {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      color: var(--text-secondary);
      cursor: pointer;
      user-select: none;
    }

    .checkbox-label input[type="checkbox"] {
      width: 16px;
      height: 16px;
      accent-color: #0ea5e9;
      cursor: pointer;
    }

    .help-link {
      color: var(--primary);
      font-weight: 600;
    }

    .help-link:hover {
      text-decoration: underline;
    }

    .login-alert {
      padding: 10px 13px;
      border-radius: 10px;
      background: rgba(244, 63, 94, 0.14);
      border: 1px solid rgba(244, 63, 94, 0.38);
      color: #fecdd3;
      font-size: 0.83rem;
      margin-bottom: 14px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .btn-block {
      width: 100%;
      height: 48px;
      font-size: 0.96rem;
    }

    .login-security-note {
      margin-top: 16px;
      padding-top: 14px;
      border-top: 1px solid rgba(148, 163, 184, 0.14);
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      font-size: 0.78rem;
      color: var(--text-muted);
    }

    /* ==========================================================================
       5. SECTION UMUM, LAYANAN UTAMA, WARTA PENDIDIKAN & PUSAT BANTUAN
       ========================================================================== */
    .section {
      padding: 64px 0;
    }

    .section-header {
      text-align: center;
      max-width: 720px;
      margin: 0 auto 42px;
    }

    .section-kicker {
      display: inline-block;
      font-size: 0.78rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.09em;
      color: var(--primary);
      margin-bottom: 10px;
    }

    .section-title {
      font-size: clamp(1.6rem, 2.8vw, 2.2rem);
      font-weight: 800;
      color: #ffffff;
      margin-bottom: 12px;
      line-height: 1.25;
    }

    .section-desc {
      font-size: 0.98rem;
      color: var(--text-secondary);
    }

    /* Grid 4 Kartu Layanan Utama */
    .features-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 22px;
    }

    .glass-card {
      background: var(--bg-surface);
      backdrop-filter: blur(14px);
      -webkit-backdrop-filter: blur(14px);
      border: 1px solid var(--border-glass);
      border-radius: var(--radius-lg);
      padding: 26px 22px;
      transition: transform 0.22s ease, border-color 0.22s ease, background 0.22s ease;
    }

    .glass-card:hover {
      transform: translateY(-4px);
      border-color: var(--border-accent);
      background: var(--bg-surface-hover);
    }

    .feature-icon-box {
      width: 48px;
      height: 48px;
      border-radius: 13px;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 18px;
      background: rgba(56, 189, 248, 0.14);
      border: 1px solid rgba(56, 189, 248, 0.3);
      color: var(--primary);
    }

    .feature-icon-box.indigo {
      background: rgba(99, 102, 241, 0.16);
      border-color: rgba(99, 102, 241, 0.34);
      color: #a5b4fc;
    }

    .feature-icon-box.emerald {
      background: rgba(16, 185, 129, 0.15);
      border-color: rgba(16, 185, 129, 0.34);
      color: #6ee7b7;
    }

    .feature-icon-box.amber {
      background: rgba(245, 158, 11, 0.15);
      border-color: rgba(245, 158, 11, 0.34);
      color: #fcd34d;
    }

    .card-title {
      font-size: 1.08rem;
      font-weight: 700;
      color: #ffffff;
      margin-bottom: 10px;
    }

    .card-text {
      font-size: 0.9rem;
      color: var(--text-secondary);
      line-height: 1.65;
    }

    /* Filter & Grid Warta Pendidikan */
    .filter-bar {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 10px;
      margin-bottom: 32px;
    }

    .filter-btn {
      padding: 8px 16px;
      border-radius: 999px;
      font-size: 0.85rem;
      font-weight: 600;
      color: var(--text-secondary);
      background: rgba(15, 23, 42, 0.7);
      border: 1px solid var(--border-glass);
      transition: all 0.2s ease;
    }

    .filter-btn:hover {
      border-color: var(--border-accent);
      color: #ffffff;
    }

    .filter-btn.active {
      background: linear-gradient(135deg, #0ea5e9, #4f46e5);
      color: #ffffff;
      border-color: transparent;
    }

    .news-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 24px;
    }

    .news-card {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      padding: 0;
      overflow: hidden;
    }

    .news-banner {
      height: 132px;
      padding: 18px 20px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      background: linear-gradient(135deg, rgba(14, 165, 233, 0.24), rgba(79, 70, 229, 0.34));
      border-bottom: 1px solid var(--border-glass);
      position: relative;
    }

    .news-tag {
      align-self: flex-start;
      font-size: 0.73rem;
      font-weight: 700;
      padding: 4px 10px;
      border-radius: 999px;
      background: rgba(6, 11, 25, 0.72);
      color: #7dd3fc;
      border: 1px solid rgba(56, 189, 248, 0.3);
    }

    .news-meta {
      font-size: 0.78rem;
      color: #e2e8f0;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .news-body {
      padding: 22px 22px 24px;
      display: flex;
      flex-direction: column;
      flex: 1;
    }

    .news-title {
      font-size: 1.08rem;
      font-weight: 700;
      color: #ffffff;
      margin-bottom: 10px;
      line-height: 1.4;
    }

    .news-excerpt {
      font-size: 0.89rem;
      color: var(--text-secondary);
      margin-bottom: 18px;
      flex: 1;
    }

    .read-more-btn {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      font-size: 0.86rem;
      font-weight: 700;
      color: var(--primary);
      align-self: flex-start;
    }

    .read-more-btn:hover {
      color: #7dd3fc;
    }

    /* Pusat Bantuan: Accordion FAQ & Indikator Kesiapan Perangkat */
    .help-grid {
      display: grid;
      grid-template-columns: 1.25fr 0.75fr;
      gap: 28px;
      align-items: start;
    }

    .faq-list {
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .faq-item {
      background: var(--bg-surface);
      border: 1px solid var(--border-glass);
      border-radius: var(--radius-md);
      overflow: hidden;
    }

    .faq-question {
      width: 100%;
      padding: 17px 20px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 14px;
      text-align: left;
      font-weight: 700;
      font-size: 0.95rem;
      color: #ffffff;
    }

    .faq-question:hover {
      background: rgba(255, 255, 255, 0.03);
    }

    .faq-chevron {
      transition: transform 0.22s ease;
      color: var(--primary);
    }

    .faq-item.open .faq-chevron {
      transform: rotate(180deg);
    }

    .faq-answer {
      display: none;
      padding: 0 20px 18px;
      font-size: 0.9rem;
      color: var(--text-secondary);
      border-top: 1px solid rgba(148, 163, 184, 0.1);
      padding-top: 13px;
    }

    .faq-item.open .faq-answer {
      display: block;
    }

    .diag-card {
      background: rgba(11, 20, 42, 0.84);
      border: 1px solid var(--border-accent);
      border-radius: var(--radius-lg);
      padding: 24px;
    }

    .diag-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 16px;
      padding-bottom: 14px;
      border-bottom: 1px solid var(--border-glass);
    }

    .diag-status-pill {
      font-size: 0.75rem;
      font-weight: 700;
      padding: 4px 10px;
      border-radius: 999px;
      background: rgba(16, 185, 129, 0.16);
      color: #6ee7b7;
      border: 1px solid rgba(16, 185, 129, 0.35);
    }

    .diag-list {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 12px;
      margin-bottom: 18px;
    }

    .diag-row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      font-size: 0.86rem;
      padding: 9px 12px;
      border-radius: 9px;
      background: rgba(6, 11, 25, 0.65);
    }

    .diag-key {
      color: var(--text-muted);
    }

    .diag-val {
      font-weight: 700;
      color: #e2e8f0;
      text-align: right;
    }

    /* ==========================================================================
       6. FOOTER RESMI DENGAN KREDIT PENGEMBANG
       ========================================================================== */
    .footer {
      margin-top: auto;
      background: rgba(5, 9, 21, 0.92);
      border-top: 1px solid var(--border-glass);
      padding: 40px 0 28px;
    }

    .footer-top {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      gap: 28px;
      padding-bottom: 26px;
      border-bottom: 1px solid rgba(148, 163, 184, 0.14);
    }

    .footer-info {
      max-width: 440px;
    }

    .footer-desc {
      margin-top: 12px;
      font-size: 0.88rem;
      color: var(--text-muted);
    }

    .footer-links {
      display: flex;
      flex-wrap: wrap;
      gap: 22px;
      align-items: center;
      font-size: 0.88rem;
      color: var(--text-secondary);
    }

    .footer-links a:hover {
      color: var(--primary);
    }

    .footer-bottom {
      padding-top: 20px;
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: 14px;
      font-size: 0.85rem;
      color: var(--text-muted);
    }

    .developer-credit {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 6px 14px;
      border-radius: 999px;
      background: rgba(56, 189, 248, 0.1);
      border: 1px solid rgba(56, 189, 248, 0.28);
      color: #e0f2fe;
      font-weight: 600;
    }

    /* ==========================================================================
       7. WORKSPACE SETELAH LOGIN (PESERTA, PENGAWAS, ADMINISTRATOR)
       ========================================================================== */
    .workspace-bar {
      background: rgba(8, 15, 34, 0.9);
      backdrop-filter: blur(16px);
      border-bottom: 1px solid var(--border-glass);
      padding: 14px 0;
      position: sticky;
      top: 0;
      z-index: 45;
    }

    .workspace-bar-inner {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: 14px;
    }

    .user-chip {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 6px 14px;
      border-radius: 999px;
      background: rgba(30, 41, 59, 0.75);
      border: 1px solid var(--border-glass);
      font-size: 0.85rem;
    }

    .role-pill {
      font-size: 0.72rem;
      font-weight: 700;
      text-transform: uppercase;
      padding: 3px 9px;
      border-radius: 999px;
      background: rgba(56, 189, 248, 0.18);
      color: #7dd3fc;
    }

    .workspace-main {
      padding: 34px 0 60px;
      flex: 1;
    }

    .stats-row {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 18px;
      margin-bottom: 28px;
    }

    .stat-card {
      background: var(--bg-surface);
      border: 1px solid var(--border-glass);
      border-radius: var(--radius-md);
      padding: 20px;
    }

    .stat-label {
      font-size: 0.82rem;
      color: var(--text-muted);
      margin-bottom: 6px;
    }

    .stat-value {
      font-size: 1.65rem;
      font-weight: 800;
      color: #ffffff;
    }

    /* Exam Cards untuk Peserta */
    .exam-cards-grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 22px;
    }

    .exam-card {
      background: var(--bg-surface);
      border: 1px solid var(--border-glass);
      border-radius: var(--radius-lg);
      padding: 24px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      gap: 18px;
    }

    .exam-meta-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 10px;
      padding: 12px;
      border-radius: 10px;
      background: rgba(6, 11, 25, 0.65);
      font-size: 0.82rem;
    }

    /* Ruang Ujian CBT Interaktif */
    .cbt-topbar {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: 14px;
      padding: 16px 22px;
      background: rgba(11, 20, 42, 0.9);
      border: 1px solid var(--border-accent);
      border-radius: var(--radius-lg);
      margin-bottom: 22px;
    }

    .timer-box {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 8px 16px;
      border-radius: 10px;
      background: rgba(14, 165, 233, 0.16);
      border: 1px solid rgba(56, 189, 248, 0.4);
      font-weight: 800;
      font-size: 1.1rem;
      color: #7dd3fc;
      font-variant-numeric: tabular-nums;
    }

    .timer-box.warning {
      background: rgba(244, 63, 94, 0.2);
      border-color: rgba(244, 63, 94, 0.5);
      color: #fda4af;
    }

    .cbt-layout {
      display: grid;
      grid-template-columns: 1fr 310px;
      gap: 24px;
      align-items: start;
    }

    .question-box {
      background: var(--bg-surface);
      border: 1px solid var(--border-glass);
      border-radius: var(--radius-lg);
      padding: 28px;
    }

    .question-header {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      padding-bottom: 16px;
      margin-bottom: 20px;
      border-bottom: 1px solid var(--border-glass);
    }

    .question-prompt {
      font-size: 1.08rem;
      font-weight: 600;
      color: #ffffff;
      line-height: 1.7;
      margin-bottom: 24px;
    }

    .options-list {
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .option-item {
      display: flex;
      align-items: center;
      gap: 14px;
      padding: 14px 18px;
      border-radius: 12px;
      background: rgba(6, 11, 25, 0.68);
      border: 1px solid var(--border-glass);
      cursor: pointer;
      transition: all 0.18s ease;
      text-align: left;
      width: 100%;
    }

    .option-item:hover {
      border-color: var(--primary);
      background: rgba(14, 165, 233, 0.08);
    }

    .option-item.selected {
      background: rgba(14, 165, 233, 0.2);
      border-color: #38bdf8;
      box-shadow: 0 0 0 1px #38bdf8;
    }

    .option-key {
      width: 32px;
      height: 32px;
      border-radius: 8px;
      background: rgba(30, 41, 59, 0.9);
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 800;
      font-size: 0.85rem;
      color: var(--primary);
      flex-shrink: 0;
    }

    .option-item.selected .option-key {
      background: #0ea5e9;
      color: #ffffff;
    }

    .short-answer-input {
      width: 100%;
      padding: 14px 16px;
      border-radius: 12px;
      background: rgba(6, 11, 25, 0.8);
      border: 1px solid var(--border-accent);
      color: #ffffff;
      font-size: 1rem;
    }

    .short-answer-input:focus {
      outline: none;
      box-shadow: 0 0 0 3px rgba(56, 189, 248, 0.2);
    }

    .question-footer {
      margin-top: 28px;
      padding-top: 20px;
      border-top: 1px solid var(--border-glass);
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
    }

    .nav-panel {
      background: var(--bg-surface);
      border: 1px solid var(--border-glass);
      border-radius: var(--radius-lg);
      padding: 22px;
    }

    .num-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 9px;
      margin: 16px 0 20px;
    }

    .num-btn {
      height: 42px;
      border-radius: 9px;
      font-weight: 700;
      font-size: 0.9rem;
      background: rgba(15, 23, 42, 0.85);
      border: 1px solid var(--border-glass);
      color: var(--text-secondary);
      transition: all 0.15s ease;
    }

    .num-btn.answered {
      background: rgba(16, 185, 129, 0.22);
      border-color: #10b981;
      color: #6ee7b7;
    }

    .num-btn.flagged {
      background: rgba(245, 158, 11, 0.24);
      border-color: #f59e0b;
      color: #fcd34d;
    }

    .num-btn.current {
      box-shadow: 0 0 0 2px #38bdf8;
      color: #ffffff;
    }

    .legend-list {
      display: flex;
      flex-direction: column;
      gap: 7px;
      font-size: 0.78rem;
      color: var(--text-muted);
      margin-bottom: 18px;
    }

    .legend-item {
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .legend-dot {
      width: 12px;
      height: 12px;
      border-radius: 3px;
    }

    /* Tabel Pengawas & Admin */
    .table-card {
      background: var(--bg-surface);
      border: 1px solid var(--border-glass);
      border-radius: var(--radius-lg);
      padding: 22px;
      overflow-x: auto;
    }

    .table-toolbar {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: 14px;
      margin-bottom: 18px;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      min-width: 680px;
    }

    th, td {
      padding: 13px 14px;
      text-align: left;
      border-bottom: 1px solid rgba(148, 163, 184, 0.12);
      font-size: 0.88rem;
    }

    th {
      color: var(--text-muted);
      font-weight: 700;
      font-size: 0.78rem;
      text-transform: uppercase;
      letter-spacing: 0.05em;
    }

    .progress-track {
      width: 110px;
      height: 8px;
      border-radius: 999px;
      background: rgba(15, 23, 42, 0.9);
      overflow: hidden;
      display: inline-block;
      vertical-align: middle;
      margin-right: 8px;
    }

    .progress-fill {
      height: 100%;
      background: linear-gradient(90deg, #38bdf8, #10b981);
      border-radius: 999px;
    }

    .status-badge {
      display: inline-flex;
      align-items: center;
      padding: 3px 10px;
      border-radius: 999px;
      font-size: 0.75rem;
      font-weight: 700;
    }

    .status-badge.ok {
      background: rgba(16, 185, 129, 0.16);
      color: #6ee7b7;
    }

    .status-badge.warn {
      background: rgba(245, 158, 11, 0.18);
      color: #fcd34d;
    }

    .status-badge.danger {
      background: rgba(244, 63, 94, 0.18);
      color: #fda4af;
    }

    .status-badge.info {
      background: rgba(56, 189, 248, 0.16);
      color: #7dd3fc;
    }

    /* ==========================================================================
       8. MODAL DIALOG & TOAST NOTIFICATION (PENGGANTI ALERT/CONFIRM)
       ========================================================================== */
    .modal-backdrop {
      position: fixed;
      inset: 0;
      z-index: 100;
      background: rgba(3, 7, 18, 0.82);
      backdrop-filter: blur(8px);
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 20px;
    }

    .modal-box {
      width: 100%;
      max-width: 560px;
      max-height: 88vh;
      overflow-y: auto;
      background: #0d162d;
      border: 1px solid var(--border-accent);
      border-radius: var(--radius-xl);
      padding: 28px;
      box-shadow: 0 25px 60px rgba(0, 0, 0, 0.8);
    }

    .modal-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      margin-bottom: 16px;
      padding-bottom: 14px;
      border-bottom: 1px solid var(--border-glass);
    }

    .modal-title {
      font-size: 1.18rem;
      font-weight: 800;
      color: #ffffff;
    }

    .modal-close {
      width: 34px;
      height: 34px;
      border-radius: 9px;
      background: rgba(255, 255, 255, 0.06);
      color: var(--text-secondary);
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .modal-close:hover {
      background: rgba(244, 63, 94, 0.2);
      color: #fda4af;
    }

    .toast-container {
      position: fixed;
      bottom: 22px;
      right: 22px;
      z-index: 120;
      display: flex;
      flex-direction: column;
      gap: 10px;
      max-width: 360px;
    }

    .toast {
      padding: 13px 16px;
      border-radius: 12px;
      background: rgba(13, 22, 45, 0.96);
      border: 1px solid var(--border-accent);
      color: #f8fafc;
      font-size: 0.86rem;
      box-shadow: 0 12px 30px rgba(0, 0, 0, 0.6);
      display: flex;
      align-items: flex-start;
      gap: 10px;
      animation: slideInToast 0.22s ease;
    }

    @keyframes slideInToast {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* ==========================================================================
       9. MEDIA QUERIES RESPONSIF (DESKTOP, TABLET, MOBILE)
       ========================================================================== */
    @media (max-width: 1024px) {
      .hero-grid {
        grid-template-columns: 1fr;
        gap: 34px;
      }
      .features-grid {
        grid-template-columns: repeat(2, 1fr);
      }
      .news-grid {
        grid-template-columns: repeat(2, 1fr);
      }
      .help-grid {
        grid-template-columns: 1fr;
      }
      .stats-row {
        grid-template-columns: repeat(2, 1fr);
      }
      .cbt-layout {
        grid-template-columns: 1fr;
      }
    }

    @media (max-width: 768px) {
      .nav-links {
        display: none;
      }
      .mobile-menu-btn {
        display: flex;
      }
      .hero-section {
        padding: 36px 0 48px;
      }
      .exam-cards-grid {
        grid-template-columns: 1fr;
      }
      .news-grid {
        grid-template-columns: 1fr;
      }
    }

    @media (max-width: 520px) {
      .container {
        padding: 0 16px;
      }
      .features-grid {
        grid-template-columns: 1fr;
      }
      .stats-row {
        grid-template-columns: 1fr;
      }
      .login-card {
        padding: 24px 18px;
      }
      .role-tab {
        font-size: 0.74rem;
        padding: 8px 4px;
      }
    }
  </style>
</head>
<body>
  <!-- ========================================================================
       LAPISAN LATAR BELAKANG VIDEO & ANIMASI CANVAS TERKUNCI (FIXED)
       ======================================================================== -->
  <div class="bg-stage" aria-hidden="true">
    <video
      id="bg-video"
      class="bg-video"
      autoplay
      muted
      loop
      playsinline
      preload="metadata"
      onerror="this.style.display='none'"
    >
      <source
        src="https://assets.mixkit.co/videos/preview/mixkit-abstract-technology-network-lines-27662-large.mp4"
        type="video/mp4"
        onerror="this.parentElement.style.display='none'"
      />
    </video>
    <canvas id="bg-motion-canvas"></canvas>
    <div class="bg-overlay"></div>
  </div>

  <!-- ========================================================================
       SHELL APLIKASI UTAMA
       ======================================================================== -->
  <div class="app-shell">
    <!-- ======================================================================
         TAMPILAN 1: PORTAL WEBSITE & HALAMAN LOGIN
         ====================================================================== -->
    <div id="portal-view">
      <!-- Sticky Glassmorphism Navbar (Tinggi Terkunci 74px) -->
      <header class="navbar">
        <div class="container navbar-inner">
          <a href="#beranda" class="brand">
            <div class="brand-icon">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#38bdf8" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                <polygon points="12 2 22 8.5 22 15.5 12 22 2 15.5 2 8.5 12 2"></polygon>
                <circle cx="12" cy="12" r="3.2" fill="#38bdf8"></circle>
              </svg>
            </div>
            <div class="brand-text">
              <span class="brand-title">CBT-PRO <span class="brand-badge">2026</span></span>
              <span class="brand-sub">Portal Evaluasi Terpadu</span>
            </div>
          </a>

          <nav aria-label="Navigasi Utama">
            <ul class="nav-links">
              <li><a href="#beranda">Beranda</a></li>
              <li><a href="#fitur">Layanan Utama</a></li>
              <li><a href="#berita">Warta Pendidikan</a></li>
              <li><a href="#bantuan">Pusat Bantuan</a></li>
            </ul>
          </nav>

          <div class="nav-actions">
            <button type="button" class="btn btn-primary" id="nav-login-focus-btn">
              <svg width="17" height="17" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M15 3h4a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2h-4"></path>
                <polyline points="10 17 15 12 10 7"></polyline>
                <line x1="15" y1="12" x2="3" y2="12"></line>
              </svg>
              <span>Masuk Portal</span>
            </button>
            <button type="button" class="mobile-menu-btn" id="mobile-menu-toggle" aria-label="Buka Menu Navigasi">
              <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round">
                <line x1="3" y1="6" x2="21" y2="6"></line>
                <line x1="3" y1="12" x2="21" y2="12"></line>
                <line x1="3" y1="18" x2="21" y2="18"></line>
              </svg>
            </button>
          </div>
        </div>
      </header>

      <!-- Drawer Navigasi Mobile -->
      <div class="mobile-drawer" id="mobile-drawer">
        <a href="#beranda" class="mobile-nav-link">Beranda</a>
        <a href="#fitur" class="mobile-nav-link">Layanan Utama</a>
        <a href="#berita" class="mobile-nav-link">Warta Pendidikan</a>
        <a href="#bantuan" class="mobile-nav-link">Pusat Bantuan</a>
      </div>

      <!-- Hero Section 2 Kolom -->
      <main>
        <section id="beranda" class="hero-section">
          <div class="container hero-grid">
            <!-- Kolom Kiri: Identitas Portal & Keunggulan -->
            <div>
              <div class="hero-badge">
                <span class="pulse-dot"></span>
                <span>PORTAL EVALUASI DIGITAL TERPADU &bull; 2026</span>
              </div>

              <h1 class="hero-title">
                Ekosistem Ujian Berbasis Komputer yang <span>Presisi, Aman, dan Terintegrasi</span>
              </h1>

              <p class="hero-desc">
                Platform evaluasi akademik terpadu untuk penyelenggaraan asesmen digital berskala institusi. Dilengkapi pemantauan pengawas secara real-time, proteksi integritas sesi ujian, serta analisis hasil otomatis.
              </p>

              <div class="hero-pills">
                <div class="pill-item">
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="#38bdf8" stroke-width="2.3" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"></path>
                  </svg>
                  <span>Anti-Cheat &amp; Deteksi Tab</span>
                </div>
                <div class="pill-item">
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="#10b981" stroke-width="2.3" stroke-linecap="round" stroke-linejoin="round">
                    <polyline points="22 12 18 12 15 21 9 3 6 12 2 12"></polyline>
                  </svg>
                  <span>Penilaian Real-Time</span>
                </div>
                <div class="pill-item">
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="#a5b4fc" stroke-width="2.3" stroke-linecap="round" stroke-linejoin="round">
                    <rect x="2" y="3" width="20" height="14" rx="2" ry="2"></rect>
                    <line x1="8" y1="21" x2="16" y2="21"></line>
                    <line x1="12" y1="17" x2="12" y2="21"></line>
                  </svg>
                  <span>Multi-Perangkat Responsif</span>
                </div>
              </div>

              <div class="hero-cta">
                <button type="button" class="btn btn-primary" id="hero-start-btn">
                  <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                    <polygon points="5 3 19 12 5 21 5 3"></polygon>
                  </svg>
                  <span>Akses Ruang Evaluasi</span>
                </button>
                <a href="#fitur" class="btn btn-secondary">
                  <span>Pelajari Infrastruktur</span>
                </a>
              </div>
            </div>

            <!-- Kolom Kanan: Kartu Login Glassmorphism Bersih (Tanpa Daftar User/Password Demo) -->
            <div class="login-card" id="login-card-box">
              <div class="login-header">
                <h2 class="login-title">Masuk ke Sistem CBT-PRO</h2>
                <p class="login-subtitle">Pilih peran akses Anda dan masukkan kredensial resmi yang terdaftar.</p>
              </div>

              <!-- Tab Pilihan Peran -->
              <div class="role-tabs" role="tablist" aria-label="Pilih Peran Pengguna">
                <button type="button" class="role-tab active" data-role="peserta" role="tab" aria-selected="true">Peserta Ujian</button>
                <button type="button" class="role-tab" data-role="pengawas" role="tab" aria-selected="false">Pengawas</button>
                <button type="button" class="role-tab" data-role="admin" role="tab" aria-selected="false">Administrator</button>
              </div>

              <form id="login-form" novalidate>
                <div id="login-error-box" class="login-alert hidden" role="alert">
                  <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                    <circle cx="12" cy="12" r="10"></circle>
                    <line x1="12" y1="8" x2="12" y2="12"></line>
                    <line x1="12" y1="16" x2="12.01" y2="16"></line>
                  </svg>
                  <span id="login-error-text">Mohon lengkapi ID dan kata sandi Anda.</span>
                </div>

                <div class="form-group">
                  <label for="login-username" class="form-label" id="login-id-label">Nomor Peserta / Username</label>
                  <div class="input-wrap">
                    <span class="input-icon">
                      <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path>
                        <circle cx="12" cy="7" r="4"></circle>
                      </svg>
                    </span>
                    <input
                      type="text"
                      id="login-username"
                      class="form-control"
                      placeholder="Masukkan Nomor Peserta atau ID"
                      autocomplete="username"
                      required
                    />
                  </div>
                </div>

                <div class="form-group">
                  <label for="login-password" class="form-label">Kata Sandi</label>
                  <div class="input-wrap">
                    <span class="input-icon">
                      <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <rect x="3" y="11" width="18" height="11" rx="2" ry="2"></rect>
                        <path d="M7 11V7a5 5 0 0 1 10 0v4"></path>
                      </svg>
                    </span>
                    <input
                      type="password"
                      id="login-password"
                      class="form-control"
                      placeholder="Masukkan kata sandi akses"
                      autocomplete="current-password"
                      required
                    />
                    <button type="button" class="toggle-pwd-btn" id="toggle-pwd-btn" aria-label="Tampilkan atau sembunyikan kata sandi">
                      <svg id="eye-icon-show" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"></path>
                        <circle cx="12" cy="12" r="3"></circle>
                      </svg>
                      <svg id="eye-icon-hide" class="hidden" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <path d="M17.94 17.94A10.07 10.07 0 0 1 12 20c-7 0-11-8-11-8a18.45 18.45 0 0 1 5.06-5.94"></path>
                        <path d="M9.9 4.24A9.12 9.12 0 0 1 12 4c7 0 11 8 11 8a18.5 18.5 0 0 1-2.16 3.19"></path>
                        <line x1="1" y1="1" x2="23" y2="23"></line>
                      </svg>
                    </button>
                  </div>
                </div>

                <div class="login-options">
                  <label class="checkbox-label">
                    <input type="checkbox" id="remember-session" checked />
                    <span>Ingat Sesi</span>
                  </label>
                  <button type="button" class="help-link" id="account-help-btn">Bantuan Akun?</button>
                </div>

                <button type="submit" class="btn btn-primary btn-block">
                  <span>Masuk ke Sistem</span>
                  <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                    <line x1="5" y1="12" x2="19" y2="12"></line>
                    <polyline points="12 5 19 12 12 19"></polyline>
                  </svg>
                </button>
              </form>

              <div class="login-security-note">
                <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="#10b981" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                  <rect x="3" y="11" width="18" height="11" rx="2" ry="2"></rect>
                  <path d="M7 11V7a5 5 0 0 1 10 0v4"></path>
                </svg>
                <span>Koneksi Sesi Terenkripsi &amp; Terpantau</span>
              </div>
            </div>
          </div>
        </section>

        <!-- Section Layanan Utama & Keunggulan (#fitur) -->
        <section id="fitur" class="section">
          <div class="container">
            <div class="section-header">
              <span class="section-kicker">Arsitektur Evaluasi Modern</span>
              <h2 class="section-title">Layanan Utama &amp; Keunggulan Sistem</h2>
              <p class="section-desc">
                Dirancang untuk menjamin keandalan pelaksanaan ujian berbasis komputer dengan standar integritas akademik tertinggi.
              </p>
            </div>

            <div class="features-grid">
              <article class="glass-card">
                <div class="feature-icon-box">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.1" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
                    <polyline points="14 2 14 8 20 8"></polyline>
                    <line x1="16" y1="13" x2="8" y2="13"></line>
                    <line x1="16" y1="17" x2="8" y2="17"></line>
                  </svg>
                </div>
                <h3 class="card-title">Multi-Tipe Soal Lengkap</h3>
                <p class="card-text">
                  Mendukung format Pilihan Ganda, Benar/Salah, hingga Isian Singkat dalam satu paket evaluasi terstruktur dengan navigasi butir soal interaktif.
                </p>
              </article>

              <article class="glass-card">
                <div class="feature-icon-box indigo">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.1" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"></path>
                    <path d="M9 12l2 2 4-4"></path>
                  </svg>
                </div>
                <h3 class="card-title">Sistem Pengawasan &amp; Anti-Cheat</h3>
                <p class="card-text">
                  Sensor fokus layar otomatis mendeteksi perpindahan tab atau jendela browser, mencatat log pelanggaran, dan mengirim peringatan langsung ke pengawas.
                </p>
              </article>

              <article class="glass-card">
                <div class="feature-icon-box emerald">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.1" stroke-linecap="round" stroke-linejoin="round">
                    <line x1="18" y1="20" x2="18" y2="10"></line>
                    <line x1="12" y1="20" x2="12" y2="4"></line>
                    <line x1="6" y1="20" x2="6" y2="14"></line>
                  </svg>
                </div>
                <h3 class="card-title">Penilaian &amp; Analisis Real-Time</h3>
                <p class="card-text">
                  Kalkulasi skor otomatis seketika setelah peserta menyelesaikan sesi ujian, lengkap dengan rincian ketepatan jawaban dan rekapitulasi nilai.
                </p>
              </article>

              <article class="glass-card">
                <div class="feature-icon-box amber">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.1" stroke-linecap="round" stroke-linejoin="round">
                    <rect x="2" y="3" width="20" height="14" rx="2" ry="2"></rect>
                    <line x1="8" y1="21" x2="16" y2="21"></line>
                    <line x1="12" y1="17" x2="12" y2="21"></line>
                  </svg>
                </div>
                <h3 class="card-title">Stabilitas &amp; Kompatibilitas Perangkat</h3>
                <p class="card-text">
                  Arsitektur ringan tanpa ketergantungan framework eksternal berat, menjaga tata letak tetap terkunci rapi di desktop, laptop, tablet, maupun ponsel.
                </p>
              </article>
            </div>
          </div>
        </section>

        <!-- Section Warta & Informasi Perkembangan Pendidikan (#berita) -->
        <section id="berita" class="section">
          <div class="container">
            <div class="section-header">
              <span class="section-kicker">Informasi &amp; Publikasi Resmi</span>
              <h2 class="section-title">Warta &amp; Perkembangan Pendidikan</h2>
              <p class="section-desc">
                Pembaruan kebijakan asesmen nasional, transformasi digital pembelajaran, serta pengumuman jadwal evaluasi akademik.
              </p>
            </div>

            <!-- Filter Kategori -->
            <div class="filter-bar" role="group" aria-label="Filter Kategori Berita">
              <button type="button" class="filter-btn active" data-category="all">Semua</button>
              <button type="button" class="filter-btn" data-category="Kebijakan &amp; Kurikulum">Kebijakan &amp; Kurikulum</button>
              <button type="button" class="filter-btn" data-category="Transformasi Digital">Transformasi Digital</button>
              <button type="button" class="filter-btn" data-category="Info Evaluasi">Info Evaluasi</button>
            </div>

            <!-- Grid Kartu Berita -->
            <div class="news-grid" id="news-grid-container"></div>
          </div>
        </section>

        <!-- Section Pusat Bantuan (#bantuan) -->
        <section id="bantuan" class="section">
          <div class="container">
            <div class="section-header">
              <span class="section-kicker">Dukungan Teknis &amp; Diagnostik</span>
              <h2 class="section-title">Pusat Bantuan Peserta &amp; Pengawas</h2>
              <p class="section-desc">
                Panduan singkat mengatasi kendala teknis serta pemeriksaan otomatis kesiapan perangkat sebelum memulai sesi evaluasi.
              </p>
            </div>

            <div class="help-grid">
              <!-- Kolom Kiri: Accordion FAQ -->
              <div class="faq-list" id="faq-accordion">
                <div class="faq-item open">
                  <button type="button" class="faq-question">
                    <span>1. Bagaimana prosedur masuk ke ruang ujian CBT-PRO?</span>
                    <svg class="faq-chevron" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                      <polyline points="6 9 12 15 18 9"></polyline>
                    </svg>
                  </button>
                  <div class="faq-answer">
                    Pilih tab peran <strong>Peserta Ujian</strong> pada kartu login di bagian atas halaman, masukkan Nomor Peserta/ID serta Kata Sandi resmi Anda, lalu klik tombol <strong>Masuk ke Sistem</strong>. Setelah masuk, pilih jadwal ujian aktif dan setujui tata tertib ujian.
                  </div>
                </div>

                <div class="faq-item">
                  <button type="button" class="faq-question">
                    <span>2. Apa yang terjadi jika peserta berpindah tab atau membuka aplikasi lain saat ujian?</span>
                    <svg class="faq-chevron" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                      <polyline points="6 9 12 15 18 9"></polyline>
                    </svg>
                  </button>
                  <div class="faq-answer">
                    Sistem pengawasan anti-cheat akan mendeteksi perpindahan fokus jendela secara otomatis, mencatat waktu kejadian ke dashboard pengawas, dan menampilkan peringatan keras. Jika pelanggaran mencapai batas maksimal (3 kali), sesi ujian akan dikunci dan dikumpulkan otomatis.
                  </div>
                </div>

                <div class="faq-item">
                  <button type="button" class="faq-question">
                    <span>3. Apakah jawaban tersimpan aman apabila koneksi internet sempat melambat?</span>
                    <svg class="faq-chevron" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                      <polyline points="6 9 12 15 18 9"></polyline>
                    </svg>
                  </button>
                  <div class="faq-answer">
                    Ya. Setiap pilihan jawaban yang diklik peserta langsung disimpan ke memori sesi lokal perangkat secara real-time sehingga progres pengerjaan tidak hilang akibat fluktuasi jaringan sementara.
                  </div>
                </div>

                <div class="faq-item">
                  <button type="button" class="faq-question">
                    <span>4. Bagaimana jika saya lupa kata sandi atau akun terkunci?</span>
                    <svg class="faq-chevron" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                      <polyline points="6 9 12 15 18 9"></polyline>
                    </svg>
                  </button>
                  <div class="faq-answer">
                    Hubungi pengawas ruang ujian atau panitia administrator IT institusi Anda untuk melakukan reset sesi maupun pembaruan kredensial akun secara resmi.
                  </div>
                </div>
              </div>

              <!-- Kolom Kanan: Indikator Kesiapan Perangkat Otomatis -->
              <aside class="diag-card" aria-label="Indikator Kesiapan Perangkat">
                <div class="diag-header">
                  <div>
                    <h3 class="card-title" style="margin-bottom: 2px;">Kesiapan Perangkat</h3>
                    <p style="font-size: 0.78rem; color: var(--text-muted);">Diagnostik Browser &amp; Sistem Otomatis</p>
                  </div>
                  <span class="diag-status-pill" id="diag-overall-badge">SIAP UJIAN</span>
                </div>

                <ul class="diag-list">
                  <li class="diag-row">
                    <span class="diag-key">Peramban (Browser)</span>
                    <span class="diag-val" id="diag-browser">Mendeteksi...</span>
                  </li>
                  <li class="diag-row">
                    <span class="diag-key">Resolusi Layar</span>
                    <span class="diag-val" id="diag-screen">Mendeteksi...</span>
                  </li>
                  <li class="diag-row">
                    <span class="diag-key">Status Jaringan</span>
                    <span class="diag-val" id="diag-network">Mendeteksi...</span>
                  </li>
                  <li class="diag-row">
                    <span class="diag-key">Penyimpanan Lokal</span>
                    <span class="diag-val" id="diag-storage">Mendeteksi...</span>
                  </li>
                  <li class="diag-row">
                    <span class="diag-key">Waktu Sistem</span>
                    <span class="diag-val" id="diag-clock">Mendeteksi...</span>
                  </li>
                </ul>

                <button type="button" class="btn btn-secondary btn-block" id="recheck-diag-btn" style="height: 42px;">
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                    <polyline points="23 4 23 10 17 10"></polyline>
                    <path d="M20.49 15a9 9 0 1 1-2.12-9.36L23 10"></path>
                  </svg>
                  <span>Uji Ulang Kesiapan</span>
                </button>
              </aside>
            </div>
          </div>
        </section>
      </main>

      <!-- Footer Resmi -->
      <footer class="footer">
        <div class="container">
          <div class="footer-top">
            <div class="footer-info">
              <div class="brand">
                <div class="brand-icon" style="width: 36px; height: 36px;">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#38bdf8" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                    <polygon points="12 2 22 8.5 22 15.5 12 22 2 15.5 2 8.5 12 2"></polygon>
                    <circle cx="12" cy="12" r="3" fill="#38bdf8"></circle>
                  </svg>
                </div>
                <span class="brand-title">CBT-PRO</span>
              </div>
              <p class="footer-desc">
                Portal Website &amp; Sistem Evaluasi Terpadu Berbasis Komputer. Dirancang dengan arsitektur web modern yang ringan, aman, dan presisi.
              </p>
            </div>

            <div class="footer-links">
              <a href="#beranda">Beranda</a>
              <a href="#fitur">Layanan Utama</a>
              <a href="#berita">Warta Pendidikan</a>
              <a href="#bantuan">Pusat Bantuan</a>
            </div>
          </div>

          <div class="footer-bottom">
            <span>&copy; 2026 CBT-PRO &bull; Sistem Evaluasi Terpadu. Seluruh hak cipta dilindungi.</span>
            <span class="developer-credit">
              <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="#38bdf8" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                <polyline points="16 18 22 12 16 6"></polyline>
                <polyline points="8 6 2 12 8 18"></polyline>
              </svg>
              <span>Pembuat Aplikasi: Jovano F Kakalang, S.Ak</span>
            </span>
          </div>
        </div>
      </footer>
    </div>

    <!-- ======================================================================
         TAMPILAN 2: WORKSPACE TERPADU SETELAH LOGIN
         ====================================================================== -->
    <div id="workspace-view" class="hidden">
      <header class="workspace-bar">
        <div class="container workspace-bar-inner">
          <div class="brand">
            <div class="brand-icon" style="width: 38px; height: 38px;">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#38bdf8" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                <polygon points="12 2 22 8.5 22 15.5 12 22 2 15.5 2 8.5 12 2"></polygon>
                <circle cx="12" cy="12" r="3" fill="#38bdf8"></circle>
              </svg>
            </div>
            <div class="brand-text">
              <span class="brand-title">CBT-PRO Workspace</span>
              <span class="brand-sub" id="ws-subtitle">Panel Evaluasi Terpadu</span>
            </div>
          </div>

          <div style="display: flex; align-items: center; gap: 12px; flex-wrap: wrap;">
            <div class="user-chip">
              <span class="role-pill" id="ws-role-badge">PESERTA</span>
              <strong id="ws-user-display">ID Pengguna</strong>
            </div>
            <button type="button" class="btn btn-danger btn-sm" id="logout-btn">
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4"></path>
                <polyline points="16 17 21 12 16 7"></polyline>
                <line x1="21" y1="12" x2="9" y2="12"></line>
              </svg>
              <span>Keluar</span>
            </button>
          </div>
        </div>
      </header>

      <main class="workspace-main">
        <div class="container">
          <!-- A. DASHBOARD PESERTA UJIAN -->
          <section id="peserta-dashboard" class="hidden">
            <!-- Sub-view 1: Daftar Jadwal Ujian -->
            <div id="peserta-home-subview">
              <div class="glass-card" style="margin-bottom: 26px; display: flex; flex-wrap: wrap; align-items: center; justify-content: space-between; gap: 16px;">
                <div>
                  <span class="section-kicker" style="margin-bottom: 4px;">Ruang Peserta Terverifikasi</span>
                  <h2 style="font-size: 1.45rem; font-weight: 800; color: #fff;" id="peserta-welcome-title">Selamat Datang di Sesi Evaluasi</h2>
                  <p style="font-size: 0.9rem; color: var(--text-secondary);">Pastikan Anda membaca tata tertib sebelum memulai ujian. Selama ujian berlangsung, perpindahan tab akan dipantau sistem.</p>
                </div>
                <span class="status-badge ok">Status Perangkat: Terkoneksi</span>
              </div>

              <div class="exam-cards-grid" id="peserta-exam-list"></div>
            </div>

            <!-- Sub-view 2: Ruang Ujian CBT Interaktif -->
            <div id="peserta-exam-room" class="hidden">
              <div class="cbt-topbar">
                <div>
                  <span style="font-size: 0.76rem; color: var(--primary); font-weight: 700; text-transform: uppercase;">Sesi Ujian Aktif</span>
                  <h2 style="font-size: 1.15rem; font-weight: 800; color: #fff;" id="active-exam-title">Judul Ujian</h2>
                </div>

                <div style="display: flex; align-items: center; gap: 12px; flex-wrap: wrap;">
                  <span class="status-badge warn" id="violation-counter-badge">Pelanggaran Tab: 0 / 3</span>
                  <div class="timer-box" id="exam-timer-box">
                    <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                      <circle cx="12" cy="12" r="10"></circle>
                      <polyline points="12 6 12 12 16 14"></polyline>
                    </svg>
                    <span id="exam-timer-text">30:00</span>
                  </div>
                </div>
              </div>

              <div class="cbt-layout">
                <!-- Area Soal -->
                <div class="question-box">
                  <div class="question-header">
                    <div style="display: flex; align-items: center; gap: 10px;">
                      <span class="role-pill" id="q-number-badge">Soal 1 dari 8</span>
                      <span class="status-badge info" id="q-type-badge">Pilihan Ganda</span>
                    </div>
                    <span style="font-size: 0.82rem; color: var(--text-muted);" id="q-category-label">Kompetensi Dasar</span>
                  </div>

                  <div class="question-prompt" id="q-prompt-text">Memuat soal...</div>

                  <div id="q-answer-area"></div>

                  <div class="question-footer">
                    <button type="button" class="btn btn-secondary" id="prev-q-btn">
                      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                        <polyline points="15 18 9 12 15 6"></polyline>
                      </svg>
                      <span>Sebelumnya</span>
                    </button>

                    <button type="button" class="btn btn-amber" id="flag-q-btn">
                      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                        <path d="M4 15s1-1 4-1 5 2 8 2 4-1 4-1V3s-1 1-4 1-5-2-8-2-4 1-4 1z"></path>
                        <line x1="4" y1="22" x2="4" y2="15"></line>
                      </svg>
                      <span id="flag-btn-label">Tandai Ragu-ragu</span>
                    </button>

                    <button type="button" class="btn btn-primary" id="next-q-btn">
                      <span>Selanjutnya</span>
                      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                        <polyline points="9 18 15 12 9 6"></polyline>
                      </svg>
                    </button>
                  </div>
                </div>

                <!-- Panel Navigasi Nomor Soal -->
                <aside class="nav-panel">
                  <h3 class="card-title" style="font-size: 1rem;">Navigasi Butir Soal</h3>
                  <div class="num-grid" id="question-nav-grid"></div>

                  <div class="legend-list">
                    <div class="legend-item">
                      <span class="legend-dot" style="background: #10b981;"></span>
                      <span>Sudah Dijawab (<strong id="count-answered">0</strong>)</span>
                    </div>
                    <div class="legend-item">
                      <span class="legend-dot" style="background: #f59e0b;"></span>
                      <span>Ragu-ragu (<strong id="count-flagged">0</strong>)</span>
                    </div>
                    <div class="legend-item">
                      <span class="legend-dot" style="background: #334155;"></span>
                      <span>Belum Dijawab (<strong id="count-unanswered">0</strong>)</span>
                    </div>
                  </div>

                  <button type="button" class="btn btn-emerald btn-block" id="finish-exam-btn" style="height: 44px;">
                    <svg width="17" height="17" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                      <polyline points="20 6 9 17 4 12"></polyline>
                    </svg>
                    <span>Selesai &amp; Kumpulkan</span>
                  </button>
                </aside>
              </div>
            </div>

            <!-- Sub-view 3: Rekap Hasil Ujian Otomatis -->
            <div id="peserta-result-subview" class="hidden">
              <div class="glass-card" style="max-width: 860px; margin: 0 auto;">
                <div style="text-align: center; padding-bottom: 22px; border-bottom: 1px solid var(--border-glass); margin-bottom: 22px;">
                  <span class="status-badge ok" style="margin-bottom: 10px;">Evaluasi Selesai &amp; Tersimpan</span>
                  <h2 style="font-size: 1.6rem; font-weight: 800; color: #fff; margin-bottom: 6px;" id="result-exam-name">Rekap Hasil Ujian</h2>
                  <p style="font-size: 0.9rem; color: var(--text-secondary);" id="result-meta-info">Peserta &bull; Waktu Selesai</p>

                  <div style="margin: 22px auto 8px; width: 136px; height: 136px; border-radius: 50%; background: linear-gradient(135deg, rgba(14,165,233,0.22), rgba(99,102,241,0.32)); border: 3px solid #38bdf8; display: flex; flex-direction: column; align-items: center; justify-content: center;">
                    <span style="font-size: 0.75rem; color: var(--text-muted); font-weight: 700;">SKOR AKHIR</span>
                    <span style="font-size: 2.4rem; font-weight: 800; color: #ffffff; line-height: 1.1;" id="result-score-val">0</span>
                  </div>
                  <p style="font-weight: 700; color: #7dd3fc;" id="result-predicate-text">Predikat: Sangat Baik</p>
                </div>

                <div class="stats-row" style="grid-template-columns: repeat(3, 1fr); margin-bottom: 22px;">
                  <div class="stat-card" style="text-align: center;">
                    <div class="stat-label">Jawaban Benar</div>
                    <div class="stat-value" style="color: #6ee7b7;" id="result-correct-val">0</div>
                  </div>
                  <div class="stat-card" style="text-align: center;">
                    <div class="stat-label">Jawaban Salah / Kosong</div>
                    <div class="stat-value" style="color: #fda4af;" id="result-wrong-val">0</div>
                  </div>
                  <div class="stat-card" style="text-align: center;">
                    <div class="stat-label">Catatan Pelanggaran Tab</div>
                    <div class="stat-value" style="color: #fcd34d;" id="result-violation-val">0</div>
                  </div>
                </div>

                <div id="result-review-list" style="display: flex; flex-direction: column; gap: 10px; margin-bottom: 24px;"></div>

                <div style="text-align: center;">
                  <button type="button" class="btn btn-primary" id="back-to-peserta-home-btn">
                    <span>Kembali ke Daftar Ujian</span>
                  </button>
                </div>
              </div>
            </div>
          </section>

          <!-- B. DASHBOARD PENGAWAS -->
          <section id="pengawas-dashboard" class="hidden">
            <div class="stats-row">
              <div class="stat-card">
                <div class="stat-label">Total Peserta Terpantau</div>
                <div class="stat-value" id="proctor-stat-total">0</div>
              </div>
              <div class="stat-card">
                <div class="stat-label">Sedang Mengerjakan</div>
                <div class="stat-value" style="color: #38bdf8;" id="proctor-stat-active">0</div>
              </div>
              <div class="stat-card">
                <div class="stat-label">Telah Menyelesaikan</div>
                <div class="stat-value" style="color: #10b981;" id="proctor-stat-done">0</div>
              </div>
              <div class="stat-card">
                <div class="stat-label">Peringatan Integritas Tab</div>
                <div class="stat-value" style="color: #f59e0b;" id="proctor-stat-warn">0</div>
              </div>
            </div>

            <div class="table-card">
              <div class="table-toolbar">
                <div>
                  <h2 class="card-title" style="margin-bottom: 2px;">Pemantauan Sesi Peserta Real-Time</h2>
                  <p style="font-size: 0.83rem; color: var(--text-muted);">Pantau progres soal, status fokus jendela, dan tindakan pengawasan ruang.</p>
                </div>
                <div style="display: flex; gap: 10px; flex-wrap: wrap;">
                  <input type="text" id="proctor-search-input" class="form-control" style="height: 38px; padding: 0 14px; width: 220px;" placeholder="Cari ID / Nama peserta..." />
                  <button type="button" class="btn btn-secondary btn-sm" id="proctor-simulate-btn">
                    <span>Simulasi Sinkronisasi</span>
                  </button>
                </div>
              </div>

              <table>
                <thead>
                  <tr>
                    <th>ID Peserta</th>
                    <th>Nama Peserta</th>
                    <th>Ruang</th>
                    <th>Progres</th>
                    <th>Status</th>
                    <th>Pelanggaran Tab</th>
                    <th>Aksi Pengawas</th>
                  </tr>
                </thead>
                <tbody id="proctor-table-body"></tbody>
              </table>
            </div>
          </section>

          <!-- C. DASHBOARD ADMINISTRATOR -->
          <section id="admin-dashboard" class="hidden">
            <div class="stats-row">
              <div class="stat-card">
                <div class="stat-label">Bank Soal Aktif</div>
                <div class="stat-value" id="admin-stat-questions">0</div>
              </div>
              <div class="stat-card">
                <div class="stat-label">Paket Evaluasi</div>
                <div class="stat-value" style="color: #38bdf8;" id="admin-stat-exams">2</div>
              </div>
              <div class="stat-card">
                <div class="stat-label">Peserta Terjadwal</div>
                <div class="stat-value" style="color: #10b981;">148</div>
              </div>
              <div class="stat-card">
                <div class="stat-label">Status Server</div>
                <div class="stat-value" style="color: #a5b4fc; font-size: 1.25rem; padding-top: 6px;">OPTIMAL</div>
              </div>
            </div>

            <!-- Manajemen Bank Soal -->
            <div class="table-card" style="margin-bottom: 26px;">
              <div class="table-toolbar">
                <div>
                  <h2 class="card-title" style="margin-bottom: 2px;">Manajemen Bank Soal Terpadu</h2>
                  <p style="font-size: 0.83rem; color: var(--text-muted);">Soal yang ditambahkan di sini langsung aktif pada ruang ujian peserta.</p>
                </div>
                <button type="button" class="btn btn-primary btn-sm" id="open-add-question-btn">
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round">
                    <line x1="12" y1="5" x2="12" y2="19"></line>
                    <line x1="5" y1="12" x2="19" y2="12"></line>
                  </svg>
                  <span>Tambah Soal Baru</span>
                </button>
              </div>

              <table>
                <thead>
                  <tr>
                    <th>No</th>
                    <th>Tipe Soal</th>
                    <th>Kategori</th>
                    <th>Pertanyaan</th>
                    <th>Kunci Jawaban</th>
                    <th>Aksi</th>
                  </tr>
                </thead>
                <tbody id="admin-questions-tbody"></tbody>
              </table>
            </div>

            <!-- Manajemen Jadwal Ujian -->
            <div class="table-card">
              <div class="table-toolbar">
                <div>
                  <h2 class="card-title" style="margin-bottom: 2px;">Pengaturan Jadwal &amp; Sesi Evaluasi</h2>
                  <p style="font-size: 0.83rem; color: var(--text-muted);">Kontrol ketersediaan paket ujian bagi peserta.</p>
                </div>
              </div>

              <table>
                <thead>
                  <tr>
                    <th>Kode Paket</th>
                    <th>Nama Evaluasi</th>
                    <th>Durasi</th>
                    <th>Status Sesi</th>
                    <th>Kontrol</th>
                  </tr>
                </thead>
                <tbody id="admin-schedules-tbody"></tbody>
              </table>
            </div>
          </section>
        </div>
      </main>
    </div>
  </div>

  <!-- ========================================================================
       MODAL DINAMIS & TOAST CONTAINER
       ======================================================================== -->
  <div id="app-modal-backdrop" class="modal-backdrop hidden" role="dialog" aria-modal="true">
    <div class="modal-box">
      <div class="modal-header">
        <h3 class="modal-title" id="app-modal-title">Judul Modal</h3>
        <button type="button" class="modal-close" id="app-modal-close-btn" aria-label="Tutup Modal">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round">
            <line x1="18" y1="6" x2="6" y2="18"></line>
            <line x1="6" y1="6" x2="18" y2="18"></line>
          </svg>
        </button>
      </div>
      <div id="app-modal-body"></div>
    </div>
  </div>

  <div id="toast-container" class="toast-container" aria-live="polite"></div>

  <!-- ========================================================================
       JAVASCRIPT MANDIRI (ANIMASI LATAR, LOGIN, CBT ENGINE, PENGAWAS, ADMIN)
       ======================================================================== -->
  <script>
    (function () {
      'use strict';

      /* ----------------------------------------------------------------------
         1. ANIMASI LATAR BELAKANG CANVAS 60FPS (AURORA + JARINGAN SIMPUL)
         ---------------------------------------------------------------------- */
      function initBackgroundMotion() {
        const canvas = document.getElementById('bg-motion-canvas');
        if (!canvas) return;
        const ctx = canvas.getContext('2d');
        if (!ctx) return;

        let width = 0;
        let height = 0;
        let dpr = 1;
        let particles = [];
        let tick = 0;

        function resizeCanvas() {
          dpr = Math.min(window.devicePixelRatio || 1, 2);
          width = window.innerWidth;
          height = window.innerHeight;
          canvas.width = Math.floor(width * dpr);
          canvas.height = Math.floor(height * dpr);
          ctx.setTransform(dpr, 0, 0, dpr, 0, 0);

          const count = Math.min(58, Math.max(24, Math.floor((width * height) / 26000)));
          particles = [];
          for (let i = 0; i < count; i++) {
            particles.push({
              x: Math.random() * width,
              y: Math.random() * height,
              vx: (Math.random() - 0.5) * 0.42,
              vy: (Math.random() - 0.5) * 0.42,
              r: Math.random() * 2 + 1.1,
              hue: Math.random() > 0.45 ? '56, 189, 248' : '129, 140, 248'
            });
          }
        }

        function drawAuroraWaves() {
          tick += 0.008;
          const grad1 = ctx.createRadialGradient(
            width * (0.28 + Math.sin(tick) * 0.08),
            height * (0.25 + Math.cos(tick * 0.8) * 0.06),
            20,
            width * 0.3,
            height * 0.3,
            Math.max(width, height) * 0.55
          );
          grad1.addColorStop(0, 'rgba(56, 189, 248, 0.14)');
          grad1.addColorStop(1, 'rgba(56, 189, 248, 0)');
          ctx.fillStyle = grad1;
          ctx.fillRect(0, 0, width, height);

          const grad2 = ctx.createRadialGradient(
            width * (0.76 + Math.cos(tick * 0.9) * 0.08),
            height * (0.68 + Math.sin(tick * 0.7) * 0.06),
            20,
            width * 0.75,
            height * 0.65,
            Math.max(width, height) * 0.52
          );
          grad2.addColorStop(0, 'rgba(99, 102, 241, 0.15)');
          grad2.addColorStop(1, 'rgba(99, 102, 241, 0)');
          ctx.fillStyle = grad2;
          ctx.fillRect(0, 0, width, height);
        }

        function renderFrame() {
          ctx.clearRect(0, 0, width, height);
          drawAuroraWaves();

          const maxDist = 145;
          for (let i = 0; i < particles.length; i++) {
            const p = particles[i];
            p.x += p.vx;
            p.y += p.vy;

            if (p.x < 0 || p.x > width) p.vx *= -1;
            if (p.y < 0 || p.y > height) p.vy *= -1;

            for (let j = i + 1; j < particles.length; j++) {
              const q = particles[j];
              const dx = p.x - q.x;
              const dy = p.y - q.y;
              const dist = Math.hypot(dx, dy);
              if (dist < maxDist) {
                const alpha = (1 - dist / maxDist) * 0.22;
                ctx.strokeStyle = 'rgba(125, 211, 252, ' + alpha.toFixed(3) + ')';
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.moveTo(p.x, p.y);
                ctx.lineTo(q.x, q.y);
                ctx.stroke();
              }
            }

            ctx.fillStyle = 'rgba(' + p.hue + ', 0.78)';
            ctx.beginPath();
            ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
            ctx.fill();
          }

          requestAnimationFrame(renderFrame);
        }

        resizeCanvas();
        window.addEventListener('resize', resizeCanvas);
        renderFrame();
      }

      /* ----------------------------------------------------------------------
         2. DATA PORTAL, WARTA PENDIDIKAN, BANK SOAL & PENGAWASAN
         ---------------------------------------------------------------------- */
      const NEWS_ITEMS = [
        {
          id: 'n1',
          category: 'Kebijakan & Kurikulum',
          date: '18 November 2026',
          readTime: '4 Menit Baca',
          title: 'Penguatan Standar Asesmen Diagnostik Berbasis Kompetensi Literasi & Numerasi',
          excerpt: 'Evaluasi akademik modern menekankan pengukuran penalaran kritis, pemecahan masalah kontekstual, dan analisis data secara terukur.',
          content: 'Pelaksanaan evaluasi pendidikan tahun akademik 2026 menitikberatkan pada asesmen diagnostik berbasis kompetensi. Melalui integrasi butir soal multi-format seperti pilihan ganda kompleks, pernyataan benar/salah, dan isian singkat, institusi dapat memetakan capaian literasi serta numerasi peserta didik secara lebih objektif dan komprehensif.'
        },
        {
          id: 'n2',
          category: 'Transformasi Digital',
          date: '12 November 2026',
          readTime: '3 Menit Baca',
          title: 'Arsitektur Cloud-Ready & Ketahanan Sesi Ujian di Berbagai Kondisi Jaringan',
          excerpt: 'Penerapan penyimpanan progres lokal otomatis memastikan stabilitas pengerjaan soal meski terjadi fluktuasi konektivitas.',
          content: 'Infrastruktur CBT-PRO dirancang menggunakan standar antarmuka ringan tanpa ketergantungan aset berat. Setiap interaksi jawaban peserta dicatat secara instan ke penyimpanan lokal terenkripsi dan disinkronisasikan berkala ke panel pengawas, sehingga meminimalkan risiko kehilangan data saat ujian berlangsung.'
        },
        {
          id: 'n3',
          category: 'Info Evaluasi',
          date: '05 November 2026',
          readTime: '3 Menit Baca',
          title: 'Panduan Tata Tertib & Integritas Akademik Peserta Evaluasi Berbasis Komputer',
          excerpt: 'Ketahui prosedur verifikasi perangkat, aturan fokus layar browser, serta mekanisme pemantauan ruang virtual oleh pengawas.',
          content: 'Seluruh peserta diwajibkan melakukan pengecekan kesiapan perangkat minimal 15 menit sebelum jadwal sesi dimulai. Selama ujian berlangsung, peserta dilarang meninggalkan jendela browser ujian atau membuka tab lain. Sistem pengawasan akan mencatat setiap perpindahan fokus layar secara otomatis.'
        }
      ];

      let QUESTIONS_BANK = [
        {
          id: 'Q01',
          type: 'multiple_choice',
          category: 'Literasi Digital & Sistem',
          prompt: 'Apa tujuan utama penerapan mekanisme deteksi perpindahan tab (focus monitoring) pada sistem evaluasi berbasis komputer?',
          options: [
            'Mempercepat proses pengunduhan gambar pada halaman web',
            'Menjaga integritas ujian dengan mendeteksi aktivitas meninggalkan halaman soal',
            'Mengurangi kapasitas memori RAM yang digunakan browser',
            'Mengubah ukuran tampilan huruf secara otomatis saat ujian'
          ],
          correctAnswer: 1
        },
        {
          id: 'Q02',
          type: 'multiple_choice',
          category: 'Penalaran Numerasi',
          prompt: 'Sebuah server ujian memproses 120 paket jawaban dalam waktu 4 menit dengan kecepatan konstan. Berapa paket jawaban yang diproses dalam 7 menit?',
          options: [
            '180 paket',
            '200 paket',
            '210 paket',
            '240 paket'
          ],
          correctAnswer: 2
        },
        {
          id: 'Q03',
          type: 'true_false',
          category: 'Keamanan Informasi',
          prompt: 'Pernyataan: Menyimpan progres jawaban peserta secara berkala pada penyimpanan sesi lokal membantu mencegah hilangnya jawaban ketika koneksi internet terputus sesaat.',
          options: ['Benar', 'Salah'],
          correctAnswer: 0
        },
        {
          id: 'Q04',
          type: 'multiple_choice',
          category: 'Literasi Sains & Data',
          prompt: 'Dalam analisis hasil evaluasi, indikator tingkat ketuntasan klasikal 85% dari 40 peserta menunjukkan bahwa jumlah peserta yang tuntas adalah...',
          options: [
            '32 peserta',
            '34 peserta',
            '36 peserta',
            '38 peserta'
          ],
          correctAnswer: 1
        },
        {
          id: 'Q05',
          type: 'true_false',
          category: 'Tata Tertib Evaluasi',
          prompt: 'Pernyataan: Peserta ujian diperbolehkan membuka tab peramban baru untuk mencari referensi selama penghitung waktu mundur belum berakhir.',
          options: ['Benar', 'Salah'],
          correctAnswer: 1
        },
        {
          id: 'Q06',
          type: 'short_answer',
          category: 'Penalaran Logika',
          prompt: 'Lengkapi barisan bilangan berikut dengan satu angka yang tepat: 3, 6, 12, 24, ...',
          correctAnswer: '48'
        },
        {
          id: 'Q07',
          type: 'multiple_choice',
          category: 'Kompetensi Akademik',
          prompt: 'Manakah langkah pertama yang paling tepat dilakukan peserta sebelum menekan tombol "Mulai Ujian" pada portal CBT-PRO?',
          options: [
            'Menutup seluruh aplikasi latar belakang dan memeriksa kesiapan perangkat',
            'Menghapus riwayat peramban saat soal pertama sudah tampil',
            'Membuka beberapa jendela browser sekaligus sebagai cadangan',
            'Menonaktifkan koneksi jaringan sebelum masuk ke ruang ujian'
          ],
          correctAnswer: 0
        },
        {
          id: 'Q08',
          type: 'short_answer',
          category: 'Terminologi Sistem',
          prompt: 'Tuliskan singkatan tiga huruf untuk sistem ujian berbasis komputer yang digunakan pada portal ini (contoh format: ABC).',
          correctAnswer: 'CBT'
        }
      ];

      let EXAM_SCHEDULES = [
        {
          id: 'PKT-2026-A',
          title: 'Asesmen Kompetensi Literasi & Numerasi Terpadu 2026',
          subject: 'Evaluasi Utama Institusi',
          durationMinutes: 30,
          active: true
        },
        {
          id: 'PKT-2026-B',
          title: 'Uji Pemahaman Penalaran Logika & Literasi Digital',
          subject: 'Evaluasi Pengayaan',
          durationMinutes: 20,
          active: true
        }
      ];

      let PROCTOR_MONITORING_DATA = [
        { id: 'PST-2026-001', name: 'Alya Putri Maharani', room: 'Lab-01', answered: 7, total: 8, status: 'Aktif', violations: 0 },
        { id: 'PST-2026-002', name: 'Dimas Pratama Putra', room: 'Lab-01', answered: 8, total: 8, status: 'Selesai', violations: 0 },
        { id: 'PST-2026-003', name: 'Nadia Salsabila', room: 'Lab-02', answered: 5, total: 8, status: 'Peringatan', violations: 1 },
        { id: 'PST-2026-004', name: 'Rizky Ramadhan', room: 'Lab-02', answered: 6, total: 8, status: 'Aktif', violations: 0 },
        { id: 'PST-2026-005', name: 'Clarissa Aurelia', room: 'Lab-03', answered: 4, total: 8, status: 'Aktif', violations: 0 }
      ];

      /* ----------------------------------------------------------------------
         3. STATE APLIKASI & UTILITAS UI (MODAL & TOAST)
         ---------------------------------------------------------------------- */
      const state = {
        selectedRole: 'peserta',
        currentUser: null,
        activeExam: null,
        currentQuestionIdx: 0,
        answers: {},
        flagged: {},
        violations: 0,
        timerInterval: null,
        secondsRemaining: 1800,
        examInProgress: false
      };

      const ROLE_CONFIG = {
        peserta: {
          label: 'Nomor Peserta / Username',
          placeholder: 'Masukkan Nomor Peserta atau ID',
          badge: 'PESERTA UJIAN',
          subtitle: 'Portal Evaluasi Peserta'
        },
        pengawas: {
          label: 'NIP / ID Pengawas Ruang',
          placeholder: 'Masukkan NIP atau ID Pengawas',
          badge: 'PENGAWAS RUANG',
          subtitle: 'Konsol Pemantauan Pengawas'
        },
        admin: {
          label: 'ID Administrator Sistem',
          placeholder: 'Masukkan ID Administrator',
          badge: 'ADMINISTRATOR',
          subtitle: 'Panel Manajemen Evaluasi'
        }
      };

      function showToast(message, type) {
        const container = document.getElementById('toast-container');
        if (!container) return;

        const toast = document.createElement('div');
        toast.className = 'toast';
        const accentColor = type === 'danger' ? '#fda4af' : type === 'warn' ? '#fcd34d' : '#7dd3fc';
        toast.innerHTML =
          '<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="' + accentColor + '" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" style="margin-top:2px;">' +
          '<circle cx="12" cy="12" r="10"></circle><line x1="12" y1="16" x2="12" y2="12"></line><line x1="12" y1="8" x2="12.01" y2="8"></line>' +
          '</svg>' +
          '<div>' + message + '</div>';
        container.appendChild(toast);

        setTimeout(function () {
          toast.style.opacity = '0';
          toast.style.transition = 'opacity 0.25s ease';
          setTimeout(function () {
            if (toast.parentNode) toast.parentNode.removeChild(toast);
          }, 260);
        }, 3800);
      }

      function openModal(title, htmlContent) {
        const backdrop = document.getElementById('app-modal-backdrop');
        const titleEl = document.getElementById('app-modal-title');
        const bodyEl = document.getElementById('app-modal-body');
        if (!backdrop || !titleEl || !bodyEl) return;

        titleEl.textContent = title;
        bodyEl.innerHTML = htmlContent;
        backdrop.classList.remove('hidden');
      }

      function closeModal() {
        const backdrop = document.getElementById('app-modal-backdrop');
        if (backdrop) backdrop.classList.add('hidden');
      }

      function escapeHtml(str) {
        return String(str)
          .replace(/&/g, '&amp;')
          .replace(/</g, '&lt;')
          .replace(/>/g, '&gt;')
          .replace(/"/g, '&quot;')
          .replace(/'/g, '&#39;');
      }

      /* ----------------------------------------------------------------------
         4. RENDER WARTA PENDIDIKAN, FAQ & DIAGNOSTIK PERANGKAT
         ---------------------------------------------------------------------- */
      function renderNews(category) {
        const container = document.getElementById('news-grid-container');
        if (!container) return;

        const filtered = category === 'all'
          ? NEWS_ITEMS
          : NEWS_ITEMS.filter(function (item) { return item.category === category; });

        container.innerHTML = filtered.map(function (item) {
          return (
            '<article class="glass-card news-card">' +
              '<div class="news-banner">' +
                '<span class="news-tag">' + escapeHtml(item.category) + '</span>' +
                '<div class="news-meta">' +
                  '<span>' + escapeHtml(item.date) + '</span>' +
                  '<span>&bull;</span>' +
                  '<span>' + escapeHtml(item.readTime) + '</span>' +
                '</div>' +
              '</div>' +
              '<div class="news-body">' +
                '<h3 class="news-title">' + escapeHtml(item.title) + '</h3>' +
                '<p class="news-excerpt">' + escapeHtml(item.excerpt) + '</p>' +
                '<button type="button" class="read-more-btn" data-news-id="' + item.id + '">' +
                  '<span>Baca Selengkapnya</span>' +
                  '<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">' +
                    '<line x1="5" y1="12" x2="19" y2="12"></line>' +
                    '<polyline points="12 5 19 12 12 19"></polyline>' +
                  '</svg>' +
                '</button>' +
              '</div>' +
            '</article>'
          );
        }).join('');

        container.querySelectorAll('.read-more-btn').forEach(function (btn) {
          btn.addEventListener('click', function () {
            const id = btn.getAttribute('data-news-id');
            const article = NEWS_ITEMS.find(function (n) { return n.id === id; });
            if (!article) return;
            openModal(
              article.title,
              '<div style="margin-bottom: 14px; display: flex; gap: 10px; flex-wrap: wrap;">' +
                '<span class="status-badge info">' + escapeHtml(article.category) + '</span>' +
                '<span style="font-size: 0.82rem; color: var(--text-muted);">' + escapeHtml(article.date) + ' &bull; ' + escapeHtml(article.readTime) + '</span>' +
              '</div>' +
              '<p style="color: var(--text-secondary); line-height: 1.75; font-size: 0.95rem;">' + escapeHtml(article.content) + '</p>'
            );
          });
        });
      }

      function runDeviceDiagnostics() {
        const ua = navigator.userAgent;
        let browserName = 'Browser Modern';
        if (ua.indexOf('Edg') > -1) browserName = 'Microsoft Edge';
        else if (ua.indexOf('Chrome') > -1) browserName = 'Google Chrome';
        else if (ua.indexOf('Firefox') > -1) browserName = 'Mozilla Firefox';
        else if (ua.indexOf('Safari') > -1) browserName = 'Apple Safari';

        const browserEl = document.getElementById('diag-browser');
        const screenEl = document.getElementById('diag-screen');
        const netEl = document.getElementById('diag-network');
        const storageEl = document.getElementById('diag-storage');
        const clockEl = document.getElementById('diag-clock');
        const badgeEl = document.getElementById('diag-overall-badge');

        if (browserEl) browserEl.textContent = browserName + ' (Kompatibel)';
        if (screenEl) screenEl.textContent = window.innerWidth + ' x ' + window.innerHeight + ' px';

        const isOnline = navigator.onLine;
        if (netEl) {
          netEl.textContent = isOnline ? 'Terhubung (Online)' : 'Offline / Terbatas';
          netEl.style.color = isOnline ? '#6ee7b7' : '#fcd34d';
        }

        let storageOk = false;
        try {
          localStorage.setItem('cbt_pro_diag_test', '1');
          localStorage.removeItem('cbt_pro_diag_test');
          storageOk = true;
        } catch (e) {
          storageOk = false;
        }
        if (storageEl) {
          storageEl.textContent = storageOk ? 'Aktif & Siap' : 'Terbatas';
          storageEl.style.color = storageOk ? '#6ee7b7' : '#fcd34d';
        }

        const now = new Date();
        if (clockEl) {
          clockEl.textContent = now.toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit', second: '2-digit' });
        }
        if (badgeEl) {
          badgeEl.textContent = isOnline ? 'SIAP UJIAN' : 'MODE LOKAL';
        }
      }

      /* ----------------------------------------------------------------------
         5. LOGIKA LOGIN & NAVIGASI WORKSPACE
         ---------------------------------------------------------------------- */
      function setActiveRoleTab(role) {
        state.selectedRole = role;
        const cfg = ROLE_CONFIG[role] || ROLE_CONFIG.peserta;
        document.querySelectorAll('.role-tab').forEach(function (tab) {
          const isMatch = tab.getAttribute('data-role') === role;
          tab.classList.toggle('active', isMatch);
          tab.setAttribute('aria-selected', isMatch ? 'true' : 'false');
        });

        const labelEl = document.getElementById('login-id-label');
        const inputEl = document.getElementById('login-username');
        const errBox = document.getElementById('login-error-box');
        if (labelEl) labelEl.textContent = cfg.label;
        if (inputEl) inputEl.placeholder = cfg.placeholder;
        if (errBox) errBox.classList.add('hidden');
      }

      function enterWorkspace(user) {
        state.currentUser = user;
        const cfg = ROLE_CONFIG[user.role] || ROLE_CONFIG.peserta;

        document.getElementById('portal-view').classList.add('hidden');
        document.getElementById('workspace-view').classList.remove('hidden');

        document.getElementById('ws-role-badge').textContent = cfg.badge;
        document.getElementById('ws-subtitle').textContent = cfg.subtitle;
        document.getElementById('ws-user-display').textContent = user.username;

        document.getElementById('peserta-dashboard').classList.add('hidden');
        document.getElementById('pengawas-dashboard').classList.add('hidden');
        document.getElementById('admin-dashboard').classList.add('hidden');

        if (user.role === 'peserta') {
          document.getElementById('peserta-dashboard').classList.remove('hidden');
          document.getElementById('peserta-welcome-title').textContent = 'Selamat Datang, ' + user.username;
          renderPesertaExamCards();
        } else if (user.role === 'pengawas') {
          document.getElementById('pengawas-dashboard').classList.remove('hidden');
          renderProctorDashboard();
        } else if (user.role === 'admin') {
          document.getElementById('admin-dashboard').classList.remove('hidden');
          renderAdminDashboard();
        }

        window.scrollTo({ top: 0, behavior: 'smooth' });
      }

      function logoutWorkspace() {
        stopExamTimer();
        state.examInProgress = false;
        state.currentUser = null;
        try {
          localStorage.removeItem('cbt_pro_session');
        } catch (e) {}

        document.getElementById('workspace-view').classList.add('hidden');
        document.getElementById('portal-view').classList.remove('hidden');
        document.getElementById('login-password').value = '';
        showToast('Anda telah keluar dari sesi CBT-PRO.', 'info');
      }

      /* ----------------------------------------------------------------------
         6. WORKSPACE PESERTA UJIAN & ENGINE CBT INTERAKTIF
         ---------------------------------------------------------------------- */
      function renderPesertaExamCards() {
        const container = document.getElementById('peserta-exam-list');
        if (!container) return;

        document.getElementById('peserta-home-subview').classList.remove('hidden');
        document.getElementById('peserta-exam-room').classList.add('hidden');
        document.getElementById('peserta-result-subview').classList.add('hidden');

        container.innerHTML = EXAM_SCHEDULES.map(function (exam) {
          return (
            '<div class="exam-card">' +
              '<div>' +
                '<div style="display: flex; align-items: center; justify-content: space-between; gap: 10px; margin-bottom: 12px;">' +
                  '<span class="role-pill">' + escapeHtml(exam.id) + '</span>' +
                  '<span class="status-badge ' + (exam.active ? 'ok' : 'warn') + '">' + (exam.active ? 'Sesi Aktif' : 'Terjadwal') + '</span>' +
                '</div>' +
                '<h3 class="card-title" style="font-size: 1.15rem;">' + escapeHtml(exam.title) + '</h3>' +
                '<p class="card-text">' + escapeHtml(exam.subject) + '</p>' +
              '</div>' +
              '<div class="exam-meta-grid">' +
                '<div><div style="color:var(--text-muted);">Jumlah Soal</div><strong>' + QUESTIONS_BANK.length + ' Butir</strong></div>' +
                '<div><div style="color:var(--text-muted);">Durasi</div><strong>' + exam.durationMinutes + ' Menit</strong></div>' +
                '<div><div style="color:var(--text-muted);">Pengawasan</div><strong>Anti-Cheat</strong></div>' +
              '</div>' +
              '<button type="button" class="btn btn-primary btn-block start-exam-trigger" data-exam-id="' + exam.id + '" ' + (exam.active ? '' : 'disabled style="opacity:0.5;cursor:not-allowed;"') + '>' +
                '<span>' + (exam.active ? 'Mulai Ujian Sekarang' : 'Belum Dibuka') + '</span>' +
              '</button>' +
            '</div>'
          );
        }).join('');

        container.querySelectorAll('.start-exam-trigger').forEach(function (btn) {
          btn.addEventListener('click', function () {
            const examId = btn.getAttribute('data-exam-id');
            const exam = EXAM_SCHEDULES.find(function (e) { return e.id === examId; });
            if (!exam || !exam.active) return;
            openExamRulesModal(exam);
          });
        });
      }

      function openExamRulesModal(exam) {
        openModal(
          'Tata Tertib & Pakta Integritas Ujian',
          '<div style="font-size: 0.9rem; color: var(--text-secondary); line-height: 1.7;">' +
            '<p style="margin-bottom: 12px;">Anda akan memasuki sesi <strong>' + escapeHtml(exam.title) + '</strong> dengan durasi <strong>' + exam.durationMinutes + ' menit</strong>.</p>' +
            '<ul style="padding-left: 20px; margin-bottom: 16px; display: flex; flex-direction: column; gap: 8px;">' +
              '<li>Waktu hitung mundur berjalan otomatis sejak tombol mulai ditekan.</li>' +
              '<li>Dilarang berpindah tab browser, meminimalkan jendela, atau membuka aplikasi lain.</li>' +
              '<li>Setiap perpindahan fokus layar tercatat sebagai pelanggaran integritas (maksimal 3 kali).</li>' +
              '<li>Gunakan tombol <strong>Tandai Ragu-ragu</strong> apabila ingin meninjau ulang butir soal tertentu.</li>' +
            '</ul>' +
            '<label class="checkbox-label" style="margin-bottom: 18px; padding: 10px 12px; border-radius: 10px; background: rgba(56,189,248,0.1); border: 1px solid rgba(56,189,248,0.28); width: 100%;">' +
              '<input type="checkbox" id="agree-rules-checkbox" />' +
              '<span>Saya telah membaca dan menyetujui seluruh tata tertib ujian di atas.</span>' +
            '</label>' +
            '<div style="display: flex; justify-content: flex-end; gap: 10px;">' +
              '<button type="button" class="btn btn-secondary" id="cancel-rules-btn">Batal</button>' +
              '<button type="button" class="btn btn-primary" id="confirm-start-exam-btn">Masuk Ruang Ujian</button>' +
            '</div>' +
          '</div>'
        );

        document.getElementById('cancel-rules-btn').addEventListener('click', closeModal);
        document.getElementById('confirm-start-exam-btn').addEventListener('click', function () {
          const agreed = document.getElementById('agree-rules-checkbox').checked;
          if (!agreed) {
            showToast('Silakan centang persetujuan tata tertib ujian terlebih dahulu.', 'warn');
            return;
          }
          closeModal();
          startCbtSession(exam);
        });
      }

      function startCbtSession(exam) {
        state.activeExam = exam;
        state.currentQuestionIdx = 0;
        state.answers = {};
        state.flagged = {};
        state.violations = 0;
        state.secondsRemaining = exam.durationMinutes * 60;
        state.examInProgress = true;

        // Sinkronkan peserta aktif ke daftar pemantauan pengawas
        const existingIdx = PROCTOR_MONITORING_DATA.findIndex(function (p) { return p.id === state.currentUser.username; });
        const participantRecord = {
          id: state.currentUser.username,
          name: state.currentUser.username + ' (Sesi Aktif)',
          room: 'Virtual-01',
          answered: 0,
          total: QUESTIONS_BANK.length,
          status: 'Aktif',
          violations: 0
        };
        if (existingIdx > -1) PROCTOR_MONITORING_DATA[existingIdx] = participantRecord;
        else PROCTOR_MONITORING_DATA.unshift(participantRecord);

        document.getElementById('peserta-home-subview').classList.add('hidden');
        document.getElementById('peserta-result-subview').classList.add('hidden');
        document.getElementById('peserta-exam-room').classList.remove('hidden');

        document.getElementById('active-exam-title').textContent = exam.title;
        updateViolationBadge();
        renderCurrentQuestion();
        renderQuestionNavGrid();
        startExamTimer();
      }

      function updateViolationBadge() {
        const badge = document.getElementById('violation-counter-badge');
        if (!badge) return;
        badge.textContent = 'Pelanggaran Tab: ' + state.violations + ' / 3';
        badge.className = 'status-badge ' + (state.violations > 0 ? 'danger' : 'warn');
      }

      function startExamTimer() {
        stopExamTimer();
        updateTimerDisplay();
        state.timerInterval = setInterval(function () {
          state.secondsRemaining -= 1;
          updateTimerDisplay();
          if (state.secondsRemaining <= 0) {
            stopExamTimer();
            showToast('Waktu ujian telah habis. Jawaban dikumpulkan otomatis.', 'warn');
            submitCbtExam();
          }
        }, 1000);
      }

      function stopExamTimer() {
        if (state.timerInterval) {
          clearInterval(state.timerInterval);
          state.timerInterval = null;
        }
      }

      function updateTimerDisplay() {
        const mins = Math.max(0, Math.floor(state.secondsRemaining / 60));
        const secs = Math.max(0, state.secondsRemaining % 60);
        const formatted = String(mins).padStart(2, '0') + ':' + String(secs).padStart(2, '0');
        const textEl = document.getElementById('exam-timer-text');
        const boxEl = document.getElementById('exam-timer-box');
        if (textEl) textEl.textContent = formatted;
        if (boxEl) {
          boxEl.classList.toggle('warning', state.secondsRemaining <= 180);
        }
      }

      function renderCurrentQuestion() {
        const q = QUESTIONS_BANK[state.currentQuestionIdx];
        if (!q) return;

        document.getElementById('q-number-badge').textContent = 'Soal ' + (state.currentQuestionIdx + 1) + ' dari ' + QUESTIONS_BANK.length;
        document.getElementById('q-category-label').textContent = q.category || 'Evaluasi Umum';

        const typeLabelMap = {
          multiple_choice: 'Pilihan Ganda',
          true_false: 'Benar / Salah',
          short_answer: 'Isian Singkat'
        };
        document.getElementById('q-type-badge').textContent = typeLabelMap[q.type] || 'Soal';
        document.getElementById('q-prompt-text').textContent = q.prompt;

        const isFlagged = !!state.flagged[q.id];
        document.getElementById('flag-btn-label').textContent = isFlagged ? 'Batal Ragu-ragu' : 'Tandai Ragu-ragu';

        const answerArea = document.getElementById('q-answer-area');
        const savedVal = state.answers[q.id];

        if (q.type === 'multiple_choice' || q.type === 'true_false') {
          const letters = ['A', 'B', 'C', 'D', 'E'];
          answerArea.innerHTML =
            '<div class="options-list">' +
              q.options.map(function (opt, idx) {
                const isSelected = savedVal === idx;
                const keyLabel = q.type === 'true_false' ? (idx === 0 ? 'B' : 'S') : letters[idx];
                return (
                  '<button type="button" class="option-item ' + (isSelected ? 'selected' : '') + '" data-opt-idx="' + idx + '">' +
                    '<span class="option-key">' + keyLabel + '</span>' +
                    '<span>' + escapeHtml(opt) + '</span>' +
                  '</button>'
                );
              }).join('') +
            '</div>';

          answerArea.querySelectorAll('.option-item').forEach(function (optBtn) {
            optBtn.addEventListener('click', function () {
              const chosen = Number(optBtn.getAttribute('data-opt-idx'));
              state.answers[q.id] = chosen;
              syncParticipantProgress();
              renderCurrentQuestion();
              renderQuestionNavGrid();
            });
          });
        } else {
          answerArea.innerHTML =
            '<div>' +
              '<label class="form-label" for="short-answer-field">Ketik Jawaban Singkat Anda:</label>' +
              '<input type="text" id="short-answer-field" class="short-answer-input" placeholder="Masukkan jawaban singkat di sini..." value="' + escapeHtml(savedVal || '') + '" />' +
            '</div>';

          const field = document.getElementById('short-answer-field');
          field.addEventListener('input', function () {
            const val = field.value.trim();
            if (val.length > 0) {
              state.answers[q.id] = val;
            } else {
              delete state.answers[q.id];
            }
            syncParticipantProgress();
            renderQuestionNavGrid();
          });
        }

        document.getElementById('prev-q-btn').disabled = state.currentQuestionIdx === 0;
        document.getElementById('prev-q-btn').style.opacity = state.currentQuestionIdx === 0 ? '0.45' : '1';
      }

      function syncParticipantProgress() {
        if (!state.currentUser) return;
        const p = PROCTOR_MONITORING_DATA.find(function (item) { return item.id === state.currentUser.username; });
        if (p) {
          p.answered = Object.keys(state.answers).length;
          p.total = QUESTIONS_BANK.length;
          p.violations = state.violations;
          p.status = state.violations > 0 ? 'Peringatan' : 'Aktif';
        }
      }

      function renderQuestionNavGrid() {
        const grid = document.getElementById('question-nav-grid');
        if (!grid) return;

        let answeredCount = 0;
        let flaggedCount = 0;

        grid.innerHTML = QUESTIONS_BANK.map(function (q, idx) {
          const hasAnswer = state.answers[q.id] !== undefined && state.answers[q.id] !== '';
          const isFlagged = !!state.flagged[q.id];
          if (hasAnswer) answeredCount++;
          if (isFlagged) flaggedCount++;

          let cls = 'num-btn';
          if (isFlagged) cls += ' flagged';
          else if (hasAnswer) cls += ' answered';
          if (idx === state.currentQuestionIdx) cls += ' current';

          return '<button type="button" class="' + cls + '" data-q-idx="' + idx + '">' + (idx + 1) + '</button>';
        }).join('');

        grid.querySelectorAll('.num-btn').forEach(function (btn) {
          btn.addEventListener('click', function () {
            state.currentQuestionIdx = Number(btn.getAttribute('data-q-idx'));
            renderCurrentQuestion();
            renderQuestionNavGrid();
          });
        });

        document.getElementById('count-answered').textContent = answeredCount;
        document.getElementById('count-flagged').textContent = flaggedCount;
        document.getElementById('count-unanswered').textContent = Math.max(0, QUESTIONS_BANK.length - answeredCount);
      }

      function submitCbtExam() {
        stopExamTimer();
        state.examInProgress = false;

        let correct = 0;
        const reviewHtml = QUESTIONS_BANK.map(function (q, idx) {
          const userAns = state.answers[q.id];
          let isCorrect = false;
          let userAnsText = 'Tidak dijawab';
          let correctAnsText = '';

          if (q.type === 'multiple_choice' || q.type === 'true_false') {
            isCorrect = userAns === q.correctAnswer;
            if (userAns !== undefined) userAnsText = q.options[userAns];
            correctAnsText = q.options[q.correctAnswer];
          } else {
            const normalizedUser = String(userAns || '').trim().toLowerCase();
            const normalizedKey = String(q.correctAnswer).trim().toLowerCase();
            isCorrect = normalizedUser !== '' && normalizedUser === normalizedKey;
            if (normalizedUser !== '') userAnsText = String(userAns).trim();
            correctAnsText = String(q.correctAnswer);
          }

          if (isCorrect) correct++;

          return (
            '<div style="padding: 12px 14px; border-radius: 10px; background: rgba(6,11,25,0.68); border: 1px solid ' + (isCorrect ? 'rgba(16,185,129,0.35)' : 'rgba(244,63,94,0.3)') + ';">' +
              '<div style="display:flex; justify-content:space-between; gap:8px; margin-bottom:4px;">' +
                '<strong style="font-size:0.86rem;">Butir #' + (idx + 1) + ' &bull; ' + escapeHtml(q.category) + '</strong>' +
                '<span class="status-badge ' + (isCorrect ? 'ok' : 'danger') + '">' + (isCorrect ? 'Tepat' : 'Kurang Tepat') + '</span>' +
              '</div>' +
              '<div style="font-size:0.84rem; color:var(--text-secondary); margin-bottom:4px;">' + escapeHtml(q.prompt) + '</div>' +
              '<div style="font-size:0.8rem; color:var(--text-muted);">Jawaban Anda: <strong style="color:#fff;">' + escapeHtml(userAnsText) + '</strong> | Kunci: <strong style="color:#6ee7b7;">' + escapeHtml(correctAnsText) + '</strong></div>' +
            '</div>'
          );
        }).join('');

        const total = QUESTIONS_BANK.length;
        const score = total > 0 ? Math.round((correct / total) * 100) : 0;
        let predicate = 'Perlu Peningkatan';
        if (score >= 85) predicate = 'Predikat: Sangat Baik (A)';
        else if (score >= 70) predicate = 'Predikat: Baik (B)';
        else if (score >= 55) predicate = 'Predikat: Cukup (C)';

        // Perbarui status pada pengawas
        const p = PROCTOR_MONITORING_DATA.find(function (item) { return item.id === state.currentUser.username; });
        if (p) {
          p.answered = Object.keys(state.answers).length;
          p.status = 'Selesai';
        }

        document.getElementById('peserta-exam-room').classList.add('hidden');
        document.getElementById('peserta-result-subview').classList.remove('hidden');

        document.getElementById('result-exam-name').textContent = state.activeExam ? state.activeExam.title : 'Rekap Hasil Evaluasi';
        document.getElementById('result-meta-info').textContent = 'Peserta: ' + state.currentUser.username + ' • Selesai pada ' + new Date().toLocaleTimeString('id-ID');
        document.getElementById('result-score-val').textContent = score;
        document.getElementById('result-predicate-text').textContent = predicate;
        document.getElementById('result-correct-val').textContent = correct;
        document.getElementById('result-wrong-val').textContent = total - correct;
        document.getElementById('result-violation-val').textContent = state.violations;
        document.getElementById('result-review-list').innerHTML = reviewHtml;
      }

      /* ----------------------------------------------------------------------
         7. WORKSPACE PENGAWAS & ADMINISTRATOR
         ---------------------------------------------------------------------- */
      function renderProctorDashboard() {
        const searchVal = (document.getElementById('proctor-search-input').value || '').toLowerCase();
        const filtered = PROCTOR_MONITORING_DATA.filter(function (p) {
          return p.id.toLowerCase().indexOf(searchVal) > -1 || p.name.toLowerCase().indexOf(searchVal) > -1;
        });

        let activeCount = 0;
        let doneCount = 0;
        let warnCount = 0;

        PROCTOR_MONITORING_DATA.forEach(function (p) {
          if (p.status === 'Selesai') doneCount++;
          else activeCount++;
          warnCount += p.violations;
        });

        document.getElementById('proctor-stat-total').textContent = PROCTOR_MONITORING_DATA.length;
        document.getElementById('proctor-stat-active').textContent = activeCount;
        document.getElementById('proctor-stat-done').textContent = doneCount;
        document.getElementById('proctor-stat-warn').textContent = warnCount;

        const tbody = document.getElementById('proctor-table-body');
        tbody.innerHTML = filtered.map(function (p) {
          const pct = Math.round((p.answered / Math.max(1, p.total)) * 100);
          const badgeClass = p.status === 'Selesai' ? 'ok' : p.violations > 0 ? 'danger' : 'info';
          return (
            '<tr>' +
              '<td><strong>' + escapeHtml(p.id) + '</strong></td>' +
              '<td>' + escapeHtml(p.name) + '</td>' +
              '<td>' + escapeHtml(p.room) + '</td>' +
              '<td>' +
                '<div class="progress-track"><div class="progress-fill" style="width:' + pct + '%;"></div></div>' +
                '<span>' + p.answered + '/' + p.total + '</span>' +
              '</td>' +
              '<td><span class="status-badge ' + badgeClass + '">' + escapeHtml(p.status) + '</span></td>' +
              '<td><strong style="color:' + (p.violations > 0 ? '#fda4af' : '#6ee7b7') + ';">' + p.violations + 'x</strong></td>' +
              '<td>' +
                '<div style="display:flex; gap:6px;">' +
                  '<button type="button" class="btn btn-amber btn-sm proctor-warn-btn" data-pid="' + escapeHtml(p.id) + '">Peringatkan</button>' +
                  '<button type="button" class="btn btn-secondary btn-sm proctor-reset-btn" data-pid="' + escapeHtml(p.id) + '">Reset</button>' +
                '</div>' +
              '</td>' +
            '</tr>'
          );
        }).join('');

        tbody.querySelectorAll('.proctor-warn-btn').forEach(function (btn) {
          btn.addEventListener('click', function () {
            const pid = btn.getAttribute('data-pid');
            showToast('Peringatan pengawas dikirim ke sesi peserta ' + pid + '.', 'warn');
          });
        });

        tbody.querySelectorAll('.proctor-reset-btn').forEach(function (btn) {
          btn.addEventListener('click', function () {
            const pid = btn.getAttribute('data-pid');
            const target = PROCTOR_MONITORING_DATA.find(function (item) { return item.id === pid; });
            if (target) {
              target.violations = 0;
              if (target.status !== 'Selesai') target.status = 'Aktif';
              renderProctorDashboard();
              showToast('Catatan pelanggaran sesi ' + pid + ' telah direset.', 'info');
            }
          });
        });
      }

      function renderAdminDashboard() {
        document.getElementById('admin-stat-questions').textContent = QUESTIONS_BANK.length;
        document.getElementById('admin-stat-exams').textContent = EXAM_SCHEDULES.length;

        const qTbody = document.getElementById('admin-questions-tbody');
        const typeLabels = {
          multiple_choice: 'Pilihan Ganda',
          true_false: 'Benar / Salah',
          short_answer: 'Isian Singkat'
        };

        qTbody.innerHTML = QUESTIONS_BANK.map(function (q, idx) {
          const keyDisplay = (q.type === 'multiple_choice' || q.type === 'true_false')
            ? q.options[q.correctAnswer]
            : q.correctAnswer;

          return (
            '<tr>' +
              '<td><strong>' + (idx + 1) + '</strong></td>' +
              '<td><span class="status-badge info">' + (typeLabels[q.type] || q.type) + '</span></td>' +
              '<td>' + escapeHtml(q.category) + '</td>' +
              '<td style="max-width:340px;">' + escapeHtml(q.prompt) + '</td>' +
              '<td><strong style="color:#6ee7b7;">' + escapeHtml(keyDisplay) + '</strong></td>' +
              '<td>' +
                '<button type="button" class="btn btn-danger btn-sm admin-del-q-btn" data-qid="' + escapeHtml(q.id) + '">Hapus</button>' +
              '</td>' +
            '</tr>'
          );
        }).join('');

        qTbody.querySelectorAll('.admin-del-q-btn').forEach(function (btn) {
          btn.addEventListener('click', function () {
            if (QUESTIONS_BANK.length <= 2) {
              showToast('Minimal harus tersisa 2 butir soal di bank soal.', 'warn');
              return;
            }
            const qid = btn.getAttribute('data-qid');
            QUESTIONS_BANK = QUESTIONS_BANK.filter(function (q) { return q.id !== qid; });
            renderAdminDashboard();
            showToast('Butir soal ' + qid + ' dihapus dari bank soal.', 'info');
          });
        });

        const sTbody = document.getElementById('admin-schedules-tbody');
        sTbody.innerHTML = EXAM_SCHEDULES.map(function (ex) {
          return (
            '<tr>' +
              '<td><strong>' + escapeHtml(ex.id) + '</strong></td>' +
              '<td>' + escapeHtml(ex.title) + '</td>' +
              '<td>' + ex.durationMinutes + ' Menit</td>' +
              '<td><span class="status-badge ' + (ex.active ? 'ok' : 'warn') + '">' + (ex.active ? 'Aktif' : 'Nonaktif') + '</span></td>' +
              '<td>' +
                '<button type="button" class="btn btn-secondary btn-sm admin-toggle-ex-btn" data-exid="' + escapeHtml(ex.id) + '">' +
                  (ex.active ? 'Nonaktifkan' : 'Aktifkan Sesi') +
                '</button>' +
              '</td>' +
            '</tr>'
          );
        }).join('');

        sTbody.querySelectorAll('.admin-toggle-ex-btn').forEach(function (btn) {
          btn.addEventListener('click', function () {
            const exid = btn.getAttribute('data-exid');
            const target = EXAM_SCHEDULES.find(function (e) { return e.id === exid; });
            if (target) {
              target.active = !target.active;
              renderAdminDashboard();
              showToast('Status paket ' + exid + ' diperbarui.', 'info');
            }
          });
        });
      }

      function openAddQuestionModal() {
        openModal(
          'Tambah Butir Soal Baru ke Bank Soal',
          '<form id="add-question-form" style="display:flex; flex-direction:column; gap:14px;">' +
            '<div>' +
              '<label class="form-label" for="new-q-type">Tipe Butir Soal</label>' +
              '<select id="new-q-type" class="form-control" style="padding:0 14px; background:#060b19;">' +
                '<option value="multiple_choice">Pilihan Ganda (4 Opsi)</option>' +
                '<option value="true_false">Benar / Salah</option>' +
                '<option value="short_answer">Isian Singkat</option>' +
              '</select>' +
            '</div>' +
            '<div>' +
              '<label class="form-label" for="new-q-category">Kategori / Mata Uji</label>' +
              '<input type="text" id="new-q-category" class="form-control" style="padding:0 14px;" placeholder="Contoh: Literasi Numerasi" required />' +
            '</div>' +
            '<div>' +
              '<label class="form-label" for="new-q-prompt">Pertanyaan Soal</label>' +
              '<textarea id="new-q-prompt" rows="3" style="width:100%; padding:12px 14px; border-radius:11px; background:#060b19; border:1px solid rgba(148,163,184,0.25); color:#fff;" placeholder="Tuliskan teks pertanyaan secara lengkap..." required></textarea>' +
            '</div>' +
            '<div id="new-q-dynamic-fields"></div>' +
            '<div style="display:flex; justify-content:flex-end; gap:10px; margin-top:6px;">' +
              '<button type="button" class="btn btn-secondary" id="cancel-add-q-btn">Batal</button>' +
              '<button type="submit" class="btn btn-primary">Simpan ke Bank Soal</button>' +
            '</div>' +
          '</form>'
        );

        const typeSelect = document.getElementById('new-q-type');
        const dynamicArea = document.getElementById('new-q-dynamic-fields');

        function renderDynamicKeyInputs() {
          const t = typeSelect.value;
          if (t === 'multiple_choice') {
            dynamicArea.innerHTML =
              '<div style="display:grid; grid-template-columns:1fr 1fr; gap:10px; margin-bottom:10px;">' +
                '<input type="text" id="opt-0" class="form-control" style="padding:0 12px;" placeholder="Opsi A" required />' +
                '<input type="text" id="opt-1" class="form-control" style="padding:0 12px;" placeholder="Opsi B" required />' +
                '<input type="text" id="opt-2" class="form-control" style="padding:0 12px;" placeholder="Opsi C" required />' +
                '<input type="text" id="opt-3" class="form-control" style="padding:0 12px;" placeholder="Opsi D" required />' +
              '</div>' +
              '<label class="form-label" for="mc-correct-idx">Kunci Jawaban Benar</label>' +
              '<select id="mc-correct-idx" class="form-control" style="padding:0 14px; background:#060b19;">' +
                '<option value="0">Opsi A</option>' +
                '<option value="1">Opsi B</option>' +
                '<option value="2">Opsi C</option>' +
                '<option value="3">Opsi D</option>' +
              '</select>';
          } else if (t === 'true_false') {
            dynamicArea.innerHTML =
              '<label class="form-label" for="tf-correct-idx">Kunci Jawaban Pernyataan</label>' +
              '<select id="tf-correct-idx" class="form-control" style="padding:0 14px; background:#060b19;">' +
                '<option value="0">Benar</option>' +
                '<option value="1">Salah</option>' +
              '</select>';
          } else {
            dynamicArea.innerHTML =
              '<label class="form-label" for="sa-correct-text">Kunci Jawaban Singkat</label>' +
              '<input type="text" id="sa-correct-text" class="form-control" style="padding:0 14px;" placeholder="Masukkan kata/angka kunci jawaban" required />';
          }
        }

        renderDynamicKeyInputs();
        typeSelect.addEventListener('change', renderDynamicKeyInputs);
        document.getElementById('cancel-add-q-btn').addEventListener('click', closeModal);

        document.getElementById('add-question-form').addEventListener('submit', function (e) {
          e.preventDefault();
          const t = typeSelect.value;
          const category = document.getElementById('new-q-category').value.trim() || 'Umum';
          const prompt = document.getElementById('new-q-prompt').value.trim();
          if (!prompt) return;

          const newQuestion = {
            id: 'Q' + String(Date.now()).slice(-4),
            type: t,
            category: category,
            prompt: prompt
          };

          if (t === 'multiple_choice') {
            newQuestion.options = [
              document.getElementById('opt-0').value.trim(),
              document.getElementById('opt-1').value.trim(),
              document.getElementById('opt-2').value.trim(),
              document.getElementById('opt-3').value.trim()
            ];
            newQuestion.correctAnswer = Number(document.getElementById('mc-correct-idx').value);
          } else if (t === 'true_false') {
            newQuestion.options = ['Benar', 'Salah'];
            newQuestion.correctAnswer = Number(document.getElementById('tf-correct-idx').value);
          } else {
            newQuestion.correctAnswer = document.getElementById('sa-correct-text').value.trim();
          }

          QUESTIONS_BANK.push(newQuestion);
          closeModal();
          renderAdminDashboard();
          showToast('Soal baru berhasil ditambahkan dan langsung tersedia untuk ujian.', 'info');
        });
      }

      /* ----------------------------------------------------------------------
         8. SENSOR ANTI-CHEAT DETEKSI PERPINDAHAN TAB BROWSER
         ---------------------------------------------------------------------- */
      function initAntiCheatListener() {
        document.addEventListener('visibilitychange', function () {
          if (document.hidden && state.examInProgress) {
            state.violations += 1;
            updateViolationBadge();
            syncParticipantProgress();

            if (state.violations >= 3) {
              showToast('Batas maksimal pelanggaran tab (3x) tercapai. Ujian dikumpulkan otomatis!', 'danger');
              submitCbtExam();
            } else {
              openModal(
                'Peringatan Integritas Sesi Ujian (' + state.violations + '/3)',
                '<div style="color: var(--text-secondary); font-size: 0.92rem; line-height: 1.65;">' +
                  '<p style="color: #fda4af; font-weight: 700; margin-bottom: 10px;">Sistem mendeteksi Anda meninggalkan jendela/tab ujian!</p>' +
                  '<p style="margin-bottom: 16px;">Aktivitas ini telah dicatat pada log pengawas ruang. Jika pelanggaran mencapai 3 kali, sesi ujian akan dihentikan secara otomatis.</p>' +
                  '<div style="text-align: right;">' +
                    '<button type="button" class="btn btn-primary" id="ack-violation-btn">Saya Mengerti &amp; Lanjutkan Ujian</button>' +
                  '</div>' +
                '</div>'
              );
              const ackBtn = document.getElementById('ack-violation-btn');
              if (ackBtn) ackBtn.addEventListener('click', closeModal);
            }
          }
        });
      }

      /* ----------------------------------------------------------------------
         9. INISIALISASI EVENT LISTENER & STARTUP APLIKASI
         ---------------------------------------------------------------------- */
      window.addEventListener('DOMContentLoaded', function () {
        initBackgroundMotion();
        renderNews('all');
        runDeviceDiagnostics();
        initAntiCheatListener();

        // Mobile Drawer Toggle
        const mobileBtn = document.getElementById('mobile-menu-toggle');
        const mobileDrawer = document.getElementById('mobile-drawer');
        if (mobileBtn && mobileDrawer) {
          mobileBtn.addEventListener('click', function () {
            mobileDrawer.classList.toggle('open');
          });
          mobileDrawer.querySelectorAll('a').forEach(function (link) {
            link.addEventListener('click', function () {
              mobileDrawer.classList.remove('open');
            });
          });
        }

        // Focus ke kartu login dari tombol Hero & Navbar
        function focusLoginForm() {
          const card = document.getElementById('login-card-box');
          const input = document.getElementById('login-username');
          if (card) card.scrollIntoView({ behavior: 'smooth', block: 'center' });
          setTimeout(function () {
            if (input) input.focus();
          }, 300);
        }

        document.getElementById('nav-login-focus-btn').addEventListener('click', focusLoginForm);
        document.getElementById('hero-start-btn').addEventListener('click', focusLoginForm);

        // Role Tabs pada Kartu Login
        document.querySelectorAll('.role-tab').forEach(function (tab) {
          tab.addEventListener('click', function () {
            setActiveRoleTab(tab.getAttribute('data-role'));
          });
        });

        // Toggle Tampilkan / Sembunyikan Kata Sandi
        const pwdInput = document.getElementById('login-password');
        const togglePwdBtn = document.getElementById('toggle-pwd-btn');
        const eyeShow = document.getElementById('eye-icon-show');
        const eyeHide = document.getElementById('eye-icon-hide');
        togglePwdBtn.addEventListener('click', function () {
          const isPassword = pwdInput.type === 'password';
          pwdInput.type = isPassword ? 'text' : 'password';
          eyeShow.classList.toggle('hidden', isPassword);
          eyeHide.classList.toggle('hidden', !isPassword);
        });

        // Modal Bantuan Akun
        document.getElementById('account-help-btn').addEventListener('click', function () {
          openModal(
            'Informasi Bantuan Akses Akun',
            '<div style="color: var(--text-secondary); font-size: 0.92rem; line-height: 1.7;">' +
              '<p style="margin-bottom: 12px;">Kredensial login (ID Pengguna dan Kata Sandi) diterbitkan secara resmi oleh Panitia Evaluasi / Administrator Akademik institusi Anda.</p>' +
              '<div style="padding: 14px; border-radius: 12px; background: rgba(6,11,25,0.75); border: 1px solid var(--border-glass); margin-bottom: 16px;">' +
                '<div style="margin-bottom: 6px;"><strong>Meja Bantuan Teknis CBT-PRO:</strong></div>' +
                '<div>Email Layanan: <strong>helpdesk@cbt-pro.ac.id</strong></div>' +
                '<div>Jam Operasional: <strong>Senin &ndash; Sabtu, 07.00 &ndash; 17.00 WITA</strong></div>' +
              '</div>' +
              '<div style="text-align: right;">' +
                '<button type="button" class="btn btn-primary" id="close-help-modal-btn">Tutup</button>' +
              '</div>' +
            '</div>'
          );
          document.getElementById('close-help-modal-btn').addEventListener('click', closeModal);
        });

        // Submit Form Login
        document.getElementById('login-form').addEventListener('submit', function (e) {
          e.preventDefault();
          const username = document.getElementById('login-username').value.trim();
          const password = document.getElementById('login-password').value;
          const remember = document.getElementById('remember-session').checked;
          const errBox = document.getElementById('login-error-box');
          const errText = document.getElementById('login-error-text');

          if (username.length < 3) {
            errText.textContent = 'ID / Username minimal terdiri dari 3 karakter.';
            errBox.classList.remove('hidden');
            return;
          }
          if (password.length < 4) {
            errText.textContent = 'Kata sandi minimal terdiri dari 4 karakter.';
            errBox.classList.remove('hidden');
            return;
          }

          errBox.classList.add('hidden');
          const userSession = {
            username: username,
            role: state.selectedRole
          };

          if (remember) {
            try {
              localStorage.setItem('cbt_pro_session', JSON.stringify(userSession));
            } catch (err) {}
          }

          enterWorkspace(userSession);
          showToast('Berhasil masuk sebagai ' + username + '.', 'info');
        });

        // Filter Kategori Berita
        document.querySelectorAll('.filter-btn').forEach(function (btn) {
          btn.addEventListener('click', function () {
            document.querySelectorAll('.filter-btn').forEach(function (b) { b.classList.remove('active'); });
            btn.classList.add('active');
            renderNews(btn.getAttribute('data-category'));
          });
        });

        // FAQ Accordion
        document.querySelectorAll('.faq-question').forEach(function (qBtn) {
          qBtn.addEventListener('click', function () {
            const item = qBtn.parentElement;
            item.classList.toggle('open');
          });
        });

        // Uji Ulang Diagnostik Perangkat
        document.getElementById('recheck-diag-btn').addEventListener('click', function () {
          runDeviceDiagnostics();
          showToast('Pemeriksaan kesiapan perangkat diperbarui.', 'info');
        });

        // Tombol Logout Workspace
        document.getElementById('logout-btn').addEventListener('click', logoutWorkspace);

        // Navigasi Butir Soal CBT
        document.getElementById('prev-q-btn').addEventListener('click', function () {
          if (state.currentQuestionIdx > 0) {
            state.currentQuestionIdx -= 1;
            renderCurrentQuestion();
            renderQuestionNavGrid();
          }
        });

        document.getElementById('next-q-btn').addEventListener('click', function () {
          if (state.currentQuestionIdx < QUESTIONS_BANK.length - 1) {
            state.currentQuestionIdx += 1;
            renderCurrentQuestion();
            renderQuestionNavGrid();
          }
        });

        document.getElementById('flag-q-btn').addEventListener('click', function () {
          const q = QUESTIONS_BANK[state.currentQuestionIdx];
          if (!q) return;
          state.flagged[q.id] = !state.flagged[q.id];
          renderCurrentQuestion();
          renderQuestionNavGrid();
        });

        document.getElementById('finish-exam-btn').addEventListener('click', function () {
          const answeredCount = Object.keys(state.answers).length;
          const remaining = QUESTIONS_BANK.length - answeredCount;
          openModal(
            'Konfirmasi Pengumpulan Jawaban',
            '<div style="color: var(--text-secondary); font-size: 0.92rem; line-height: 1.65;">' +
              '<p style="margin-bottom: 12px;">Anda telah menjawab <strong>' + answeredCount + ' dari ' + QUESTIONS_BANK.length + '</strong> butir soal.</p>' +
              (remaining > 0
                ? '<p style="color: #fcd34d; margin-bottom: 16px;">Masih terdapat <strong>' + remaining + ' soal</strong> yang belum diisi. Apakah Anda yakin ingin mengakhiri ujian sekarang?</p>'
                : '<p style="color: #6ee7b7; margin-bottom: 16px;">Seluruh butir soal telah terjawab. Tekan tombol konfirmasi di bawah untuk melihat hasil evaluasi.</p>') +
              '<div style="display: flex; justify-content: flex-end; gap: 10px;">' +
                '<button type="button" class="btn btn-secondary" id="cancel-submit-exam-btn">Tinjau Kembali</button>' +
                '<button type="button" class="btn btn-emerald" id="confirm-submit-exam-btn">Ya, Kumpulkan Jawaban</button>' +
              '</div>' +
            '</div>'
          );
          document.getElementById('cancel-submit-exam-btn').addEventListener('click', closeModal);
          document.getElementById('confirm-submit-exam-btn').addEventListener('click', function () {
            closeModal();
            submitCbtExam();
          });
        });

        document.getElementById('back-to-peserta-home-btn').addEventListener('click', renderPesertaExamCards);

        // Pengawas Controls
        document.getElementById('proctor-search-input').addEventListener('input', renderProctorDashboard);
        document.getElementById('proctor-simulate-btn').addEventListener('click', function () {
          PROCTOR_MONITORING_DATA.forEach(function (p) {
            if (p.status !== 'Selesai' && p.answered < p.total) {
              p.answered += 1;
              if (p.answered === p.total) p.status = 'Selesai';
            }
          });
          renderProctorDashboard();
          showToast('Data pemantauan peserta berhasil disinkronkan.', 'info');
        });

        // Admin Tambah Soal Baru
        document.getElementById('open-add-question-btn').addEventListener('click', openAddQuestionModal);

        // Modal Close Handlers
        document.getElementById('app-modal-close-btn').addEventListener('click', closeModal);
        document.getElementById('app-modal-backdrop').addEventListener('click', function (e) {
          if (e.target === this) closeModal();
        });

        // Pulihkan sesi jika sebelumnya mencentang "Ingat Sesi"
        try {
          const savedSessionRaw = localStorage.getItem('cbt_pro_session');
          if (savedSessionRaw) {
            const parsed = JSON.parse(savedSessionRaw);
            if (parsed && parsed.username && parsed.role) {
              enterWorkspace(parsed);
            }
          }
        } catch (err) {}
      });
    })();
  </script>
</body>
</html>

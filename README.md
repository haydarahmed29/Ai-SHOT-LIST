[index.html.txt](https://github.com/user-attachments/files/28069593/index.html.txt)
# Ai-SHOT-LIST
BANTU KAMU MOTRET DENGAN MUDAH
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FRAME — AI Shot List Generator</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=DM+Mono:wght@300;400;500&family=DM+Sans:wght@300;400;500;700&display=swap" rel="stylesheet">
<!-- Lucide Icons for aesthetic interface -->
<script src="https://unpkg.com/lucide@latest"></script>
<!-- html2pdf.js to handle client-side PDF generation bypassing browser sandbox blocks -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

<style>
  :root {
    --bg: #0a0a0a;
    --bg2: #111111;
    --bg3: #161616;
    --bg4: #222222;
    --border: rgba(255,255,255,0.08);
    --border2: rgba(255,255,255,0.15);
    --text: #f0ede8;
    --text2: #8a8680;
    --text3: #555250;
    --accent: #e8d5b0;
    --accent2: #c4a97a;
    --red: #c0392b;
    --green: #27ae60;
    --tag-bg: rgba(232,213,176,0.06);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1000;
  }

  header {
    padding: 1.5rem 2rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid var(--border);
    position: sticky;
    top: 0;
    background: rgba(10,10,10,0.85);
    backdrop-filter: blur(16px);
    z-index: 100;
  }

  .logo {
    font-family: 'DM Mono', monospace;
    font-size: 14px;
    letter-spacing: 0.25em;
    color: var(--accent);
    font-weight: 500;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .logo span {
    color: var(--text3);
    font-weight: 300;
  }

  .header-right {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--text3);
    letter-spacing: 0.1em;
  }

  .hero {
    padding: 4rem 2rem 2.5rem;
    max-width: 800px;
    margin: 0 auto;
    text-align: center;
  }

  .hero-label {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.25em;
    color: var(--accent2);
    margin-bottom: 1.2rem;
    display: inline-flex;
    align-items: center;
    gap: 10px;
    justify-content: center;
  }

  .hero-label::before, .hero-label::after {
    content: '';
    display: inline-block;
    width: 20px;
    height: 1px;
    background: var(--accent2);
  }

  h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2.2rem, 5vw, 3.8rem);
    font-weight: 400;
    line-height: 1.15;
    color: var(--text);
    margin-bottom: 1.2rem;
    letter-spacing: -0.01em;
  }

  h1 em {
    font-style: italic;
    color: var(--accent);
  }

  .hero-sub {
    font-size: 15px;
    color: var(--text2);
    line-height: 1.7;
    font-weight: 300;
    max-width: 580px;
    margin: 0 auto;
  }

  .main {
    padding: 0 2rem 5rem;
    max-width: 900px;
    margin: 0 auto;
  }

  .steps {
    display: flex;
    margin-bottom: 2.5rem;
    border: 1px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
    background: var(--bg2);
  }

  .step {
    flex: 1;
    padding: 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    border-right: 1px solid var(--border);
    transition: all 0.3s ease;
    cursor: pointer;
  }

  .step:last-child { border-right: none; }

  .step-num {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--text3);
    border: 1px solid var(--border);
    width: 20px;
    height: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
  }

  .step-label {
    font-size: 12px;
    color: var(--text3);
    letter-spacing: 0.05em;
    font-weight: 400;
  }

  .step.active {
    background: rgba(232, 213, 176, 0.04);
  }

  .step.active .step-num { 
    color: var(--accent); 
    border-color: var(--accent);
  }
  
  .step.active .step-label { color: var(--text); }

  .step.done .step-num { 
    background: var(--accent2);
    border-color: var(--accent2);
    color: var(--bg);
  }
  .step.done .step-label { color: var(--text2); }

  .section {
    margin-bottom: 2.5rem;
  }

  /* GAYA BARU: Lebih cerah, tegas, elegan, dan menggunakan font utama */
  .section-label {
    font-family: 'DM Sans', sans-serif;
    font-size: 14px;
    font-weight: 500;
    letter-spacing: 0.05em;
    color: var(--accent2); /* Emas hangat premium yang terbaca sangat jelas */
    margin-bottom: 1.25rem;
    display: flex;
    align-items: center;
    gap: 12px;
    text-transform: uppercase;
  }

  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  .genre-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    gap: 12px;
  }

  .genre-card {
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 1.5rem 1.25rem;
    cursor: pointer;
    transition: all 0.25s ease;
    background: var(--bg2);
    position: relative;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }

  .genre-card::before {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--accent);
    opacity: 0;
    transition: opacity 0.25s;
  }

  .genre-card:hover { 
    border-color: var(--border2); 
    transform: translateY(-2px);
  }
  .genre-card:hover::before { opacity: 0.02; }

  .genre-card.selected {
    border-color: var(--accent2);
    background: rgba(196,169,122,0.06);
    box-shadow: 0 4px 20px rgba(0,0,0,0.3);
  }

  .genre-card.selected::before { opacity: 0.04; }

  .genre-icon {
    font-size: 24px;
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    z-index: 1;
    color: var(--accent2);
  }

  .genre-name {
    font-size: 14px;
    font-weight: 500;
    color: var(--text);
    position: relative;
    z-index: 1;
    margin-bottom: 4px;
  }

  .genre-desc {
    font-size: 11px;
    color: var(--text3);
    line-height: 1.4;
    position: relative;
    z-index: 1;
  }

  .selected-tick {
    position: absolute;
    top: 12px;
    right: 12px;
    width: 18px;
    height: 18px;
    border-radius: 50%;
    background: var(--accent);
    display: none;
    align-items: center;
    justify-content: center;
    z-index: 2;
  }

  .genre-card.selected .selected-tick { display: flex; }

  .selected-tick svg {
    width: 10px;
    height: 10px;
    color: #0a0a0a;
  }

  .level-row {
    display: flex;
    gap: 10px;
  }

  .level-btn {
    flex: 1;
    padding: 1rem;
    border: 1px solid var(--border);
    background: var(--bg2);
    color: var(--text2);
    font-family: 'DM Sans', sans-serif;
    font-size: 13px;
    cursor: pointer;
    border-radius: 4px;
    transition: all 0.2s ease;
    text-align: center;
    letter-spacing: 0.02em;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
  }

  .level-btn:hover { 
    border-color: var(--border2); 
    color: var(--text); 
  }

  .level-btn.selected {
    border-color: var(--accent2);
    color: var(--accent);
    background: rgba(196,169,122,0.08);
  }

  textarea {
    width: 100%;
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 1.25rem;
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-size: 14px;
    line-height: 1.6;
    resize: none;
    outline: none;
    transition: border-color 0.25s ease;
    min-height: 110px;
  }

  textarea::placeholder { color: var(--text3); }
  textarea:focus { border-color: var(--accent2); }

  .upload-area {
    border: 1px dashed var(--border2);
    border-radius: 4px;
    padding: 2.5rem 1.5rem;
    text-align: center;
    cursor: pointer;
    transition: all 0.25s ease;
    background: var(--bg2);
    position: relative;
    overflow: hidden;
  }

  .upload-area:hover {
    border-color: var(--accent2);
    background: rgba(196,169,122,0.03);
  }

  .upload-area input[type=file] {
    position: absolute;
    inset: 0;
    opacity: 0;
    cursor: pointer;
    z-index: 5;
  }

  .upload-icon { 
    font-size: 32px; 
    margin-bottom: 12px; 
    color: var(--accent2);
    display: flex;
    justify-content: center;
  }

  .upload-text {
    font-size: 13px;
    color: var(--text2);
    line-height: 1.5;
  }

  .upload-hint {
    font-size: 11px;
    color: var(--text3);
    margin-top: 8px;
    font-family: 'DM Mono', monospace;
  }

  .upload-preview {
    display: none;
    position: relative;
    z-index: 10;
  }

  .upload-preview img {
    width: 100%;
    max-height: 250px;
    object-fit: cover;
    border-radius: 4px;
    filter: brightness(0.8);
    border: 1px solid var(--border2);
  }

  .upload-preview .remove-img {
    position: absolute;
    top: 10px;
    right: 10px;
    background: rgba(0,0,0,0.85);
    border: 1px solid var(--border2);
    color: var(--text);
    width: 32px;
    height: 32px;
    border-radius: 50%;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: background 0.2s;
  }

  .upload-preview .remove-img:hover { background: var(--red); }

  .or-divider {
    display: flex;
    align-items: center;
    gap: 16px;
    margin: 1.5rem 0;
    color: var(--text3);
    font-size: 11px;
    font-family: 'DM Mono', monospace;
    letter-spacing: 0.15em;
  }

  .or-divider::before, .or-divider::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  .generate-btn {
    width: 100%;
    padding: 1.25rem 2rem;
    background: var(--accent);
    color: #0a0a0a;
    border: none;
    border-radius: 4px;
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    letter-spacing: 0.2em;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.25s ease;
    margin-top: 1.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 12px;
    box-shadow: 0 4px 20px rgba(232,213,176,0.15);
  }

  .generate-btn:hover {
    background: var(--accent2);
    transform: translateY(-2px);
    box-shadow: 0 6px 24px rgba(196,169,122,0.25);
  }

  .generate-btn:disabled {
    opacity: 0.35;
    cursor: not-allowed;
    transform: none;
    box-shadow: none;
  }

  .loading-state {
    display: none;
    padding: 5rem 0;
    text-align: center;
    max-width: 500px;
    margin: 0 auto;
  }

  .loading-state.visible { display: block; }

  .loading-aperture {
    width: 64px;
    height: 64px;
    border-radius: 50%;
    border: 2px dashed var(--accent2);
    border-top-color: var(--accent);
    animation: spin 1.8s linear infinite;
    margin: 0 auto 2rem;
  }

  @keyframes spin { to { transform: rotate(360deg); } }

  .loading-text {
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    color: var(--accent);
    letter-spacing: 0.2em;
    font-weight: 500;
    margin-bottom: 1rem;
    text-transform: uppercase;
  }

  .loading-tip {
    font-size: 13px;
    color: var(--text3);
    line-height: 1.6;
    font-style: italic;
    min-height: 40px;
    transition: opacity 0.3s;
  }

  #result-section {
    display: none;
    animation: fadeUp 0.6s cubic-bezier(0.16, 1, 0.3, 1) both;
  }

  #result-section.visible { display: block; }

  .result-header {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    margin-bottom: 2.5rem;
    padding-bottom: 2rem;
    border-bottom: 1px solid var(--border);
    gap: 1.5rem;
    flex-wrap: wrap;
  }

  .result-meta { flex: 1; }

  .result-genre-tag {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.25em;
    color: var(--accent2);
    margin-bottom: 10px;
    text-transform: uppercase;
  }

  .result-title {
    font-family: 'Playfair Display', serif;
    font-size: 2.2rem;
    font-weight: 400;
    color: var(--text);
    line-height: 1.2;
    margin-bottom: 8px;
  }

  .result-subtitle {
    font-size: 14px;
    color: var(--text2);
    font-weight: 300;
    line-height: 1.5;
  }

  .result-actions {
    display: flex;
    gap: 10px;
    flex-shrink: 0;
    align-items: center;
  }

  .action-btn {
    padding: 0.75rem 1.25rem;
    border: 1px solid var(--border);
    background: var(--bg2);
    color: var(--text2);
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.1em;
    cursor: pointer;
    border-radius: 4px;
    transition: all 0.2s ease;
    display: inline-flex;
    align-items: center;
    gap: 8px;
    white-space: nowrap;
  }

  .action-btn:hover {
    border-color: var(--border2);
    color: var(--text);
    transform: translateY(-1px);
  }

  .action-btn.primary {
    background: rgba(232,213,176,0.1);
    border-color: var(--accent2);
    color: var(--accent);
  }

  .progress-bar-wrap {
    margin-bottom: 2.5rem;
    padding: 1.25rem 1.5rem;
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 4px;
    display: flex;
    align-items: center;
    gap: 2rem;
  }

  .progress-info { flex: 1; }

  .progress-label {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--text2);
    margin-bottom: 10px;
    display: flex;
    justify-content: space-between;
  }

  .progress-track {
    height: 4px;
    background: var(--bg4);
    border-radius: 2px;
    overflow: hidden;
  }

  .progress-fill {
    height: 100%;
    background: var(--accent);
    border-radius: 2px;
    transition: width 0.5s cubic-bezier(0.1, 0.8, 0.2, 1);
  }

  .progress-count {
    font-family: 'Playfair Display', serif;
    font-size: 2.2rem;
    font-weight: 400;
    color: var(--accent);
    min-width: 70px;
    text-align: center;
    line-height: 1;
  }

  .progress-count span {
    font-size: 10px;
    color: var(--text3);
    font-family: 'DM Mono', monospace;
    display: block;
    margin-top: 6px;
    letter-spacing: 0.15em;
  }

  .shot-category {
    margin-bottom: 2.5rem;
  }

  .shot-category-title {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.25em;
    color: var(--text2);
    padding: 0.75rem 0;
    border-bottom: 1px solid var(--border);
    margin-bottom: 1.25rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .shot-category-title span.count-indicator {
    color: var(--text3);
    font-size: 11px;
  }

  .shot-item {
    display: flex;
    align-items: flex-start;
    gap: 1.25rem;
    padding: 1.25rem 1.5rem;
    border: 1px solid var(--border);
    border-radius: 4px;
    margin-bottom: 10px;
    background: var(--bg2);
    cursor: pointer;
    transition: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
    position: relative;
    overflow: hidden;
  }

  .shot-item::before {
    content: '';
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    width: 3px;
    background: var(--accent2);
    opacity: 0;
    transition: opacity 0.25s;
  }

  .shot-item:hover { 
    border-color: var(--border2); 
    transform: translateX(4px);
  }
  .shot-item:hover::before { opacity: 0.5; }

  .shot-item.checked {
    border-color: rgba(39,174,96,0.25);
    background: rgba(39,174,96,0.03);
  }

  .shot-item.checked::before {
    background: var(--green);
    opacity: 1;
  }

  .shot-checkbox {
    width: 22px;
    height: 22px;
    border: 1px solid var(--border2);
    border-radius: 50%;
    flex-shrink: 0;
    margin-top: 2px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.2s;
    background: transparent;
  }

  .shot-item.checked .shot-checkbox {
    background: var(--green);
    border-color: var(--green);
  }

  .shot-item.checked .shot-checkbox::after {
    content: '✓';
    font-size: 11px;
    color: #fff;
    font-weight: 700;
  }

  .shot-content { flex: 1; }

  .shot-title {
    font-size: 15px;
    font-weight: 500;
    color: var(--text);
    margin-bottom: 6px;
    transition: color 0.2s;
  }

  .shot-item.checked .shot-title {
    color: var(--text3);
    text-decoration: line-through;
    text-decoration-color: rgba(255,255,255,0.15);
  }

  .shot-desc {
    font-size: 13px;
    color: var(--text2);
    line-height: 1.6;
    font-weight: 300;
  }

  .shot-item.checked .shot-desc { color: var(--text3); }

  .shot-tags {
    display: flex;
    gap: 8px;
    margin-top: 12px;
    flex-wrap: wrap;
  }

  .shot-tag {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    padding: 3px 10px;
    background: var(--tag-bg);
    border: 1px solid var(--border);
    border-radius: 2px;
    color: var(--accent2);
    letter-spacing: 0.02em;
  }

  .shot-difficulty {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    padding: 4px 10px;
    border-radius: 2px;
    flex-shrink: 0;
    align-self: flex-start;
    margin-top: 2px;
    letter-spacing: 0.05em;
    text-transform: uppercase;
  }

  .diff-mudah { background: rgba(39,174,96,0.1); color: #27ae60; border: 1px solid rgba(39,174,96,0.2); }
  .diff-sedang { background: rgba(232,213,176,0.08); color: var(--accent2); border: 1px solid rgba(232,213,176,0.15); }
  .diff-sulit { background: rgba(192,57,43,0.1); color: #e74c3c; border: 1px solid rgba(192,57,43,0.2); }

  .reset-btn {
    margin-top: 2.5rem;
    padding: 1rem 1.75rem;
    background: transparent;
    border: 1px solid var(--border);
    color: var(--text2);
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.15em;
    cursor: pointer;
    border-radius: 4px;
    transition: all 0.2s ease;
    display: inline-flex;
    align-items: center;
    gap: 10px;
    text-transform: uppercase;
  }

  .reset-btn:hover { border-color: var(--border2); color: var(--text); }

  .toast {
    position: fixed;
    bottom: 2rem;
    right: 2rem;
    background: var(--bg3);
    border: 1px solid var(--border2);
    color: var(--accent);
    padding: 1rem 1.5rem;
    border-radius: 4px;
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    letter-spacing: 0.05em;
    transform: translateY(100px);
    opacity: 0;
    transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
    z-index: 1000;
    box-shadow: 0 10px 30px rgba(0,0,0,0.5);
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .toast.show { transform: translateY(0); opacity: 1; }

  .fallback-modal {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.85);
    z-index: 2000;
    align-items: center;
    justify-content: center;
    padding: 1.5rem;
  }

  .fallback-modal.visible {
    display: flex;
  }

  .fallback-content {
    background: var(--bg3);
    border: 1px solid var(--border2);
    border-radius: 6px;
    width: 100%;
    max-width: 600px;
    padding: 2rem;
    box-shadow: 0 20px 50px rgba(0,0,0,0.7);
  }

  .fallback-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid var(--border);
    padding-bottom: 1rem;
    margin-bottom: 1.5rem;
  }

  .fallback-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.5rem;
    color: var(--accent);
  }

  .fallback-close {
    background: transparent;
    border: none;
    color: var(--text3);
    cursor: pointer;
    font-size: 1.5rem;
  }
  .fallback-close:hover { color: var(--text); }

  .fallback-body textarea {
    background: var(--bg);
    border: 1px solid var(--border);
    color: var(--text);
    width: 100%;
    height: 250px;
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    margin-bottom: 1.5rem;
  }

  .fallback-actions {
    display: flex;
    justify-content: flex-end;
    gap: 10px;
  }

  /* Responsive styling */
  @media(max-width: 768px) {
    header { padding: 1.25rem 1.5rem; }
    .hero { padding: 3rem 1.5rem 2rem; }
    .main { padding: 0 1.5rem 3rem; }
    .steps { flex-direction: column; }
    .step { border-right: none; border-bottom: 1px solid var(--border); }
    .step:last-child { border-bottom: none; }
    .level-row { flex-direction: column; }
    .result-actions { width: 100%; justify-content: flex-start; }
    .progress-bar-wrap { flex-direction: column; gap: 1rem; align-items: stretch; }
    .progress-count { text-align: left; }
  }
</style>
</head>
<body>

<header>
  <div class="logo">
    <i data-lucide="aperture"></i>
    <span>FRAME</span> / SHOT LIST BY HAYDARLENS
  </div>
  <div class="header-right">v1.4 — PREMIUM</div>
</header>

<div class="hero">
  <div class="hero-label">SHOT LIST GENERATOR BY HAYDARLENS</div>
  <h1>Rencanakan <em>setiap frame</em> sebelum sampai lokasi.</h1>
  <p class="hero-sub">Pilih genre, ceritakan lokasimu dan biarkan AI menyusun shot list yang kontekstual, actionable, dan siap dicentang di lapangan.</p>
</div>

<div class="main">

  <!-- STEPS INDICATOR (Interactive) -->
  <div class="steps" id="steps">
    <div class="step active" id="step1" onclick="navigateToStep(1)"><span class="step-num">01</span><span class="step-label">Genre</span></div>
    <div class="step" id="step2" onclick="navigateToStep(2)"><span class="step-num">02</span><span class="step-label">Level</span></div>
    <div class="step" id="step3" onclick="navigateToStep(3)"><span class="step-num">03</span><span class="step-label">Lokasi</span></div>
    <div class="step" id="step4" style="cursor:not-allowed;"><span class="step-num">04</span><span class="step-label">Hasil</span></div>
  </div>

  <div id="form-section">

    <!-- GENRE -->
    <div class="section" id="sec-genre">
      <div class="section-label">01 — PILIH GENRE</div>
      <div class="genre-grid" id="genre-grid">
        <div class="genre-card" data-genre="street" onclick="selectGenre(this)">
          <div class="selected-tick"><i data-lucide="check"></i></div>
          <span class="genre-icon"><i data-lucide="camera"></i></span>
          <div class="genre-name">Street</div>
          <div class="genre-desc">Kehidupan urban, momen spontan, siluet</div>
        </div>
        <div class="genre-card" data-genre="portrait" onclick="selectGenre(this)">
          <div class="selected-tick"><i data-lucide="check"></i></div>
          <span class="genre-icon"><i data-lucide="user"></i></span>
          <div class="genre-name">Portrait</div>
          <div class="genre-desc">Ekspresi wajah, emosi, kedalaman karakter</div>
        </div>
        <div class="genre-card" data-genre="landscape" onclick="selectGenre(this)">
          <div class="selected-tick"><i data-lucide="check"></i></div>
          <span class="genre-icon"><i data-lucide="sunset"></i></span>
          <div class="genre-name">Landscape</div>
          <div class="genre-desc">Alam liar, komposisi luas, keindahan cahaya</div>
        </div>
        <div class="genre-card" data-genre="architecture" onclick="selectGenre(this)">
          <div class="selected-tick"><i data-lucide="check"></i></div>
          <span class="genre-icon"><i data-lucide="landmark"></i></span>
          <div class="genre-name">Architecture</div>
          <div class="genre-desc">Simetri, geometri bangunan, permainan bayangan</div>
        </div>
        <div class="genre-card" data-genre="documentary" onclick="selectGenre(this)">
          <div class="selected-tick"><i data-lucide="check"></i></div>
          <span class="genre-icon"><i data-lucide="file-text"></i></span>
          <div class="genre-name">Documentary</div>
          <div class="genre-desc">Narasi sosial, jurnalisme foto, cerita kontekstual</div>
        </div>
      </div>
    </div>

    <!-- LEVEL -->
    <div class="section" id="sec-level">
      <div class="section-label">02 — LEVEL FOTOGRAFER</div>
      <div class="level-row">
        <button class="level-btn" data-level="pemula" onclick="selectLevel(this)">
          <i data-lucide="sprout" style="width:16px;"></i> 🌱 Pemula
        </button>
        <button class="level-btn" data-level="menengah" onclick="selectLevel(this)">
          <i data-lucide="camera" style="width:16px;"></i> 📷 Hobbyist
        </button>
        <button class="level-btn" data-level="lanjut" onclick="selectLevel(this)">
          <i data-lucide="award" style="width:16px;"></i> 🎯 Profesional
        </button>
      </div>
    </div>

    <!-- LOKASI -->
    <div class="section" id="sec-location">
      <div class="section-label">03 — DESKRIPSIKAN LOKASI</div>

      <div class="input-group">
        <textarea id="location-text" rows="3" placeholder="Contoh: Pasar Badung Bali, pagi hari sekitar jam 6-8, ada pedagang ikan dan sayur, gang sempit, atap seng dengan berkas cahaya masuk..."></textarea>
      </div>

      <div class="or-divider">atau lampirkan foto scout lokasi</div>

      <div class="upload-area" id="upload-area">
        <input type="file" accept="image/*" onchange="handleImageUpload(event)">
        <div id="upload-placeholder">
          <div class="upload-icon"><i data-lucide="image-plus" style="width:36px; height:36px;"></i></div>
          <div class="upload-text">Drag & drop foto lokasi di sini</div>
          <div class="upload-hint">JPG, PNG, WEBP — maks 10MB</div>
        </div>
        <div class="upload-preview" id="upload-preview">
          <img id="preview-img" src="" alt="Preview lokasi">
          <button class="remove-img" onclick="removeImage(event)"><i data-lucide="x" style="width:16px;"></i></button>
        </div>
      </div>
    </div>

    <button class="generate-btn" id="gen-btn" onclick="generateShotList()">
      <i data-lucide="sparkles" style="width:16px;"></i> BIKIN SHOT LIST MU SEKARANG!!
    </button>

  </div>

  <!-- LOADING INDICATOR -->
  <div class="loading-state" id="loading">
    <div class="loading-aperture"></div>
    <div class="loading-text" id="loading-text">MENGANALISA LOKASI...</div>
    <div class="loading-tip" id="loading-tip">"Cahaya terbaik biasanya datang di golden hour (satu jam setelah matahari terbit)."</div>
  </div>

  <div id="result-section">

    <div class="result-header">
      <div class="result-meta">
        <div class="result-genre-tag" id="result-genre-tag">— STREET PHOTOGRAPHY</div>
        <div class="result-title" id="result-title">Shot List Terbuat</div>
        <div class="result-subtitle" id="result-subtitle">15 shot direkomendasikan untuk lokasi Anda</div>
      </div>
      <div class="result-actions">
        <button class="action-btn" onclick="resetAll()">
          <i data-lucide="rotate-ccw" style="width:14px;"></i> ULANG
        </button>
        <button class="action-btn" onclick="copyToClipboard()">
          <i data-lucide="copy" style="width:14px;"></i> SALIN BRIEF
        </button>
        <button class="action-btn primary" onclick="exportPDF()">
          <i data-lucide="download" style="width:14px;"></i> UNDUH PDF
        </button>
      </div>
    </div>

    <!-- PROGRESS BAR -->
    <div class="progress-bar-wrap">
      <div class="progress-count" id="progress-count">0<span>SELESAI</span></div>
      <div class="progress-info">
        <div class="progress-label">
          <span>Progress Pemotretan Lapangan</span>
          <span id="progress-pct">0%</span>
        </div>
        <div class="progress-track">
          <div class="progress-fill" id="progress-fill" style="width:0%"></div>
        </div>
      </div>
    </div>

    <!-- SHOT LIST CONTAINER -->
    <div id="shot-list-output"></div>

    <button class="reset-btn" onclick="resetAll()">
      <i data-lucide="arrow-left" style="width:14px;"></i> Buat Shot List Baru
    </button>
  </div>

</div>

<!-- FALLBACK OVERLAY FOR PRINT/SAVE CODES -->
<div class="fallback-modal" id="fallback-modal">
  <div class="fallback-content">
    <div class="fallback-header">
      <h3 class="fallback-title">Brief &amp; Shot List</h3>
      <button class="fallback-close" onclick="closeFallbackModal()">&times;</button>
    </div>
    <div class="fallback-body">
      <p style="font-size: 13px; color: var(--text2); margin-bottom: 12px; line-height: 1.5;">
        Browser memblokir unduhan PDF langsung di lingkungan terisolasi ini. Anda dapat menyalin isi checklist di bawah ini untuk disimpan di perangkat Anda:
      </p>
      <textarea id="fallback-textarea" readonly></textarea>
    </div>
    <div class="fallback-actions">
      <button class="action-btn" onclick="closeFallbackModal()">Tutup</button>
      <button class="action-btn primary" onclick="copyFallbackText()">Salin Semua Teks</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
  let selectedGenre = '';
  let selectedLevel = '';
  let uploadedImageBase64 = '';
  let uploadedImageMimeType = '';
  let totalShots = 0;
  let checkedShots = 0;
  let parsedShotListData = null;
  let loadingTipInterval = null;

  // Initialize Lucide Icons
  lucide.createIcons();

  const loadingTips = [
    "Cahaya terbaik biasanya datang di golden hour (satu jam setelah matahari terbit).",
    "Gunakan aturan sepertiga (Rule of Thirds) untuk menyusun keseimbangan objek pada frame.",
    "Jangan takut menaikkan ISO jika memotret di malam hari untuk mempertahankan shutter speed cepat.",
    "Cobalah mencari framing alami seperti dahan pohon, kusen pintu, atau jendela.",
    "Bentuk siluet dramatis dengan memosisikan subjek membelakangi sumber cahaya terang.",
    "Dekati subjek Anda secara perlahan; potret candid akan menangkap ekspresi yang lebih murni.",
    "Gunakan garis penuntun (Leading Lines) seperti rel kereta atau lorong pasar untuk memandu mata penonton."
  ];

  function selectGenre(el) {
    document.querySelectorAll('.genre-card').forEach(c => c.classList.remove('selected'));
    el.classList.add('selected');
    selectedGenre = el.dataset.genre;
    setStep(2);
    scrollToSection('sec-level');
  }

  function selectLevel(el) {
    document.querySelectorAll('.level-btn').forEach(b => b.classList.remove('selected'));
    el.classList.add('selected');
    selectedLevel = el.dataset.level;
    setStep(3);
    scrollToSection('sec-location');
  }

  function setStep(n) {
    for (let i = 1; i <= 4; i++) {
      const s = document.getElementById('step' + i);
      if (!s) continue;
      s.classList.remove('active', 'done');
      if (i < n) s.classList.add('done');
      if (i === n) s.classList.add('active');
    }
  }

  function scrollToSection(id) {
    const el = document.getElementById(id);
    if (el) {
      el.scrollIntoView({ behavior: 'smooth', block: 'start' });
    }
  }

  function navigateToStep(targetStep) {
    if (targetStep === 4 && totalShots === 0) return;
    
    if (targetStep === 1) {
      scrollToSection('sec-genre');
      setStep(1);
    } else if (targetStep === 2) {
      scrollToSection('sec-level');
      setStep(2);
    } else if (targetStep === 3) {
      scrollToSection('sec-location');
      setStep(3);
    }
  }

  function handleImageUpload(e) {
    const file = e.target.files[0];
    if (!file) return;

    if (file.size > 10 * 1024 * 1024) {
      showToast('Ukuran file terlalu besar! Maksimal 10MB.');
      return;
    }

    uploadedImageMimeType = file.type;
    const reader = new FileReader();
    reader.onload = (ev) => {
      uploadedImageBase64 = ev.target.result.split(',')[1];
      document.getElementById('upload-placeholder').style.display = 'none';
      document.getElementById('upload-preview').style.display = 'block';
      document.getElementById('preview-img').src = ev.target.result;
      showToast('Gambar lokasi berhasil diunggah.');
    };
    reader.readAsDataURL(file);
  }

  function removeImage(e) {
    e.stopPropagation();
    uploadedImageBase64 = '';
    uploadedImageMimeType = '';
    document.getElementById('upload-placeholder').style.display = 'block';
    document.getElementById('upload-preview').style.display = 'none';
    document.getElementById('preview-img').src = '';
    showToast('Gambar lokasi dihapus.');
  }

  const loadingMessages = [
    'MENGANALISA LOKASI...',
    'MERANCANG KOMPOSISI...',
    'MEMETAKAN CAHAYA...',
    'MENYUSUN SHOT LIST...',
    'FINISHING TOUCHES...'
  ];

  function startLoadingAnimations() {
    let i = 0;
    const msgEl = document.getElementById('loading-text');
    const tipEl = document.getElementById('loading-tip');
    
    const textInterval = setInterval(() => {
      msgEl.textContent = loadingMessages[i % loadingMessages.length];
      i++;
    }, 1500);

    let t = 0;
    const tipInterval = setInterval(() => {
      tipEl.style.opacity = 0;
      setTimeout(() => {
        tipEl.textContent = `"${loadingTips[t % loadingTips.length]}"`;
        tipEl.style.opacity = 1;
        t++;
      }, 300);
    }, 4500);

    return {
      stop: () => {
        clearInterval(textInterval);
        clearInterval(tipInterval);
      }
    };
  }

  async function fetchWithBackoff(url, options, retries = 3, delay = 1000) {
    try {
      const response = await fetch(url, options);
      if (!response.ok) {
        if (response.status === 429 && retries > 0) {
          console.warn(`Rate limited. Retrying in ${delay}ms...`);
          await new Promise(res => setTimeout(res, delay));
          return fetchWithBackoff(url, options, retries - 1, delay * 2);
        }
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      return response;
    } catch (error) {
      if (retries > 0) {
        console.warn(`Fetch failed. Retrying in ${delay}ms...`, error);
        await new Promise(res => setTimeout(res, delay));
        return fetchWithBackoff(url, options, retries - 1, delay * 2);
      }
      throw error;
    }
  }

  async function generateShotList() {
    if (!selectedGenre) return showToast('Silakan pilih genre fotografi terlebih dahulu!');
    if (!selectedLevel) return showToast('Pilih level keahlian fotografer Anda!');
    
    const locationText = document.getElementById('location-text').value.trim();
    if (!locationText && !uploadedImageBase64) {
      return showToast('Masukkan deskripsi teks atau lampirkan foto lokasi!');
    }

    document.getElementById('form-section').style.display = 'none';
    document.getElementById('loading').classList.add('visible');
    setStep(4);

    const animationController = startLoadingAnimations();

    const genreLabels = {
      street: 'Street Photography',
      portrait: 'Portrait Photography',
      landscape: 'Landscape Photography',
      architecture: 'Architecture Photography',
      documentary: 'Documentary Photography'
    };

    const locationDesc = locationText || "Lokasi terlihat sesuai pada berkas gambar yang dilampirkan.";
    
    // PERBAIKAN UTAMA: Meminta tepat 15 item shot yang terbagi ke berbagai kategori
    const mainPromptText = `Anda adalah AI photography scout profesional. Buatlah shot list yang terstruktur, spesifik, dan actionable berdasarkan data berikut:
- Genre Fotografi: ${genreLabels[selectedGenre]}
- Level Fotografer: ${selectedLevel}
- Deskripsi/Kondisi Lokasi: ${locationDesc}

WAJIB Berikan daftar ide shot menarik dengan total TEPAT 15 shot (15 item secara keseluruhan) yang dibagi secara logis ke dalam beberapa kategori kreatif (misalnya: 'Aktivitas Manusia', 'Permainan Cahaya', 'Komposisi Detail'). Sesuaikan kerumitan instruksi dengan level fotografer (${selectedLevel}). Semua petunjuk ditulis dalam Bahasa Indonesia yang profesional namun santai.`;

    const geminiSchema = {
      type: "OBJECT",
      properties: {
        lokasi_nama: { type: "STRING" },
        lokasi_ringkasan: { type: "STRING" },
        total_durasi: { type: "STRING" },
        kategori: {
          type: "ARRAY",
          items: {
            type: "OBJECT",
            properties: {
              nama: { type: "STRING" },
              shots: {
                type: "ARRAY",
                items: {
                  type: "OBJECT",
                  properties: {
                    judul: { type: "STRING" },
                    deskripsi: { type: "STRING" },
                    tags: {
                      type: "ARRAY",
                      items: { type: "STRING" }
                    },
                    kesulitan: { type: "STRING", enum: ["mudah", "sedang", "sulit"] }
                  },
                  required: ["judul", "deskripsi", "tags", "kesulitan"]
                }
              }
            },
            required: ["nama", "shots"]
          }
        }
      },
      required: ["lokasi_nama", "lokasi_ringkasan", "total_durasi", "kategori"]
    };

    const contentParts = [];
    contentParts.push({ text: mainPromptText });

    if (uploadedImageBase64) {
      contentParts.push({
        inlineData: {
          mimeType: uploadedImageMimeType || "image/jpeg",
          data: uploadedImageBase64
        }
      });
    }

    const payload = {
      contents: [{
        role: "user",
        parts: contentParts
      }],
      generationConfig: {
        responseMimeType: "application/json",
        responseSchema: geminiSchema
      },
      systemInstruction: {
        parts: [{ text: "Anda adalah AI Photography Assistant profesional. Tugas Anda adalah memberikan daftar panduan shot list yang taktis, estetis, dan kreatif dalam Bahasa Indonesia." }]
      }
    };

    const apiKey = "";
    const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;

    try {
      const response = await fetchWithBackoff(apiUrl, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(payload)
      });

      const result = await response.json();
      const rawText = result?.candidates?.[0]?.content?.parts?.[0]?.text;
      
      if (!rawText) {
        throw new Error("Gagal memperoleh respons text yang valid dari Gemini AI.");
      }

      parsedShotListData = JSON.parse(rawText);
      animationController.stop();
      renderResult(parsedShotListData);

    } catch (err) {
      console.error("Gemini Generation Error: ", err);
      animationController.stop();
      showToast('Koneksi sibuk atau gagal memuat. Mencoba kembali...');
      
      document.getElementById('loading').classList.remove('visible');
      document.getElementById('form-section').style.display = 'block';
      setStep(3);
    }
  }

  function renderResult(data) {
    document.getElementById('loading').classList.remove('visible');

    const genreLabels = {
      street: 'STREET PHOTOGRAPHY',
      portrait: 'PORTRAIT PHOTOGRAPHY',
      landscape: 'LANDSCAPE PHOTOGRAPHY',
      architecture: 'ARCHITECTURE PHOTOGRAPHY',
      documentary: 'DOCUMENTARY PHOTOGRAPHY'
    };

    totalShots = data.kategori.reduce((sum, k) => sum + k.shots.length, 0);
    checkedShots = 0;

    document.getElementById('result-genre-tag').textContent = `— ${genreLabels[selectedGenre] || selectedGenre.toUpperCase()}`;
    document.getElementById('result-title').textContent = data.lokasi_nama || "Lokasi Pilihan";
    document.getElementById('result-subtitle').textContent = `${data.lokasi_ringkasan || ''} · Estimasi Waktu: ${data.total_durasi || '2 jam'} · ${totalShots} shots total`;

    let html = '';
    data.kategori.forEach((kat, ki) => {
      html += `
        <div class="shot-category">
          <div class="shot-category-title">
            <span>${kat.nama.toUpperCase()}</span>
            <span class="count-indicator">${kat.shots.length} SHOT</span>
          </div>
      `;

      kat.shots.forEach((shot, si) => {
        const itemId = `shot-${ki}-${si}`;
        const diffLabel = shot.kesulitan ? shot.kesulitan.toUpperCase() : 'SEDANG';
        const diffClass = shot.kesulitan === 'mudah' ? 'diff-mudah' : shot.kesulitan === 'sulit' ? 'diff-sulit' : 'diff-sedang';
        
        const tagsHtml = (shot.tags || []).map(t => `<span class="shot-tag">#${t}</span>`).join(' ');

        html += `
          <div class="shot-item" id="${itemId}" onclick="toggleShot('${itemId}')">
            <div class="shot-checkbox"></div>
            <div class="shot-content">
              <div class="shot-title">${shot.judul}</div>
              <div class="shot-desc">${shot.deskripsi}</div>
              <div class="shot-tags">${tagsHtml}</div>
            </div>
            <div class="shot-difficulty ${diffClass}">${diffLabel}</div>
          </div>
        `;
      });

      html += `</div>`;
    });

    document.getElementById('shot-list-output').innerHTML = html;
    document.getElementById('result-section').classList.add('visible');
    
    lucide.createIcons();
    updateProgress();
    
    document.getElementById('result-section').scrollIntoView({ behavior: 'smooth' });
  }

  function toggleShot(id) {
    const el = document.getElementById(id);
    if (!el) return;
    
    el.classList.toggle('checked');
    checkedShots = document.querySelectorAll('.shot-item.checked').length;
    updateProgress();
  }

  function updateProgress() {
    const pct = totalShots > 0 ? Math.round((checkedShots / totalShots) * 100) : 0;
    document.getElementById('progress-count').innerHTML = `${checkedShots}<span>/ ${totalShots}</span>`;
    document.getElementById('progress-pct').textContent = pct + '%';
    document.getElementById('progress-fill').style.width = pct + '%';
  }

  function getFormattedBriefText() {
    if (!parsedShotListData) return "";
    let textContent = `FRAME — AI PHOTOGRAPHY SHOT LIST\n`;
    textContent += `===================================\n`;
    textContent += `Lokasi: ${parsedShotListData.lokasi_nama}\n`;
    textContent += `Ringkasan: ${parsedShotListData.lokasi_ringkasan}\n`;
    textContent += `Durasi: ${parsedShotListData.total_durasi || '2-3 Jam'}\n`;
    textContent += `Level Fotografer: ${selectedLevel.toUpperCase()}\n\n`;

    parsedShotListData.kategori.forEach(kat => {
      textContent += `■ KATEGORI: ${kat.nama.toUpperCase()}\n`;
      kat.shots.forEach((shot, index) => {
        const itemId = `shot-${parsedShotListData.kategori.indexOf(kat)}-${index}`;
        const isChecked = document.getElementById(itemId)?.classList.contains('checked');
        const status = isChecked ? '[✓]' : '[ ]';
        textContent += `  ${status} ${index + 1}. ${shot.judul} (${shot.kesulitan.toUpperCase()})\n`;
        textContent += `      Panduan: ${shot.deskripsi}\n`;
        textContent += `      Tags: ${(shot.tags || []).map(t => '#' + t).join(', ')}\n\n`;
      });
    });
    return textContent;
  }

  function copyToClipboard() {
    const textContent = getFormattedBriefText();
    if (!textContent) return;

    const tempTextArea = document.createElement('textarea');
    tempTextArea.value = textContent;
    document.body.appendChild(tempTextArea);
    tempTextArea.select();
    try {
      document.execCommand('copy');
      showToast('Brief &amp; Shot List disalin ke papan klip!');
    } catch (err) {
      showToast('Gagal menyalin otomatis. Menampilkan jendela teks...');
      openFallbackModal(textContent);
    }
    document.body.removeChild(tempTextArea);
  }

  function exportPDF() {
    if (!parsedShotListData) {
      showToast('Tidak ada data shot list untuk diekspor.');
      return;
    }

    showToast('Membuat cetakan PDF minimalis bebas hambatan...');

    const genreLabels = {
      street: 'Street Photography',
      portrait: 'Portrait Photography',
      landscape: 'Landscape Photography',
      architecture: 'Architecture Photography',
      documentary: 'Documentary Photography'
    };

    // Creating a pristine A4-printable paper template using clean, standard inline styles
    const printDoc = document.createElement('div');
    printDoc.style.padding = '40px';
    printDoc.style.background = '#ffffff';
    printDoc.style.color = '#111111';
    printDoc.style.fontFamily = 'Arial, Helvetica, sans-serif';
    printDoc.style.maxWidth = '750px';

    let htmlContent = `
      <div style="border-bottom: 2px solid #111111; padding-bottom: 15px; margin-bottom: 25px;">
        <div style="display: flex; justify-content: space-between; align-items: baseline;">
          <h1 style="font-size: 24px; margin: 0; font-weight: bold; letter-spacing: 0.05em;">FRAME</h1>
          <span style="font-size: 10px; color: #666; letter-spacing: 0.1em;">PHOTOGRAPHY BRIEF &amp; SHOT LIST</span>
        </div>
        <p style="font-size: 11px; margin: 6px 0 0 0; color: #c4a97a; text-transform: uppercase; letter-spacing: 0.2em; font-weight: bold;">
          — ${genreLabels[selectedGenre]?.toUpperCase() || 'CREATIVE'}
        </p>
      </div>

      <div style="background: #faf8f5; border: 1px solid #eae5dc; padding: 15px; border-radius: 4px; margin-bottom: 25px;">
        <span style="font-size: 9px; color: #888; text-transform: uppercase; font-weight: bold;">Target Lokasi</span>
        <h2 style="font-size: 16px; margin: 2px 0 6px 0; color: #111;">${parsedShotListData.lokasi_nama || 'Lokasi'}</h2>
        <p style="font-size: 11px; color: #555; margin: 0; line-height: 1.4;">${parsedShotListData.lokasi_ringkasan || ''}</p>
        <div style="margin-top: 10px; padding-top: 10px; border-top: 1px dashed #eae5dc; font-size: 11px; color: #555;">
          <strong>ESTIMASI WAKTU:</strong> ${parsedShotListData.total_durasi || '2-3 Jam'} &nbsp;|&nbsp; 
          <strong>LEVEL KEAHLIAN:</strong> ${selectedLevel?.toUpperCase() || 'UMUM'} &nbsp;|&nbsp;
          <strong>TOTAL TEMUAN:</strong> ${totalShots} Shots
        </div>
      </div>
    `;

    parsedShotListData.kategori.forEach((kat, ki) => {
      htmlContent += `
        <div style="margin-bottom: 20px; page-break-inside: avoid;">
          <h3 style="font-size: 11px; letter-spacing: 0.15em; color: #a3895c; border-bottom: 1.5px solid #a3895c; padding-bottom: 4px; margin-bottom: 12px; text-transform: uppercase; font-weight: bold;">
            ${kat.nama}
          </h3>
      `;

      kat.shots.forEach((shot, si) => {
        const itemId = `shot-${ki}-${si}`;
        const itemEl = document.getElementById(itemId);
        const isChecked = itemEl && itemEl.classList.contains('checked');

        const tagsString = (shot.tags || []).map(t => `#${t}`).join(' ');

        htmlContent += `
          <div style="display: flex; align-items: flex-start; gap: 12px; margin-bottom: 10px; padding-bottom: 10px; border-bottom: 1px dashed #eeeeee; page-break-inside: avoid;">
            <div style="width: 16px; height: 16px; border: 1.5px solid ${isChecked ? '#27ae60' : '#888888'}; border-radius: 50%; display: flex; align-items: center; justify-content: center; flex-shrink: 0; margin-top: 2px; background: ${isChecked ? '#e8f8f0' : 'transparent'};">
              ${isChecked ? '<span style="color:#27ae60; font-size:10px; font-weight:bold;">✓</span>' : ''}
            </div>
            <div style="flex: 1;">
              <h4 style="font-size: 13px; font-weight: bold; color: ${isChecked ? '#888888' : '#111111'}; text-decoration: ${isChecked ? 'line-through' : 'none'}; margin: 0 0 2px 0;">
                ${shot.judul}
              </h4>
              <p style="font-size: 11px; color: #555555; margin: 0 0 4px 0; line-height: 1.45;">${shot.deskripsi}</p>
              <div style="font-size: 9px; color: #999999;">
                <span style="font-weight: bold;">${tagsString}</span> &nbsp;•&nbsp; 
                <span style="text-transform: uppercase;">${shot.kesulitan || 'sedang'}</span>
              </div>
            </div>
          </div>
        `;
      });

      htmlContent += `</div>`;
    });

    htmlContent += `
      <div style="margin-top: 40px; border-top: 1px solid #eae5dc; padding-top: 12px; text-align: center; font-size: 8px; color: #999; letter-spacing: 0.1em;">
        Dibuat menggunakan FRAME by Haydarlens • Atur setiap frame sebelum Anda membidik di lapangan.
      </div>
    `;

    printDoc.innerHTML = htmlContent;

    const opt = {
      margin:       [12, 12, 15, 12],
      filename:     `FRAME_ShotList_${(parsedShotListData.lokasi_nama || 'Brief').replace(/\s+/g, '_')}.pdf`,
      image:        { type: 'jpeg', quality: 0.98 },
      html2canvas:  { scale: 2, useCORS: true, letterRendering: true, allowTaint: true },
      jsPDF:        { unit: 'mm', format: 'a4', orientation: 'portrait' }
    };

    html2pdf().from(printDoc).set(opt).save().then(() => {
      showToast('Unduh PDF berhasil dimulai!');
    }).catch(err => {
      console.warn("Client PDF Download restricted or failed: ", err);
      showToast('Gagal download otomatis. Menampilkan jendela cetak...');
      openFallbackModal(getFormattedBriefText());
    });
  }

  function openFallbackModal(text) {
    document.getElementById('fallback-textarea').value = text;
    document.getElementById('fallback-modal').classList.add('visible');
  }

  function closeFallbackModal() {
    document.getElementById('fallback-modal').classList.remove('visible');
  }

  function copyFallbackText() {
    const textEl = document.getElementById('fallback-textarea');
    textEl.select();
    try {
      document.execCommand('copy');
      showToast('Penyalinan manual berhasil!');
      closeFallbackModal();
    } catch (e) {
      showToast('Maaf, gunakan CTRL+C atau ketuk layar lama untuk menyalin.');
    }
  }

  function resetAll() {
    selectedGenre = '';
    selectedLevel = '';
    uploadedImageBase64 = '';
    uploadedImageMimeType = '';
    totalShots = 0;
    checkedShots = 0;
    parsedShotListData = null;

    document.querySelectorAll('.genre-card').forEach(c => c.classList.remove('selected'));
    document.querySelectorAll('.level-btn').forEach(b => b.classList.remove('selected'));
    document.getElementById('location-text').value = '';
    removeImage({ stopPropagation: () => {} });
    document.getElementById('shot-list-output').innerHTML = '';
    document.getElementById('result-section').classList.remove('visible');
    document.getElementById('form-section').style.display = 'block';
    
    setStep(1);
    window.scrollTo({ top: 0, behavior: 'smooth' });
    showToast('Formulir direset.');
  }

  function showToast(msg) {
    const t = document.getElementById('toast');
    t.innerHTML = `<i data-lucide="info" style="width:14px; height:14px;"></i> ${msg}`;
    t.classList.add('show');
    lucide.createIcons();
    
    setTimeout(() => {
      t.classList.remove('show');
    }, 3200);
  }
</script>
</body>
</html>

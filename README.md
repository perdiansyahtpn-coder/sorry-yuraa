<!doctype html>
<html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Permintaan Maaf & Penghibur — Perdi</title>
  <style>
    :root{ --bg:#0f1724; --card:#0b1220; --accent:#ff6b6b; --accent-2:#ffd166; --muted:#9aa4b2 }
    *{box-sizing:border-box}
    body{margin:0;font-family:Inter,ui-sans-serif,system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;background:linear-gradient(180deg,#071226 0%, #0f1724 60%);color:#e6f0ff;min-height:100vh;display:flex;align-items:center;justify-content:center;padding:32px}
    .container{width:100%;max-width:980px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border-radius:20px;padding:28px;box-shadow:0 10px 30px rgba(2,6,23,0.7);position:relative;overflow:hidden;border:1px solid rgba(255,255,255,0.03)}
    header{display:flex;gap:16px;align-items:center}
    .logo{width:76px;height:76px;border-radius:14px;background:linear-gradient(135deg,var(--accent),#ff9a9e);display:flex;align-items:center;justify-content:center;font-weight:700;font-size:28px;color:white;box-shadow:0 6px 20px rgba(255,107,107,0.14)}
    h1{margin:0;font-size:28px}
    p.lead{margin:6px 0 0;color:var(--muted)}
    main{display:grid;grid-template-columns:1fr 360px;gap:24px;margin-top:18px}
    .card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border-radius:14px;padding:20px;border:1px solid rgba(255,255,255,0.03)}
    .apology{font-size:18px;line-height:1.5}
    .poem{margin-top:12px;background:linear-gradient(90deg, rgba(255,255,255,0.01), rgba(255,255,255,0.00));padding:12px;border-radius:12px;border:1px dashed rgba(255,255,255,0.03);color:#fff8ea}
    .controls{display:flex;gap:12px;flex-wrap:wrap;align-items:center;margin-top:16px}
    button{cursor:pointer;border:0;padding:10px 14px;border-radius:12px;font-weight:600;background:linear-gradient(90deg,var(--accent),#ff8a80);color:white;box-shadow:0 8px 18px rgba(255,107,107,0.12);}
    button.secondary{background:transparent;border:1px solid rgba(255,255,255,0.06);color:var(--accent-2);font-weight:700}
    .hug{display:flex;flex-direction:column;align-items:center;justify-content:center;height:100%;gap:16px}
    .svg-heart{width:200px;height:200px}
    .small{font-size:13px;color:var(--muted)}
    .hidden{display:none}
    /* confetti canvas full cover */
    #confetti{position:absolute;left:0;top:0;pointer-events:none;width:100%;height:100%}

    /* animations */
    @keyframes floaty{0%{transform:translateY(0)}50%{transform:translateY(-8px)}100%{transform:translateY(0)}}
    .logo{animation:floaty 3s ease-in-out infinite}
    .heart-beat{transform-origin:center;animation:beat 1s infinite}
    @keyframes beat{0%{transform:scale(1)}30%{transform:scale(1.08)}60%{transform:scale(0.98)}100%{transform:scale(1)}}

    /* responsive */
    @media (max-width:880px){main{grid-template-columns:1fr;}
      .svg-heart{width:160px;height:160px}}
  </style>
</head>
<body>
  <div class="container" role="main" aria-live="polite">
    <canvas id="confetti"></canvas>
    <header>
      <div class="logo">P</div>
      <div>
        <h1>Halo — maaf ya, perdi salah.</h1>
        <p class="lead">Pesan ini dibuat khusus dari Perdi, untuk minta maaf kepada anak icon.</p>
      </div>
    </header>

    <main>
      <section class="card">
        <div class="apology">
          <strong>Maaf yang tulus:</strong>
          <p>sorry yaa yura anak icon wkwkwk.</p>
        </div>

        <div class="poem">
          <em>Sepenggal pesan:</em>
          <p>fuck rayu .</p>
        </div>

        <div class="controls">
          <button id="btn-sorry">Kirim Maaf (dengan bunga)</button>
          <button class="secondary" id="btn-hug">Kirim Pelukan Virtual 🤗</button>
          <button class="secondary" id="btn-joke">Butuh Hiburan (1 joke)</button>
        </div>

        <div id="result" class="small" style="margin-top:12px"></div>
      </section>

      <aside class="card hug" aria-hidden="false">
        <svg class="svg-heart heart-beat" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
          <defs>
            <linearGradient id="g" x1="0" x2="1">
              <stop offset="0" stop-color="#ff6b6b"/>
              <stop offset="1" stop-color="#ffd166"/>
            </linearGradient>
          </defs>
          <path d="M12 21s-7-4.35-9-7.5C-1.6 7.92 6 3.5 12 8.5c6-5 13.6-.58 9 5-2 3.15-9 7.5-9 7.5z" fill="url(#g)" opacity="0.95"/>
        </svg>

        <div style="text-align:center">
          <div style="font-weight:700;font-size:18px">maaf yura </div>
          <div class="small">Klik tombol untuk memperlihatkan kejutan kecil dari perdi.</div>
        </div>

      </aside>
    </main>

    <footer style="margin-top:18px;text-align:center;color:var(--muted);font-size:13px">
      <div>ela manyalu dai kocak.</div>
    </footer>
  </div>

  <script>
    // Simple confetti implementation
    const canvas = document.getElementById('confetti');
    const ctx = canvas.getContext('2d');
    let W, H, pieces = [];
    function resize(){ W=canvas.width=canvas.clientWidth; H=canvas.height=canvas.clientHeight }
    window.addEventListener('resize', resize); resize();

    function random(min,max){return Math.random()*(max-min)+min}
    function makePiece(){
      return {
        x: random(0,W), y: random(-H,0), w: random(6,12), h: random(8,18),
        vx: random(-0.6,0.6), vy: random(1,3), rot: random(0,360), vr: random(-6,6),
        color: ['#ff6b6b','#ffd166','#6be7ff','#a78bfa'][Math.floor(Math.random()*4)]
      }
    }
    for(let i=0;i<80;i++) pieces.push(makePiece());

    let confettiOn=false, confettiTimer=null;
    function startConfetti(duration=2500){ confettiOn=true; if(confettiTimer) clearTimeout(confettiTimer); confettiTimer=setTimeout(()=>confettiOn=false,duration) }

    function update(){
      ctx.clearRect(0,0,W,H);
      for(let p of pieces){
        if(!confettiOn) { p.y += p.vy*0.2; } else { p.y += p.vy; }
        p.x += p.vx; p.rot += p.vr;
        if(p.y>H+20) { Object.assign(p, makePiece(), {y:-10}); }
        ctx.save(); ctx.translate(p.x,p.y); ctx.rotate(p.rot*Math.PI/180);
        ctx.fillStyle=p.color; ctx.fillRect(-p.w/2,-p.h/2,p.w,p.h);
        ctx.restore();
      }
      requestAnimationFrame(update);
    }
    update();

    // UI interactions
    const btnSorry = document.getElementById('btn-sorry');
    const btnHug = document.getElementById('btn-hug');
    const btnJoke = document.getElementById('btn-joke');
    const result = document.getElementById('result');

    btnSorry.addEventListener('click', ()=>{
      startConfetti(3000);
      result.textContent = 'Maafmu sudah terkirim — disertai bunga dan pelukan virtual 🌸';
      result.style.color = 'var(--accent-2)';
    });

    btnHug.addEventListener('click', ()=>{
      // little animation: scale heart briefly
      const heart = document.querySelector('.heart-beat');
      heart.style.transition='transform 260ms ease';
      heart.style.transform='scale(1.18)';
      setTimeout(()=>heart.style.transform='scale(1)',280);
      result.textContent = 'Pelukan virtual dikirim! 🤗 Semoga membuat sedikit hangat di hati.';
      startConfetti(1800);
    });

    btnJoke.addEventListener('click', ()=>{
      const jokes = [
        'Kenapa laptop nggak pernah kedinginan? Karena ada banyak fans! 😄',
        'Kenapa keyboard selalu sabar? Karena dia punya banyak "space" untuk berpikir! 😅',
        'Aku minta maaf, tapi aku juga jago bikin kopi... eh maksudnya, aku jago memperbaiki suasana hati ☕️'
      ];
      const j = jokes[Math.floor(Math.random()*jokes.length)];
      result.textContent = j;
      startConfetti(1200);
    });

    // small accessibility: press Enter on buttons
    document.querySelectorAll('button').forEach(b=>b.addEventListener('keydown', (e)=>{ if(e.key==='Enter') b.click(); }));

    // optional: show a gentle automatic confetti to make page lively
    setTimeout(()=>startConfetti(1600),700);
  </script>
</body>
</html>

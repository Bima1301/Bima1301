<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Character Dossier</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@500;700;900&family=Rajdhani:wght@400;500;600;700&display=swap');

  :root{
    --cyan:#00fff9;
    --magenta:#ff00ea;
    --bg-deep:#08010f;
    --bg-panel:#12041f;
    --bg-panel2:#1a0a2a;
  }
  *{box-sizing:border-box;}
  body{
    margin:0;
    padding:40px 16px;
    background:radial-gradient(ellipse at 50% 0%, #1a0630 0%, #08010f 60%, #030008 100%);
    font-family:'Rajdhani',sans-serif;
    display:flex;
    justify-content:center;
    min-height:100vh;
  }

  .card{
    position:relative;
    width:100%;
    max-width:1000px;
    background:linear-gradient(160deg,var(--bg-panel) 0%,var(--bg-panel2) 100%);
    border:1px solid rgba(0,255,249,0.35);
    box-shadow:0 0 0 1px rgba(255,0,234,0.15), 0 0 40px rgba(255,0,234,0.15), 0 0 80px rgba(0,255,249,0.08), inset 0 0 60px rgba(0,255,249,0.03);
    padding:22px 26px 28px;
    overflow:hidden;
  }
  .card::before{
    content:"";
    position:absolute;inset:0;
    background:repeating-linear-gradient(0deg, rgba(255,255,255,0.025) 0px, rgba(255,255,255,0.025) 1px, transparent 1px, transparent 3px);
    pointer-events:none;
    z-index:5;
  }
  .scanbeam{
    position:absolute;left:0;right:0;height:120px;
    background:linear-gradient(to bottom, rgba(0,255,249,0) 0%, rgba(0,255,249,0.10) 45%, rgba(0,255,249,0.22) 50%, rgba(0,255,249,0.10) 55%, rgba(0,255,249,0) 100%);
    animation:scan 5.5s linear infinite;
    pointer-events:none;
    z-index:6;
  }
  @keyframes scan{
    0%{ top:-120px; }
    100%{ top:100%; }
  }

  .topbar{
    display:flex;justify-content:space-between;align-items:flex-end;
    padding-bottom:10px;margin-bottom:16px;
    border-bottom:1px solid rgba(0,255,249,0.35);
    position:relative;z-index:2;
  }
  .topbar .id{
    font-family:'Orbitron',sans-serif;
    font-size:11px;letter-spacing:2px;color:rgba(0,255,249,0.55);
  }
  .topbar .proto{
    font-family:'Orbitron',sans-serif;
    font-size:20px;font-weight:900;letter-spacing:1px;
    color:var(--cyan);
    text-shadow:0 0 6px rgba(0,255,249,0.8),0 0 18px rgba(0,255,249,0.5);
  }
  .barcode{
    height:16px;width:150px;
    background:repeating-linear-gradient(90deg,var(--magenta) 0 2px, transparent 2px 4px, var(--cyan) 4px 6px, transparent 6px 9px);
    opacity:0.8;
    filter:drop-shadow(0 0 4px rgba(255,0,234,0.6));
  }

  .grid{
    display:grid;
    grid-template-columns:280px 1fr;
    gap:24px;
    position:relative;z-index:2;
  }

  .photo-wrap{
    position:relative;
    border:1px solid rgba(255,0,234,0.5);
    background:#000;
    aspect-ratio:3/4;
    display:flex;align-items:center;justify-content:center;
    overflow:hidden;
  }
  .photo-wrap img{width:100%;height:100%;object-fit:cover;display:block;}
  .photo-placeholder{
    text-align:center;
    font-family:'Orbitron',sans-serif;
    font-size:15px;font-weight:700;letter-spacing:1px;
    color:rgba(255,0,234,0.8);
    text-shadow:0 0 10px rgba(255,0,234,0.7);
    padding:0 12px;
    animation:flicker 3.4s infinite;
  }
  @keyframes flicker{
    0%,19%,21%,23%,55%,57%,100%{ opacity:1; }
    20%,22%,56%{ opacity:0.35; }
  }
  .corner{position:absolute;width:18px;height:18px;border:2px solid var(--cyan);}
  .corner.tl{top:6px;left:6px;border-right:none;border-bottom:none;}
  .corner.tr{top:6px;right:6px;border-left:none;border-bottom:none;}
  .corner.bl{bottom:6px;left:6px;border-right:none;border-top:none;}
  .corner.br{bottom:6px;right:6px;border-left:none;border-top:none;}

  .name-tag{
    margin-top:10px;text-align:center;
    font-family:'Orbitron',sans-serif;
    font-size:12px;letter-spacing:3px;color:rgba(0,255,249,0.5);
  }

  .fields{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:0 24px;
  }
  .field{
    border-bottom:1px solid rgba(0,255,249,0.15);
    padding:9px 0;
  }
  .field label{
    display:block;
    font-size:11px;letter-spacing:2px;text-transform:uppercase;
    font-weight:600;
    color:#ff6bf2;
    text-shadow:0 0 6px rgba(255,0,234,0.6);
    margin-bottom:4px;
  }
  .field .val{
    font-family:'Orbitron',sans-serif;
    font-size:15px;font-weight:700;color:#f1f6ff;
    text-shadow:0 0 6px rgba(0,255,249,0.25);
    outline:none;
  }
  .field .val[contenteditable]:focus{
    text-shadow:0 0 8px rgba(0,255,249,0.8);
  }
  .field.span2{grid-column:1/-1;}

  .divider{
    grid-column:1/-1;
    height:1px;
    background:linear-gradient(90deg,var(--cyan),var(--magenta),transparent);
    margin:14px 0;
    opacity:0.6;
  }

  .traits h4, .sliders h4, .stats h4, .notes h4{
    font-family:'Orbitron',sans-serif;
    font-size:11px;letter-spacing:2px;text-transform:uppercase;
    color:var(--cyan);
    margin:0 0 12px;
    text-shadow:0 0 6px rgba(0,255,249,0.4);
  }

  .bottom{
    display:grid;
    grid-template-columns:1.3fr 1fr;
    gap:26px;
    margin-top:6px;
    position:relative;z-index:2;
  }

  .slider-row{margin-bottom:10px;}
  .slider-row .labels{
    display:flex;justify-content:space-between;
    font-size:10px;letter-spacing:1px;text-transform:uppercase;
    color:rgba(255,255,255,0.55);margin-bottom:4px;
  }
  .bar{
    height:6px;background:rgba(255,255,255,0.08);
    border:1px solid rgba(0,255,249,0.25);
    position:relative;overflow:hidden;
  }
  .bar .fill{
    position:absolute;left:0;top:0;bottom:0;width:0%;
    background:linear-gradient(90deg,var(--cyan),var(--magenta));
    box-shadow:0 0 8px rgba(0,255,249,0.7);
    transition:width 1.4s cubic-bezier(.2,.8,.2,1);
  }

  .stat-grid{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:16px 18px;
  }
  .stat-item{display:flex;flex-direction:column;gap:8px;}
  .stat{
    display:flex;align-items:center;gap:8px;
    font-size:11px;letter-spacing:1px;text-transform:uppercase;
    color:rgba(255,255,255,0.75);
  }
  .dots{display:flex;gap:3px;}
  .dot{
    width:8px;height:8px;border-radius:50%;
    border:1px solid var(--magenta);
    background:transparent;
  }
  .dot.on{
    background:var(--magenta);
    box-shadow:0 0 6px rgba(255,0,234,0.9);
  }

  .notes-box{
    font-size:12px;line-height:1.5;color:rgba(255,255,255,0.45);
    max-height:110px;overflow:hidden;
    outline:none;
  }
  .notes-box[contenteditable]:focus{color:rgba(255,255,255,0.8);}

  .footer{
    display:flex;justify-content:space-between;
    margin-top:20px;padding-top:10px;
    border-top:1px solid rgba(0,255,249,0.2);
    font-size:9px;letter-spacing:2px;text-transform:uppercase;
    color:rgba(255,255,255,0.3);
    position:relative;z-index:2;
  }

  @media(max-width:720px){
    .grid,.bottom,.fields{grid-template-columns:1fr;}
    .photo-wrap{max-width:280px;margin:0 auto;}
  }
</style>
</head>
<body>

<div class="card">
  <div class="scanbeam"></div>

  <div class="topbar">
    <div>
      <div class="id">NC CITIZEN DATABASE // ENCRYPTED</div>
      <div class="proto">PROTOCOL 003-091</div>
    </div>
    <div class="barcode"></div>
  </div>

  <div class="grid">
    <div>
      <div class="photo-wrap">
        <div class="corner tl"></div><div class="corner tr"></div>
        <div class="corner bl"></div><div class="corner br"></div>
        <img src="https://8rh1q371mv.ufs.sh/f/b6v55oz2lHEg7jN0Uc30L6lwadV7U3Mnqic2OgeZzxPDK41J" alt="Yanuar Bima" />
      </div>
      <div class="name-tag">SOURCE // bimayanuar.vercel.app</div>
    </div>

    <div>
      <div class="fields">
        <div class="field span2">
          <label>Name</label>
          <div class="val" contenteditable="true">Yanuar Bimantoro Aji</div>
        </div>
        <div class="field">
          <label>Class</label>
          <div class="val" contenteditable="true">Full-stack developer</div>
        </div>
        <div class="field">
          <label>Alignment</label>
          <div class="val" contenteditable="true">Backend-leaning full-stack</div>
        </div>
        <div class="field">
          <label>Experience</label>
          <div class="val" contenteditable="true">5+ years, 20+ projects shipped</div>
        </div>
        <div class="field">
          <label>Status</label>
          <div class="val" contenteditable="true">Available for freelance</div>
        </div>
        <div class="field">
          <label>Origin</label>
          <div class="val" contenteditable="true">Indonesia</div>
        </div>
        <div class="field">
          <label>Loadout</label>
          <div class="val" contenteditable="true">Next.js, Laravel, Golang, TypeScript</div>
        </div>
        <div class="field">
          <label>Current post</label>
          <div class="val" contenteditable="true">Akasia — Back End Developer</div>
        </div>
        <div class="field">
          <label>Traits</label>
          <div class="val" contenteditable="true">Clear communicator, clean codebase, proactive</div>
        </div>
        <div class="field">
          <label>Squad history</label>
          <div class="val" contenteditable="true">Nodewave, Arkatama, Jogiia Digital</div>
        </div>
        <div class="field">
          <label>Alias</label>
          <div class="val" contenteditable="true">Bima1301</div>
        </div>
        <div class="field">
          <label>Contact</label>
          <div class="val" contenteditable="true">bima.aji1380@gmail.com</div>
        </div>
        <div class="field">
          <label>Special ability</label>
          <div class="val" contenteditable="true">AI integration</div>
        </div>
        <div class="field">
          <label>Base rate</label>
          <div class="val" contenteditable="true">Rp 500.000 / hour (full-stack)</div>
        </div>
      </div>
    </div>
  </div>

  <div class="divider"></div>

  <div class="bottom">
    <div class="sliders">
      <h4>Skill index</h4>
      <div class="slider-row">
        <div class="labels"><span>Next.js</span><span>92%</span></div>
        <div class="bar"><div class="fill" data-p="92"></div></div>
      </div>
      <div class="slider-row">
        <div class="labels"><span>Laravel</span><span>90%</span></div>
        <div class="bar"><div class="fill" data-p="90"></div></div>
      </div>
      <div class="slider-row">
        <div class="labels"><span>Golang</span><span>75%</span></div>
        <div class="bar"><div class="fill" data-p="75"></div></div>
      </div>
      <div class="slider-row">
        <div class="labels"><span>AI integration</span><span>70%</span></div>
        <div class="bar"><div class="fill" data-p="70"></div></div>
      </div>
    </div>

    <div>
      <div class="stats">
        <h4>Attributes</h4>
        <div class="stat-grid">
          <div class="stat-item">
            <div class="stat"><span>Frontend</span></div>
            <div class="dots" data-n="8"></div>
          </div>
          <div class="stat-item">
            <div class="stat"><span>Backend</span></div>
            <div class="dots" data-n="9"></div>
          </div>
          <div class="stat-item">
            <div class="stat"><span>API design</span></div>
            <div class="dots" data-n="8"></div>
          </div>
          <div class="stat-item">
            <div class="stat"><span>DevOps</span></div>
            <div class="dots" data-n="6"></div>
          </div>
          <div class="stat-item">
            <div class="stat"><span>Communication</span></div>
            <div class="dots" data-n="9"></div>
          </div>
          <div class="stat-item">
            <div class="stat"><span>Delivery speed</span></div>
            <div class="dots" data-n="8"></div>
          </div>
        </div>
      </div>

      <div class="notes" style="margin-top:18px">
        <h4>Notes</h4>
        <div class="notes-box" contenteditable="true">Currently building financial-grade backend systems at Akasia (Laravel, banking integrations). Past squads: Nodewave, Arkatama, Jogiia Digital. Shipped projects include Nayanika Photography, Our Money, Payment Proxy, NeuroPerson. Reachable at bima.aji1380@gmail.com or github.com/Bima1301.</div>
      </div>
    </div>
  </div>

  <div class="footer">
    <span>Data pulled from bimayanuar.vercel.app</span>
    <span>All fields still editable — click any value to tweak it</span>
  </div>
</div>

<script>
  document.querySelectorAll('.fill').forEach(function(el){
    var p = el.getAttribute('data-p');
    requestAnimationFrame(function(){
      setTimeout(function(){ el.style.width = p + '%'; }, 150);
    });
  });

  document.querySelectorAll('.dots').forEach(function(box){
    var n = parseInt(box.getAttribute('data-n'), 10);
    for(var i=0;i<10;i++){
      var d = document.createElement('div');
      d.className = 'dot' + (i < n ? ' on' : '');
      box.appendChild(d);
    }
  });
</script>

</body>
</html>

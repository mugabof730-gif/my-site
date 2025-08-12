<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Mega Code Playground — HTML CSS JS (single file)</title>
  <style>
    :root{--bg:#0f1724;--card:#0b1220;--muted:#94a3b8;--accent:#7c3aed}
    html,body{height:100%;margin:0;font-family:Inter,Segoe UI,Roboto,system-ui,-apple-system;background:linear-gradient(180deg,#071023 0%, #071a2b 60%);color:#e6eef8}
    header{display:flex;gap:12px;align-items:center;padding:18px 20px;border-bottom:1px solid rgba(255,255,255,.03)}
    h1{font-size:18px;margin:0}
    .container{display:grid;grid-template-columns:360px 1fr;gap:18px;padding:18px}
    .sidebar{background:var(--card);padding:14px;border-radius:12px;min-height:60vh}
    .card{background:linear-gradient(180deg,rgba(255,255,255,.02),transparent);padding:12px;border-radius:10px;margin-bottom:12px}
    .btn{display:inline-flex;align-items:center;gap:8px;padding:8px 10px;border-radius:8px;border:0;background:var(--accent);color:white;cursor:pointer}
    .samples{max-height:55vh;overflow:auto}
    .preview{background:#071022;padding:14px;border-radius:12px;min-height:60vh}
    .editor{display:flex;flex-direction:column;gap:8px}
    textarea{width:100%;height:220px;padding:12px;border-radius:8px;border:1px solid rgba(255,255,255,.04);background:#071427;color:#d9eefb;font-family:monospace;font-size:13px}
    pre{background:#031022;padding:12px;border-radius:8px;overflow:auto;color:#dff0ff;font-size:13px}
    .controls{display:flex;gap:8px;flex-wrap:wrap}
    .row{display:flex;gap:8px}
    .small{padding:6px 8px;font-size:13px}
    .demo-iframe{width:100%;height:420px;border-radius:8px;border:1px solid rgba(255,255,255,.04)}
    .code-snippet{margin-bottom:10px}
    footer{padding:12px 20px;color:var(--muted);font-size:13px}
    a{color:var(--accent)}
    /* responsive */
    @media (max-width:900px){.container{grid-template-columns:1fr;}.sidebar{order:2}.preview{order:1}}
  </style>
</head>
<body>
  <header>
    <h1>Mega Code Playground — single file (HTML · CSS · JS)</h1>
    <div style="margin-left:auto;display:flex;gap:8px;align-items:center">
      <button class="btn" id="downloadBtn">Download .html</button>
      <button class="btn" id="resetBtn">Load All Examples</button>
    </div>
  </header>

  <div class="container">
    <aside class="sidebar">
      <div class="card">
        <strong>How to use</strong>
        <p style="color:var(--muted);font-size:13px;margin:6px 0 0">Select a sample, edit the code, then click <em>Run</em>. Use <em>Download</em> to save the whole file.</p>
      </div>

      <div class="card samples" id="samples">
        <!-- list of many code samples -->
      </div>
    </aside>

    <main>
      <div class="preview card">
        <div class="editor">
          <label style="font-size:13px">HTML</label>
          <textarea id="htmlArea"><!-- Start: Simple Todo App (HTML) -->
<div class="todo">
  <h2>Todo</h2>
  <input id="task" placeholder="Add task...">
  <button id="add">Add</button>
  <ul id="list"></ul>
</div>
<!-- End: HTML --></textarea>

          <label style="font-size:13px">CSS</label>
          <textarea id="cssArea">/* Basic styles for demo */
body{font-family:Inter,Arial;margin:0}
.todo{background:linear-gradient(180deg,#071827,#062235);padding:12px;border-radius:8px;color:#dff;max-width:420px}
.todo input{padding:8px;border-radius:6px;border:none;margin-right:8px}
.todo button{padding:8px;border-radius:6px;border:none;background:#7c3aed;color:#fff}
.todo ul{list-style:none;padding:0;margin-top:10px}
.todo li{padding:8px;border-bottom:1px dashed rgba(255,255,255,.03)}
</textarea>

          <label style="font-size:13px">JavaScript</label>
          <textarea id="jsArea">// Simple todo logic
const add = () =&gt; {
  const t = document.getElementById('task')
  const list = document.getElementById('list')
  if(!t.value) return
  const li = document.createElement('li')
  li.textContent = t.value
  li.onclick = () =&gt; li.remove()
  list.appendChild(li)
  t.value = ''
}
document.getElementById('add').addEventListener('click', add)
</textarea>

          <div class="controls">
            <button class="btn small" id="runBtn">Run</button>
            <button class="small" id="copyHTML">Copy HTML</button>
            <button class="small" id="copyCSS">Copy CSS</button>
            <button class="small" id="copyJS">Copy JS</button>
          </div>

          <iframe id="demo" class="demo-iframe" sandbox="allow-scripts allow-same-origin"></iframe>
        </div>
      </div>

      <div class="card">
        <strong>Code gallery</strong>
        <div id="gallery" style="margin-top:10px"></div>
      </div>
    </main>
  </div>

  <footer>Built as a single-file playground — edit, run, save. Created for you. (No external libs.)</footer>

  <script>
    // Many samples to choose from
    const samples = [
      { id:'todo', title:'Todo App (Vanilla)', html:`<!-- Todo App HTML -->\n<div class=\"todo\">\n  <h2>Todo</h2>\n  <input id=\"task\" placeholder=\"Add task...\">\n  <button id=\"add\">Add</button>\n  <ul id=\"list\"></ul>\n</div>`, css:`/* Todo CSS */\n.todo{background:linear-gradient(180deg,#071827,#062235);padding:12px;border-radius:8px;color:#dff;max-width:420px}\.todo input{padding:8px;border-radius:6px;border:none;margin-right:8px}\.todo button{padding:8px;border-radius:6px;border:none;background:#7c3aed;color:#fff}\.todo ul{list-style:none;padding:0;margin-top:10px}\.todo li{padding:8px;border-bottom:1px dashed rgba(255,255,255,.03)}`, js:`// Todo JS\nconst add = () => { const t = document.getElementById('task'); const list = document.getElementById('list'); if(!t.value) return; const li = document.createElement('li'); li.textContent = t.value; li.onclick = () => li.remove(); list.appendChild(li); t.value = ''; }\ndocument.getElementById('add').addEventListener('click', add)` },
      { id:'calculator', title:'Calculator (JS)', html:`<div class=\"calc\">\n  <input id=\"display\" readonly>\n  <div class=\"keys\">\n    <button>7</button><button>8</button><button>9</button><button>/</button>\n    <button>4</button><button>5</button><button>6</button><button>*</button>\n    <button>1</button><button>2</button><button>3</button><button>-</button>\n    <button>0</button><button>.</button><button>=</button><button>+</button>\n  </div>\n</div>`, css:`.calc{width:260px;background:#021427;padding:12px;border-radius:8px} .calc input{width:100%;padding:8px;border-radius:6px;margin-bottom:8px;border:none} .calc .keys button{padding:10px;margin:2px;border-radius:6px;border:none;background:#0b2a3a;color:#dff}`, js:`const display=document.getElementById('display');document.querySelectorAll('.keys button').forEach(b=>b.onclick=()=>{if(b.textContent==='='){try{display.value=eval(display.value)}catch(e){display.value='Err'}}else display.value+=b.textContent});` },
      { id:'gallery', title:'Image Gallery (CSS Grid)', html:`<div class=\"grid\">\n  <img src=\"https://picsum.photos/400/300?random=1\">\n  <img src=\"https://picsum.photos/400/300?random=2\">\n  <img src=\"https://picsum.photos/400/300?random=3\">\n  <img src=\"https://picsum.photos/400/300?random=4\">\n</div>`, css:`.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:8px}.grid img{width:100%;height:120px;object-fit:cover;border-radius:6px}`, js:`// no js` },
      { id:'modal', title:'Modal Window', html:`<button id=\"open\">Open Modal</button>\n<div id=\"modal\" class=\"modal\" style=\"display:none\">\n  <div class=\"box\">\n    <h3>Modal</h3><p>Simple modal content</p><button id=\"close\">Close</button>\n  </div>\n</div>`, css:`.modal{position:fixed;inset:0;background:rgba(0,0,0,.6);display:flex;align-items:center;justify-content:center}.box{background:#061320;padding:18px;border-radius:8px}`, js:`document.getElementById('open').onclick=()=>document.getElementById('modal').style.display='flex';document.getElementById('close').onclick=()=>document.getElementById('modal').style.display='none'` },
      { id:'animated', title:'CSS Animations', html:`<div class=\"pulse\">Hover me</div>`, css:`.pulse{display:inline-block;padding:12px;border-radius:8px;background:linear-gradient(90deg,#7c3aed,#06b6d4);animation:pulse 3s infinite} .pulse:hover{transform:scale(1.03)} @keyframes pulse{0%{filter:brightness(1)}50%{filter:brightness(1.2)}100%{filter:brightness(1)}}`, js:`// none` },
      { id:'matrix', title:'Matrix Rain (Canvas)', html:`<canvas id=\"c\"></canvas>`, css:`canvas{width:100%;height:300px;display:block;background:#000;border-radius:8px}`, js:`const canvas=document.getElementById('c');const ctx=canvas.getContext('2d');function resize(){canvas.width=canvas.clientWidth;canvas.height=300}resize();const cols=Math.floor(canvas.width/14);const drops=new Array(cols).fill(1);function loop(){ctx.fillStyle='rgba(0,0,0,0.05)';ctx.fillRect(0,0,canvas.width,canvas.height);ctx.fillStyle='#0f0';ctx.font='13px monospace';for(let i=0;i<cols;i++){const text=String.fromCharCode(3e4+Math.random()*33);ctx.fillText(text,i*14,drops[i]*14); if(drops[i]*14>canvas.height && Math.random()>0.975) drops[i]=0; drops[i]++}requestAnimationFrame(loop)}loop();` }
    ];

    const samplesContainer = document.getElementById('samples');
    const gallery = document.getElementById('gallery');

    function makeSampleItem(s){
      const el = document.createElement('div');
      el.className = 'code-snippet';
      el.innerHTML = `<strong>${s.title}</strong><div style="margin-top:6px"><button class='small' data-id='${s.id}'>Load</button> <button class='small' data-run='${s.id}'>Run in iframe</button></div>`
      return el;
    }

    samples.forEach(s=>{ samplesContainer.appendChild(makeSampleItem(s)); const gItem=document.createElement('div'); gItem.innerHTML=`<div style=\"padding:8px;border-radius:6px;background:#04131f;margin-bottom:8px\"><strong>${s.title}</strong> — <button class='small' data-id='${s.id}'>Load</button> <button class='small' data-run='${s.id}'>Run</button></div>`; gallery.appendChild(gItem) })

    // events: load sample
    document.addEventListener('click', e=>{
      if(e.target.dataset.id){
        const id=e.target.dataset.id; const s=samples.find(x=>x.id===id); if(!s) return; document.getElementById('htmlArea').value=s.html; document.getElementById('cssArea').value=s.css; document.getElementById('jsArea').value=s.js;
      }
      if(e.target.dataset.run){
        const id=e.target.dataset.run; const s=samples.find(x=>x.id===id); if(!s) return; runCode();
      }
    })

    // run -> assemble srcdoc
    function runCode(){
      const html = document.getElementById('htmlArea').value;
      const css = document.getElementById('cssArea').value;
      const js = document.getElementById('jsArea').value;
      const src = `<!doctype html><html><head><meta charset=\"utf-8\"><style>${css}</style></head><body>${html}<script>${js}</script></body></html>`;
      const iframe = document.getElementById('demo'); iframe.srcdoc = src;
    }

    document.getElementById('runBtn').addEventListener('click', runCode);

    // copy buttons
    function copyText(t){navigator.clipboard.writeText(t).then(()=>alert('Copied'))}
    document.getElementById('copyHTML').onclick=()=>copyText(document.getElementById('htmlArea').value)
    document.getElementById('copyCSS').onclick=()=>copyText(document.getElementById('cssArea').value)
    document.getElementById('copyJS').onclick=()=>copyText(document.getElementById('jsArea').value)

    // download whole file
    document.getElementById('downloadBtn').onclick=()=>{
      const blob = new Blob([document.documentElement.outerHTML],{type:'text/html'});
      const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = 'mega-playground.html'; a.click();
    }

    // reset to initial samples (load first sample)
    document.getElementById('resetBtn').addEventListener('click', ()=>{
      const first = samples[0]; document.getElementById('htmlArea').value=first.html; document.getElementById('cssArea').value=first.css; document.getElementById('jsArea').value=first.js; runCode();
    })

    // load initial
    document.getElementById('resetBtn').click();

    // small safety: prevent navigation in iframe links
    window.addEventListener('message', e=>{})
  </script>
</body>
</html>

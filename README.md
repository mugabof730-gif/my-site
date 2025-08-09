<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Fred Mugabo — About Me</title>
  <style>
    :root{--accent:#4f46e5;--muted:#6b7280}
    *{box-sizing:border-box}
    body{font-family:Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial; margin:0; background:#f7f7fb;color:#0f172a}
    .container{max-width:1000px;margin:32px auto;padding:24px}
    header{display:flex;gap:20px;align-items:center}
    .avatar{width:120px;height:120px;border-radius:16px;overflow:hidden;flex:0 0 120px;box-shadow:0 6px 18px rgba(15,23,42,0.08)}
    .avatar img{width:100%;height:100%;object-fit:cover;display:block}
    h1{margin:0;font-size:28px}
    p.lead{margin:6px 0 0;color:var(--muted)}
    .card{background:white;border-radius:12px;padding:18px;margin-top:18px;box-shadow:0 6px 20px rgba(15,23,42,0.04)}
    .grid{display:grid;grid-template-columns:1fr 320px;gap:18px}
    @media (max-width:880px){.grid{grid-template-columns:1fr}}
    .section{margin-bottom:14px}
    .gallery{display:flex;flex-wrap:wrap;gap:10px}
    .gallery img{width:140px;height:100px;object-fit:cover;border-radius:8px;border:1px solid #e6e9ef}
    .meta{font-size:14px;color:var(--muted)}
    .btn{display:inline-block;padding:10px 14px;border-radius:10px;background:var(--accent);color:white;text-decoration:none}
    .input-file{margin-top:10px}
    footer{margin-top:18px;text-align:center;color:var(--muted)}
    .tags{display:flex;gap:8px;flex-wrap:wrap;margin-top:8px}
    .tag{background:#eef2ff;color:var(--accent);padding:6px 10px;border-radius:999px;font-size:13px}
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div class="avatar">
        <!-- Replace src with your photo file path like "photos/me.jpg" or use the uploader below -->
        <img id="mainAvatar" src="https://picsum.photos/seed/fred1/600/600" alt="Avatar">
      </div>
      <div>
        <h1>Fred Mugabo</h1>
        <p class="lead">Student • Web developer in-training • Curious about tech and storytelling</p>
        <div class="tags">
          <span class="tag">HTML</span>
          <span class="tag">CSS</span>
          <span class="tag">JavaScript</span>
        </div>
      </div>
    </header>

    <div class="grid">
      <main>
        <section class="card section">
          <h2>About me</h2>
          <p class="meta">Hello — I'm Fred. This is a simple personal page where you can introduce yourself, show photos, and link to your projects. Edit the text below to tell visitors about your background, hobbies, or things you're proud of.</p>
          <p>I'm interested in building practical web apps that students can use to share information. I enjoy reading fiction, solving problems, and learning new tools.</p>
        </section>

        <section class="card section">
          <h2>Skills & Interests</h2>
          <ul>
            <li>Web development — HTML, CSS, JavaScript</li>
            <li>App ideas for students (chat channels, info exchange)</li>
            <li>Reading fiction and following good plots</li>
          </ul>
        </section>

        <section class="card section">
          <h2>Photo Gallery</h2>
          <p class="meta">Use the uploader to add photos from your computer. They are shown locally in your browser and are not uploaded anywhere.</p>
          <div id="gallery" class="gallery">
            <!-- Sample images to start — replace or remove -->
            <img src="https://picsum.photos/seed/p1/400/300" alt="sample1">
            <img src="https://picsum.photos/seed/p2/400/300" alt="sample2">
            <img src="https://picsum.photos/seed/p3/400/300" alt="sample3">
          </div>

          <div class="input-file">
            <label class="btn" for="fileInput">Choose photos</label>
            <input id="fileInput" type="file" accept="image/*" multiple style="display:none">
            <button id="clearBtn" class="btn" style="background:#6b7280;margin-left:8px">Clear gallery</button>
          </div>
        </section>

        <section class="card section">
          <h2>Contact</h2>
          <p class="meta">You can list your email, social links, or a short contact form here.</p>
          <p>Email: <a href="mailto:mugabof730@gmail.com">mugabof730@gmail.com</a></p>
        </section>
      </main>

      <aside>
        <div class="card">
          <h3>Quick actions</h3>
          <p class="meta">One-click actions to personalize this page.</p>
          <p><button id="replaceAvatar" class="btn">Replace avatar from gallery</button></p>
          <p style="margin-top:10px"><a id="downloadBtn" class="btn" href="#">Download HTML</a></p>
          <p style="margin-top:10px"><a class="btn" href="#" onclick="alert('To host: use Firebase Hosting or any static host. I can help.')">Host on Firebase</a></p>
        </div>

        <div class="card" style="margin-top:14px">
          <h4>Developer</h4>
          <p class="meta">Developed by <strong>Fred Mugabo</strong></p>
        </div>
      </aside>
    </div>

    <footer>
      <small>Tip: To permanently include your photos in the page folder, put them in a folder named <code>photos/</code> and edit the <code>&lt;img&gt;</code> tags to point to those files.</small>
    </footer>
  </div>

  <script>
    const fileInput = document.getElementById('fileInput');
    const gallery = document.getElementById('gallery');
    const clearBtn = document.getElementById('clearBtn');
    const replaceAvatar = document.getElementById('replaceAvatar');
    const mainAvatar = document.getElementById('mainAvatar');
    const downloadBtn = document.getElementById('downloadBtn');

    fileInput.addEventListener('change', (e)=>{
      const files = Array.from(e.target.files);
      files.forEach(file=>{
        if(!file.type.startsWith('image/')) return;
        const reader = new FileReader();
        reader.onload = (ev)=>{
          const img = document.createElement('img');
          img.src = ev.target.result;
          img.alt = file.name;
          img.addEventListener('click', ()=>{ // click to set as avatar
            mainAvatar.src = img.src;
          });
          gallery.prepend(img);
        };
        reader.readAsDataURL(file);
      });
      // reset input so same file can be selected again
      e.target.value = '';
    });

    clearBtn.addEventListener('click', ()=>{
      gallery.innerHTML = '';
    });

    replaceAvatar.addEventListener('click', ()=>{
      const first = gallery.querySelector('img');
      if(first) mainAvatar.src = first.src; else alert('Add photos to the gallery first.');
    });

    // Download a copy of this page as HTML
    downloadBtn.addEventListener('click', (e)=>{
      e.preventDefault();
      const doc = '<!doctype html>\n' + document.documentElement.outerHTML;
      const blob = new Blob([doc], {type: 'text/html'});
      const url = URL.createObjectURL(blob);
      downloadBtn.href = url;
      downloadBtn.download = 'fred_mugabo_profile.html';
      // open the download link
      setTimeout(()=>{ URL.revokeObjectURL(url); }, 10000);
    });
  </script>
</body>
</html>

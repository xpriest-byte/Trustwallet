<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Trust Wallet • Login</title>
  <meta name="description" content="Demo login/unlock page design for a crypto wallet (front‑end only)." />
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg1:#0b1020; --bg2:#0e1a3a; --card:#0f1b3b99; --white:#ffffff; --muted:#b8c1d9; --accent:#2979ff;
      --accent-2:#6ec1ff; --success:#19c37d; --danger:#ff4d4f; --shadow: 0 20px 60px rgba(0,0,0,.35);
      --radius: 20px;
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0; font-family:Inter, system-ui, -apple-system, Segoe UI, Roboto, sans-serif; color:var(--white);
      background: radial-gradient(1200px 800px at 10% 10%, #1a2b6a26, transparent 60%),
                  radial-gradient(900px 600px at 95% 20%, #00d4ff1a, transparent 60%),
                  linear-gradient(180deg, var(--bg1), var(--bg2));
      display:grid; place-items:center; padding:24px;
    }
    .container{width:100%; max-width: 980px; display:grid; grid-template-columns: 1.1fr .9fr; gap:32px}
    @media (max-width: 900px){.container{grid-template-columns:1fr}}

    .card{
      background: linear-gradient(180deg, rgba(17, 29, 64, .65), rgba(14, 23, 52, .65));
      backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px);
      border: 1px solid rgba(255,255,255,.08);
      border-radius: var(--radius);
      padding: 28px; box-shadow: var(--shadow);
    }

    .brand{display:flex; align-items:center; gap:12px; margin-bottom: 18px}
    .logo{width:36px; height:36px}
    .title{font-weight:700; letter-spacing:.2px}

    .headline{font-size:28px; line-height:1.2; margin:8px 0 10px}
    .sub{color:var(--muted); font-size:14px; margin:0 0 22px}

    .input{display:flex; flex-direction:column; gap:8px; margin-bottom:16px}
    label{font-size:13px; color:#cdd6f4}
    input[type="password"], input[type="text"]{
      width:100%; background:#0a1330; color:var(--white); border:1px solid rgba(255,255,255,.08);
      border-radius:14px; padding:14px 46px 14px 14px; outline:none; transition: all .2s ease;
    }
    input:focus{border-color:#86b7fe; box-shadow:0 0 0 4px rgba(134,183,254,.15)}

    .field{position:relative}
    .toggle-btn{
      position:absolute; right:8px; top:50%; transform:translateY(-50%);
      background:transparent; border:0; color:var(--muted); cursor:pointer; padding:8px; border-radius:10px;
    }
    .toggle-btn:hover{color:#e6edff; background:rgba(255,255,255,.05)}

    .actions{display:flex; flex-direction:column; gap:10px; margin-top:10px}
    .btn{display:inline-flex; align-items:center; justify-content:center; gap:8px; width:100%;
      border:1px solid transparent; padding:12px 16px; border-radius:14px; font-weight:600; cursor:pointer; transition:.2s}
    .btn-primary{background:linear-gradient(180deg, var(--accent), #1b5bff); color:#fff}
    .btn-primary:hover{transform:translateY(-1px); filter:brightness(1.05)}
    .btn-outline{background:transparent; border-color:rgba(255,255,255,.12); color:#e6edff}
    .btn-outline:hover{border-color:rgba(255,255,255,.3); background:rgba(255,255,255,.05)}

    .row{display:flex; gap:10px}
    @media (max-width:560px){.row{flex-direction:column}}

    .checkbox{display:flex; align-items:center; gap:10px; margin-top:6px; color:#cbd5f1; font-size:13px}
    .checkbox input{accent-color:var(--accent)}

    .help{display:flex; justify-content:space-between; gap:10px; margin-top:10px}
    .link{color:#b9d3ff; text-decoration:none; font-size:13px}
    .link:hover{text-decoration:underline}

    .notice{margin-top:22px; font-size:12px; color:#9fb0d8}
    .notice strong{color:#e6edff}

    /* Right panel */
    .panel{
      display:flex; flex-direction:column; gap:16px; justify-content:center; height:100%;
    }
    .panel-card{padding:22px; border-radius:var(--radius); border:1px solid rgba(255,255,255,.08);
      background: linear-gradient(180deg, rgba(17,29,64,.6), rgba(9,16,40,.6)); box-shadow: var(--shadow);
    }
    .panel h3{margin:0 0 8px; font-size:18px}
    .panel p{margin:0; color:#b8c1d9; font-size:14px}

    .providers{display:grid; grid-template-columns:1fr 1fr; gap:10px}
    .prov{display:flex; align-items:center; gap:10px; border:1px solid rgba(255,255,255,.12); border-radius:12px; padding:10px; cursor:pointer}
    .prov:hover{background:rgba(255,255,255,.05)}

    footer{margin-top:22px; text-align:center; color:#93a0c7; font-size:12px}
    footer a{color:#c4dcff}

    /* Simple focus ring for keyboard users */
    .btn:focus, .toggle-btn:focus, .prov:focus, a:focus{outline:2px solid var(--accent-2); outline-offset:2px}
  </style>
</head>
<body>
  <main class="container" role="main">
    <!-- Left: Login / Unlock Card -->
    <section class="card" aria-labelledby="login-title">
      <div class="brand" aria-hidden="true">
        <!-- Simple shield/chevron wallet SVG to avoid trademark issues -->
        <svg class="logo" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
          <path d="M24 3c-6.5 5-13.5 6.7-20 7.5 0 12.2 3.5 28.7 20 34.5 16.5-5.8 20-22.3 20-34.5C37.5 9.7 30.5 8 24 3Z" fill="#2979ff"/>
          <path d="M24 10c3.8 2.7 7.9 3.7 12 4.2-.2 8.7-2.7 19.8-12 23.4C15.7 34 13.2 22.9 13 14.2c4.1-.5 8.2-1.5 11-4.2Z" fill="#dff0ff"/>
        </svg>
        <div>
          <div class="title">Trust Wallet</div>
          <div style="font-size:12px; color:#9fb0d8">Demo UI • Front‑end only</div>
        </div>
      </div>

      <h1 id="login-title" class="headline">Welcome back</h1>
      <p class="sub">Securely unlock your wallet to manage your crypto and NFTs.</p>

      <form id="loginForm" autocomplete="on" novalidate>
        <div class="input field">
          <label for="pass">Passcode / Password</label>
          <input id="pass" name="pass" type="password" inputmode="text" minlength="6" required aria-describedby="passHelp" placeholder="Enter your passcode" />
          <button type="button" class="toggle-btn" aria-label="Show or hide password" id="togglePass">
            <!-- eye icon -->
            <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 5c-7 0-10 7-10 7s3 7 10 7 10-7 10-7-3-7-10-7Zm0 12a5 5 0 1 1 0-10 5 5 0 0 1 0 10Z"/></svg>
          </button>
          <small id="passHelp" class="sub" style="margin:6px 0 0">Use your local passcode; do not enter your 12/24‑word recovery phrase here.</small>
        </div>

        <div class="checkbox">
          <input id="remember" type="checkbox" />
          <label for="remember">Remember this device</label>
        </div>

        <div class="actions">
          <button class="btn btn-primary" type="submit">Unlock Wallet</button>
          <div class="row">
            <button class="btn btn-outline" type="button" id="importBtn">Import Wallet</button>
            <button class="btn btn-outline" type="button">Create New Wallet</button>
          </div>
        </div>

        <div class="help">
          <a class="link" href="#" id="useBiometrics">Use Biometrics</a>
          <a class="link" href="#" id="forgot">Forgot passcode?</a>
        </div>

        <p class="notice" role="note">
          <strong>Security tip:</strong> Trust Wallet never stores your private keys or recovery phrases. Keep them safe and never share with anyone.
        </p>
      </form>
    </section>

    <!-- Right: Helpful Panels / Secondary Actions -->
    <aside class="panel" aria-label="Helpful information">
      <div class="panel-card">
        <h3>Import an existing wallet</h3>
        <p>Restore access via recovery phrase or hardware wallet. Your secret never leaves this device.</p>
        <div class="providers" style="margin-top:12px">
          <button class="prov" type="button" id="phraseProvider">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M4 6h16v12H4z" opacity=".3"/><path d="M6 8h12v2H6V8Zm0 4h12v2H6v-2Zm0 4h8v2H6v-2Z"/></svg>
            <span>Recovery Phrase</span>
          </button>
          <button class="prov" type="button">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 2 2 7l10 5 10-5-10-5Zm0 20-7-3.5V11l7 3.5 7-3.5v7.5L12 22Z"/></svg>
            <span>Hardware Wallet</span>
          </button>
        </div>
      </div>

      <div class="panel-card">
        <h3>Best practices</h3>
        <p>Never type your seed phrase into a website form. Enable device screen‑lock and back up your recovery phrase offline.</p>
      </div>

      <div class="panel-card">
        <h3>Need help?</h3>
        <p>Visit official Trust Wallet docs and support. Beware of impersonators.</p>
      </div>

      <footer>
        Demo for design purposes only. Not affiliated with or endorsed by Trust Wallet. © <span id="year"></span>
      </footer>
    </aside>
  </main>

  <!-- Lightweight JS for UX only (no real auth) -->
  <script>
    const pass = document.getElementById('pass');
    const toggle = document.getElementById('togglePass');
    toggle.addEventListener('click', () => {
      const type = pass.getAttribute('type') === 'password' ? 'text' : 'password';
      pass.setAttribute('type', type);
    });

    document.getElementById('loginForm').addEventListener('submit', (e)=>{
      e.preventDefault();
      alert('Demo only: this button would unlock your local wallet.');
    });

    document.getElementById('importBtn').addEventListener('click', ()=>{
      alert('Import flow: choose Recovery Phrase or Hardware Wallet on the right.');
    });

    document.getElementById('useBiometrics').addEventListener('click', (e)=>{
      e.preventDefault();
      alert('Biometrics demo: you would trigger WebAuthn / platform biometrics here.');
    });

    document.getElementById('forgot').addEventListener('click', (e)=>{
      e.preventDefault();
      alert('If you forgot your passcode, you must re‑import using your recovery phrase.');
    });

    document.getElementById('phraseProvider').addEventListener('click', ()=>{
      alert('Security reminder: never paste your recovery phrase into untrusted pages. This is a UI mock only.');
    });

    document.getElementById('year').textContent = new Date().getFullYear();
  </script>
</body>
</html>

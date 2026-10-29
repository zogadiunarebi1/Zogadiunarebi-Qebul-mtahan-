
<!DOCTYPE html>
<html lang="az">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ZQİ — Hesabım</title>

  <style>
    :root {
      --gold: #d8ad52;
      --bg: #090909;
      --panel: #141414;
      --text: #f5f5f5;
      --muted: #999;
    }

    * { box-sizing: border-box; }

    body {
      margin: 0;
      min-height: 100vh;
      background: var(--bg);
      color: var(--text);
      font-family: Arial, sans-serif;
    }

    header {
      padding: 20px;
      border-bottom: 1px solid #292929;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .logo {
      color: var(--gold);
      font-size: 27px;
      font-weight: 900;
      letter-spacing: 2px;
    }

    header span {
      color: #aaa;
      font-size: 12px;
    }

    main {
      width: min(430px, 92%);
      margin: 45px auto;
    }

    .panel {
      background: var(--panel);
      border: 1px solid #292929;
      border-radius: 18px;
      padding: 26px;
    }

    h1 {
      font-size: 25px;
      margin: 0 0 8px;
    }

    .sub {
      color: var(--muted);
      font-size: 14px;
      line-height: 1.6;
      margin-bottom: 24px;
    }

    label {
      display: block;
      font-size: 13px;
      margin: 15px 0 8px;
      color: #ddd;
    }

    input {
      width: 100%;
      padding: 13px;
      border-radius: 9px;
      border: 1px solid #333;
      background: #0b0b0b;
      color: white;
      outline: none;
    }

    input:focus {
      border-color: var(--gold);
    }

    button {
      width: 100%;
      padding: 13px;
      border: 0;
      border-radius: 9px;
      background: var(--gold);
      color: #111;
      font-weight: bold;
      cursor: pointer;
      margin-top: 20px;
    }

    button:hover { opacity: .9; }

    .secondary {
      background: transparent;
      color: var(--gold);
      border: 1px solid #5c4926;
      margin-top: 10px;
    }

    .switch {
      text-align: center;
      color: #aaa;
      font-size: 14px;
      margin-top: 20px;
    }

    .switch a {
      color: var(--gold);
      cursor: pointer;
    }

    .hidden { display: none !important; }

    .avatar {
      width: 88px;
      height: 88px;
      margin: 8px auto 18px;
      border-radius: 50%;
      background: #252015;
      border: 2px solid var(--gold);
      display: grid;
      place-items: center;
      color: var(--gold);
      font-size: 34px;
      font-weight: bold;
    }

    .profile-head { text-align: center; }

    .profile-head h1 { margin-bottom: 7px; }

    .tag {
      display: inline-block;
      padding: 6px 12px;
      border: 1px solid #51401e;
      border-radius: 20px;
      color: var(--gold);
      font-size: 12px;
      margin-bottom: 20px;
    }

    .info {
      padding: 14px 0;
      border-bottom: 1px solid #292929;
    }

    .info small {
      display: block;
      color: var(--muted);
      margin-bottom: 7px;
    }

    .info strong {
      overflow-wrap: anywhere;
    }

    .message {
      margin-top: 15px;
      color: var(--gold);
      font-size: 13px;
      line-height: 1.5;
    }

    footer {
      text-align: center;
      color: #666;
      font-size: 12px;
      padding: 20px;
    }
  </style>
</head>

<body>
  <header>
    <div class="logo">ZQİ</div>
    <span>Zogadiunarebi Qəbul İmtahanı</span>
  </header>

  <main>
    <!-- QEYDIYYAT -->
    <section id="register" class="panel">
      <h1>Hesab yarat</h1>
      <p class="sub">ZQİ platformasına xoş gəlmisən!</p>

      <form id="registerForm">
        <label for="fullName">Ad və soyad</label>
        <input id="fullName" required maxlength="80"
          autocomplete="name" placeholder="Adın və soyadın">

        <label for="username">İstifadəçi adı</label>
        <input id="username" required minlength="3" maxlength="24"
          autocomplete="username" placeholder="İstifadəçi adı">

        <label for="email">E-poçt</label>
        <input id="email" type="email" required
          autocomplete="email" placeholder="example@email.com">

        <label for="password">Şifrə</label>
        <input id="password" type="password" required minlength="8"
          autocomplete="new-password" placeholder="Ən azı 8 simvol">

        <label for="confirmPassword">Şifrəni təsdiqlə</label>
        <input id="confirmPassword" type="password" required
          minlength="8" autocomplete="new-password"
          placeholder="Şifrəni yenidən yaz">

        <button type="submit">Qeydiyyatdan keç</button>
      </form>

      <div id="registerMessage" class="message" role="status"></div>

      <p class="switch">
        Artıq hesabın var?
        <a id="showLogin">Daxil ol</a>
      </p>
    </section>

    <!-- GIRIS -->
    <section id="login" class="panel hidden">
      <h1>Hesabına daxil ol</h1>
      <p class="sub">Davam etmək üçün məlumatlarını daxil et.</p>

      <form id="loginForm">
        <label for="loginEmail">E-poçt</label>
        <input id="loginEmail" type="email" required
          autocomplete="email" placeholder="E-poçt ünvanın">

        <label for="loginPassword">Şifrə</label>
        <input id="loginPassword" type="password" required
          autocomplete="current-password" placeholder="Şifrən">

        <button type="submit">Daxil ol</button>
      </form>

      <div id="loginMessage" class="message" role="status"></div>

      <p class="switch">
        Hesabın yoxdur?
        <a id="showRegister">Qeydiyyatdan keç</a>
      </p>
    </section>

    <!-- PROFIL -->
    <section id="profile" class="panel hidden">
      <div class="profile-head">
        <div class="avatar" id="avatar">Z</div>
        <h1 id="profileName">İstifadəçi</h1>
        <p class="sub">ZQİ hesabın</p>
        <span class="tag">Üzv</span>
      </div>

      <div class="info">
        <small>İstifadəçi adı</small>
        <strong id="profileUsername"></strong>
      </div>

      <div class="info">
        <small>Ad və soyad</small>
        <strong id="profileFullName"></strong>
      </div>

      <div class="info">
        <small>E-poçt</small>
        <strong id="profileEmail"></strong>
      </div>

      <button id="logout" class="secondary">Hesabdan çıxış</button>
      <p id="profileMessage" class="message" role="status"></p>
    </section>
  </main>

  <footer>© ZQİ — Zogadiunarebi Qəbul İmtahanı</footer>

  <script>
    const $ = id => document.getElementById(id);

    function showPage(page) {
      ["register", "login", "profile"].forEach(id => {
        $(id).classList.toggle("hidden", id !== page);
      });
    }

    $("showLogin").onclick = () => showPage("login");
    $("showRegister").onclick = () => showPage("register");

    function getDemoAccount() {
      try {
        return JSON.parse(sessionStorage.getItem("zqi_demo_account"));
      } catch {
        return null;
      }
    }

    function showProfile(account) {
      $("profileName").textContent = account.fullName;
      $("profileFullName").textContent = account.fullName;
      $("profileUsername").textContent = "@" + account.username;
      $("profileEmail").textContent = account.email;
      $("avatar").textContent =
        account.fullName.trim().charAt(0).toUpperCase() || "Z";
      showPage("profile");
    }

    $("registerForm").addEventListener("submit", event => {
      event.preventDefault();

      const fullName = $("fullName").value.trim();
      const username = $("username").value.trim();
      const email = $("email").value.trim();
      const password = $("password").value;
      const confirm = $("confirmPassword").value;

      if (password !== confirm) {
        $("registerMessage").textContent = "Şifrələr eyni deyil.";
        return;
      }

      $("registerMessage").textContent =
        "Görünüş hazırdır, lakin real qeydiyyat üçün Firebase bağlantısı lazımdır.";
    });

    $("loginForm").addEventListener("submit", event => {
      event.preventDefault();
      $("loginMessage").textContent =
        "Giriş hələ aktiv deyil. Növbəti mərhələdə Firebase qoşacağıq.";
    });

    $("logout").addEventListener("click", () => {
      showPage("login");
    });
  </script>
</body>
</html>

<!DOCTYPE html>
<html lang="az">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ZQİ | Texniki işlər</title>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  min-height: 100vh;
  font-family: Arial, sans-serif;
  color: white;
  background: #050505;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 22px;
}

.container {
  width: 100%;
  max-width: 480px;
  text-align: center;
}

.logo {
  width: min(100%, 340px);
  border-radius: 18px;
  margin-bottom: 24px;
}

.brand {
  color: #e8c66a;
  font-size: 13px;
  font-weight: bold;
  letter-spacing: 3px;
  margin-bottom: 12px;
}

h1 {
  font-size: clamp(27px, 7vw, 38px);
  margin-bottom: 15px;
}

h1 span {
  color: #e8c66a;
}

.description {
  color: #c0c0c0;
  line-height: 1.8;
  font-size: 15px;
  margin-bottom: 23px;
}

.status {
  border: 1px solid #735c28;
  background: linear-gradient(135deg, #19150b, #100e09);
  border-radius: 16px;
  padding: 19px;
  margin-bottom: 20px;
}

.status-icon {
  font-size: 35px;
  margin-bottom: 10px;
}

.status h2 {
  color: #f0ce73;
  font-size: 19px;
  margin-bottom: 9px;
}

.status p {
  color: #c9c2b0;
  font-size: 13px;
  line-height: 1.7;
}

.profile {
  border: 1px solid #393020;
  background: #101010;
  border-radius: 16px;
  padding: 19px;
  margin-bottom: 18px;
}

.profile h3 {
  color: #f0ce73;
  margin-bottom: 14px;
}

.profile input {
  display: block;
  width: 100%;
  padding: 13px;
  margin-bottom: 11px;
  border: 1px solid #51452a;
  border-radius: 10px;
  background: #080808;
  color: white;
  font-size: 14px;
}

button, .contact {
  display: block;
  width: 100%;
  padding: 14px;
  border: 1px solid #d2ad4d;
  border-radius: 11px;
  background: linear-gradient(135deg, #f2d67e, #b88b2c);
  color: #090909;
  font-weight: bold;
  font-size: 14px;
  text-decoration: none;
  cursor: pointer;
}

.contact {
  margin-top: 10px;
}

.profile-info {
  display: none;
  color: #ddd;
  line-height: 1.8;
  overflow-wrap: anywhere;
}

footer {
  color: #777;
  font-size: 12px;
  line-height: 1.8;
  margin-top: 25px;
}

footer strong {
  color: #d8b85e;
}

</style>
</head>

<body>

<div class="container">

  <!-- LOQONU ƏVVƏLCƏ GITHUB-A YÜKLƏ VƏ URL-İ DƏYİŞ -->
  <img
    class="logo"
    src="zqi-logo.jpg"
    alt="ZQİ — Zogadiunarebi Qəbul İmtahanı loqosu"
  >

  <div class="brand">ZQİ • TƏHSİL PLATFORMASI</div>

  <h1>Texniki <span>işlər</span> gedir</h1>

  <p class="description">
    Zogadiunarebi Qəbul İmtahanı platformasında
    yenilənmə işləri aparılır. Komandamız saytın
    daha rahat və keyfiyyətli olması üçün çalışır.
  </p>

  <section class="status">
    <div class="status-icon">⚙️</div>
    <h2>Sayt müvəqqəti bağlıdır</h2>
    <p>
      Admin texniki işləri tamamladıqdan sonra saytı
      yenidən aktiv vəziyyətə gətirəcək.
      Dəqiq açılış vaxtı hələ müəyyən edilməyib.
    </p>
  </section>

  <section class="profile">
    <h3>👤 İstifadəçi profili</h3>

    <div id="profileForm">
      <input
        id="username"
        type="text"
        maxlength="30"
        placeholder="Adını daxil et"
      >

      <button onclick="showProfile()">
        Profilə daxil ol
      </button>
    </div>

    <div id="profileInfo" class="profile-info">
      <p>İstifadəçi: <strong id="showName"></strong></p>
      <p>Status: Texniki fasilə</p>
      <button onclick="logout()" style="margin-top:12px">
        Çıxış
      </button>
    </div>
  </section>

  <a class="contact" href="tel:+995555936547">
    ☎ Əlaqə: +995 555 93 65 47
  </a>

  <footer>
    Zogadiunarebi Qəbul İmtahanı<br>
    <strong>Hazırladı: Haldun Məmmədov</strong><br>
    © 2026 ZQİ — Bütün hüquqlar qorunur.
  </footer>

</div>

<script>
function showProfile() {
  const name = document.getElementById("username")
    .value.trim();

  if (name.length < 2) {
    alert("Zəhmət olmasa adını daxil et.");
    return;
  }

  document.getElementById("showName").textContent = name;
  document.getElementById("profileForm").style.display = "none";
  document.getElementById("profileInfo").style.display = "block";

  try {
    localStorage.setItem("zqiVisitorName", name);
  } catch (e) {}
}

function logout() {
  document.getElementById("profileForm").style.display = "block";
  document.getElementById("profileInfo").style.display = "none";
}

try {
  const savedName = localStorage.getItem("zqiVisitorName");

  if (savedName) {
    document.getElementById("username").value = savedName;
  }
} catch (e) {}
</script>

</body>
</html>

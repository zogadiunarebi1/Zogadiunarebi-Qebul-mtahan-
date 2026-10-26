<!DOCTYPE html>
<html lang="az">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>ZQİ — Qəbul İmtahanı</title>
<style>
:root{--bg:#080808;--panel:#141414;--gold:#e8c66a;--line:#514122;--muted:#bbb}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:#fff;font-family:Arial,sans-serif}
header,main,footer{max-width:1100px;margin:auto;padding:18px}
header{display:flex;align-items:center;justify-content:space-between;gap:12px}
.logo{background:linear-gradient(135deg,#f4dc8b,#a77b22);color:#111;font-size:24px;font-weight:900;padding:15px;border-radius:14px}
h1{font-size:20px}h2{font-size:30px}
button{padding:12px;border:1px solid var(--line);border-radius:10px;background:#211b0e;color:white;font-weight:bold;cursor:pointer}
button.gold{background:linear-gradient(135deg,#f2d982,#b88b2c);color:#111}
input{width:100%;padding:12px;margin:7px 0 12px;background:#090909;border:1px solid var(--line);border-radius:9px;color:white}
nav{display:flex;flex-wrap:wrap;gap:8px;padding:12px}
nav button{flex:1}
.panel,.hero,.card{background:var(--panel);border:1px solid #40341c;border-radius:17px;padding:19px;margin-bottom:15px}
.hero{background:linear-gradient(130deg,#241d0d,#101010);padding:28px}
.goldtext{color:var(--gold)}
.muted{color:var(--muted);line-height:1.6}
.grid{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:12px}
.card p{color:var(--muted);font-size:13px;line-height:1.5}
.card button{width:100%}
.stats{display:grid;grid-template-columns:repeat(3,1fr);gap:9px}
.stat{background:#080808;border:1px solid var(--line);padding:13px;border-radius:10px}
.stat strong{display:block;color:var(--gold);font-size:22px}
.stat span{font-size:12px;color:var(--muted)}
.bar{height:8px;background:#332b1b;border-radius:9px;overflow:hidden;margin:12px 0}
.bar div{height:100%;background:var(--gold);width:0}
.answer{display:block;width:100%;text-align:left;margin:9px 0}
.correct{background:#12402c;border-color:#47d99a}
.wrong{background:#421820;border-color:#ff7185}
.rank{display:flex;justify-content:space-between;gap:12px;padding:12px;border-bottom:1px solid #332b1b}
.hidden{display:none!important}
footer{text-align:center;color:#888;font-size:12px;line-height:1.8}
@media(max-width:650px){.grid{grid-template-columns:repeat(2,minmax(0,1fr))}h1{font-size:15px}.hero{padding:20px}}
@media(max-width:400px){.grid{grid-template-columns:1fr}}
</style>
</head>
<body>

<header>
 <div style="display:flex;align-items:center;gap:12px">
  <div class="logo">ZQİ</div>
  <div><h1>Zogadiunarebi Qəbul İmtahanı</h1><span class="muted">Öyrən • Məşq et • İnkişaf et</span></div>
 </div>
 <b class="goldtext">⚡ <span id="topXP">0</span> XP</b>
</header>

<nav>
 <button onclick="show('home')">🏠 Ana səhifə</button>
 <button onclick="show('subjects')">📚 Fənlər</button>
 <button onclick="daily()">⚡ Quiz</button>
 <button onclick="show('profile')">👤 Profil</button>
 <button onclick="show('leaders')">🏆 Reytinq</button>
 <button onclick="show('admin')">🛠️ Admin</button>
</nav>

<main>
<section id="maintenance" class="hero hidden">
 <h2 class="goldtext">⚙️ Texniki işlər gedir</h2>
 <p class="muted">Zogadiunarebi Qəbul İmtahanı platformasında yenilənmə işləri aparılır. Admin işləri tamamladıqdan sonra saytı yenidən aktiv edəcək.</p>
 <p>Əlaqə: <a class="goldtext" href="tel:+995555936547">+995 555 93 65 47</a></p>
</section>

<section id="home">
 <div class="hero">
  <p class="goldtext">QƏBUL HAZIRLIĞI PLATFORMASI</p>
  <h2>Biliklərini yoxla.<br><span class="goldtext">Hədəfinə yaxınlaş!</span></h2>
  <p class="muted">Testləri həll et, quizlərdə iştirak et, XP qazan və səviyyəni yüksəlt.</p>
  <button class="gold" onclick="daily()">🚀 Quizə başla</button>
  <div class="stats" style="margin-top:20px">
   <div class="stat"><strong id="myXP">0</strong><span>Toplam XP</span></div>
   <div class="stat"><strong id="myLevel">1</strong><span>Səviyyə</span></div>
   <div class="stat"><strong id="myCorrect">0</strong><span>Düzgün cavab</span></div>
  </div>
 </div>
 <div class="panel">
  <h3>🏅 Səviyyə göstəricisi</h3>
  <div class="bar"><div id="xpBar"></div></div>
  <p class="muted" id="levelText">100 XP növbəti səviyyəyə</p>
 </div>
 <div class="panel">
  <h3>🕣 Gündəlik quiz</h3>
  <p class="muted">Planlaşdırılmış vaxt: <b id="quizTimeText">20:30</b>. Quizə aşağıdakı düymə ilə məşq üçün istənilən vaxt başlaya bilərsən.</p>
  <button class="gold" onclick="daily()">Quizə başla</button>
 </div>
 <div class="panel"><h3>📚 Fənlər</h3><div class="grid" id="homeSubjects"></div></div>
</section>

<section id="subjects" class="hidden">
 <div class="panel"><h2>📚 Bütün fənlər</h2><div class="grid" id="allSubjects"></div></div>
</section>

<section id="quiz" class="hidden">
 <div class="panel">
  <button onclick="show('subjects')">← Fənlərə qayıt</button>
  <p class="goldtext" id="subjectName">QUIZ</p>
  <div class="bar"><div id="quizBar"></div></div>
  <div style="display:flex;justify-content:space-between;gap:12px">
   <span id="qNumber" class="muted">Sual 1</span>
   <b class="goldtext">⏱ <span id="timer">60</span></b>
  </div>
  <h2 id="question"></h2>
  <div id="answers"></div>
  <p id="explanation" class="muted"></p>
  <button id="next" class="gold hidden" onclick="nextQuestion()">Növbəti →</button>
 </div>
</section>

<section id="profile" class="hidden">
 <div class="panel">
  <h2>👤 Profil və qeydiyyat</h2>
  <div id="registerArea" class="grid">
   <div class="card"><h3>Qeydiyyat</h3>
    <input id="regName" placeholder="İstifadəçi adı">
    <input id="regEmail" type="email" placeholder="E-poçt">
    <input id="regPass" type="password" placeholder="Şifrə">
    <button class="gold" onclick="register()">Qeydiyyatdan keç</button>
   </div>
   <div class="card"><h3>Hesaba giriş</h3>
    <input id="loginEmail" type="email" placeholder="E-poçt">
    <input id="loginPass" type="password" placeholder="Şifrə">
    <button onclick="login()">Daxil ol</button>
   </div>
  </div>
  <p id="authMessage" class="muted"></p>
  <div id="profileInfo" class="hidden card">
   <div style="font-size:35px">🎓</div>
   <h2 id="profileName"></h2>
   <p id="profileEmail" class="muted"></p>
   <div class="stats">
    <div class="stat"><strong id="profileXP">0</strong><span>XP</span></div>
    <div class="stat"><strong id="profileLevel">1</strong><span>Səviyyə</span></div>
    <div class="stat"><strong id="profileCorrect">0</strong><span>Düzgün cavab</span></div>
   </div>
   <button style="margin-top:14px" onclick="logout()">Çıxış</button>
  </div>
  <p class="muted">Bu ilkin versiyada məlumatlar yalnız bu brauzerdə saxlanılır. Həqiqi hesab təhlükəsizliyi üçün server əsaslı qeydiyyat lazımdır.</p>
 </div>
</section>

<section id="leaders" class="hidden">
 <div class="panel"><h2>🏆 Liderlər cədvəli</h2><div id="leaderboard"></div>
 <p class="muted">Bu demo reytinq yalnız bu brauzerdəki profilləri göstərir; ortaq canlı reytinq deyil.</p></div>
</section>

<section id="admin" class="hidden">
 <div class="panel">
  <h2>🛠️ Admin paneli</h2>
  <p class="muted">Demo parol: <b>ZQI2026</b>. Bu parol təhlükəsiz deyil; ictimai saytda real admin üçün server yoxlaması qurulmalıdır.</p>
  <div id="adminLogin">
   <input id="adminPass" type="password" placeholder="Admin parolu">
   <button class="gold" onclick="adminEnter()">Daxil ol</button>
  </div>
  <div id="adminControls" class="hidden">
   <h3>Saytın vəziyyəti</h3>
   <p id="adminStatus" class="muted"></p>
   <button class="gold" onclick="toggleMaintenance()">Texniki fasiləni dəyiş</button>
   <h3 style="margin-top:25px">Quiz vaxtı</h3>
   <input id="timeSetting" type="time" value="20:30">
   <button onclick="saveTime()">Vaxtı yadda saxla</button>
   <p id="adminMessage" class="muted"></p>
  </div>
 </div>
</section>
</main>

<footer>
 Zogadiunarebi Qəbul İmtahanı<br>
 <strong class="goldtext">Hazırladı: Haldun Məmmədov</strong><br>
 Əlaqə: +995 555 93 65 47
</footer>

<script>
const subjects = {
"Riyaziyyat":[
["12 + 8 = ?",["18","20","22","24"],1,"12 + 8 = 20."],
["−5 + 9 = ?",["−14","−4","4","14"],2,"9 − 5 = 4."],
["7 × 8 = ?",["54","56","64","48"],1,"7 × 8 = 56."],
["144 ÷ 12 = ?",["10","11","12","14"],2,"Cavab 12-dir."],
["3² + 4 = ?",["10","12","13","14"],2,"9 + 4 = 13."],
["200-ün 25%-i?",["25","40","50","75"],2,"200 × 0,25 = 50."],
["x + 7 = 19. x = ?",["10","11","12","13"],2,"19 − 7 = 12."],
["5 sm və 8 sm tərəfli düzbucaqlının sahəsi?",["13","26","40","80"],2,"5 × 8 = 40 sm²."],
["1/2 + 1/4 = ?",["2/6","3/4","1/6","1"],1,"2/4 + 1/4 = 3/4."],
["Üçbucağın bucaqlarının cəmi?",["90°","180°","270°","360°"],1,"180°."]
],
"Məntiq":[
["2, 4, 6, 8, ...",["9","10","11","12"],1,"Hər dəfə 2 artırılır."],
["3, 6, 12, 24, ...",["30","36","42","48"],3,"Hər dəfə 2-yə vurulur."],
["Artıq olanı seç.",["Üçbucaq","Kvadrat","Dairə","Alma"],3,"Alma həndəsi fiqur deyil."],
["Bir saat neçə dəqiqədir?",["30","45","60","100"],2,"60 dəqiqə."],
["1, 4, 9, 16, ...",["20","24","25","36"],2,"5² = 25."],
["Bütün güllər bitkidir. Qızılgül güldür. Nəticə?",["Qızılgül bitkidir","Bütün bitkilər güldür","Qızılgül heyvandır","Nəticə yoxdur"],0,"Qızılgül bitkidir."],
["Bazar ertəsindən 3 gün sonra?",["Çərşənbə axşamı","Çərşənbə","Cümə axşamı","Cümə"],2,"Cümə axşamı."],
["5 qələm 10 manatdır. 2 qələm?",["2","4","5","8"],1,"Bir qələm 2 manatdır."],
["Hansı ədəd cütdür?",["13","17","21","28"],3,"28 cütdür."],
["20, 17, 14, 11, ...",["9","8","7","6"],1,"Hər dəfə 3 çıxılır."]
],
"Azərbaycan dili":[
["İsim hansı suala cavab verir?",["Necə?","Nə edir?","Kim? nə?","Neçə?"],2,"İsim əşyanın adını bildirir."],
["“Gözəl” hansı nitq hissəsidir?",["İsim","Sifət","Feil","Say"],1,"Sifət əlamət bildirir."],
["“Qaçır” hansı nitq hissəsidir?",["Feil","Əvəzlik","Zərf","İsim"],0,"Feil hərəkət bildirir."],
["“Kitablar” sözündə cəm şəkilçisi?",["-çı","-lıq","-lar","-dan"],2,"-lar cəm şəkilçisidir."],
["Düzgün yazılışı seç.",["Məktəb","Məktəp","Məgtəb","Məktəbb"],0,"Düzgün yazılış məktəbdir."],
["“Sürətlə qaçdı” ifadəsində sürətlə?",["İsim","Sifət","Zərf","Say"],2,"Zərf hərəkətin tərzini bildirir."],
["Sual cümləsinin işarəsi?",["Nöqtə","Vergül","Sual işarəsi","İki nöqtə"],2,"Sual işarəsi."],
["“Mən məktəbə gedirəm.” Mübtəda?",["Məktəbə","Gedirəm","Mən","Məktəb"],2,"Mübtəda mən sözüdür."],
["Hansı söz əvəzlikdir?",["Mən","Masa","Yaşıl","Oxumaq"],0,"Mən şəxs əvəzliyidir."],
["“Ağıllı” sözünün əksi?",["Zəkalı","Düşüncəli","Ağılsız","Çalışqan"],2,"Ağılsız."]
],
"Tarix":[
["Azərbaycan Xalq Cümhuriyyəti nə vaxt elan olunub?",["28 may 1914","28 may 1918","28 may 1920","18 oktyabr 1991"],1,"28 may 1918."],
["Müstəqilliyin bərpası aktı nə vaxt qəbul edilib?",["28 may 1918","18 oktyabr 1991","9 may 1945","20 yanvar 1990"],1,"18 oktyabr 1991."],
["İkinci Dünya müharibəsi?",["1914–1918","1939–1945","1945–1950","1929–1933"],1,"1939–1945."],
["Qədim Misir hansı çayın vadisində yaranıb?",["Amazon","Nil","Dunay","Volqa"],1,"Nil çayı."],
["İpək yolu nə üçün əhəmiyyətli idi?",["Yalnız müharibə","Ticarət və mədəni əlaqələr","Əkinçilik","Hava müşahidəsi"],1,"Ticarət və mədəni mübadilə."],
["Bakı hansı dənizin sahilindədir?",["Qara","Aralıq","Xəzər","Baltik"],2,"Xəzər dənizi."],
["Azərbaycan müstəqilliyini hansı ildə bərpa edib?",["1988","1990","1991","1995"],2,"1991-ci ildə."],
["Qalalar əsasən nə üçün tikilirdi?",["Müdafiə","Səyahət","Saat ölçmək","Əkinçilik"],0,"Müdafiə üçün."],
["Tarixi mənbəyə nümunə?",["Qədim yazılı sənəd","Hava proqnozu","Təxmin","Düstur"],0,"Qədim yazılı sənəd."],
["Arxeologiya nəyi öyrənir?",["Göy cisimləri","Maddi qalıqlar","İrsiyyət","Atmosfer"],1,"Keçmiş cəmiyyətlərin maddi qalıqları."]
],
"Coğrafiya":[
["Ən böyük okean?",["Atlantik","Hind","Sakit","Şimal Buzlu"],2,"Sakit okean."],
["Azərbaycanın paytaxtı?",["Gəncə","Şəki","Bakı","Lənkəran"],2,"Bakı."],
["Yerin təbii peyki?",["Mars","Ay","Günəş","Venera"],1,"Ay."],
["Xəritədə şimal adətən harada göstərilir?",["Aşağı","Yuxarı","Sağ","Sol"],1,"Yuxarıda."],
["Ekvator hansı yarımkürələri ayırır?",["Şərq-qərb","Şimal-cənub","Quru-su","Dağ-düzən"],1,"Şimal və cənub."],
["Ən böyük qitə?",["Afrika","Avropa","Asiya","Avstraliya"],2,"Asiya."],
["Xəzər hansı tip su hövzəsidir?",["Okean","Qapalı daxili hövzə","Çay","Buzlaq"],1,"Qapalı daxili su hövzəsi."],
["Vulkanın səthə çıxardığı ərimiş süxur?",["Lava","Qar","Su","Oksigen"],0,"Lava."],
["Atmosfer nədir?",["Su qatı","Yeri əhatə edən qaz qatı","Nüvə","Bitki örtüyü"],1,"Qaz qatı."],
["Kompas nəyi müəyyən edir?",["Temperatur","İstiqamət","Kütlə","Vaxt"],1,"İstiqamət."]
],
"Biologiya":[
["Fotosintez hansı orqanoiddə gedir?",["Nüvə","Xloroplast","Mitoxondri","Ribosom"],1,"Xloroplast."],
["Qanı dövr etdirən orqan?",["Ağciyər","Mədə","Ürək","Qaraciyər"],2,"Ürək."],
["Nəfəsalma üçün vacib qaz?",["Karbon qazı","Oksigen","Helium","Hidrogen"],1,"Oksigen."],
["Bitki suyu əsasən hansı orqanla alır?",["Çiçək","Yarpaq","Kök","Meyvə"],2,"Kök."],
["İrsiyyət məlumatını daşıyan molekul?",["DNT","Su","Qlükoza","Yağ"],0,"DNT."],
["Yetkin insanın skeletində təxminən neçə sümük var?",["106","206","306","406"],1,"Adətən 206."],
["Hansı canlı məməlidir?",["Qurbağa","Kəpənək","Delfin","Alabalıq"],2,"Delfin."],
["Qida zəncirində bitkilər?",["İstehsalçı","Parçalayıcı","İstehlakçı","Yırtıcı"],0,"İstehsalçıdır."],
["İnsanda həzm harada başlayır?",["Mədə","Ağız boşluğu","Nazik bağırsaq","Qaraciyər"],1,"Ağız boşluğunda."],
["Ekosistem nəyi əhatə edir?",["Yalnız heyvanlar","Canlılar və cansız mühit","Yalnız bitkilər","Yalnız torpaq"],1,"Canlılar və cansız mühit."]
],
"Fizika":[
["Qüvvənin SI vahidi?",["Coul","Nyuton","Vatt","Paskal"],1,"Nyuton."],
["Orta sürət necə hesablanır?",["Zaman/yol","Yol/zaman","Kütlə×həcm","Qüvvə/temperatur"],1,"Yol bölünsün zamana."],
["Normal təzyiqdə su neçə °C-də qaynayır?",["0","50","100","150"],2,"Təxminən 100°C."],
["Cərəyan şiddətinin vahidi?",["Amper","Volt","Om","Vatt"],0,"Amper."],
["İşığın vakuumdakı sürəti?",["300 km/s","3 000 km/s","300 000 km/s","30 km/s"],2,"Təxminən 300 000 km/s."],
["Enerjinin SI vahidi?",["Nyuton","Coul","Amper","Metr"],1,"Coul."],
["Cisimlərin Yerə düşməsinə nə səbəb olur?",["Sürtünmə","Cazibə","Elektrik","Elastiklik"],1,"Cazibə."],
["Səs vakuumda yayıla bilər?",["Bəli","Xeyr, maddi mühit lazımdır","Yalnız gecə","Yalnız istidə"],1,"Səs maddi mühit tələb edir."],
["Gərginliyin vahidi?",["Volt","Amper","Om","Coul"],0,"Volt."],
["Sıxlıq düsturu?",["Kütlə/həcm","Həcm/zaman","Yol×zaman","Qüvvə×məsafə"],0,"Sıxlıq = kütlə/həcm."]
],
"Kimya":[
["Suyun formulu?",["CO₂","H₂O","O₂","NaCl"],1,"H₂O."],
["Oksigenin işarəsi?",["Ox","O","Og","Om"],1,"O."],
["25°C-də pH 7 olan məhlul?",["Turş","Qələvi","Neytral","Duzlu"],2,"Neytral."],
["Mətbəx duzunun formulu?",["NaCl","HCl","KOH","CO₂"],0,"NaCl."],
["Atom nüvəsində hansı hissəciklər var?",["Yalnız elektron","Proton və neytron","Foton","Molekul"],1,"Protonlar və neytronlar; hidrogen-1 istisnadır."],
["Dövri cədvəl hansı ardıcıllığa əsaslanır?",["Rəng","Atom nömrəsi","Qaynama adı","Ölkə"],1,"Atom nömrəsi."],
["Karbon qazının formulu?",["CO","CO₂","CaO","C₂O"],1,"CO₂."],
["Katalizator nə edir?",["Həmişə məhsul olur","Reaksiya sürətinə təsir edir","Atomları yox edir","Kütlə yaradır"],1,"Reaksiyanın sürətini dəyişir."],
["Dəmirin işarəsi?",["Ir","Fe","F","D"],1,"Fe."],
["Buzun əriməsi hansı dəyişiklikdir?",["Kimyəvi","Fiziki","Nüvə","Dəyişiklik deyil"],1,"Fiziki dəyişiklik."]
],
"İnformatika":[
["Mərkəzi emal qurğusu?",["CPU","URL","USB","PDF"],0,"CPU."],
["İkilik say sistemində hansı rəqəmlər var?",["0 və 1","1 və 2","0–9","A və B"],0,"0 və 1."],
["1 bayt neçə bitdir?",["2","4","8","16"],2,"8 bit."],
["Veb səhifə strukturu üçün dil?",["HTML","SQL","C++","PNG"],0,"HTML."],
["Güclü şifrə necə olmalıdır?",["123456","Ad və doğum ili","Uzun və unikal","Hər yerdə eyni"],2,"Uzun və unikal şifrə."],
["Əməliyyat sistemi nə edir?",["Şəkil çəkir","Resursları idarə edir","Yalnız internet verir","Yalnız mətn yazır"],1,"Kompüter resurslarını idarə edir."],
["Elektron cədvəldə sətir-sütun kəsişməsi?",["Fayl","Xana","Qovluq","Slayd"],1,"Xana."],
["URL nəyi göstərir?",["Veb ünvanı","Temperatur","Şifrə uzunluğu","Ekran ölçüsü"],0,"Veb resursun ünvanı."],
["Uzunmüddətli saxlama qurğuları?",["Yalnız RAM","SSD və HDD","Prosessor","Klaviatura"],1,"SSD və HDD."],
["Fişinq nədir?",["Kompüteri təmizləmək","Aldadaraq məxfi məlumatı almaq","Fayl sıxışdırmaq","Ekran parlaqlığı"],1,"Məlumat oğurlama cəhdi."]
],
"İngilis dili":[
["“Book” sözünün mənası?",["Qələm","Kitab","Masa","Məktəb"],1,"Book — kitab."],
["She ___ a student.",["am","are","is","be"],2,"She is."],
["Child sözünün cəmi?",["childs","children","childes","childrens"],1,"Children."],
["Good sözünün əksi?",["Nice","Best","Bad","Fine"],2,"Bad."],
["Düzgün cümlə hansıdır?",["He go to school.","He goes to school.","He going school.","He gone to school."],1,"He goes to school."],
["Yesterday hansı zamanı bildirir?",["Gələcək","Keçmiş","İndiki davam edən","Əmr"],1,"Keçmiş."],
["I have two ___.",["book","books","bookes","booking"],1,"Books."],
["Where nəyi soruşur?",["Vaxt","Yer","Səbəb","Miqdar"],1,"Harada/hara."],
["___ apple",["a","an","thee","always no article"],1,"An apple."],
["They are playing hansı zamandır?",["Present Simple","Past Simple","Present Continuous","Future Simple"],2,"Present Continuous."]
]
};

let xp=Number(localStorage.getItem("zqiXP")||0);
let correct=Number(localStorage.getItem("zqiCorrect")||0);
let users=JSON.parse(localStorage.getItem("zqiUsers")||"{}");
let active=localStorage.getItem("zqiActive")||"";
let maintenance=localStorage.getItem("zqiMaintenance")==="true";
let quizTime=localStorage.getItem("zqiTime")||"20:30";
let current=[],index=0,earned=0,answered=false,timerId=null,seconds=60;

function saveProgress(){
 localStorage.setItem("zqiXP",xp);
 localStorage.setItem("zqiCorrect",correct);
 if(active&&users[active]){users[active].xp=xp;users[active].correct=correct;localStorage.setItem("zqiUsers",JSON.stringify(users))}
 update();
}
function update(){
 let level=Math.floor(xp/100)+1;
 document.getElementById("topXP").textContent=xp;
 document.getElementById("myXP").textContent=xp;
 document.getElementById("myLevel").textContent=level;
 document.getElementById("myCorrect").textContent=correct;
 document.getElementById("xpBar").style.width=(xp%100)+"%";
 document.getElementById("levelText").textContent=(100-xp%100)+" XP növbəti səviyyəyə";
 document.getElementById("quizTimeText").textContent=quizTime;
 document.getElementById("maintenance").classList.toggle("hidden",!maintenance);
 document.querySelectorAll("nav button").forEach(b=>b.disabled=maintenance);
 document.querySelectorAll("main > section").forEach(s=>{if(s.id!=="maintenance")s.classList.toggle("hidden",maintenance||!s.classList.contains("selected"))});
 renderProfile();renderLeaders();
}
function show(id){
 clearInterval(timerId);
 document.querySelectorAll("main > section").forEach(s=>{s.classList.remove("selected");if(s.id!== "maintenance")s.classList.add("hidden")});
 document.getElementById(id).classList.remove("hidden");
 document.getElementById(id).classList.add("selected");
 if(maintenance&&id!=="admin")return;
 window.scrollTo({top:0,behavior:"smooth"});
}
function buildSubjects(target){
 document.getElementById(target).innerHTML=Object.keys(subjects).map(s=>`
 <div class="card"><div style="font-size:25px">📘</div><h3>${s}</h3>
 <p>10 sual • Düzgün cavab +10 XP</p>
 <button class="gold" onclick="startSubject('${s}')">Testə başla →</button></div>`).join("");
}
function daily(){current=Object.entries(subjects).flatMap(([subject,qs])=>qs.map(q=>({subject,q:q[0],a:q[1],c:q[2],e:q[3]}))).sort(()=>Math.random()-.5).slice(0,10);begin("Gündəlik quiz")}
function startSubject(s){current=subjects[s].map(q=>({subject:s,q:q[0],a:q[1],c:q[2],e:q[3]}));begin(s)}
function begin(name){index=0;earned=0;show("quiz");document.getElementById("subjectName").textContent=name;nextQuestionDisplay()}
function nextQuestionDisplay(){
 clearInterval(timerId);answered=false;seconds=60;
 let q=current[index];
 document.getElementById("qNumber").textContent=`Sual ${index+1}/${curren
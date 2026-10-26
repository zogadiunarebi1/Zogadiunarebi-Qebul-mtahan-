
<!doctype html>
<html lang="az">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>ZQİ Quiz</title>
<style>
:root{--g:#e8c45e;--p:#151720;--l:#30333e;--m:#a4a8b4}
*{box-sizing:border-box}
body{margin:0;background:radial-gradient(ellipse at top,#282216,#090a0e 60%);color:#fafafa;font:16px system-ui}
.wrap{max-width:780px;margin:auto;padding:18px 13px 40px}
header{display:flex;gap:12px;align-items:center;margin:10px 0 22px}
.logo{border:2px solid var(--g);color:var(--g);font-weight:1000;font-size:23px;border-radius:15px;padding:13px 9px}
h1{font-size:clamp(21px,5vw,31px);margin:0}
h2{font-size:19px;margin:0 0 14px}
.muted,.note{color:var(--m);font-size:13px;line-height:1.5}
.panel{background:var(--p);border:1px solid var(--l);border-radius:17px;padding:17px;margin:13px 0}
.pill{color:var(--g);font-size:12px;margin-top:6px}
label{display:block;font-size:13px;margin:8px 0}
input{width:100%;padding:13px;border-radius:10px;background:#090a0e;border:1px solid var(--l);color:white;font-size:16px}
button{border:0;border-radius:11px;padding:13px;font-size:15px;font-weight:800;cursor:pointer}
button:disabled{opacity:.45}
.primary{background:linear-gradient(90deg,#d8ad42,#ffe59a);color:#17130a}
.secondary{background:#292c36;color:white;border:1px solid #454956}
.full{width:100%;margin-top:12px}
.hidden{display:none!important}
.stats{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}
.stat{text-align:center;background:#0b0c11;border:1px solid var(--l);border-radius:12px;padding:10px}
.stat b{display:block;color:#ffe49a;font-size:21px}
.stat span{font-size:11px;color:var(--m)}
.timerbar{height:7px;background:#343640;border-radius:9px;margin:13px 0;overflow:hidden}
.fill{height:100%;background:var(--g);width:100%}
.meta{display:flex;justify-content:space-between;color:var(--m);font-size:13px}
.question{font-size:clamp(20px,4vw,26px);font-weight:800;margin:18px 0}
.answers{display:grid;gap:9px}
.answer{width:100%;text-align:left;display:flex;gap:10px;align-items:center;background:#0b0c11;color:white;border:1px solid #383b47}
.answer.sel{border-color:var(--g);background:#2a2415}
.answer.correct{border-color:#40d69a}
.answer.wrong{border-color:#ff6577}
.letter{background:#282b35;padding:5px 9px;border-radius:7px;color:#ffe49a}
table{width:100%;border-collapse:collapse}
td,th{text-align:left;border-bottom:1px solid #30333d;padding:10px 5px;font-size:13px}
th{color:var(--m)}
.rank{color:#ffe49a;font-weight:900}
.people{display:flex;gap:7px;flex-wrap:wrap}
.person{border:1px solid #383b47;background:#0b0c11;border-radius:30px;padding:8px 10px;font-size:12px}
footer{text-align:center;color:#818694;font-size:12px;margin-top:22px}
footer b{color:#ffe49a}
</style>
</head>
<body>
<div class="wrap">
<header>
<div class="logo">ZQİ</div>
<div>
<h1>Zogadiunarebi Qəbul İmtahanı</h1>
<div class="muted">Riyaziyyat • Sürətli quiz</div>
<div class="pill">⏱ Hər suala 60 saniyə</div>
</div>
</header>

<section class="panel" id="join">
<h2>Quizə qoşul</h2>
<label for="name">Adın və ya istifadəçi adın</label>
<input id="name" maxlength="24" placeholder="Məsələn: Haldun">
<button class="primary full" id="start">İştirak et və başla</button>
<p class="note">10 sual • Cavabını seç və “Cavabı göndər” düyməsinə bas.</p>
</section>

<section class="panel hidden" id="quiz">
<div class="stats">
<div class="stat"><b id="count">1/10</b><span>Sual</span></div>
<div class="stat"><b id="time">60</b><span>Saniyə</span></div>
<div class="stat"><b id="score">0</b><span>Xal</span></div>
</div>
<div class="timerbar"><div class="fill" id="fill"></div></div>
<div class="meta"><span>Riyaziyyat</span><span id="picked">Cavab seçilməyib</span></div>
<div class="question" id="q"></div>
<div class="answers" id="answers"></div>
<button class="primary full" id="send" disabled>Cavabı göndər</button>
<button class="secondary full hidden" id="next">Növbəti sual</button>
<p class="note" id="feedback"></p>
</section>

<section class="panel hidden" id="result">
<h2>Quiz tamamlandı!</h2>
<div class="stats">
<div class="stat"><b id="finalScore">0</b><span>Xal</span></div>
<div class="stat"><b id="finalCorrect">0/10</b><span>Düzgün cavab</span></div>
<div class="stat"><b id="finalTime">0</b><span>Sərf olunan saniyə</span></div>
</div>
<button class="primary full" id="again">Yenidən başla</button>
</section>

<section class="panel">
<h2>🏆 Liderlik cədvəli</h2>
<p class="note">Bu versiyada nəticələr yalnız həmin brauzerdə saxlanılır. Ortaq liderlik cədvəli üçün Firebase lazımdır.</p>
<div style="overflow:auto">
<table>
<thead><tr><th>Yer</th><th>İştirakçı</th><th>Düzgün</th><th>Xal</th></tr></thead>
<tbody id="leaders"><tr><td colspan="4" class="note">Hələ nəticə yoxdur.</td></tr></tbody>
</table>
</div>
</section>

<section class="panel">
<h2>👥 İştirak edənlər</h2>
<div class="people" id="people"><span class="note">Hələ iştirakçı yoxdur.</span></div>
</section>

<footer>Hazırladı: <b>Haldun Məmmədov</b> • ZQİ</footer>
</div>

<script>
const qs=[
["12 + 8 = ?",["18","20","22","24"],1,"12 + 8 = 20."],
["−5 + 9 = ?",["−14","−4","4","14"],2,"−5 + 9 = 4."],
["|x − 2| + 1 = 9 tənliyinin həlləri hansıdır?",["x = 10 və ya x = −6","x = 8 və ya x = −8","x = 6 və ya x = −10","Yalnız x = 10"],0,"|x−2|=8. Deməli x=10 və ya x=−6."],
["21 − |x + 7| = 5 tənliyinin həlləri hansıdır?",["x = 9 və ya x = −23","x = 16 və ya x = −16","x = 5 və ya x = −5","Yalnız x = 9"],0,"|x+7|=16. Buna görə x=9 və ya x=−23."],
["|7 − x| = 5 tənliyinin həlləri hansıdır?",["x = 2 və ya x = 12","x = −2 və ya x = 5","x = 7 və ya x = 5","Yalnız x = 2"],0,"x=2 və ya x=12."],
["|2x + 1| = 13 tənliyinin həlləri hansıdır?",["x = 6 və ya x = −7","x = 7 və ya x = −6","x = 5 və ya x = −5","Yalnız x = 6"],0,"x=6 və ya x=−7."],
["2|x| = 10 olarsa, x hansı qiymətləri alır?",["−5 və 5","−10 və 10","Yalnız 5","−5 və 10"],0,"x=−5 və ya x=5."],
["3|x| = 12 olarsa, x hansı qiymətləri alır?",["−4 və 4","−12 və 12","Yalnız 4","−3 və 3"],0,"x=−4 və ya x=4."],
["|x| − 1 = 3 tənliyinin həlləri hansıdır?",["−4 və 4","−2 və 2","Yalnız 4","−3 və 3"],0,"x=−4 və ya x=4."],
["7 − |x| = 5 tənliyinin həlləri hansıdır?",["−2 və 2","−5 və 5","Yalnız 2","−7 və 7"],0,"x=−2 və ya x=2."]
];

let name="",i=0,sel=null,score=0,correct=0,left=60,elapsed=0,locked=false,timer;
const $=id=>document.getElementById(id);

function read(k){
 try{return JSON.parse(localStorage.getItem(k)||"[]")}
 catch(e){return []}
}
function write(k,v){
 localStorage.setItem(k,JSON.stringify(v))
}
function esc(s){
 return String(s).replace(/[&<>"']/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]))
}
function tables(){
 let r=read("zqiQuizResults");
 r.sort((a,b)=>b.score-a.score||b.correct-a.correct||a.elapsed-b.elapsed);
 $("leaders").innerHTML=r.length?r.slice(0,30).map((x,j)=>
 `<tr><td class="rank">${["🥇","🥈","🥉"][j]||j+1}</td><td>${esc(x.name)}</td><td>${x.correct}/10</td><td><b>${x.score}</b></td></tr>`
 ).join(""):'<tr><td colspan="4" class="note">Hələ nəticə yoxdur.</td></tr>';
 let p=read("zqiQuizPeople");
 $("people").innerHTML=p.length?p.map(x=>`<span class="person">👤 ${esc(x)}</span>`).join(""):'<span class="note">Hələ iştirakçı yoxdur.</span>';
}
function start(){
 name=$("name").value.trim();
 if(!name){alert("Əvvəl adını yaz.");return}
 let p=read("zqiQuizPeople");
 if(!p.includes(name)){p.push(name);write("zqiQuizPeople",p)}
 i=0;score=0;correct=0;elapsed=0;
 $("join").classList.add("hidden");
 $("result").classList.add("hidden");
 $("quiz").classList.remove("hidden");
 show();tables();
}
function show(){
 clearInterval(timer);
 sel=null;locked=false;left=60;
 $("count").textContent=`${i+1}/10`;
 $("time").textContent=60;
 $("score").textContent=score;
 $("fill").style.width="100%";
 $("picked").textContent="Cavab seçilməyib";
 $("feedback").textContent="";
 $("send").disabled=true;
 $("send").classList.remove("hidden");
 $("next").classList.add("hidden");
 $("q").textContent=qs[i][0];
 $("answers").innerHTML=qs[i][1].map((a,j)=>
 `<button class="answer" data-n="${j}"><span class="letter">${"ABCD"[j]}</span>${a}</button>`
 ).join("");
 document.querySelectorAll(".answer").forEach(b=>b.onclick=()=>{
  if(locked)return;
  sel=+b.dataset.n;
  document.querySelectorAll(".answer").forEach(x=>x.classList.toggle("sel",x===b));
  $("send").disabled=false;
  $("picked").textContent="Cavab seçildi";
 });
 timer=setInterval(()=>{
  left--;elapsed++;
  $("time").textContent=left;
  $("fill").style.width=left/60*100+"%";
  if(left<=0){clearInterval(timer);submit(true)}
 },1000);
}
function submit(timeout=false){
 if(locked||(!timeout&&sel===null))return;
 locked=true;clearInterval(timer);
 let q=qs[i],ok=sel===q[2];
 if(ok){correct++;score+=10+Math.max(0,left)}
 document.querySelectorAll(".answer").forEach((b,j)=>{
  b.disabled=true;
  if(j===q[2])b.classList.add("correct");
  else if(j===sel)b.classList.add("wrong");
 });
 $("feedback").textContent=(timeout?"Vaxt bitdi. ":ok?"Düzgün cavab! ":"Düzgün cavab deyil. ")+q[3];
 $("score").textContent=score;
 $("send").classList.add("hidden");
 $("next").classList.remove("hidden");
 $("next").textContent=i===9?"Nəticəni göstər":"Növbəti sual";
}
function next(){
 if(!locked)return;
 if(i<9){i++;show()}
 else finish();
}
function finish(){
 clearInterval(timer);
 $("quiz").classList.add("hidden");
 $("result").classList.remove("hidden");
 $("finalScore").textContent=score;
 $("finalCorrect").textContent=correct+"/10";
 $("finalTime").textContent=elapsed;
 let r=read("zqiQuizResults");
 let n=r.findIndex(x=>x.name.toLowerCase()===name.toLowerCase());
 let obj={name,score,correct,elapsed};
 if(n<0)r.push(obj);
 else if(score>r[n].score)r[n]=obj;
 write("zqiQuizResults",r);
 tables();
}
$("start").onclick=start;
$("send").onclick=()=>submit();
$("next").onclick=next;
$("again").onclick=()=>{
 $("result").classList.add("hidden");
 $("join").classList.remove("hidden");
 $("name").value=name;
};
tables();
</script>
</body>
</html>

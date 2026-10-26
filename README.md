
<!doctype html>
<html lang="az">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>ZQİ — Böyük Quiz</title>
<style>
*{box-sizing:border-box}body{margin:0;background:#0b0b10;color:#fff;font:16px Arial,sans-serif}
main{max-width:720px;margin:auto;padding:16px}
header,.card{background:#17171f;border:1px solid #38323a;border-radius:16px;padding:17px;margin-bottom:14px}
header{display:flex;align-items:center;gap:13px}
.logo{background:#080808;color:#e9c65d;border:2px solid #e9c65d;border-radius:12px;padding:12px;font-size:23px;font-weight:bold}
h1{font-size:21px;margin:0 0 5px}h2{font-size:19px;color:#f2d57c}
.small{color:#b9bac4;font-size:13px;line-height:1.6}
input{width:100%;padding:13px;background:#0b0b10;border:1px solid #444;color:white;border-radius:9px;font-size:16px}
button{padding:13px;border:0;border-radius:10px;font-size:15px;font-weight:bold;cursor:pointer}
.gold{background:#edcc68;color:#15120a}.dark{background:#30303b;color:white}
.full{width:100%;margin-top:12px}.hidden{display:none!important}
.question{font-size:23px;font-weight:bold;line-height:1.5;margin:22px 0}
.answers{display:grid;gap:9px}.ans{background:#0d0d13;color:white;border:1px solid #444;text-align:left}
.ans.selected{border:2px solid #edcc68}.ans.right{border:2px solid #35d39a}.ans.wrong{border:2px solid #ff6476}
.stats{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}
.stat{text-align:center;background:#0c0c12;padding:12px;border-radius:10px}
.stat b{display:block;color:#edcc68;font-size:22px}.stat span{font-size:11px;color:#b9bac4}
.bar{height:7px;background:#444;margin:13px 0;border-radius:8px;overflow:hidden}.fill{height:100%;background:#edcc68}
table{width:100%;border-collapse:collapse}td,th{padding:10px 4px;border-bottom:1px solid #383842;text-align:left;font-size:13px}
th{color:#c9c9d0}.goldtext{color:#edcc68;font-weight:bold}
.people{display:flex;gap:7px;flex-wrap:wrap}.person{background:#0b0b10;border:1px solid #444;border-radius:25px;padding:8px;font-size:12px}
footer{text-align:center;color:#aaa;font-size:12px;padding:15px}footer b{color:#edcc68}
</style>
</head>
<body>
<main>
<header>
 <div class="logo">ZQİ</div>
 <div><h1>Zogadiunarebi Qəbul İmtahanı</h1>
 <div class="small">Xüsusi Riyaziyyat Quizı</div>
 <div style="color:#edcc68;font-size:12px;margin-top:6px">10 sual · hər suala 60 saniyə</div></div>
</header>

<section class="card" id="waiting">
<h2>⏳ Quizə geri sayım</h2>
<div class="stats">
 <div class="stat"><b id="hh">--</b><span>Saat</span></div>
 <div class="stat"><b id="mm">--</b><span>Dəqiqə</span></div>
 <div class="stat"><b id="ss">--</b><span>Saniyə</span></div>
</div>
<p id="status" class="small">Quiz Gürcüstan vaxtı ilə saat 20:40-da başlayacaq.</p>
<label for="player">İştirakçı adı</label>
<input id="player" maxlength="24" placeholder="Adını yaz">
<p class="small">Adını əvvəlcədən yaz. Başlanma vaxtında quiz avtomatik açılacaq.</p>
</section>

<section class="card hidden" id="quiz">
<div class="stats">
<div class="stat"><b id="number">1/10</b><span>Sual</span></div>
<div class="stat"><b id="timer">60</b><span>Saniyə</span></div>
<div class="stat"><b id="points">0</b><span>Xal</span></div>
</div>
<div class="bar"><div class="fill" id="fill"></div></div>
<div class="small" id="subject">Riyaziyyat</div>
<div class="question" id="question"></div>
<div class="answers" id="answers"></div>
<button class="gold full" id="send" disabled>Cavabı göndər</button>
<button class="dark full hidden" id="next">Növbəti sual</button>
<p class="small" id="feedback"></p>
</section>

<section class="card hidden" id="result">
<h2>🏁 Quiz bitdi!</h2>
<div class="stats">
<div class="stat"><b id="finalPoints">0</b><span>Xal</span></div>
<div class="stat"><b id="finalCorrect">0/10</b><span>Düzgün cavab</span></div>
<div class="stat"><b id="finalTime">0</b><span>Saniyə</span></div>
</div>
<button class="dark full" onclick="location.reload()">Nəticəni yenilə</button>
</section>

<section class="card">
<h2>🏆 Liderlik cədvəli</h2>
<div style="overflow:auto"><table>
<thead><tr><th>Yer</th><th>İştirakçı</th><th>Düzgün</th><th>Xal</th></tr></thead>
<tbody id="leaders"><tr><td colspan="4">Hələ nəticə yoxdur.</td></tr></tbody>
</table></div>
</section>

<section class="card">
<h2>👥 İştirak edənlər</h2>
<div id="people" class="people">Hələ iştirakçı yoxdur.</div>
</section>
<footer>Hazırladı: <b>Haldun Məmmədov</b> · ZQİ</footer>
</main>

<script>
/* Gürcüstan vaxtı: Asia/Tbilisi.
   Saat keçibsə, növbəti günün 20:40-ı gözlənilir. */
const ZONE="Asia/Tbilisi";
function parts(){
 const p=new Intl.DateTimeFormat("en-GB",{
  timeZone:ZONE,hour:"2-digit",minute:"2-digit",second:"2-digit",
  hourCycle:"h23",year:"numeric",month:"2-digit",day:"2-digit"
 }).formatToParts(new Date());
 return Object.fromEntries(p.filter(x=>x.type!=="literal").map(x=>[x.type,x.value]));
}
function targetTime(){
 const p=parts();
 const now=Number(p.hour)*3600+Number(p.minute)*60+Number(p.second);
 let delta=20*3600+40*60-now;
 if(delta<=0)delta+=86400;
 return Date.now()+delta*1000;
}
let target=targetTime(),begun=false;
const questions=[
["7/10 kəsrinin surət və məxrəcindən eyni ədəd çıxıldıqda 2/3 alınır. Ədəd neçədir?",["1","2","3","4"],0,"(7−x)/(10−x)=2/3. Buradan x=1."],
["7/9 kəsrinin surət və məxrəcinə eyni ədəd əlavə edildikdə 5/6 alınır. Ədəd neçədir?",["2","3","4","5"],1,"(7+x)/(9+x)=5/6. Buradan x=3."],
["3 7/24 ÷ (−5/6 + 7/8) ifadəsinin qiymətini tapın.",["71","72","77","79"],3,"Mötərizə 1/24 edir. 79/24 ÷ 1/24 = 79."],
["2 5/16 ÷ (−3/8 + 7/16) ifadəsinin qiymətini tapın.",["31","32","35","37"],3,"Mötərizə 1/16 edir. 37/16 ÷ 1/16 = 37."],
["(2 − 1,6 : 2) ÷ (1 4/5 : 2 1/4) ifadəsinin qiyməti nədir?",["0,25","2,5","1,5","0,75"],2,"Surət 1,2; məxrəc 0,8. Nəticə 1,5."],
["(2 1/2 − (−0,5)) ÷ (3 + 3 : 3) ifadəsinin qiymətini tapın.",["−2/3","1","−1/3","3/4"],3,"Surət 3, məxrəc 4. Nəticə 3/4."],
["(4 3/4 − 3,75) ÷ (7 1/3 : 1 2/9) · 6 ifadəsinin qiyməti nədir?",["1","0,2","1/2","2/3"],0,"Surət 1, mötərizədəki bölmə 6-dır. 1/6 · 6 = 1."],
["4 1/2 · 8/9 + 5 1/3 : 10 2/3 ifadəsini hesablayın.",["0,5","1,5","4,5","3"],2,"4 1/2 · 8/9 = 4; 5 1/3 : 10 2/3 = 1/2. Cəm 4,5."],
["m və n tək ədədlərdirsə, hansı ifadə cüt ədəddir?",["2n² + m","m·n","m+n","n+2m"],2,"Tək + tək = cüt."],
["x cüt, y tək ədəddirsə, hansı ifadə mütləq cüt ədəddir?",["3(x+y)","2x+3y²","(x+y)²","(x−y)²","5x²+2y²"],4,"x cütdürsə 5x² cütdür. 2y² də cütdür; cəmləri cütdür."]
];
let name="",idx=0,chosen=null,score=0,correct=0,seconds=60,elapsed=0,locked=false,clock=null;
const $=id=>document.getElementById(id);
function load(key,fallback){try{return JSON.parse(localStorage.getItem(key)||JSON.stringify(fallback))}catch(e){return fallback}}
function save(key,value){localStorage.setItem(key,JSON.stringify(value))}
function safe(s){return String(s).replace(/[&<>"']/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]))}
function refresh(){
 let r=load("zqiHardResults",[]);
 r.sort((a,b)=>b.score-a.score||b.correct-a.correct||a.elapsed-b.elapsed);
 $("leaders").innerHTML=r.length?r.slice(0,50).map((x,j)=>`<tr><td class="goldtext">${["🥇","🥈","🥉"][j]||j+1}</td><td>${safe(x.name)}</td><td>${x.correct}/10</td><td>${x.score}</td></tr>`).join(""):'<tr><td colspan="4">Hələ nəticə yoxdur.</td></tr>';
 let p=load("zqiHardPeople",[]);
 $("people").innerHTML=p.length?p.map(n=>`<span class="person">👤 ${safe(n)}</span>`).join(""):"Hələ iştirakçı yoxdur.";
}
function countdown(){
 if(begun)return;
 let remain=Math.max(0,Math.floor((target-Date.now())/1000));
 $("hh").textContent=String(Math.floor(remain/3600)).padStart(2,"0");
 $("mm").textContent=String(Math.floor(remain%3600/60)).padStart(2,"0");
 $("ss").textContent=String(remain%60).padStart(2,"0");
 if(remain===0){
  begun=true;
  if(!$("player").value.trim()){ $("status").textContent="Quiz başladı! Adını yaz və iştirak et.";return; }
  startQuiz();
 }
}
function startQuiz(){
 name=$("player").value.trim();
 if(!name){alert("Əvvəl iştirakçı adını yaz.");return}
 let p=load("zqiHardPeople",[]);
 if(!p.some(x=>x.toLowerCase()===name.toLowerCase())){p.push(name);save("zqiHardPeople",p)}
 $("waiting").classList.add("hidden");$("quiz").classList.remove("hidden");
 idx=0;score=0;correct=0;elapsed=0;showQuestion();refresh();
}
function showQuestion(){
 clearInterval(clock);chosen=null;locked=false;seconds=60;
 const q=questions[idx];
 $("number").textContent=(idx+1)+"/10";$("timer").textContent=60;
 $("points").textContent=score;$("fill").style.width="100%";
 $("question").textContent=q[0];$("feedback").textContent="";
 $("send").disabled=true;$("send").classList.remove("hidden");$("next").classList.add("hidden");
 $("answers").innerHTML=q[1].map((a,j)=>`<button class="ans" data-i="${j}">${String.fromCharCode(65+j)}) ${a}</button>`).join("");
 document.querySelectorAll(".ans").forEach(b=>b.onclick=()=>{
  if(locked)return;chosen=Number(b.dataset.i);
  document.querySelectorAll(".ans").forEach(x=>x.classList.toggle("selected",x===b));
  $("send").disabled=false;
 });
 clock=setInterval(()=>{seconds--;elapsed++;$("timer").textContent=seconds;$("fill").style.width=seconds/60*100+"%";if(seconds<=0)submit(true)},1000);
}
function submit(timeout=false){
 if(locked||(!timeout&&chosen===null))return;
 locked=true;clearInterval(clock);
 const q=questions[idx],ok=chosen===q[2];
 if(ok){correct++;score+=10+seconds}
 document.querySelectorAll(".ans").forEach((b,j)=>{
  b.disabled=true;if(j===q[2])b.classList.add("right");if(j===chosen&&!ok)b.classList.add("wrong");
 });
 $("feedback").textContent=(timeout?"Vaxt bitdi. ":ok?"Düzgün cavab! ":"Səhv cavab. ")+q[3];
 $("points").textContent=score;$("send").classList.add("hidden");$("next").classList.remove("hidden");
 $("next").textContent=idx===9?"Nəticəni göstər":"Növbəti sual";
}
function next(){
 if(!locked)return;
 if(idx<9){idx++;showQuestion()}else finish();
}
function finish(){
 clearInterval(clock);$("quiz").classList.add("hidden");$("result").classList.remove("hidden");
 $("finalPoints").textContent=score;$("finalCorrect").textContent=correct+"/10";$("finalTime").textContent=elapsed;
 let r=load("zqiHardResults",[]),pos=r.findIndex(x=>x.name.toLowerCase()===name.toLowerCase());
 const item={name,score,correct,elapsed};
 if(pos<0)r.push(item);else if(score>r[pos].score)r[pos]=item;
 save("zqiHardResults",r);refresh();
}
$("send").onclick=()=>submit(false);
$("next").onclick=next;
$("player").addEventListener("keydown",e=>{if(e.key==="Enter"&&begun)startQuiz()});
setInterval(countdown,250);countdown();refresh();
</script>
</body>
</html>

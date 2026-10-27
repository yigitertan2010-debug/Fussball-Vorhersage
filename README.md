<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Anstoss – Tipps zu den nächsten Spielen</title>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,500;12..96,800&family=DM+Sans:wght@400;500;700&display=swap">
<style>
:root{
  --bg:#e8eee9;--surface:#f7faf7;--ink:#0d2b20;--muted:#5b7166;--line:#c5d2c9;
  --home:#0f6b45;--draw:#9aa89f;--away:#d9542b;--chalk:#ffffff;
  --display:"Bricolage Grotesque","Arial Black",sans-serif;--body:"DM Sans",system-ui,sans-serif;
  box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px);
}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){
  --bg:#0c1a14;--surface:#12251c;--ink:#e6f0ea;--muted:#8da499;--line:#25402f;
  --home:#3fbf84;--draw:#6b7f74;--away:#ff8a5c;--chalk:#e6f0ea}}
:root[data-theme="dark"]{--bg:#0c1a14;--surface:#12251c;--ink:#e6f0ea;--muted:#8da499;--line:#25402f;--home:#3fbf84;--draw:#6b7f74;--away:#ff8a5c;--chalk:#e6f0ea}
*{box-sizing:border-box}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
body{margin:0;background:var(--bg);color:var(--ink);font:400 16px/1.5 var(--body);min-height:100vh}
main{max-width:860px;margin:0 auto;padding:28px 20px 64px}
.crew{position:absolute;top:12px;right:16px;font:500 13px var(--body);color:var(--muted)}
h1{font:800 clamp(30px,7vw,44px)/1 var(--display);margin:0 0 6px;letter-spacing:-.02em}
.sub{color:var(--muted);margin:0 0 6px}
.tabs{display:flex;gap:6px;overflow-x:auto;margin:16px 0 4px;padding-bottom:6px}
.tabs button{flex:none;border:1px solid var(--line);background:var(--surface);color:var(--muted);font:500 14px var(--body);padding:8px 14px;border-radius:999px;cursor:pointer}
.tabs button[aria-pressed="true"]{background:var(--ink);color:var(--bg);border-color:var(--ink)}
.tabs button:focus-visible{outline:3px solid var(--away);outline-offset:2px}
h2{font:800 18px var(--display);margin:30px 0 10px;color:var(--muted)}
.card{background:var(--surface);border:1px solid var(--line);border-radius:16px;padding:16px 18px;margin-bottom:12px}
.card.top{background:var(--ink);color:var(--bg);border-color:var(--ink)}
.meta{font-size:13px;opacity:.7;margin-bottom:8px}
.row{display:grid;grid-template-columns:1fr auto 1fr;gap:10px;align-items:center}
.t{font:500 clamp(15px,3.6vw,18px)/1.2 var(--body)}
.t.r{text-align:right}
.t.win{font-weight:700}
.sc{font:800 clamp(36px,10vw,52px)/1 var(--display);letter-spacing:-.03em;font-variant-numeric:tabular-nums;white-space:nowrap}
.sc i{font-style:normal;opacity:.35;padding:0 .06em}
.bar{display:flex;height:8px;border-radius:99px;overflow:hidden;margin-top:12px;gap:2px}
.bar b{display:block}
.bar .h{background:var(--home)}.bar .d{background:var(--draw)}.bar .a{background:var(--away)}
.lg{display:flex;justify-content:space-between;font-size:12px;opacity:.75;margin-top:5px;font-variant-numeric:tabular-nums}
.note{font-size:13px;color:var(--muted);margin-top:28px}
</style>
</head>
<body>
<main>
<div class="crew">Yigit, Tiago, Faruk</div>
<h1>Anstoss</h1>
<p class="sub">So enden die nächsten Spiele in sieben Wettbewerben. Stand 27.10.2026.</p>
<div class="tabs" id="tabs" role="group" aria-label="Liga"></div>
<div id="out"></div>
<p class="note">Die Tipps leiten sich aus den Siegwahrscheinlichkeiten eines Sportdatenanbieters ab. Das wahrscheinlichste Ergebnis passend zum Favoriten wird als Endstand genannt. Das ist eine Schätzung, keine Garantie.</p>
</main>
<script>
const L={
"Bundesliga":[
["2026-10-30T19:30:00Z","SV Elversberg","Mainz 05",30.3,24.7,45],
["2026-10-31T14:30:00Z","Bayer Leverkusen","VfB Stuttgart",52.6,21.9,25.5],
["2026-10-31T14:30:00Z","FC Augsburg","SC Freiburg",31.7,24.8,43.5],
["2026-10-31T14:30:00Z","Gladbach","SC Paderborn",48.8,24,27.2],
["2026-10-31T14:30:00Z","Werder Bremen","TSG Hoffenheim",33.4,24.4,42.2],
["2026-10-31T14:30:00Z","Schalke 04","RB Leipzig",24.9,24.2,50.9],
["2026-10-31T17:30:00Z","Bayern München","Borussia Dortmund",72,15,13],
["2026-11-01T14:30:00Z","Union Berlin","1. FC Köln",38.3,26,35.7],
["2026-11-01T16:30:00Z","Eintracht Frankfurt","Hamburger SV",57.5,21.5,21],
["2026-11-06T19:30:00Z","Hamburger SV","Gladbach",41.7,25.4,32.9]],
"Premier League":[
["2026-10-31T12:30:00Z","Chelsea","Manchester United",53,23.9,23.1],
["2026-10-31T15:00:00Z","Bournemouth","Leeds United",45.4,27.3,27.3],
["2026-10-31T15:00:00Z","Brentford","Nottingham Forest",48,25.8,26.2],
["2026-10-31T15:00:00Z","Coventry City","Sunderland",31.5,27.7,40.8],
["2026-10-31T15:00:00Z","Hull City","Ipswich Town",36.9,27.4,35.7],
["2026-10-31T15:00:00Z","Manchester City","Brighton",58,21.6,20.4],
["2026-10-31T17:30:00Z","Tottenham","Crystal Palace",62.3,20.5,17.2],
["2026-10-31T20:00:00Z","Aston Villa","Fulham",47.7,25.5,26.8],
["2026-11-01T16:30:00Z","Liverpool","Arsenal",31.4,27,41.6],
["2026-11-02T20:00:00Z","Newcastle United","Everton",42.3,26.2,31.5]],
"La Liga":[
["2026-10-30T20:00:00Z","Villarreal","Espanyol",66.6,18.7,14.7],
["2026-10-31T13:00:00Z","Levante","Atlético Madrid",19.2,21.4,59.4],
["2026-10-31T15:15:00Z","Rayo Vallecano","Celta Vigo",40.4,28.7,30.9],
["2026-10-31T17:30:00Z","Real Betis","Málaga",70,17.3,12.7],
["2026-10-31T20:00:00Z","FC Barcelona","Alavés",88.5,7.8,3.7],
["2026-11-01T13:00:00Z","Getafe","FC Sevilla",31.1,31.6,37.3],
["2026-11-01T15:15:00Z","Racing Santander","Real Madrid",9.2,12.1,78.7],
["2026-11-01T17:30:00Z","Elche","FC Valencia",40,27.9,32.1],
["2026-11-01T20:00:00Z","Athletic Bilbao","Real Sociedad",45.2,25.8,29],
["2026-11-02T20:00:00Z","Deportivo La Coruña","Osasuna",43.7,29.4,26.9]],
"Serie A":[
["2026-10-27T17:30:00Z","Sassuolo","Lazio",27.3,26.8,45.9],
["2026-10-27T19:45:00Z","AS Roma","Cagliari",74.5,16,9.5],
["2026-10-27T19:45:00Z","Torino","Como",20.5,24.5,55],
["2026-10-28T17:30:00Z","AC Mailand","Bologna",58.4,23.7,17.9],
["2026-10-28T17:30:00Z","Parma","Udinese",32.9,29.8,37.3],
["2026-10-28T17:30:00Z","Venezia","Inter Mailand",12.8,16,71.2],
["2026-10-28T19:45:00Z","Genoa","Juventus",17.7,25.3,57],
["2026-10-28T19:45:00Z","Monza","SSC Neapel",21.5,24,54.5],
["2026-10-29T17:30:00Z","Frosinone","Lecce",57.3,22.3,20.4],
["2026-10-29T19:45:00Z","Fiorentina","Atalanta",42.9,25.9,31.2]],
"Ligue 1":[
["2026-10-30T18:00:00Z","Le Havre","Paris Saint-Germain",8.9,12.8,78.3],
["2026-10-30T18:00:00Z","OGC Nizza","Stade Rennes",34.7,25,40.3],
["2026-10-30T20:05:00Z","Lille","RC Lens",39.8,26.3,33.9],
["2026-10-31T19:45:00Z","Troyes","Le Mans",42.4,27,30.6],
["2026-11-01T14:00:00Z","Strassburg","Auxerre",52.6,23.8,23.6],
["2026-11-01T16:15:00Z","Olympique Lyon","Angers",69.4,17.8,12.8],
["2026-11-01T16:15:00Z","Paris FC","AS Monaco",41.9,26.8,31.3],
["2026-11-01T19:45:00Z","Olympique Marseille","Toulouse",50,24.3,25.7],
["2026-11-02T19:45:00Z","Lorient","Stade Brest",37.8,28.5,33.7],
["2026-11-06T19:45:00Z","Toulouse","Strassburg",46,25.3,28.7]],
"Champions League":[
["2026-11-03T17:45:00Z","Schachtar Donezk","Sporting CP",26.6,25.5,47.9],
["2026-11-03T17:45:00Z","Galatasaray","VfB Stuttgart",42.8,24.3,32.9],
["2026-11-03T20:00:00Z","Atlético Madrid","Bayern München",28.9,23.4,47.7],
["2026-11-03T20:00:00Z","FC Barcelona","Aston Villa",78.6,12.2,9.2],
["2026-11-03T20:00:00Z","Feyenoord","Inter Mailand",21.8,22,56.2],
["2026-11-03T20:00:00Z","Bodø/Glimt","Lille",49.5,24.3,26.2],
["2026-11-03T20:00:00Z","LASK Linz","Slovan Bratislava",66.6,18.3,15.1],
["2026-11-03T20:00:00Z","Manchester United","AS Roma",40.9,25,34.1],
["2026-11-03T20:00:00Z","Villarreal","Paris Saint-Germain",20.5,20.3,59.2],
["2026-11-04T17:45:00Z","AEK Athen","Real Madrid",11.5,14.9,73.6]],
"MLS":[
["2026-10-28T23:30:00Z","Charlotte FC","CF Montréal",65.2,18.8,16],
["2026-10-28T23:30:00Z","Inter Miami","FC Cincinnati",65.6,17.6,16.8],
["2026-10-28T23:30:00Z","New England","NY Red Bulls",47.3,23.8,28.9],
["2026-10-28T23:30:00Z","New York City FC","Atlanta United",53.7,23.9,22.4],
["2026-10-28T23:30:00Z","Toronto FC","DC United",47.5,24.9,27.6],
["2026-10-29T00:30:00Z","Austin FC","Real Salt Lake",35.7,25.8,38.5],
["2026-10-29T00:30:00Z","Chicago Fire","Orlando City",60.9,19.3,19.8],
["2026-10-29T00:30:00Z","FC Dallas","Columbus Crew",46.8,24.5,28.7],
["2026-10-29T00:30:00Z","Minnesota United","Sporting KC",67.5,17.5,15],
["2026-10-29T00:30:00Z","Nashville SC","Philadelphia Union",50.3,24.2,25.5]]
};
const pois=(l,k)=>{let p=Math.exp(-l);for(let i=1;i<=k;i++)p*=l/i;return p};
function matrix(lh,la){const m=[];for(let i=0;i<8;i++){m[i]=[];for(let j=0;j<8;j++)m[i][j]=pois(lh,i)*pois(la,j)}return m}
function outcome(m){let h=0,d=0,a=0,t=0;for(let i=0;i<8;i++)for(let j=0;j<8;j++){const p=m[i][j];t+=p;if(i>j)h+=p;else if(i==j)d+=p;else a+=p}return[h/t,d/t,a/t]}
function predict(ph,pd,pa){
  let best=[1.4,1.2],err=9;
  for(let lh=.2;lh<=3.6;lh+=.1)for(let la=.2;la<=3.6;la+=.1){
    const o=outcome(matrix(lh,la)),e=(o[0]-ph)**2+(o[1]-pd)**2+(o[2]-pa)**2;
    if(e<err){err=e;best=[lh,la]}}
  const m=matrix(best[0],best[1]),fav=ph>=pd&&ph>=pa?"h":pa>=pd?"a":"d";
  let s=[0,0],bp=-1;
  for(let i=0;i<8;i++)for(let j=0;j<8;j++){
    const ok=fav=="h"?i>j:fav=="a"?i<j:i==j;
    if(ok&&m[i][j]>bp){bp=m[i][j];s=[i,j]}}
  return s;
}
const dayFmt=new Intl.DateTimeFormat("de-CH",{weekday:"long",day:"numeric",month:"long",timeZone:"Europe/Zurich"});
const timeFmt=new Intl.DateTimeFormat("de-CH",{hour:"2-digit",minute:"2-digit",timeZone:"Europe/Zurich"});
const cache={};
function pred(ph,pd,pa){const k=ph+"|"+pd;return cache[k]||(cache[k]=predict(ph/100,pd/100,pa/100))}
let cur="Alle";
function render(){
  const all=[];
  Object.entries(L).forEach(([lg,g])=>{if(cur==="Alle"||cur===lg)g.forEach(x=>all.push([...x,lg]))});
  all.sort((x,y)=>x[0]<y[0]?-1:x[0]>y[0]?1:0);
  let html="",lastDay="";
  all.forEach(([iso,h,a,ph,pd,pa,lg])=>{
    const d=new Date(iso),day=dayFmt.format(d);
    if(day!==lastDay){html+=`<h2>${day}</h2>`;lastDay=day}
    const s=pred(ph,pd,pa),big=Math.max(ph,pa)>=60;
    html+=`<article class="card${big?" top":""}">
    <div class="meta">${timeFmt.format(d)} Uhr${cur==="Alle"?" – "+lg:""}</div>
    <div class="row"><div class="t${s[0]>s[1]?" win":""}">${h}</div>
    <div class="sc" aria-label="Tipp ${s[0]} zu ${s[1]}">${s[0]}<i>:</i>${s[1]}</div>
    <div class="t r${s[1]>s[0]?" win":""}">${a}</div></div>
    <div class="bar" role="img" aria-label="Heimsieg ${ph} Prozent, Unentschieden ${pd} Prozent, Auswärtssieg ${pa} Prozent"><b class="h" style="flex:${ph}"></b><b class="d" style="flex:${pd}"></b><b class="a" style="flex:${pa}"></b></div>
    <div class="lg"><span>${Math.round(ph)} %</span><span>${Math.round(pd)} %</span><span>${Math.round(pa)} %</span></div></article>`});
  document.getElementById("out").innerHTML=html;
}
const tabs=document.getElementById("tabs");
["Alle",...Object.keys(L)].forEach(n=>{const b=document.createElement("button");b.textContent=n;b.setAttribute("aria-pressed",n===cur);
  b.onclick=()=>{cur=n;[...tabs.children].forEach(x=>x.setAttribute("aria-pressed",x===b));render()};tabs.appendChild(b)});
render();
</script>
</body>
</html>

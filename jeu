<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Lancelot et la Charrette</title>
<style>
:root{box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px);--bg:#f1e9d8;--fg:#2a1d12;--btn:#7a1f2b;--btnfg:#fff6e0}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#1b1410;--fg:#eadfc6;--btn:#a8323f;--btnfg:#fff6e0}}
:root[data-theme="dark"]{--bg:#1b1410;--fg:#eadfc6;--btn:#a8323f;--btnfg:#fff6e0}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--fg);font-family:Georgia,'Times New Roman',serif;display:flex;flex-direction:column;align-items:center;padding:12px;min-height:100vh}
h1{font-size:1.15rem;margin:4px 0 10px;font-weight:700;letter-spacing:.02em;text-align:center}
canvas{width:100%;max-width:640px;height:auto;aspect-ratio:640/448;border:4px solid var(--btn);border-radius:6px;image-rendering:pixelated;touch-action:none;background:#000}
.pad{display:flex;gap:10px;width:100%;max-width:640px;margin-top:12px;user-select:none;-webkit-user-select:none}
.pad button{flex:1;padding:18px 0;font:700 1.2rem Georgia,serif;background:var(--btn);color:var(--btnfg);border:0;border-radius:8px;touch-action:none}
.pad button:active{filter:brightness(1.25)}
.pad .j{flex:1.6}
#mu{margin:-4px 0 10px;padding:6px 14px;font:600 .85rem Georgia,serif;background:var(--btn);color:var(--btnfg);border:0;border-radius:6px}
p{max-width:640px;font-size:.85rem;margin:10px 0 0;line-height:1.5}
</style>
</head>
<body>
<h1>Lancelot et la Charrette</h1>
<button id="mu" tabindex="-1">🔊 Son (M)</button>
<canvas id="c" width="640" height="448"></canvas>
<div class="pad">
<button id="bl">◀</button><button id="br">▶</button><button id="bx">Épée</button><button id="bj" class="j">Sauter</button>
</div>
<p>Clavier : flèches ou Q/D pour bouger, Espace ou ↑ pour sauter, X pour frapper de l'épée, 1/2/3 pour répondre. Frappe les blocs ? par en dessous pour répondre aux questions sur le livre. Tu as 5 cœurs : sans cœur, tu reprends au début du niveau. Parle aux gens et soulève les dalles avec X. Bonne réponse = boost, mauvaise = malédiction.</p>
<script>
const cv=document.getElementById('c'),g=cv.getContext('2d'),W=640,H=448,T=32;
const LV=[
{n:"1. La plaine",w:90,gr:[[0,21],[25,47],[51,89]],sky:['#7ec8f0','#d8f0ff'],
 it:[['=',14,9,4],['=',26,8,3],['=',36,9,5],['=',52,8,4],['=',64,9,3],['E',18,11],['E',40,11],['E',58,11],['E',70,11],['S',30,11],['S',75,11],
 ['o',15,7],['o',16,7],['o',27,6],['o',38,7],['o',39,7],['o',53,6],['o',54,6],['o',65,7],['o',22,9],['o',48,9],['o',10,11],['o',44,11],['G',86,10],['?',8,8],['?',33,8],['?',60,8],['V',24,8],['V',49,8],['V',72,7],['E',12,11],['E',65,11],['E',45,11],['E',82,11],['V',14,7]],
 t:"Guenièvre a été enlevée par Méléagant. Pour la retrouver, Lancelot accepte de monter dans la charrette d'infamie, la honte suprême pour un chevalier. Traverse la plaine !"},
{n:"2. Le Pont de l'Épée",w:80,gr:[[0,6],[73,79]],sky:['#3a1d4a','#e98a5a'],
 it:[['B',8,10,3],['B',13,9,3],['B',18,10,2],['B',23,8,3],['B',28,9,2],['B',33,10,3],['B',38,8,2],['B',43,9,3],['B',48,10,2],['B',53,9,3],['B',58,8,2],['B',63,9,3],['B',68,10,3],
 ['S',24,7],['S',34,9],['S',54,8],
 ['o',9,8],['o',14,7],['o',24,6],['o',29,7],['o',39,6],['o',44,7],['o',49,8],['o',59,6],['o',64,7],['o',69,8],['G',77,10],['?',14,6],['?',39,5],['?',64,6],['V',17,7],['V',46,6],['V',60,5],['V',10,6],['V',33,5],['V',68,6]],
 t:"Pour entrer au royaume de Gorre, il faut franchir le Pont de l'Épée : une lame tranchante au-dessus du gouffre. Ne tombe pas !"},
{n:"3. Le château de Gorre",w:100,gr:[[0,29],[33,99]],sky:['#10121f','#3b3358'],
 it:[['=',12,9,3],['=',20,8,3],['#',27,10,2],['=',37,9,4],['=',45,8,3],['#',52,9,2],['#',52,10,2],['=',60,9,4],['=',70,8,3],['=',78,9,3],
 ['E',16,11],['E',40,11],['E',47,11],['E',64,11],['E',74,11],['S',44,11],['S',68,11],['M',90,11],
 ['o',13,7],['o',21,6],['o',38,7],['o',46,6],['o',61,7],['o',71,6],['o',79,7],['o',34,11],['o',56,11],['G',97,10],['?',5,8],['?',57,8],['?',84,8],['V',23,7],['V',50,6],['V',68,6],['V',85,7],['E',55,11],['E',80,11],['E',36,11],['E',70,11],['E',24,11]],
 t:"Dans le château de Méléagant, le traître t'attend. Saute trois fois sur sa tête pour le vaincre, puis délivre la reine."}
];
const A=LV[1],B=LV[2];
Object.assign(LV[0],{n:"1. La charrette",gb:'#8a5a32',gt:'#4caf50',bk:'#b5532f',hc:'#6fa86a',nc:'#5a3a7a',nr:'h',nt:"Un nain te fait signe : « Monte dans ma charrette et je te dirai où est la reine. » Aucun chevalier n'ose : c'est la voiture des criminels, la honte suprême. Lancelot hésite à peine, puis monte."});
LV[0].it.push(['N',6,11]);
Object.assign(A,{n:"5. Le Pont de l'Épée",wind:1,gb:'#4a4660',gt:'#7a3b50',bk:'#6b3a44',hc:'#2b1535'});
Object.assign(B,{n:"6. Le château de Gorre",gb:'#4a4660',gt:'#6a6690',bk:'#5b5778',hc:'#1a1a2e',nc:'#b8902a',nr:'h',nt:"Le roi Bademagu t'arrête : « Mon fils Méléagant est un félon, et je ne peux plus le contenir. Frappe-le trois fois et ma prisonnière sera libre. »"});
B.it.push(['N',82,11]);
const L2={n:"2. Le lit périlleux",w:80,gr:[[0,79]],sky:['#0b0a14','#3a1a2a'],gb:'#4a4660',gt:'#6a6690',bk:'#6b3a44',hc:'#1a1428',rain:110,nc:'#9c2b4e',nr:'b',
 nt:"Une demoiselle te prévient : « Ce lit est maudit. Une lance de feu s'abat sur celui qui s'y couche. Mais tu n'as pas peur, n'est-ce pas ? »",
 t:"Le soir tombe sur un château étrange. Au fond de la salle, un lit magnifique t'attend, mais des lances de feu tombent du plafond. Traverse la salle sans te faire embrocher.",
 it:[['=',10,9,4],['=',18,8,3],['=',26,9,3],['=',34,8,4],['=',44,9,3],['=',52,8,3],['=',60,9,4],['N',4,11],['E',14,11],['E',30,11],['E',40,11],['E',56,11],['E',66,11],['V',22,7],['V',48,6],['V',64,6],['S',38,11],
 ['?',8,8],['?',36,6],['?',58,6],['o',11,7],['o',19,6],['o',35,6],['o',45,7],['o',61,7],['o',28,11],['o',50,11],['G',76,10]]};
const L3={n:"3. La fontaine",w:90,gr:[[0,12],[60,89]],sky:['#f5b97a','#fbe7c4'],gb:'#5a4128',gt:'#3f7f3a',bk:'#8a5a32',hc:'#3d6b46',nc:'#6b5a3a',nr:'h',
 nt:"Un ermite murmure : « Celui qui aime oublie le monde. Prends garde à ne pas t'égarer en pensées sur le gué, chevalier. »",
 t:"À l'aube, près d'une fontaine, un objet brillant traîne dans l'herbe. Les vieux troncs pourrissent sous tes pas : ne t'attarde pas. Ramasse les objets mystérieux !",
 it:[['C',14,11,3],['C',19,10,3],['C',24,11,3],['C',29,10,2],['C',34,11,3],['C',39,9,3],['C',44,10,3],['C',49,11,3],['C',54,10,3],['m',30,7],['m',50,8],['N',62,11],['E',8,11],['E',66,11],['E',74,11],['V',22,8],['V',40,6],['V',70,8],
 ['?',5,8],['?',70,8],['o',15,9],['o',20,8],['o',40,7],['o',45,8],['o',55,8],['o',10,11],['o',64,11],['G',86,10]]};
const L4={n:"4. Le cimetière",w:80,gr:[[0,79]],sky:['#0a0d1a','#2b3350'],gb:'#3c4350',gt:'#59606e',bk:'#555b66',hc:'#151a2b',lift:1,nc:'#2a2a2a',nr:'b',
 nt:"Un fossoyeur désigne la dalle la plus lourde : « Celui qui la soulèvera libérera tous les captifs de ce pays. Cours vite : les spectres rôdent. »",
 t:"Dans le cimetière, des tombes portent les noms de chevaliers qui mourront ici. L'une est scellée par une dalle gigantesque. Les spectres ne meurent pas : évite-les, puis soulève la dalle en appuyant vite sur X.",
 it:[['#',14,11,2],['#',28,10,2],['#',28,11,2],['#',44,11,3],['#',58,10,2],['#',58,11,2],['N',6,11],['m',40,7],['W',20,8],['W',42,6],['W',60,8],['W',70,7],['E',24,11],['E',50,11],['V',34,7],
 ['?',16,8],['?',46,8],['o',13,9],['o',29,8],['o',45,9],['o',59,8],['o',35,11],['G',76,10]]};
LV[0].ch=[["Monter tout de suite, malgré la honte",'h'],["Hésiter deux pas avant de monter",'r']];
L2.ch=[["Se coucher dans le lit maudit",'r'],["Avancer avec prudence",'h']];
L3.ch=[["Écouter l'ermite et se reposer",'h'],["Ignorer son conseil et courir",'s']];
L4.ch=[["Demander le secret de la dalle",'b'],["Ricaner et avancer",'r']];
B.ch=[["Accepter l'aide du roi",'h'],["Défier le roi par orgueil",'r']];
LV.length=1;LV.push(L2,L3,L4,A,B);
LV.forEach(L=>{const n={};L.it=L.it.filter(a=>{if('EVWS'.includes(a[0])){n[a[0]]=(n[a[0]]||0)+1;return n[a[0]]%2==1}return true})});
let st='title',lvl=0,lives=3,score=0,map,ents,p,camX=0,msg='',msgT=0,tick=0,coins=0,tries=0,lvScore=0,lvCoins=0,dT=0,dWhy='',qDone=[{},{},{},{},{},{}],quiz=null,xPrev=0,fx={n:'',t:0,l:''},cz={},goal=null,qc={},qm=0,hp=5,talk=null,pt=[],fl=0,flc='',sh=0,hl=0,mgc='',hq=null,safe=null,chance=true,rx=0,mode=0,bul=[];
const K={},touch={l:0,r:0,j:0,x:0};let jPrev=0,jBuf=0;
addEventListener('keydown',e=>{ac();if(e.code=='KeyM')toggleMute();K[e.code]=1;if(st=='quiz'){const n=+e.key;if(n>=1&&n<=3)answer(n-1)}else if(st=='talk'){const n=+e.key;if(n>=1&&n<=talk.ch.length)pick(n-1)}if(['Space','ArrowUp','ArrowDown','ArrowLeft','ArrowRight'].includes(e.code))e.preventDefault();if(e.code=='Enter'||e.code=='Space')advance()});
addEventListener('keyup',e=>K[e.code]=0);
addEventListener('blur',()=>{for(const k in K)K[k]=0;touch.l=touch.r=touch.j=touch.x=0});
[['bl','l'],['br','r'],['bx','x'],['bj','j']].forEach(([id,k])=>{const b=document.getElementById(id);
 b.addEventListener('pointerdown',e=>{e.preventDefault();touch[k]=1;if(k=='j')advance()});
 ['pointerup','pointerleave','pointercancel'].forEach(ev=>b.addEventListener(ev,()=>touch[k]=0))});
cv.addEventListener('pointerdown',e=>{if(st=='quiz'){const b=cv.getBoundingClientRect(),y=(e.clientY-b.top)*H/b.height,i=Math.floor((y-190)/66);if(i>=0&&i<3&&y<190+i*66+54)answer(i);return}if(st=='talk'){const b=cv.getBoundingClientRect(),y=(e.clientY-b.top)*H/b.height,i=Math.floor((y-320)/46);if(i>=0&&i<talk.ch.length&&y<320+i*46+38)pick(i);return}if(st!='play')advance()});
function advance(){
 if(st=='title'||st=='over'||st=='win'){lvl=0;lives=3;score=0;tries=0;coins=0;qDone=[{},{},{},{},{},{}];st='intro'}
 else if(st=='intro'){load();st='play'}
 else if(st=='next'){lvl++;st='intro'}
 else if(st=='talk'){}
 jBuf=0;
}
function load(){
 const d=LV[lvl];map=[];
 for(let r=0;r<14;r++)map.push(Array(d.w).fill('.'));
 d.gr.forEach(([a,b])=>{for(let c=a;c<=b;c++){map[12][c]='#';map[13][c]='#'}});
 ents=[];
 d.it.forEach(([ch,c,r,len])=>{
  if(ch=='E')ents.push({k:'E',x:c*T+4,y:r*T-4,w:24,h:30,vx:-1,vy:0,hp:1,inv:0});
  else if(ch=='W')ents.push({k:'W',x:c*T,y:r*T,w:24,h:30,vx:0,vy:0,hp:99,inv:0});
  else if(ch=='V')ents.push({k:'V',x:c*T,y:r*T,x0:c*T,y0:r*T,w:26,h:18,vx:1.2,vy:0,hp:1,inv:0});
  else if(ch=='M')ents.push({k:'M',x:c*T,y:r*T-20,w:40,h:48,vx:-1.4,vy:0,hp:3,inv:0});
  else for(let i=0;i<(len||1);i++)map[r][c+i]=ch;
 });
 p={x:2*T,y:10*T,w:22,h:30,vx:0,vy:0,on:false,face:1,coy:0,sw:0,lift:0,inv:0};
 goal=null;map.forEach((row,r)=>row.forEach((ch,c)=>{if(ch=='G')goal={x:c*T,y:r*T}}));safe={x:p.x,y:p.y};chance=true;rx=p.x;bul=[];hp=5;fx={n:'',t:0,l:''};cz={};lvScore=score;lvCoins=coins;for(const k in qDone[lvl]){const[c,r]=k.split(',');map[r][c]=map[r][c]=='N'?'n':'.'}
 camX=0;msg='';tick=0;
}
const solid=(c,r)=>{if(c<0)return true;if(r<0||r>=14)return false;const ch=(map[r]||[])[c];return ch=='#'||ch=='='||ch=='B'||ch=='?'||ch=='C'};
function box(o){
 o.x+=o.vx;let hit=false;
 let c0=Math.floor(o.x/T),c1=Math.floor((o.x+o.w-.01)/T),r0=Math.floor(o.y/T),r1=Math.floor((o.y+o.h-.01)/T);
 for(let r=r0;r<=r1;r++)for(let c=c0;c<=c1;c++)if(solid(c,r)){hit=true;
  if(o.vx>0)o.x=c*T-o.w;else if(o.vx<0)o.x=(c+1)*T;o.vx=0;}
 o.y+=o.vy;o.on=false;
 c0=Math.floor(o.x/T);c1=Math.floor((o.x+o.w-.01)/T);r0=Math.floor(o.y/T);r1=Math.floor((o.y+o.h-.01)/T);
 for(let r=r0;r<=r1;r++)for(let c=c0;c<=c1;c++)if(solid(c,r)){
  if(o.vy>0){o.y=r*T-o.h;o.on=true}else if(o.vy<0){o.y=(r+1)*T;if(o===p&&map[r][c]=='?')hq={c,r}}o.vy=0;}
 return hit;
}
const ov=(a,b,s=0)=>a.x+s<b.x+b.w&&a.x+a.w-s>b.x&&a.y+s<b.y+b.h&&a.y+a.h-s>b.y;
const Q=[
[["Qui a écrit Le Chevalier de la charrette ?","Chrétien de Troyes","Molière","Victor Hugo"],
 ["Qui enlève la reine Guenièvre ?","Méléagant","Gauvain","Keu"],
 ["Pourquoi la charrette est-elle honteuse ?","Elle servait à transporter les criminels","Elle est tirée par un dragon","Elle appartient au roi Arthur"]],
[["Comment s'appelle le pont que Lancelot traverse à mains et pieds nus ?","Le Pont de l'Épée","Le Pont de Pierre","Le Pont des Fées"],
 ["Quel objet de la reine, plein de cheveux dorés, Lancelot trouve-t-il ?","Un peigne","Un miroir","Un voile"],
 ["Quel chevalier choisit le pont sous l'eau ?","Gauvain","Perceval","Tristan"]],
[["Pourquoi Guenièvre accueille-t-elle Lancelot froidement ?","Il a hésité avant de monter dans la charrette","Il est arrivé en retard","Il a perdu son épée"],
 ["Comment s'appelle le père de Méléagant ?","Le roi Bademagu","Le roi Arthur","Le roi Pellès"],
 ["Comment s'appelle le royaume où la reine est prisonnière ?","Gorre","Camelot","Logres"]]
],QC=[[8,33,60],[14,39,64],[5,57,84]];
const QL=[
[["Qui a écrit Le Chevalier de la charrette ?","Chrétien de Troyes","Molière","Victor Hugo"],
 ["Qui enlève la reine Guenièvre ?","Méléagant","Gauvain","Keu"],
 ["Pourquoi la charrette est-elle honteuse ?","Elle servait à transporter les criminels","Elle est tirée par un dragon","Elle appartient au roi Arthur"],
 ["Qui conduit la charrette où monte Lancelot ?","Un nain","Un moine","Le roi Arthur"],
 ["Que fait Gauvain devant la charrette ?","Il refuse d'y monter","Il y monte le premier","Il la détruit"]],
[["Quelle arme s'abat sur le lit périlleux ?","Une lance enflammée","Une hache","Un filet"],
 ["Que cherche Lancelot à travers tous ces châteaux ?","La reine Guenièvre","Le Graal","Un trésor"],
 ["À quel genre appartient ce récit du Moyen Âge ?","Un roman courtois","Une pièce de théâtre","Un journal de voyage"],
 ["Qui a commandé le roman à Chrétien de Troyes ?","Marie de Champagne","Aliénor d'Aquitaine","Le roi Philippe"]],
[["Que manque-t-il d'arriver à Lancelot en voyant les cheveux de la reine dans le peigne ?","Il manque de tomber de cheval, bouleversé","Il jette le peigne dans l'eau","Il le revend"],
 ["Que fait Lancelot quand il pense à la reine, au gué ?","Il oublie tout ce qui l'entoure","Il s'enfuit","Il s'endort"],
 ["Quel sentiment guide Lancelot dans tout le roman ?","L'amour courtois","La vengeance","L'ambition"]],
[["Que se passe-t-il quand Lancelot soulève la dalle du cimetière ?","Il montre qu'il délivrera les captifs","Il trouve un trésor","Il réveille un dragon"],
 ["Que portent les tombes du cimetière ?","Les noms de chevaliers qui y mourront","Des fleurs","Des drapeaux"],
 ["Qui seul peut soulever la dalle ?","Celui qui délivrera les captifs","Le plus vieux chevalier","Le roi Arthur"]],
[["Comment s'appelle le pont que Lancelot traverse à mains et pieds nus ?","Le Pont de l'Épée","Le Pont de Pierre","Le Pont des Fées"],
 ["Quel chevalier choisit le pont sous l'eau ?","Gauvain","Perceval","Tristan"],
 ["Qu'arrive-t-il aux mains et aux pieds de Lancelot sur le pont ?","Ils saignent","Ils gèlent","Ils brûlent"],
 ["Que croit voir Lancelot à l'autre bout du pont ?","Deux lions","Deux dragons","Deux géants"]],
[["Comment s'appelle le père de Méléagant ?","Le roi Bademagu","Le roi Arthur","Le roi Pellès"],
 ["Pourquoi Guenièvre accueille-t-elle Lancelot froidement ?","Il a hésité avant de monter dans la charrette","Il est arrivé en retard","Il a perdu son épée"],
 ["Comment s'appelle le royaume où la reine est prisonnière ?","Gorre","Camelot","Logres"],
 ["Qui est Méléagant ?","Le ravisseur de la reine","Un ami de Lancelot","Le roi Arthur"]]];
const QM=[0,0,[["Tu viens de trouver un objet mystérieux : un peigne d'or où restent des cheveux blonds. À qui appartient-il ?","À la reine Guenièvre","À la fée Morgane","À la sœur de Méléagant"],["Tu trouves une mèche blonde dans le peigne : que représente-t-elle pour Lancelot ?","Un lien avec la reine qu'il aime","Un porte-bonheur de Méléagant","Un simple déchet"]],
[["Tu trouves un parchemin mystérieux : à cause de sa honte, comment surnomme-t-on Lancelot ?","Le chevalier de la charrette","Le chevalier au lion","Le chevalier vert"]]];
function startQ(h){const L=h.m?QM[lvl]:QL[lvl],k=lvl+(h.m?'m':''),d=L[(qc[k]=qc[k]||0)%L.length];qc[k]++;sfx('ask');quiz={q:d[0],right:d[1],opts:d.slice(1).sort(()=>Math.random()-.5),c:h.c,r:h.r,m:h.m};st='quiz'}
function pick(i){const o=talk.ch[i],t=o[1];sfx('pick');st='play';jBuf=0;
 if(t=='h'){hp=Math.min(hp+1,7);msg='Un cœur de plus !';mgc='#9dff8a';msgT=100;burst(p.x+11,p.y+15,'#ff3b50',20);flash('rgba(255,120,150,.35)',16)}
 else if(t=='s'){score+=300;msg='+300 points';mgc='#9dff8a';msgT=100;burst(p.x+11,p.y+15,'#ffd93d',20)}
 else giveFx(t=='b'||Math.random()<.5,'')}
function clearLevel(){sfx('clear');score+=500;st='clear';dT=0;p.vx=0;for(let i=0;i<4;i++)burst(p.x+11,p.y,'#ffd93d',20)}
const FB=[['Vitesse de Lancelot !','v'],['Super saut !','j'],['Épée géante !','s'],['Invincible !','x'],['Un cœur en plus !','h+']],
FM=[['Boue : tu es ralenti…','m'],['Sortilège : contrôles inversés…','i'],['Obscurité…','d'],['Lourdeur : sauts faibles…','h'],["Perte d'un cœur…",'-'],['Des chauves-souris surgissent…','b']];
function giveFx(good,pre){const a=good?FB:FM,o=a[Math.floor(Math.random()*a.length)],k=o[1];msg=(pre||'')+(good?'Boost : ':'Malédiction : ')+o[0];msgT=160;sfx(good?'boost':'malus',.3);mgc=good?'#9dff8a':'#ff7adf';burst(p.x+11,p.y+15,good?'#ffd93d':'#b455ff',34);flash(good?'rgba(255,230,120,.4)':'rgba(120,0,160,.45)',22);
 if(k=='x')p.inv=420;else if(k=='h+')hp=Math.min(hp+1,7);else if(k=='-')hurt('Malédiction !');
 else if(k=='b'){for(let i=0;i<3;i++){const bx=p.x+60+i*50;ents.push({k:'V',x:bx,y:p.y-80,x0:bx,y0:p.y-80,w:26,h:18,vx:1.2,vy:0,hp:1,inv:0})}}
 else fx={n:k,t:600,l:o[0]}}
function answer(i){
 if(st!='quiz')return;
 if(quiz.opts[i]==quiz.right){map[quiz.r][quiz.c]='.';qDone[lvl][quiz.c+','+quiz.r]=1;score+=200;lvScore+=200;jBuf=0;st='play';sfx('right');giveFx(1,'Bonne réponse ! +200 · ')}
 else{jBuf=0;st='play';sfx('wrong');giveFx(0,'Raté ! Réponse : '+quiz.right+'. ')}
}
function die(w,m){if(st!='play'&&st!='quiz')return;sfx('die');st='dying';dT=0;p.vx=0;p.vy=-11;p.inv=0;tries++;mode=m;dWhy=w;if(!m){score=lvScore;coins=lvCoins}}
function burst(x,y,c,n){for(let i=0;i<n;i++){const a=Math.random()*6.28,v=1+Math.random()*4;pt.push({x,y,vx:Math.cos(a)*v,vy:Math.sin(a)*v-2,l:40+Math.random()*20,c})}}
function flash(c,t){flc=c;fl=t}
function heart(x,y,s,c){g.fillStyle=c;g.beginPath();g.moveTo(x,y+s*.3);g.bezierCurveTo(x,y-s*.3,x-s*.6,y-s*.3,x-s*.6,y+s*.1);g.bezierCurveTo(x-s*.6,y+s*.5,x,y+s*.7,x,y+s);g.bezierCurveTo(x,y+s*.7,x+s*.6,y+s*.5,x+s*.6,y+s*.1);g.bezierCurveTo(x+s*.6,y-s*.3,x,y-s*.3,x,y+s*.3);g.fill()}
function hurt(w,pit){if(st!='play')return;if(!pit&&p.inv>0)return;hp--;sfx('hurt');burst(p.x+11,p.y+15,'#d62839',22);flash('rgba(214,40,57,.5)',16);sh=16;hl=50;mgc='#ff6b6b';
 if(hp<=0)return die(w+' Plus de cœurs : retour au début du niveau…',0);
 if(pit)return die(w+' Tu reprends à ton dernier appui.',1);
 p.inv=130;p.vy=-6;p.vx=-p.face*4;msg=w+' −1 ♥';msgT=70}
function update(){
 tick++;
 const L=K.ArrowLeft||K.KeyA||K.KeyQ||touch.l,R=K.ArrowRight||K.KeyD||touch.r,J=K.ArrowUp||K.KeyW||K.KeyZ||K.Space||touch.j;
 if(J&&!jPrev)jBuf=8;jPrev=J;if(jBuf>0)jBuf--;
 const tv=((R?1:0)-(L?1:0))*(fx.n=='i'?-1:1),spd=fx.n=='v'?5.4:fx.n=='m'?2:3.9;if(fx.t>0)fx.t--;else fx.n='';
 p.vx+=(tv*spd-p.vx)*.25+(LV[lvl].wind&&!p.on?Math.sin(tick/80)*.3:0);if(tv)p.face=tv;
 p.vy=Math.min(p.vy+.5,12);
 if(p.on)p.coy=6;else if(p.coy>0)p.coy--;
 if(jBuf>0&&p.coy>0){p.vy=fx.n=='j'?-13.5:fx.n=='h'?-8.2:-10.8;sfx('jump');p.coy=0;jBuf=0;p.on=false}
 if(!J&&p.vy<-4)p.vy=-4;
 box(p);
 if(hq){startQ(hq);hq=null;return}
 if(p.y>H+80)return hurt('Chute !',1);
 if(p.inv>0)p.inv--;if(p.on&&(map[Math.floor((p.y+p.h+1)/T)]||[])[Math.floor((p.x+p.w/2)/T)]!='C')safe={x:p.x,y:p.y};if(!chance&&p.x>rx+320)chance=true;
 for(let i=bul.length-1;i>=0;i--){const b=bul[i];b.x+=b.vx;b.y+=b.vy||0;if(ov(p,b)&&p.inv<=0)return hurt('Touché !');if(solid(Math.floor(b.x/T),Math.floor(b.y/T))||b.x<0||b.y>H||b.x>LV[lvl].w*T)bul.splice(i,1)}
 const X=K.KeyX||K.KeyK||K.KeyF||touch.x,xe=X&&!xPrev;if(xe&&p.sw<=0){p.sw=16;sfx('sword')}xPrev=X;
 if(p.lift>0)p.lift-=.02;
 if(LV[lvl].rain&&tick%LV[lvl].rain==0)bul.push({x:p.x+Math.random()*260-130,y:-40,w:10,h:34,vx:0,vy:5,f:1});
 if(p.on){const cc=Math.floor((p.x+p.w/2)/T),cr=Math.floor((p.y+p.h+1)/T),tb=(map[cr]||[])[cc];if(tb=='C'){const k=cc+','+cr;cz[k]=(cz[k]||0)+1;if(cz[k]>28)map[cr][cc]='.'}}
 {const pc=Math.floor(p.x/T),pr=Math.floor(p.y/T);for(let rr=pr-1;rr<=pr+1;rr++)for(let cc=pc-2;cc<=pc+2;cc++)if((map[rr]||[])[cc]=='N'){if(xe){map[rr][cc]='n';qDone[lvl][cc+','+rr]=1;sfx('talk');talk={t:LV[lvl].nt,ch:LV[lvl].ch};st='talk';return}msg='Presse X pour parler';mgc='#ffd38a';msgT=2}}if(p.sw>0)p.sw--;
 if(p.sw>6){const sl=fx.n=='s'?84:36,sb={x:p.face>0?p.x+p.w:p.x-sl,y:p.y+2,w:sl,h:26};bul=bul.filter(b=>!ov(sb,b));for(let i=ents.length-1;i>=0;i--){const e=ents[i];if(e.k=='W'||!ov(sb,e))continue;
  if(e.k=='M'){if(e.inv<=0){e.hp--;e.inv=45;if(e.hp<=0){score+=1000;ents.splice(i,1)}}}else{sfx('stomp');score+=e.k=='V'?150:100;ents.splice(i,1)}}}
 // coins, spikes, goal
 const c0=Math.floor(p.x/T),c1=Math.floor((p.x+p.w)/T),r0=Math.floor(p.y/T),r1=Math.floor((p.y+p.h)/T);
 for(let r=r0;r<=r1;r++)for(let c=c0;c<=c1;c++){
  const ch=(map[r]||[])[c];
  if(ch=='o'){map[r][c]='.';score+=10;coins++;sfx('coin')}
  else if(ch=='m'){map[r][c]='.';qDone[lvl][c+','+r]=1;startQ({c,r,m:1});return}
  else if(ch=='S'){const sb={x:c*T+6,y:r*T+8,w:20,h:24};if(ov(p,sb)&&p.inv<=0)return hurt('Piqué !')}
  else if(ch=='#G'){
   if(ents.some(e=>e.k=='M')){msg="Bats d'abord Méléagant !";msgT=90}
   else if(LV[lvl].lift&&p.lift<18){msg='Appuie vite sur X pour soulever la dalle !';msgT=2;if(xe)p.lift+=1.5}else{score+=500;st=lvl==LV.length-1?'win':'next';return}
  }
 }
 if(goal){const gx=goal.x+16,gy=goal.y+32;if(Math.abs(p.x+11-gx)<56&&Math.abs(p.y+15-gy)<72){
  mgc='#ffd38a';msgT=2;
  if(ents.some(e=>e.k=='M'))msg="Bats d'abord Méléagant !";
  else if(LV[lvl].lift){msg=p.lift>=17?'Dalle soulevée !':'Appuie vite sur X pour soulever la dalle !';if(xe){p.lift+=1.5;sfx('lift')}if(p.lift>=18)return clearLevel()}
  else{msg=lvl==5?'Presse X pour délivrer la reine':'Presse X pour passer au prochain niveau';if(xe)return clearLevel()}}}
 // enemies
 for(let i=ents.length-1;i>=0;i--){
  const e=ents[i];
  if(e.k=='V'||e.k=='W'){if(e.k=='W'){e.x+=Math.sign(p.x-e.x)*.55;e.y+=Math.sign(p.y-e.y)*.35}else{const near=Math.abs(p.x-e.x)<130;if(near)e.vx=(p.x>e.x?1:-1)*1.1;else if(Math.abs(e.x-e.x0)>90)e.vx=(e.x0>e.x?1:-1)*1.2;e.x+=e.vx;e.y+=((near?p.y-6:e.y0+Math.sin(tick/18+e.x0)*28)-e.y)*.06}
   if(ov(p,e,3)){if(e.k!='W'&&p.vy>0&&p.y+p.h-e.y<16){p.vy=-8.5;sfx('stomp');score+=150;ents.splice(i,1)}else if(p.inv<=0){if(e.k!='W')ents.splice(i,1);return hurt('Touché !')}}continue}
  e.vy=Math.min(e.vy+.5,12);if(e.inv>0)e.inv--;
  if(e.k=='M'&&tick%170==0&&Math.abs(p.x-e.x)<380)bul.push({x:e.x+e.w/2,y:e.y+20,w:14,h:6,vx:p.x<e.x?-3:3});
  e.ch=e.k=='E'&&Math.abs(p.x-e.x)<200&&Math.abs(p.y-e.y)<70;if(e.ch&&e.on)e.vx=Math.sign(p.x-e.x)||1;
  const dir=e.vx?Math.sign(e.vx):(e.d||-1);e.d=dir;const sp=e.k=='M'?1.5:(e.ch?1.3:.9);
  e.vx=dir*sp;
  const hit=box(e);if(!e.vx||hit)e.d=-dir;
  if(e.on){const fx=dir>0?e.x+e.w+2:e.x-2;if(!solid(Math.floor(fx/T),Math.floor((e.y+e.h+4)/T)))e.d=-dir}
  e.vx=e.d*sp;
  if(e.y>H+80){ents.splice(i,1);continue}
  if(ov(p,e,3)){
   if(p.vy>0&&p.y+p.h-e.y<18){
    p.vy=-8.5;sfx('stomp');
    if(e.inv<=0){e.hp--;e.inv=45;if(e.hp<=0){score+=e.k=='M'?1000:100;ents.splice(i,1)}}
   }else if(p.inv<=0&&(e.inv<=0||e.k!='M')){if(e.k!='M')ents.splice(i,1);return hurt('Aïe !')}
  }
 }
 camX=Math.max(0,Math.min(LV[lvl].w*T-W,p.x-W*.4));
 if(msgT>0)msgT--;
}
// ---- dessin ----
function sky(){
 const d=LV[lvl],gr=g.createLinearGradient(0,0,0,H);gr.addColorStop(0,d.sky[0]);gr.addColorStop(1,d.sky[1]);
 g.fillStyle=gr;g.fillRect(0,0,W,H);
 if(lvl==3){g.fillStyle='rgba(200,210,230,.14)';g.fillRect(0,230,W,220)}
 if([1,3,5].includes(lvl)){g.fillStyle='#fff';for(let i=0;i<30;i++)g.fillRect((i*97)%W,(i*53)%200,2,2)}
 if(lvl==4){g.fillStyle='#ffd38a';g.beginPath();g.arc(480,250,50,0,7);g.fill()}
 // silhouettes en parallaxe
 g.fillStyle=LV[lvl].hc;
 const o=-(camX*.3)%160;
 for(let x=o-160;x<W+160;x+=160){
  if(lvl==1||lvl==5){g.fillRect(x+20,260,120,190);for(let k=0;k<4;k++)g.fillRect(x+20+k*32,244,20,16);g.fillRect(x+70,200,22,60)}
  else{g.beginPath();g.moveTo(x,H);g.quadraticCurveTo(x+80,260,x+160,H);g.fill()}
 }
 if(lvl==0||lvl==2){g.fillStyle='#fff';[[80,60],[300,90],[520,50]].forEach(([x,y])=>{const cx=((x-camX*.15)%W+W)%W;g.fillRect(cx,y,70,14);g.fillRect(cx+14,y-10,40,12)})}
}
function tile(ch,c,r,x,y){
 if(ch=='#'){
  g.fillStyle=LV[lvl].gb;g.fillRect(x,y,T,T);
  if(!solid(c,r-1)){g.fillStyle=LV[lvl].gt;g.fillRect(x,y,T,8)}
  g.fillStyle='rgba(0,0,0,.18)';g.fillRect(x,y+T-2,T,2);g.fillRect(x+T-2,y,2,T);
 }else if(ch=='='){
  g.fillStyle=LV[lvl].bk;g.fillRect(x,y,T,T);g.fillStyle='rgba(0,0,0,.28)';
  g.fillRect(x,y+15,T,2);g.fillRect(x+15,y,2,15);g.fillRect(x+7,y+17,2,15);g.fillRect(x+23,y+17,2,15);
 }else if(ch=='C'){g.fillStyle='#8b7355';g.fillRect(x,y,T,14);g.fillStyle='#5e4a30';g.fillRect(x,y+10,T,4);g.fillRect(x+8,y,2,10);g.fillRect(x+20,y,2,10);
 }else if(ch=='m'){const b=Math.sin(tick/8+c)*4;g.fillStyle='rgba(255,230,140,.35)';g.beginPath();g.arc(x+16,y+16+b,16,0,7);g.fill();g.fillStyle='#ffe28a';g.font='bold 24px Georgia';g.textAlign='center';g.fillText('?',x+16,y+25+b);
 }else if(ch=='N'||ch=='n'){g.fillStyle=LV[lvl].nc||'#5a3a7a';g.fillRect(x+6,y-2,20,34);g.fillStyle='#f3c9a0';g.fillRect(x+10,y-14,12,12);g.fillStyle='#2a1d12';g.fillRect(x+8,y-17,16,5);
  if(ch=='N'){g.fillStyle='#ffe28a';g.font='bold 16px Georgia';g.textAlign='center';g.fillText('!',x+16,y-22+Math.sin(tick/8)*2)}
 }else if(ch=='B'){
  g.fillStyle='#c9d1d9';g.fillRect(x,y,T,12);g.fillStyle='#fff';g.fillRect(x,y,T,3);g.fillStyle='#7d8791';g.fillRect(x,y+9,T,3);
 }else if(ch=='o'){
  const b=Math.sin(tick/10+c)*3;g.strokeStyle='#ffc933';g.lineWidth=3;g.beginPath();g.arc(x+16,y+16+b,7,0,7);g.stroke();
  g.fillStyle='#ffe28a';g.fillRect(x+14,y+6+b,4,4);
 }else if(ch=='S'){
  g.fillStyle='#dfe6ee';[2,13,24].forEach(o=>{g.beginPath();g.moveTo(x+o,y+T);g.lineTo(x+o+3,y+10);g.lineTo(x+o+6,y+T);g.fill()});
  g.fillStyle='#8a5a32';g.fillRect(x,y+T-5,T,5);
 }else if(ch=='?'){
  g.fillStyle='#e8a317';g.fillRect(x,y,T,T);g.fillStyle='rgba(0,0,0,.3)';g.fillRect(x,y+T-3,T,3);g.fillRect(x+T-3,y,3,T);
  g.fillStyle='#fff6e0';g.font='bold 22px Georgia';g.textAlign='center';g.fillText('?',x+16,y+24+Math.sin(tick/8+c)*1.5);
 }else if(ch=='G'){
  if(LV[lvl].lift){g.fillStyle='#8d939c';g.fillRect(x-10,y+16,52,48);g.fillStyle='#b6bcc6';g.fillRect(x-14,y+8-p.lift*2,60,10);g.fillStyle='#55595f';g.fillRect(x+14,y+26,4,18);g.fillRect(x+8,y+31,16,4);return}
  if(lvl<5){g.fillStyle='#3b2a18';g.fillRect(x-2,y-8,36,72);g.fillStyle='#120a05';g.fillRect(x+2,y-4,28,68);g.fillStyle='#ffc933';g.fillRect(x+22,y+26,4,4);return}
  g.fillStyle='#d6336c';g.fillRect(x+6,y+24,20,40);g.fillStyle='#f3c9a0';g.fillRect(x+10,y+8,12,14);
  g.fillStyle='#e0a030';g.fillRect(x+9,y+4,14,6);g.fillRect(x+7,y+8,4,20);g.fillRect(x+21,y+8,4,20);
  g.fillRect(x+10,y-2,12,4);g.fillStyle='#ffe28a';g.fillRect(x+12,y-6,8,4);
 }
}
function knight(o,x,y,col,plume,shield,face){
 g.save();g.translate(x,y);
 g.fillStyle=col;g.fillRect(2,12,o.w-4,o.h-12);
 g.fillRect(4,0,o.w-8,13);
 g.fillStyle='#111';g.fillRect(face>0?o.w-12:4,5,8,3);
 g.fillStyle=plume;g.fillRect(o.w/2-2,-6,4,8);g.fillRect(o.w/2+(face>0?-6:2),-6,6,3);
 g.fillStyle=shield;const sx=face>0?o.w-9:-3;g.fillRect(sx,14,12,14);g.fillStyle='#fff';g.fillRect(sx+5,15,2,12);g.fillRect(sx+1,20,10,2);
 g.fillStyle='#333';g.fillRect(2,o.h-5,8,5);g.fillRect(o.w-10,o.h-5,8,5);
 g.restore();
}
function wrap(t,x,y,mw,lh){const w=t.split(' ');let l='';for(const s of w){if(g.measureText(l+s).width>mw){g.fillText(l,x,y);y+=lh;l=''}l+=s+' '}g.fillText(l,x,y)}
function panel(title,body,foot){
 g.fillStyle='rgba(20,10,5,.82)';g.fillRect(0,0,W,H);
 g.fillStyle='#ffd38a';g.textAlign='center';g.font='bold 30px Georgia';wrap(title,W/2,130,W-80,36);
 g.fillStyle='#fff6e0';g.font='17px Georgia';wrap(body,W/2,200,W-120,26);
 g.fillStyle='#ffc933';g.font='italic 16px Georgia';g.fillText(foot,W/2,400);
}
function draw(){
 g.textAlign='left';
 if(st=='title'){sky();panel("Lancelot et la Charrette","D'après le roman de Chrétien de Troyes. Traverse la plaine, le Pont de l'Épée et le château de Gorre pour délivrer la reine Guenièvre.","Appuie sur Entrée ou touche l'écran pour commencer");return}
 if(st=='intro'){sky();panel(LV[lvl].n,LV[lvl].t,"Entrée ou touche l'écran pour jouer");return}
 if(st=='over'){sky();panel("Lancelot est tombé","La reine attend toujours son chevalier… Ton score : "+score,"Entrée ou touche l'écran pour recommencer");return}
 if(st=='win'){sky();panel("Guenièvre est libre !","Lancelot a vaincu Méléagant et surmonté la honte de la charrette. Score final : "+score,"Entrée ou touche l'écran pour rejouer");return}
 g.save();if(sh>0)g.translate((Math.random()-.5)*sh*.8,(Math.random()-.5)*sh*.8);sky();
 const c0=Math.floor(camX/T),c1=c0+Math.ceil(W/T)+1;
 for(let r=0;r<14;r++)for(let c=c0;c<=c1;c++){const ch=(map[r]||[])[c];if(ch&&ch!='.')tile(ch,c,r,c*T-Math.floor(camX),r*T)}
 // charrette (décor de départ)
 const cx=2*T-24-camX;if(cx>-120){g.fillStyle='#6b4423';g.fillRect(cx,12*T-26,56,16);g.fillStyle='#3b2a18';g.beginPath();g.arc(cx+14,12*T-6,8,0,7);g.arc(cx+44,12*T-6,8,0,7);g.fill();g.fillRect(cx+54,12*T-20,26,4)}
 ents.forEach(e=>{
  if(e.inv>0&&tick%6<3)return;
  if(e.k=='W'){const gx=Math.floor(e.x-camX),gy=Math.floor(e.y);g.globalAlpha=.7;g.fillStyle='#cfe3ff';g.fillRect(gx+2,gy,20,26);g.fillRect(gx,gy+20,24,10);g.fillStyle='#111';g.fillRect(gx+6,gy+7,4,5);g.fillRect(gx+14,gy+7,4,5);g.globalAlpha=1;return}
  if(e.k=='V'){const bx=Math.floor(e.x-camX),by=Math.floor(e.y),f=Math.sin(tick/3)*6;g.fillStyle='#2a1a3a';g.fillRect(bx+8,by+4,10,12);g.fillRect(bx-6,by+4+f,14,4);g.fillRect(bx+18,by+4+f,14,4);g.fillStyle='#ff4d4d';g.fillRect(bx+10,by+7,2,2);g.fillRect(bx+14,by+7,2,2);return}
  const x=Math.floor(e.x-camX),y=Math.floor(e.y);
  if(e.k=='M')knight(e,x,y,'#2b2b3a','#7a1f2b','#7a1f2b',e.d||-1);else knight(e,x,y,'#5a4a4a','#222','#444',e.d||-1);
 });
 bul.forEach(b=>{const bx=Math.floor(b.x-camX),by=Math.floor(b.y);g.fillStyle=b.f?'#ff7a1a':'#e8f0ff';g.fillRect(bx,by,b.w,b.h);g.fillStyle='#8a5a32';g.fillRect(bx+(b.vx>0?0:b.w-4),by,4,b.h)});
 if(!(p.inv>0&&tick%6<3))knight(p,Math.floor(p.x-camX),Math.floor(p.y),'#cfd6de','#d62839','#2a5db0',p.face);
 if(p.sw>6){const sx=Math.floor(p.x-camX),bx=p.face>0?sx+p.w:sx-36,by=Math.floor(p.y)+10;g.fillStyle='#e8f0ff';g.fillRect(bx,by,36,5);g.fillStyle='#9fb3c8';g.fillRect(bx,by+5,36,2)}
 pt.forEach(q=>{g.globalAlpha=Math.min(1,q.l/25);g.fillStyle=q.c;g.fillRect(Math.floor(q.x-camX),Math.floor(q.y),5,5)});g.globalAlpha=1;g.restore();
 if(fx.n=='d'){const px=Math.floor(p.x-camX)+11,gr=g.createRadialGradient(px,p.y+15,50,px,p.y+15,170);gr.addColorStop(0,'rgba(0,0,0,0)');gr.addColorStop(1,'rgba(0,0,0,.95)');g.fillStyle=gr;g.fillRect(0,0,W,H)}
 // HUD
 g.fillStyle='rgba(0,0,0,.5)';g.fillRect(0,0,W,44);
 g.fillStyle='#fff6e0';g.font='bold 15px Georgia';g.textAlign='left';for(let i=0;i<Math.max(5,hp);i++){const x=24+i*34;if(i<hp)heart(x,7,28+(hp<=2?Math.sin(tick/4)*3:0),'#ff3b50');else if(i==hp&&hl>0)heart(x,7+(50-hl)*1.4,Math.max(4,28*hl/50),'rgba(255,59,80,'+hl/50+')');else heart(x,7,28,'rgba(255,255,255,.18)')}
 g.textAlign='center';g.fillText(LV[lvl].n,W/2,19);g.textAlign='right';g.fillText('Mèches : '+coins+'   Score : '+score,W-10,19);
 if(fx.n){g.textAlign='left';g.font='13px Georgia';g.fillText(fx.l+' '+Math.ceil(fx.t/60)+' s',10,62)}
 if(p.lift>0){g.fillStyle='#333';g.fillRect(200,130,240,14);g.fillStyle='#ffc933';g.fillRect(200,130,240*Math.min(p.lift/18,1),14)}
 if(msgT>0){g.textAlign='center';g.font='bold 18px Georgia';g.fillStyle=mgc||'#ffd38a';wrap(msg,W/2,92,W-40,22)}
 if(fl>0){g.fillStyle=flc;g.globalAlpha=Math.min(1,fl/10);g.fillRect(0,0,W,H);g.globalAlpha=1}
 if(st=='dying'){g.fillStyle='rgba(20,10,5,.7)';g.fillRect(0,64,W,96);g.fillStyle='#ffd38a';g.textAlign='center';g.font='bold 18px Georgia';wrap(dWhy||'Aïe ! Retour au début du niveau…',W/2,92,W-60,24)}
 if(st=='quiz'){g.fillStyle='rgba(20,10,5,.9)';g.fillRect(0,0,W,H);g.textAlign='center';g.fillStyle='#ffd38a';g.font='bold 20px Georgia';wrap(quiz.q,W/2,80,W-100,28);
  quiz.opts.forEach((o,i)=>{const y=190+i*66;g.fillStyle='#7a1f2b';g.fillRect(40,y,W-80,54);g.fillStyle='#fff6e0';g.font='16px Georgia';g.textAlign='left';wrap((i+1)+'. '+o,56,y+23,W-110,20)});
  g.textAlign='center';g.fillStyle='#ffc933';g.font='italic 14px Georgia';g.fillText('Touche une réponse ou appuie sur 1, 2 ou 3. Une erreur déclenche une malédiction.',W/2,420)}
 if(st=='talk'){g.fillStyle='rgba(20,10,5,.94)';g.fillRect(20,150,W-40,285);g.strokeStyle='#ffd38a';g.strokeRect(20,150,W-40,285);g.fillStyle='#fff6e0';g.textAlign='left';g.font='17px Georgia';wrap(talk.t,40,185,W-80,26);
  talk.ch.forEach((o,i)=>{const y=320+i*46;g.fillStyle='#7a1f2b';g.fillRect(40,y,W-80,38);g.fillStyle='#fff6e0';g.font='16px Georgia';g.textAlign='left';g.fillText((i+1)+'. '+o[0],54,y+24)});
  g.fillStyle='#ffc933';g.font='italic 13px Georgia';g.fillText('Fais ton choix : touche une réponse ou appuie sur 1 ou 2',40,424)}
 if(st=='clear'){const k=Math.min(1,dT/18),bn=1+Math.sin(dT/6)*.04;g.save();g.translate(W/2,190);g.scale(k*bn,k*bn);g.textAlign='center';g.lineWidth=8;g.strokeStyle='#7a1f2b';g.font='bold 58px Georgia';g.strokeText('NIVEAU PASSÉ !',0,0);g.fillStyle='#ffd38a';g.fillText('NIVEAU PASSÉ !',0,0);g.restore();g.textAlign='center';g.fillStyle='#fff6e0';g.font='bold 20px Georgia';g.fillText('Score : '+score+'   Mèches : '+coins,W/2,250)}
 if(st=='next'){panel("Niveau réussi !","Score : "+score,"Entrée ou touche l'écran pour continuer")}
}
let AC=null,muted=false,mT=0,mStep=0;
function ac(){if(!AC){try{AC=new(window.AudioContext||window.webkitAudioContext)()}catch(e){}}
 if(AC){if(AC.state=='suspended')AC.resume();if(!mT){mT=1;mloop()}}return AC}
function toggleMute(){muted=!muted;document.getElementById('mu').textContent=muted?'🔇 Son coupé (M)':'🔊 Son (M)'}
document.getElementById('mu').addEventListener('pointerdown',e=>{e.preventDefault();ac();toggleMute()});
addEventListener('pointerdown',()=>ac());
function tone(f,t0,d,type,v,f2){const a=AC;if(!a||muted)return;try{const o=a.createOscillator(),gn=a.createGain(),t=a.currentTime+t0;o.type=type||'square';o.frequency.setValueAtTime(f,t);if(f2)o.frequency.exponentialRampToValueAtTime(f2,t+d);gn.gain.setValueAtTime(v||.08,t);gn.gain.exponentialRampToValueAtTime(.0001,t+d);o.connect(gn);gn.connect(a.destination);o.start(t);o.stop(t+d+.02)}catch(e){}}
function noise(t0,d,v){const a=AC;if(!a||muted)return;try{const n=Math.floor(a.sampleRate*d),b=a.createBuffer(1,n,a.sampleRate),dt=b.getChannelData(0);for(let i=0;i<n;i++)dt[i]=(Math.random()*2-1)*(1-i/n);const s=a.createBufferSource(),gn=a.createGain();s.buffer=b;gn.gain.value=v||.1;s.connect(gn);gn.connect(a.destination);s.start(a.currentTime+t0)}catch(e){}}
const N=m=>440*Math.pow(2,(m-69)/12);
function sfx(n,d){d=d||0;
 switch(n){
 case 'jump':tone(300,d,.18,'triangle',.12,700);break;
 case 'sword':noise(d,.12,.12);tone(900,d,.1,'sawtooth',.04,200);break;
 case 'hurt':tone(260,d,.3,'sawtooth',.12,70);noise(d,.15,.1);break;
 case 'die':[0,1,2,3,4].forEach(i=>tone(N(67-i*3),d+i*.12,.2,'square',.09));break;
 case 'coin':tone(N(79),d,.07,'sine',.12);tone(N(86),d+.07,.18,'sine',.1);break;
 case 'stomp':tone(160,d,.12,'square',.12,60);break;
 case 'boost':[60,64,67,72,76].forEach((m,i)=>tone(N(m),d+i*.07,.2,'triangle',.11));break;
 case 'malus':tone(N(60),d,.25,'sawtooth',.1,N(54));tone(N(54),d+.2,.35,'sawtooth',.1,N(47));break;
 case 'right':[62,66,69,74].forEach((m,i)=>tone(N(m),d+i*.09,.18,'sine',.13));break;
 case 'wrong':tone(150,d,.25,'square',.1);tone(110,d+.2,.35,'square',.1);break;
 case 'ask':tone(N(76),d,.1,'sine',.1);tone(N(81),d+.1,.15,'sine',.1);break;
 case 'talk':tone(520,d,.06,'triangle',.1);tone(620,d+.06,.08,'triangle',.1);break;
 case 'pick':tone(N(72),d,.08,'triangle',.12);tone(N(79),d+.08,.12,'triangle',.12);break;
 case 'lift':tone(110,d,.12,'square',.1,80);noise(d,.08,.08);break;
 case 'clear':[62,66,69,74,69,74,78,81].forEach((m,i)=>tone(N(m),d+i*.13,.25,'triangle',.13));break;
 }}
const MO=[[0,2,3,5,7,9,10],[0,2,3,5,7,8,10],[0,2,4,5,7,9,11],[0,1,3,5,7,8,10],[0,2,3,5,7,8,11],[0,1,3,5,6,8,10]],
MU=[[50,300],[45,340],[55,270],[43,430],[52,210],[47,250]],IDX=[0,2,4,2,5,4,2,0,1,3,5,3,6,5,3,1];
function mloop(){try{if(!muted&&AC&&st!='title'){const l=Math.min(lvl,5),m=MU[l],mo=MO[l],i=IDX[mStep%16];
 tone(N(m[0]+12+mo[i%7]+12*Math.floor(i/7)),0,.3,'triangle',.045);
 if(mStep%4==0)tone(N(m[0]-12+mo[[0,3,4,2][(mStep>>2)%4]]),0,.55,'sine',.06);mStep++}}catch(e){}
 setTimeout(mloop,(MU[Math.min(lvl,5)]||MU[0])[1])}
let last=0,acc=0;
function loop(t){
 const dt=Math.min(100,t-last);last=t;acc+=dt;
 while(acc>=16.67){acc-=16.67;try{pt.forEach(q=>{q.x+=q.vx;q.y+=q.vy;q.vy+=.15;q.l--});pt=pt.filter(q=>q.l>0);if(fl>0)fl--;if(sh>0)sh--;if(hl>0)hl--;if(st=='play')update();else if(st=='clear'){dT++;tick++;if(dT%10==0)burst(camX+80+Math.random()*480,60+Math.random()*180,['#ffd93d','#ff5d73','#6ee7ff','#9dff8a'][dT%4],26);if(dT>180){if(lvl==LV.length-1)st='win';else{lvl++;st='intro'}}}else if(st=='dying'){dT++;tick++;p.vy+=.5;p.y+=p.vy;if(dT>75){if(mode==1){p.x=safe.x;p.y=safe.y;p.vx=0;p.vy=0;p.inv=140;rx=p.x;jBuf=0;st='play'}else{load();st='play'}}}else tick++}catch(e){console.error(e)}}
 try{draw()}catch(e){g.restore();console.error(e)}requestAnimationFrame(loop);
}
requestAnimationFrame(loop);
</script>
</body>
</html>

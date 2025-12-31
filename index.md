<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy New Year 2026 🎉</title>

<style>
*{margin:0;padding:0;box-sizing:border-box}

body{
    height:100vh;
    overflow:hidden;
    font-family:Arial,Helvetica,sans-serif;
    background:linear-gradient(135deg,#1a0033,#4a0080,#1a0033);
    background-size:400% 400%;
    animation:bg 12s ease infinite;
    color:white;
    cursor:crosshair;
}

@keyframes bg{
    0%,100%{background-position:0% 50%}
    50%{background-position:100% 50%}
}

.center{
    position:absolute;
    top:50%;
    left:50%;
    transform:translate(-50%,-50%);
    text-align:center;
    pointer-events:none;
}

h1{
    font-size:5rem;
    text-shadow:0 0 30px white;
}

.year{
    font-size:10rem;
    font-weight:bold;
    background:linear-gradient(45deg,#ffd700,#ff6b6b,#ffd700);
    -webkit-background-clip:text;
    -webkit-text-fill-color:transparent;
    animation:float 4s ease-in-out infinite;
}

@keyframes float{
    0%,100%{transform:translateY(0)}
    50%{transform:translateY(-20px)}
}

.controls{
    position:fixed;
    top:20px;
    left:20px;
    display:flex;
    flex-direction:column;
    gap:10px;
    z-index:99;
}

button{
    padding:12px 18px;
    border-radius:10px;
    border:none;
    font-weight:bold;
    cursor:pointer;
    background:rgba(255,255,255,0.2);
    color:white;
    backdrop-filter:blur(10px);
    transition:0.3s;
}

button:hover{transform:scale(1.08)}

.firework{
    position:fixed;
    pointer-events:none;
}

.particle{
    position:absolute;
    width:5px;
    height:5px;
    border-radius:50%;
}

.confetti{
    position:fixed;
    width:10px;
    height:10px;
    top:-10px;
    animation:fall linear forwards;
}

@keyframes fall{
    to{transform:translateY(110vh) rotate(360deg)}
}

/* Share */
.share-btn{
    position:fixed;
    bottom:60px;
    right:20px;
    background:linear-gradient(135deg,#ff6a00,#ee0979);
    box-shadow:0 0 20px rgba(255,105,180,.6);
    z-index:100;
}

.share-menu{
    position:fixed;
    bottom:120px;
    right:20px;
    background:rgba(0,0,0,.85);
    padding:15px;
    border-radius:15px;
    display:none;
    flex-direction:column;
    gap:10px;
    z-index:101;
}

.share-menu button{
    background:#ffd700;
    color:black;
}

/* CREDITS */
.credits{
    position:fixed;
    bottom:10px;
    left:50%;
    transform:translateX(-50%);
    background:rgba(0,0,0,0.6);
    padding:8px 18px;
    border-radius:20px;
    font-size:0.85rem;
    color:rgba(255,255,255,0.8);
    backdrop-filter:blur(10px);
    pointer-events:none;
    z-index:100;
}

.credits span{
    color:#ffd700;
    font-weight:bold;
    text-shadow:0 0 6px rgba(255,215,0,0.6);
}

@media(max-width:768px){
    h1{font-size:3rem}
    .year{font-size:6rem}
    .credits{font-size:0.7rem}
}
</style>
</head>

<body>

<div class="controls">
    <button onclick="megaFireworks()">🎆 Fireworks</button>
    <button onclick="confettiBomb()">🎉 Confetti</button>
    <button onclick="toggleSound()">🔊 Sound</button>
</div>

<div class="center">
    <h1>HAPPY</h1>
    <div class="year">2026</div>
    <h1>NEW YEAR 🎊</h1>
</div>

<button class="share-btn" onclick="toggleShare()">🔗 SHARE</button>

<div class="share-menu" id="shareMenu">
    <button onclick="shareWhatsApp()">📱 WhatsApp</button>
    <button onclick="shareNative()">🌐 Share</button>
    <button onclick="copyLink()">📋 Copy Link</button>
    <button onclick="toggleShare()">❌ Close</button>
</div>

<!-- ✅ CREDITS (VISIBLE AT END) -->
<div class="credits">
    From <span>Ajitesh Shirodkar</span> made in collab with <span>Claude</span> and <span>ChatGPT</span>
</div>

<script>
const colors=["#ff0000","#00ff00","#00ffff","#ffd700","#ff69b4","#ff4500"];
let sound=true;
const ctx=new (window.AudioContext||window.webkitAudioContext)();

function beep(f,d){
    if(!sound) return;
    const o=ctx.createOscillator();
    const g=ctx.createGain();
    o.connect(g);g.connect(ctx.destination);
    o.frequency.value=f;
    g.gain.setValueAtTime(.3,ctx.currentTime);
    g.gain.exponentialRampToValueAtTime(.01,ctx.currentTime+d);
    o.start();o.stop(ctx.currentTime+d);
}

function firework(x,y){
    const fw=document.createElement("div");
    fw.className="firework";
    fw.style.left=x+"px";
    fw.style.top=y+"px";
    document.body.appendChild(fw);
    const c=colors[Math.random()*colors.length|0];
    for(let i=0;i<40;i++){
        const p=document.createElement("div");
        p.className="particle";
        p.style.background=c;
        const a=Math.PI*2*i/40;
        const d=120+Math.random()*80;
        p.style.transform=`translate(${Math.cos(a)*d}px,${Math.sin(a)*d}px)`;
        p.style.transition="1.5s";
        fw.appendChild(p);
    }
    setTimeout(()=>fw.remove(),1500);
}

document.addEventListener("click",e=>{
    firework(e.clientX,e.clientY);
    beep(700,0.1);
});

function megaFireworks(){
    for(let i=0;i<20;i++){
        setTimeout(()=>{
            firework(Math.random()*innerWidth,Math.random()*innerHeight*0.7);
            beep(500+Math.random()*500,0.15);
        },i*120);
    }
}

function confettiBomb(){
    for(let i=0;i<100;i++){
        setTimeout(()=>{
            const c=document.createElement("div");
            c.className="confetti";
            c.style.left=Math.random()*100+"%";
            c.style.background=colors[Math.random()*colors.length|0];
            c.style.animationDuration=2+Math.random()*3+"s";
            document.body.appendChild(c);
            setTimeout(()=>c.remove(),5000);
        },i*20);
    }
    beep(400,0.3);
}

function toggleSound(){sound=!sound}

setInterval(()=>{
    firework(Math.random()*innerWidth,Math.random()*innerHeight*0.6);
},1200);

/* SHARE */
function toggleShare(){
    const m=document.getElementById("shareMenu");
    m.style.display=m.style.display==="flex"?"none":"flex";
}

function shareWhatsApp(){
    const t=encodeURIComponent("🎉 Happy New Year 2026! 🎆\n"+location.href);
    open(`https://wa.me/?text=${t}`,"_blank");
    confettiBomb();
}

function shareNative(){
    if(navigator.share){
        navigator.share({
            title:"Happy New Year 2026",
            text:"Check this New Year celebration!",
            url:location.href
        });
        confettiBomb();
    } else alert("Not supported");
}

function copyLink(){
    navigator.clipboard.writeText(location.href);
    alert("Link copied!");
    confettiBomb();
}
</script>

</body>
</html>

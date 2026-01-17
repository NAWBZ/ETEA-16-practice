# ETEA-16-

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ETEA Practice Test</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
<style>
body{font-family:'Poppins',sans-serif;background:linear-gradient(135deg,#ff9a9e,#fecfef);margin:0}
.container{max-width:900px;margin:20px auto;background:#fff;padding:30px;border-radius:20px;box-shadow:0 10px 30px rgba(0,0,0,.2)}
h2{text-align:center}
.center{text-align:center}
input{width:100%;padding:12px;margin-bottom:15px;border-radius:10px;border:2px solid #ddd}
button{padding:12px;border:none;border-radius:10px;font-size:16px;font-weight:bold;cursor:pointer;margin:5px}
#startBtn{background:#2980b9;color:#fff;width:100%}
#timer{background:#e74c3c;color:#fff;padding:15px;text-align:center;border-radius:10px}
.option{border:2px solid #ddd;padding:15px;border-radius:10px;margin-bottom:12px;cursor:pointer}
.option.correct{background:#2980b9;color:#fff}
.option.wrong{background:#e74c3c;color:#fff}
.buttons{display:flex;justify-content:space-between}
#submitBtn{display:none;background:#27ae60;color:white;width:100%}
.subject-box{background:#f4f6f7;padding:12px;border-radius:10px;margin:8px 0}
.review-option.correct{background:#2980b9;color:#fff;padding:8px;border-radius:8px;margin:4px 0}
.review-option.wrong{background:#e74c3c;color:#fff;padding:8px;border-radius:8px;margin:4px 0}
.footer{text-align:center;color:#555;margin:20px 0;font-size:14px}
</style>
</head>
<body>

<!-- LOGIN -->
<div class="container center" id="loginDiv">
<h2>ETEA Practice Test</h2>
<input id="studentName" placeholder="Student Name">
<input id="rollNo" placeholder="Roll Number">
<button id="startBtn" onclick="startCountdown()">Start Test</button>
<div id="countdown" style="font-size:28px;color:red"></div>
</div>

<!-- QUIZ -->
<div class="container" id="quizDiv" style="display:none">
<div id="timer">Time Left: 40:00</div>
<div id="questionBox"></div>
<div id="optionsBox"></div>
<div class="buttons">
<button onclick="prevQ()">Previous</button>
<button onclick="skipQ()">Skip</button>
<button onclick="nextQ()" id="nextBtn" disabled>Next</button>
</div>
<button id="submitBtn" onclick="submitTest()">Submit Test</button>
</div>

<!-- RESULT -->
<div class="container center" id="resultDiv" style="display:none">
<h2 id="resStatus"></h2>
<p id="resScore"></p>
<p id="resTime"></p>

<h3>Subject-Wise Result</h3>
<div id="subjectResult"></div>

<button onclick="showReview()">Review Test</button>
<button onclick="location.reload()">Restart</button>
</div>

<!-- REVIEW -->
<div class="container" id="reviewDiv" style="display:none">
<h2 class="center">Test Review</h2>
<div id="reviewContent"></div>
<button onclick="backToResult()">Back to Result</button>
</div>

<div class="footer">
Created by <b>MUHAMMAD FAIZAN NAWAB</b>
</div>

<script>
// ==========================
// 3 MCQs (TEST)
// ==========================

const questions = [


/* BIOLOGY (1–35) */

{subject:"Biology", q:"The process by which pollen grains reach the stigma is known as:", o:["Fertilization","Germination","Pollination","Reproduction"], c:2},
{subject:"Biology", q:"Which part of the flower develops into fruit after fertilization?", o:["Ovule","Ovary","Stigma","Style"], c:1},
{subject:"Biology", q:"The male reproductive organ of a flower consists of:", o:["Ovary and ovule","Anther and filament","Stigma and style","Sepal and petal"], c:1},
{subject:"Biology", q:"Which of the following is an example of asexual reproduction?", o:["Seed formation","Pollination","Cutting","Fertilization"], c:2},
{subject:"Biology", q:"Bryophyllum reproduces through:", o:["Roots","Seeds","Leaf buds","Flowers"], c:2},
{subject:"Biology", q:"Which structure contains the female gamete?", o:["Anther","Ovule","Stigma","Filament"], c:1},
{subject:"Biology", q:"Fertilization occurs when:", o:["Pollen grain lands on stigma","Ovule enters ovary","Male and female gametes fuse","Seed coat hardens"], c:2},
{subject:"Biology", q:"Vegetative propagation results in offspring that are:", o:["Genetically different","Genetically identical","Weak","Sterile"], c:1},
{subject:"Biology", q:"Which plant reproduces by tuber?", o:["Onion","Ginger","Potato","Carrot"], c:2},
{subject:"Biology", q:"The transfer of pollen within the same flower is called:", o:["Cross-pollination","Artificial pollination","Self-pollination","Fertilization"], c:2},
{subject:"Biology", q:"Which agent of pollination is MOST common?", o:["Roots","Wind","Soil","Minerals"], c:1},
{subject:"Biology", q:"Seeds are dispersed by wind in:", o:["Coconut","Cotton","Pea","Mango"], c:1},
{subject:"Biology", q:"Which of the following is NOT a method of vegetative reproduction?", o:["Cutting","Layering","Grafting","Pollination"], c:3},
{subject:"Biology", q:"After fertilization, ovule develops into:", o:["Seed","Fruit","Flower","Root"], c:0},
{subject:"Biology", q:"Which plant reproduces through runners?", o:["Potato","Strawberry","Onion","Ginger"], c:1},
{subject:"Biology", q:"Which reproductive method causes variation?", o:["Cutting","Layering","Sexual reproduction","Grafting"], c:2},
{subject:"Biology", q:"The female reproductive part of a flower is called:", o:["Stamen","Pistil","Sepal","Anther"], c:1},
{subject:"Biology", q:"Which part of seed protects the embryo?", o:["Cotyledon","Plumule","Seed coat","Radicle"], c:2},
{subject:"Biology", q:"Which structure receives pollen grains?", o:["Style","Stigma","Ovary","Ovule"], c:1},
{subject:"Biology", q:"Which plant reproduces by bulbs?", o:["Potato","Onion","Carrot","Radish"], c:1},
{subject:"Biology", q:"Artificial vegetative reproduction is used to:", o:["Reduce yield","Increase variation","Produce healthy plants","Stop growth"], c:2},
{subject:"Biology", q:"Which of the following is NOT required for germination?", o:["Water","Oxygen","Light","Suitable temperature"], c:2},
{subject:"Biology", q:"The process of seed formation occurs after:", o:["Pollination","Fertilization","Germination","Dispersal"], c:1},
{subject:"Biology", q:"Which part connects stigma to ovary?", o:["Filament","Sepal","Style","Anther"], c:2},
{subject:"Biology", q:"Pollen grains are produced in:", o:["Stigma","Ovule","Anther","Ovary"], c:2},
{subject:"Biology", q:"Which reproduction method is fastest?", o:["Sexual","Seed germination","Vegetative","Pollination"], c:2},
{subject:"Biology", q:"Which plant reproduces by rhizome?", o:["Ginger","Onion","Potato","Pea"], c:0},
{subject:"Biology", q:"Which of these ensures survival of species?", o:["Germination","Reproduction","Pollination","Dispersal"], c:1},
{subject:"Biology", q:"Which is NOT a flowering plant?", o:["Rose","Sunflower","Fern","Pea"], c:2},
{subject:"Biology", q:"Which part stores food in seed?", o:["Cotyledon","Radicle","Plumule","Seed coat"], c:0},
{subject:"Biology", q:"In which type of reproduction seeds are formed?", o:["Asexual","Vegetative","Sexual","Artificial"], c:2},
{subject:"Biology", q:"The young plant inside seed is called:", o:["Bud","Embryo","Root","Shoot"], c:1},
{subject:"Biology", q:"Which of the following is bisexual flower?", o:["Papaya","Mustard","Maize","Date palm"], c:1},
{subject:"Biology", q:"Seed dispersal helps in:", o:["Competition","Overcrowding","Survival","Germination"], c:2},
{subject:"Biology", q:"Which method is used to grow seedless fruits?", o:["Sexual reproduction","Pollination","Vegetative propagation","Germination"], c:2},
{subject:"Mathematics", q:"Simplify the ratio 18 : 24", o:["2 : 3","3 : 4","4 : 3","6 : 8"], c:0},
{subject:"Mathematics", q:"If 5 pens cost Rs. 50, cost of one pen is:", o:["Rs. 8","Rs. 9","Rs. 10","Rs. 12"], c:2},
{subject:"Mathematics", q:"Convert 25% into fraction:", o:["1/2","1/3","1/4","1/5"], c:2},
{subject:"Mathematics", q:"The ratio of 2 kg to 500 g is:", o:["2 : 5","4 : 1","1 : 4","5 : 2"], c:1},
{subject:"Mathematics", q:"40% of 200 is:", o:["60","70","80","90"], c:2},
{subject:"Mathematics", q:"If distance = 120 km and time = 3 h, find speed:", o:["30 km/h","40 km/h","50 km/h","60 km/h"], c:1},
{subject:"Mathematics", q:"Increase 150 by 20%", o:["170","175","180","185"], c:2},
{subject:"Mathematics", q:"Reduce the ratio 3.5 : 7", o:["1 : 2","2 : 1","7 : 3","3 : 2"], c:0},
{subject:"Mathematics", q:"What percent is 30 of 120?", o:["20%","25%","30%","35%"], c:1},
{subject:"Mathematics", q:"A man earns Rs. 900 in 9 days. His daily earning is:", o:["Rs. 80","Rs. 90","Rs. 100","Rs. 110"], c:2},
{subject:"Mathematics", q:"Convert 0.2 into percentage:", o:["2%","20%","200%","0.2%"], c:1},
{subject:"Mathematics", q:"Ratio of 45 minutes to 1 hour is:", o:["3 : 4","4 : 3","45 : 60","1 : 2"], c:0},
{subject:"Mathematics", q:"12.5% equals:", o:["1/6","1/7","1/8","1/10"], c:2},
{subject:"Mathematics", q:"If 60% of a number is 180, the number is:", o:["240","260","300","320"], c:0},
{subject:"Mathematics", q:"Which ratio is equivalent to 6 : 9?", o:["3 : 2","2 : 3","9 : 6","1 : 3"], c:1},
{subject:"Mathematics", q:"Decrease 500 by 10%", o:["440","450","460","480"], c:1},
{subject:"Mathematics", q:"Speed of a cyclist who covers 15 km in 30 minutes is:", o:["20 km/h","25 km/h","30 km/h","35 km/h"], c:2},
{subject:"Mathematics", q:"Convert 3/5 into percentage:", o:["50%","60%","65%","75%"], c:1},
{subject:"Mathematics", q:"The ratio of boys to girls is 7 : 8. If boys are 28, girls are:", o:["30","32","34","36"], c:1},
{subject:"Mathematics", q:"What is 5% of 400?", o:["10","15","20","25"], c:2},
{subject:"Mathematics", q:"Simplify 2.4 : 3.6", o:["2 : 3","3 : 2","4 : 6","6 : 4"], c:0},
{subject:"Mathematics", q:"A car covers 300 km in 5 hours. Speed is:", o:["50 km/h","55 km/h","60 km/h","65 km/h"], c:2},
{subject:"Mathematics", q:"Which is greater: 25% or 1/3?", o:["25%","1/3","Equal","Cannot be compared"], c:1},
{subject:"Mathematics", q:"150 is what percent of 600?", o:["20%","25%","30%","35%"], c:1},
{subject:"Mathematics", q:"If ratio of red to blue balls is 4 : 5 and total balls are 45, red balls are:", o:["18","20","24","25"], c:0},
{subject:"Mathematics", q:"Convert 75% into decimal:", o:["0.75","7.5","0.075","75"], c:0},
{subject:"Mathematics", q:"A worker earns Rs. 240 in 8 hours. Rate per hour is:", o:["25","30","35","40"], c:1},
{subject:"Mathematics", q:"Which is the simplest form of 10 : 15?", o:["5 : 3","3 : 2","2 : 3","15 : 10"], c:2},
{subject:"Mathematics", q:"1/5 of a number is 40. Number is:", o:["150","180","200","240"], c:2},
{subject:"Mathematics", q:"Convert 0.125 into fraction:", o:["1/4","1/6","1/8","1/10"], c:2},
{subject:"Mathematics", q:"Increase 80 by 25%", o:["90","95","100","105"], c:2},
{subject:"Mathematics", q:"Speed is measured in:", o:["km","hour","km/h","m"], c:2},
{subject:"Mathematics", q:"3 : 4 is equivalent to:", o:["6 : 7","9 : 12","12 : 9","8 : 5"], c:1},
{subject:"Mathematics", q:"What percent of 50 is 5?", o:["5%","8%","10%","15%"], c:2},
{subject:"Mathematics", q:"If distance is doubled and time remains same, speed will:", o:["Decrease","Remain same","Double","Become half"], c:2},
{subject:"English", q:"The book is ___ the table.", o:["in","on","at","under"], c:1},
{subject:"English", q:"He has been living here ___ 2015.", o:["for","since","from","by"], c:1},
{subject:"English", q:"She ___ her work before sunset.", o:["completes","completed","had completed","will complete"], c:2},
{subject:"English", q:"The cat jumped ___ the wall.", o:["in","on","over","at"], c:2},
{subject:"English", q:"We were waiting ___ the bus stop ___ an hour.", o:["on, since","at, for","in, by","from, for"], c:1},
{subject:"English", q:"By next year, he ___ ten books.", o:["writes","wrote","will have written","has written"], c:2},
{subject:"English", q:"The keys are ___ the drawer.", o:["at","in","on","under"], c:1},
{subject:"English", q:"She did not attend school because she ___ sick.", o:["is","was","has been","will be"], c:1},
{subject:"English", q:"The train ___ before we reached the station.", o:["leaves","left","had left","has left"], c:2},
{subject:"English", q:"He ran ___ the road ___ great speed.", o:["on, by","across, at","in, with","over, on"], c:1},
{subject:"English", q:"I have known him ___ five years.", o:["since","from","for","by"], c:2},
{subject:"English", q:"While I ___ TV, the lights went off.", o:["watch","watched","was watching","am watching"], c:2},
{subject:"English", q:"The picture is hanging ___ the wall.", o:["at","on","in","over"], c:1},
{subject:"English", q:"She ___ already finished her homework.", o:["is","was","has","had"], c:2},
{subject:"English", q:"He fell ___ the stairs.", o:["on","in","down","into"], c:2},
{subject:"English", q:"They have been working ___ morning.", o:["for","since","from","by"], c:1},
{subject:"English", q:"The teacher entered ___ the classroom.", o:["at","on","in","into"], c:3},
{subject:"English", q:"He ___ a letter when I saw him.", o:["writes","wrote","was writing","has written"], c:2},
{subject:"English", q:"The ball rolled ___ the bed.", o:["in","under","on","at"], c:1},
{subject:"English", q:"She will return ___ Monday.", o:["on","in","at","since"], c:0},
{subject:"English", q:"The baby is sleeping ___ the cradle.", o:["on","in","at","over"], c:1},
{subject:"English", q:"We ___ our lesson before the bell rang.", o:["finish","finished","had finished","have finished"], c:2},
{subject:"English", q:"He stood ___ the door and waited.", o:["on","in","at","over"], c:2},
{subject:"English", q:"They ___ to school every day.", o:["go","went","gone","going"], c:0},
{subject:"English", q:"The cat is hiding ___ the sofa.", o:["at","in","under","on"], c:2},
{subject:"English", q:"She has lived here ___ a long time.", o:["since","for","from","by"], c:1},
{subject:"English", q:"He ___ his homework last night.", o:["does","did","has done","will do"], c:1},
{subject:"English", q:"The bird flew ___ the tree.", o:["in","on","into","at"], c:2},
{subject:"English", q:"We shall meet ___ the evening.", o:["on","at","in","by"], c:2},
{subject:"English", q:"She ___ not seen him since Monday.", o:["did","does","has","had"], c:2},

];



let answers=new Array(questions.length).fill(null);
let index=0,time=3600,startTime,timerInt;

// ==========================
function startCountdown(){
if(!studentName.value||!rollNo.value){alert("Fill all fields");return;}
let c=5;countdown.innerText=c;
let i=setInterval(()=>{
c--;countdown.innerText=c;
if(c===0){
clearInterval(i);
loginDiv.style.display="none";
quizDiv.style.display="block";
startTime=Date.now();
loadQ();startTimer();
}},1000);
}

function loadQ(){
let q=questions[index];
questionBox.innerHTML=`<h3>${index+1}. (${q.subject}) ${q.q}</h3>`;
optionsBox.innerHTML="";
q.o.forEach((op,i)=>{
let d=document.createElement("div");
d.className="option";d.innerText=op;
d.onclick=()=>{
if(answers[index]!=null)return;
answers[index]=i;
d.classList.add(i===q.c?"correct":"wrong");
nextBtn.disabled=false;
};
optionsBox.appendChild(d);
});
nextBtn.disabled=answers[index]==null;
submitBtn.style.display=index===questions.length-1?"block":"none";
}

function nextQ(){if(index<questions.length-1){index++;loadQ();}}
function prevQ(){if(index>0){index--;loadQ();}}
function skipQ(){index=(index+1)%questions.length;loadQ();}

function startTimer(){
timerInt=setInterval(()=>{
let m=Math.floor(time/60),s=time%60;
timer.innerText=`Time Left: ${m}:${s<10?'0':''}${s}`;
if(time--<=0){clearInterval(timerInt);submitTest();}
},1000);
}

function submitTest(){
clearInterval(timerInt);
quizDiv.style.display="none";
resultDiv.style.display="block";

let score=0,subjectStats={};

questions.forEach((q,i)=>{
if(!subjectStats[q.subject]) subjectStats[q.subject]={total:0,correct:0};
subjectStats[q.subject].total++;
if(answers[i]===q.c){score++;subjectStats[q.subject].correct++;}
});

let pct=Math.round(score/questions.length*100);
resStatus.innerText=pct>=50?"PASSED":"FAILED";
resScore.innerText=`Overall Score: ${score}/${questions.length} (${pct}%)`;
resTime.innerText=`Time Taken: ${Math.floor((Date.now()-startTime)/60000)} minutes`;

subjectResult.innerHTML="";
for(let s in subjectStats){
let x=subjectStats[s];
subjectResult.innerHTML+=`<div class="subject-box"><b>${s}</b>: ${x.correct}/${x.total} → ${Math.round(x.correct/x.total*100)}%</div>`;
}
}

function showReview(){
resultDiv.style.display="none";
reviewDiv.style.display="block";
reviewContent.innerHTML="";
questions.forEach((q,i)=>{
let html=`<h4>${i+1}. ${q.q}</h4>`;
q.o.forEach((op,idx)=>{
let cls="review-option";
if(idx===q.c) cls+=" correct";
else if(answers[i]===idx) cls+=" wrong";
html+=`<div class="${cls}">${op}</div>`;
});
html+=`<p><i>${q.exp}</i></p>`;
reviewContent.innerHTML+=html;
});
}

function backToResult(){
reviewDiv.style.display="none";
resultDiv.style.display="block";
}
</script>

</body>
</html>

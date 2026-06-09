# Day 9 –Build & Enhance an AI Nutrition Analytics App

### 🎯 Objective

To explore how iterative prompt engineering can transform a simple nutrition tracking MVP into a feature-rich Nutrition Intelligence Platform. The goal was to understand how AI-assisted development can accelerate product design, feature expansion, and user experience enhancement using only structured prompts.

### 📚 Learn About

* Prompt Engineering for product development
* AI-assisted frontend application generation
* MVP-to-product evolution strategy
* Nutrition analytics and recommendation systems
* User-centric SaaS dashboard design
* Data visualization and health insights
* Feature prioritization and iterative development

### Prompt Used
PROMPT 1 — Build MVP

Build a complete single-file HTML application called NutriScope.

Requirements:

Profile Inputs:
Age, gender, Height, Weight, Activity Level, Dietary Preference (Vegetarian, Non-Vegetarian, Eggetarian).

Food Logging:
Add Food, Quantity, Unit, Editable Table, Remove Entry.

Food Database:
Include 20 common foods only:
Rice, Roti, Dal, Paneer, Curd, Chana, Rajma, Banana, Apple, Milk, Oats, Bread, Egg, Chicken, Fish, Potato, Poha, Idli, Dosa, Spinach.

Track:
Calories, Protein, Carbs, Fat, Fiber, Iron, Calcium, Vitamin C, Vitamin D, Vitamin B12.

Calculations:
Energy, Macro Targets, Micronutrient Targets, Percentage Completion.

Dashboard:
Energy Progress, Macro Chart, Top Deficiencies, Top Excesses, Nutrient Table.

Recommendations:
Food additions, food swaps, portion adjustments based on dietary preference.

Design:
Premium SaaS UI, Mobile Responsive, Chart.js, Dark Theme, Modern Cards, No Backend, Single HTML File.

Return only the complete HTML code.

PROMPT 2 — Enhance Application

Enhance the existing NutriScope application.

Add:
CSV Upload, 40 more foods, Additional micronutrients, 2-day meal planner, Risk Analysis, Educational Disclaimer, Nutrition Sources, Better Charts, Advanced Recommendations.

Return the updated HTML only.
### Normal Html file code
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NutriScope</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
:root{
--bg:#0f172a;
--card:#1e293b;
--card2:#111827;
--text:#f8fafc;
--muted:#94a3b8;
--accent:#22c55e;
--danger:#ef4444;
--border:#334155;
}

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Inter,Segoe UI,sans-serif;
}

body{
background:linear-gradient(135deg,#020617,#0f172a);
color:var(--text);
min-height:100vh;
padding:20px;
}

.container{
max-width:1400px;
margin:auto;
}

.header{
margin-bottom:24px;
}

.header h1{
font-size:2rem;
margin-bottom:6px;
}

.header p{
color:var(--muted);
}

.grid{
display:grid;
gap:18px;
}

.grid-3{
grid-template-columns:repeat(auto-fit,minmax(320px,1fr));
}

.card{
background:rgba(30,41,59,.95);
border:1px solid var(--border);
border-radius:20px;
padding:20px;
backdrop-filter:blur(10px);
box-shadow:0 10px 25px rgba(0,0,0,.3);
}

.card h2{
margin-bottom:15px;
font-size:1.1rem;
}

.row{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(140px,1fr));
gap:10px;
}

input,select,button{
width:100%;
padding:12px;
border-radius:12px;
border:1px solid var(--border);
background:#0b1220;
color:white;
}

button{
background:var(--accent);
font-weight:700;
border:none;
cursor:pointer;
}

button:hover{
opacity:.9;
}

.remove-btn{
background:var(--danger);
}

.progress{
height:14px;
background:#0b1220;
border-radius:20px;
overflow:hidden;
margin-top:10px;
}

.progress-bar{
height:100%;
background:linear-gradient(90deg,#22c55e,#16a34a);
width:0%;
}

.metric-grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(160px,1fr));
gap:12px;
}

.metric{
background:#0b1220;
padding:12px;
border-radius:14px;
}

.metric span{
display:block;
color:var(--muted);
font-size:.85rem;
margin-bottom:4px;
}

table{
width:100%;
border-collapse:collapse;
}

th,td{
padding:12px;
border-bottom:1px solid var(--border);
text-align:left;
}

.badge{
display:inline-block;
padding:8px 12px;
background:#0b1220;
border-radius:999px;
margin:4px;
font-size:.85rem;
}

.section{
margin-top:20px;
}

canvas{
max-height:320px;
}

@media(max-width:768px){
table{
font-size:12px;
}
}
</style>
</head>

<body>

<div class="container">

<div class="header">
<h1>🥗 NutriScope</h1>
<p>Smart Nutrition Tracking Dashboard</p>
</div>

<div class="grid grid-3">

<div class="card">
<h2>Profile</h2>

<div class="row">
<input type="number" id="age" value="28" placeholder="Age">
<select id="gender">
<option>Male</option>
<option>Female</option>
</select>
<input type="number" id="height" value="170" placeholder="Height cm">
<input type="number" id="weight" value="70" placeholder="Weight kg">
</div>

<br>

<div class="row">
<select id="activity">
<option>Sedentary</option>
<option>Light</option>
<option>Moderate</option>
<option>Active</option>
<option>Very Active</option>
</select>

<select id="diet">
<option>Vegetarian</option>
<option>Eggetarian</option>
<option>Non-Vegetarian</option>
</select>
</div>
</div>

<div class="card">
<h2>Add Food</h2>

<div class="row">
<select id="food"></select>
<input type="number" id="quantity" value="100">
<select id="unit">
<option>g</option>
<option>piece</option>
<option>cup</option>
</select>
</div>

<br>

<button onclick="addFood()">Add Food</button>
</div>

<div class="card">
<h2>Energy Progress</h2>

<div id="energyText">0 / 0 kcal</div>

<div class="progress">
<div id="energyBar" class="progress-bar"></div>
</div>
</div>

</div>

<div class="section card">
<h2>Food Log</h2>

<table>
<thead>
<tr>
<th>Food</th>
<th>Quantity</th>
<th>Unit</th>
<th>Calories</th>
<th>Protein</th>
<th>Action</th>
</tr>
</thead>
<tbody id="foodTable"></tbody>
</table>
</div>

<div class="section grid grid-3">

<div class="card">
<h2>Macro Distribution</h2>
<canvas id="macroChart"></canvas>
</div>

<div class="card">
<h2>Top Deficiencies</h2>
<div id="deficiencies"></div>
</div>

<div class="card">
<h2>Top Excesses</h2>
<div id="excesses"></div>
</div>

</div>

<div class="section card">
<h2>Nutrient Dashboard</h2>

<table>
<thead>
<tr>
<th>Nutrient</th>
<th>Consumed</th>
<th>Target</th>
<th>Completion</th>
</tr>
</thead>
<tbody id="nutrientTable"></tbody>
</table>
</div>

<div class="section card">
<h2>Recommendations</h2>
<div id="recommendations"></div>
</div>

</div>

<script>

const foodDB = {

Rice:{cal:130,protein:2.7,carbs:28,fat:0.3,fiber:0.4,iron:0.2,calcium:10,vitc:0,vitd:0,b12:0},
Roti:{cal:120,protein:4,carbs:22,fat:1.5,fiber:3,iron:1.2,calcium:15,vitc:0,vitd:0,b12:0},
Dal:{cal:116,protein:9,carbs:20,fat:0.4,fiber:8,iron:3.3,calcium:19,vitc:1,vitd:0,b12:0},
Paneer:{cal:265,protein:18,carbs:1,fat:20,fiber:0,iron:0.2,calcium:208,vitc:0,vitd:0,b12:1},
Curd:{cal:61,protein:3.5,carbs:4.7,fat:3.3,fiber:0,iron:0.1,calcium:121,vitc:0,vitd:0,b12:0.5},
Chana:{cal:164,protein:9,carbs:27,fat:2.6,fiber:8,iron:2.9,calcium:49,vitc:1,vitd:0,b12:0},
Rajma:{cal:127,protein:8.7,carbs:23,fat:0.5,fiber:6.4,iron:2.9,calcium:28,vitc:2,vitd:0,b12:0},
Banana:{cal:89,protein:1.1,carbs:23,fat:0.3,fiber:2.6,iron:0.3,calcium:5,vitc:9,vitd:0,b12:0},
Apple:{cal:52,protein:0.3,carbs:14,fat:0.2,fiber:2.4,iron:0.1,calcium:6,vitc:5,vitd:0,b12:0},
Milk:{cal:60,protein:3.2,carbs:5,fat:3.3,fiber:0,iron:0,calcium:113,vitc:0,vitd:1,b12:0.4},
Oats:{cal:389,protein:17,carbs:66,fat:7,fiber:10,iron:4.7,calcium:54,vitc:0,vitd:0,b12:0},
Bread:{cal:265,protein:9,carbs:49,fat:3.2,fiber:2.7,iron:3.6,calcium:107,vitc:0,vitd:0,b12:0},
Egg:{cal:155,protein:13,carbs:1,fat:11,fiber:0,iron:1.8,calcium:50,vitc:0,vitd:2,b12:1.1},
Chicken:{cal:239,protein:27,carbs:0,fat:14,fiber:0,iron:1.3,calcium:15,vitc:0,vitd:0,b12:0.3},
Fish:{cal:206,protein:22,carbs:0,fat:12,fiber:0,iron:0.8,calcium:16,vitc:0,vitd:5,b12:2.4},
Potato:{cal:77,protein:2,carbs:17,fat:0.1,fiber:2.2,iron:0.8,calcium:12,vitc:20,vitd:0,b12:0},
Poha:{cal:130,protein:2.5,carbs:25,fat:2,fiber:1.5,iron:1,calcium:10,vitc:2,vitd:0,b12:0},
Idli:{cal:58,protein:2,carbs:12,fat:0.4,fiber:0.8,iron:0.3,calcium:10,vitc:0,vitd:0,b12:0},
Dosa:{cal:168,protein:4,carbs:28,fat:4,fiber:1.5,iron:0.7,calcium:20,vitc:0,vitd:0,b12:0},
Spinach:{cal:23,protein:2.9,carbs:3.6,fat:0.4,fiber:2.2,iron:2.7,calcium:99,vitc:28,vitd:0,b12:0}

};

const targets = {
protein:75,
carbs:275,
fat:70,
fiber:30,
iron:17,
calcium:1000,
vitc:90,
vitd:15,
b12:2.4
};

let logs = [];

const foodSelect = document.getElementById("food");

Object.keys(foodDB).forEach(food=>{
const option=document.createElement("option");
option.value=food;
option.textContent=food;
foodSelect.appendChild(option);
});

function energyTarget(){

const age=+document.getElementById("age").value;
const weight=+document.getElementById("weight").value;
const height=+document.getElementById("height").value;
const gender=document.getElementById("gender").value;

let bmr = gender==="Male"
? 10*weight + 6.25*height - 5*age + 5
: 10*weight + 6.25*height - 5*age - 161;

const factors={
Sedentary:1.2,
Light:1.375,
Moderate:1.55,
Active:1.725,
"Very Active":1.9
};

return Math.round(bmr*factors[document.getElementById("activity").value]);
}

function addFood(){

logs.push({
food:food.value,
qty:+quantity.value,
unit:unit.value
});

render();
}

function removeFood(index){
logs.splice(index,1);
render();
}

function totals(){

let total={
cal:0,protein:0,carbs:0,fat:0,fiber:0,
iron:0,calcium:0,vitc:0,vitd:0,b12:0
};

logs.forEach(item=>{

const f=foodDB[item.food];
const factor=item.qty/100;

Object.keys(total).forEach(k=>{
total[k]+=f[k]*factor;
});

});

return total;
}

let chart = new Chart(
document.getElementById("macroChart"),
{
type:"doughnut",
data:{
labels:["Protein","Carbs","Fat"],
datasets:[{
data:[0,0,0]
}]
}
}
);

function render(){

const body=document.getElementById("foodTable");
body.innerHTML="";

logs.forEach((item,index)=>{

const factor=item.qty/100;
const food=foodDB[item.food];

body.innerHTML += `
<tr>
<td>${item.food}</td>
<td>${item.qty}</td>
<td>${item.unit}</td>
<td>${(food.cal*factor).toFixed(0)}</td>
<td>${(food.protein*factor).toFixed(1)}</td>
<td>
<button class="remove-btn" onclick="removeFood(${index})">
Remove
</button>
</td>
</tr>`;
});

const t=totals();
const targetEnergy=energyTarget();

document.getElementById("energyText").innerHTML=
`${t.cal.toFixed(0)} / ${targetEnergy} kcal`;

document.getElementById("energyBar").style.width=
Math.min(100,(t.cal/targetEnergy)*100)+"%";

chart.data.datasets[0].data=[
t.protein,t.carbs,t.fat
];
chart.update();

const nutrients=[
["Calories",t.cal,targetEnergy],
["Protein",t.protein,targets.protein],
["Carbs",t.carbs,targets.carbs],
["Fat",t.fat,targets.fat],
["Fiber",t.fiber,targets.fiber],
["Iron",t.iron,targets.iron],
["Calcium",t.calcium,targets.calcium],
["Vitamin C",t.vitc,targets.vitc],
["Vitamin D",t.vitd,targets.vitd],
["Vitamin B12",t.b12,targets.b12]
];

const table=document.getElementById("nutrientTable");
table.innerHTML="";

nutrients.forEach(n=>{

table.innerHTML+=`
<tr>
<td>${n[0]}</td>
<td>${n[1].toFixed(1)}</td>
<td>${n[2]}</td>
<td>${((n[1]/n[2])*100).toFixed(0)}%</td>
</tr>`;
});

let deficits=[];
let excess=[];

nutrients.slice(1).forEach(n=>{
const pct=(n[1]/n[2])*100;
deficits.push({name:n[0],pct});
excess.push({name:n[0],pct});
});

deficits.sort((a,b)=>a.pct-b.pct);
excess.sort((a,b)=>b.pct-a.pct);

document.getElementById("deficiencies").innerHTML=
deficits.slice(0,3)
.map(x=>`<span class="badge">${x.name} ${x.pct.toFixed(0)}%</span>`)
.join("");

document.getElementById("excesses").innerHTML=
excess.filter(x=>x.pct>100)
.slice(0,3)
.map(x=>`<span class="badge">${x.name} ${x.pct.toFixed(0)}%</span>`)
.join("") || "No Excesses";

const rec=[];

const diet=document.getElementById("diet").value;

if(t.protein<targets.protein*0.8){

if(diet==="Vegetarian"){
rec.push("Add Paneer, Dal, Chana");
}

if(diet==="Eggetarian"){
rec.push("Add Eggs and Dal");
}

if(diet==="Non-Vegetarian"){
rec.push("Add Chicken or Fish");
}
}

if(t.fiber<targets.fiber*0.8){
rec.push("Increase Spinach, Fruits and Legumes");
}

if(t.vitc<targets.vitc*0.8){
rec.push("Add Spinach, Banana, Apple");
}

if(t.fat>targets.fat*1.3){
rec.push("Reduce Paneer or Fat-Rich Foods");
}

if(t.cal>targetEnergy*1.15){
rec.push("Reduce Rice, Roti, Dosa Portions");
}

document.getElementById("recommendations").innerHTML=
(rec.length?rec:["Diet looks balanced today"])
.map(r=>`<span class="badge">${r}</span>`)
.join("");
}

[
"age",
"gender",
"height",
"weight",
"activity",
"diet"
].forEach(id=>{
document.getElementById(id).addEventListener("change",render);
});

render();

</script>

</body>
</html>

### Enhance html file code
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>NutriScope Pro</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
body{margin:0;background:#0f172a;color:#fff;font-family:Inter,Arial,sans-serif}
.container{max-width:1500px;margin:auto;padding:20px}
.card{background:#1e293b;border:1px solid #334155;border-radius:18px;padding:18px;margin-bottom:18px}
.grid{display:grid;gap:16px}
.grid-3{grid-template-columns:repeat(auto-fit,minmax(320px,1fr))}
input,select,button{width:100%;padding:10px;border-radius:10px;border:1px solid #334155;background:#111827;color:#fff}
button{background:#22c55e;border:none;font-weight:700;cursor:pointer}
table{width:100%;border-collapse:collapse}
th,td{padding:10px;border-bottom:1px solid #334155;text-align:left}
.badge{display:inline-block;padding:6px 10px;background:#111827;border-radius:999px;margin:4px}
.small{color:#94a3b8;font-size:.85rem}
</style>
</head>
<body>

<div class="container">

<h1>🥗 NutriScope Pro</h1>
<p class="small">Advanced Nutrition Intelligence Platform</p>

<div class="grid grid-3">

<div class="card">
<h3>User Profile</h3>
<input id="age" type="number" placeholder="Age" value="28"><br><br>
<select id="gender"><option>Male</option><option>Female</option></select><br><br>
<input id="height" type="number" value="170" placeholder="Height"><br><br>
<input id="weight" type="number" value="70" placeholder="Weight"><br><br>
<select id="activity">
<option>Sedentary</option>
<option>Light</option>
<option selected>Moderate</option>
<option>Active</option>
<option>Very Active</option>
</select><br><br>
<select id="diet">
<option>Vegetarian</option>
<option>Eggetarian</option>
<option>Non-Vegetarian</option>
</select>
</div>

<div class="card">
<h3>Food Logging</h3>
<select id="food"></select><br><br>
<input id="qty" type="number" value="100"><br><br>
<button onclick="addFood()">Add Food</button>
<br><br>
<input type="file" id="csvUpload" accept=".csv">
<p class="small">CSV: Food,Quantity</p>
</div>

<div class="card">
<h3>2-Day Meal Planner</h3>
<div id="mealPlanner"></div>
</div>

</div>

<div class="card">
<h3>Food Log</h3>
<table>
<thead>
<tr>
<th>Food</th>
<th>Qty</th>
<th>Calories</th>
<th>Protein</th>
<th>Action</th>
</tr>
</thead>
<tbody id="foodTable"></tbody>
</table>
</div>

<div class="grid grid-3">

<div class="card">
<h3>Macro Distribution</h3>
<canvas id="macroChart"></canvas>
</div>

<div class="card">
<h3>Micronutrient Coverage</h3>
<canvas id="microChart"></canvas>
</div>

<div class="card">
<h3>Risk Analysis</h3>
<div id="riskAnalysis"></div>
</div>

</div>

<div class="card">
<h3>Nutrient Dashboard</h3>
<table>
<thead>
<tr>
<th>Nutrient</th>
<th>Consumed</th>
<th>Target</th>
<th>%</th>
</tr>
</thead>
<tbody id="nutrientTable"></tbody>
</table>
</div>

<div class="card">
<h3>Advanced Recommendations</h3>
<div id="recommendations"></div>
</div>

<div class="card">
<h3>Nutrition Sources</h3>
<ul>
<li>USDA FoodData Central</li>
<li>ICMR Dietary Guidelines</li>
<li>WHO Nutrition References</li>
<li>NIH Office of Dietary Supplements</li>
</ul>
</div>

<div class="card">
<h3>Educational Disclaimer</h3>
<p class="small">
NutriScope is an educational nutrition tracking tool. Values are estimates and not medical advice.
Consult a qualified dietitian or physician for diagnosis, treatment, or personalized nutrition plans.
</p>
</div>

</div>

<script>

const foods = {

Rice:{cal:130,protein:2.7,carbs:28,fat:0.3,fiber:0.4,iron:0.2,calcium:10,vitc:0,vitd:0,b12:0,potassium:35,magnesium:12,zinc:0.4},
Roti:{cal:120,protein:4,carbs:22,fat:1.5,fiber:3,iron:1.2,calcium:15,vitc:0,vitd:0,b12:0,potassium:85,magnesium:20,zinc:0.7},
Dal:{cal:116,protein:9,carbs:20,fat:.4,fiber:8,iron:3.3,calcium:19,vitc:1,vitd:0,b12:0,potassium:369,magnesium:36,zinc:1.3},
Paneer:{cal:265,protein:18,carbs:1,fat:20,fiber:0,iron:.2,calcium:208,vitc:0,vitd:0,b12:1,potassium:104,magnesium:8,zinc:2.5},
Curd:{cal:61,protein:3.5,carbs:4.7,fat:3.3,fiber:0,iron:.1,calcium:121,vitc:0,vitd:0,b12:.5,potassium:155,magnesium:11,zinc:.6},

Chana:{cal:164,protein:9,carbs:27,fat:2.6,fiber:8,iron:2.9,calcium:49,vitc:1,vitd:0,b12:0,potassium:291,magnesium:48,zinc:1.5},
Rajma:{cal:127,protein:8.7,carbs:23,fat:.5,fiber:6.4,iron:2.9,calcium:28,vitc:2,vitd:0,b12:0,potassium:405,magnesium:45,zinc:1.1},
Banana:{cal:89,protein:1.1,carbs:23,fat:.3,fiber:2.6,iron:.3,calcium:5,vitc:9,vitd:0,b12:0,potassium:358,magnesium:27,zinc:.2},
Apple:{cal:52,protein:.3,carbs:14,fat:.2,fiber:2.4,iron:.1,calcium:6,vitc:5,vitd:0,b12:0,potassium:107,magnesium:5,zinc:.1},
Milk:{cal:60,protein:3.2,carbs:5,fat:3.3,fiber:0,iron:0,calcium:113,vitc:0,vitd:1,b12:.4,potassium:150,magnesium:10,zinc:.4},

Oats:{cal:389,protein:17,carbs:66,fat:7,fiber:10,iron:4.7,calcium:54,vitc:0,vitd:0,b12:0,potassium:429,magnesium:177,zinc:4},
Bread:{cal:265,protein:9,carbs:49,fat:3.2,fiber:2.7,iron:3.6,calcium:107,vitc:0,vitd:0,b12:0,potassium:115,magnesium:25,zinc:1},
Egg:{cal:155,protein:13,carbs:1,fat:11,fiber:0,iron:1.8,calcium:50,vitc:0,vitd:2,b12:1.1,potassium:126,magnesium:12,zinc:1.3},
Chicken:{cal:239,protein:27,carbs:0,fat:14,fiber:0,iron:1.3,calcium:15,vitc:0,vitd:0,b12:.3,potassium:256,magnesium:29,zinc:1},
Fish:{cal:206,protein:22,carbs:0,fat:12,fiber:0,iron:.8,calcium:16,vitc:0,vitd:5,b12:2.4,potassium:363,magnesium:30,zinc:.7},

Potato:{cal:77,protein:2,carbs:17,fat:.1,fiber:2.2,iron:.8,calcium:12,vitc:20,vitd:0,b12:0,potassium:425,magnesium:23,zinc:.3},
Poha:{cal:130,protein:2.5,carbs:25,fat:2,fiber:1.5,iron:1,calcium:10,vitc:2,vitd:0,b12:0,potassium:60,magnesium:15,zinc:.3},
Idli:{cal:58,protein:2,carbs:12,fat:.4,fiber:.8,iron:.3,calcium:10,vitc:0,vitd:0,b12:0,potassium:35,magnesium:8,zinc:.2},
Dosa:{cal:168,protein:4,carbs:28,fat:4,fiber:1.5,iron:.7,calcium:20,vitc:0,vitd:0,b12:0,potassium:80,magnesium:18,zinc:.4},
Spinach:{cal:23,protein:2.9,carbs:3.6,fat:.4,fiber:2.2,iron:2.7,calcium:99,vitc:28,vitd:0,b12:0,potassium:558,magnesium:79,zinc:.5},

Broccoli:{cal:34,protein:2.8,carbs:7,fat:.4,fiber:2.6,iron:.7,calcium:47,vitc:89,vitd:0,b12:0,potassium:316,magnesium:21,zinc:.4},
Orange:{cal:47,protein:.9,carbs:12,fat:.1,fiber:2.4,iron:.1,calcium:40,vitc:53,vitd:0,b12:0,potassium:181,magnesium:10,zinc:.1},
Almonds:{cal:579,protein:21,carbs:22,fat:50,fiber:12,iron:3.7,calcium:269,vitc:0,vitd:0,b12:0,potassium:733,magnesium:270,zinc:3.1},
Walnuts:{cal:654,protein:15,carbs:14,fat:65,fiber:7,iron:2.9,calcium:98,vitc:1,vitd:0,b12:0,potassium:441,magnesium:158,zinc:3},
Peanuts:{cal:567,protein:25,carbs:16,fat:49,fiber:8,iron:4.6,calcium:92,vitc:0,vitd:0,b12:0,potassium:705,magnesium:168,zinc:3.3},

Tofu:{cal:144,protein:17,carbs:3,fat:8,fiber:2,iron:2.7,calcium:350,vitc:0,vitd:0,b12:0,potassium:121,magnesium:37,zinc:1.6},
Soybeans:{cal:173,protein:16,carbs:10,fat:9,fiber:6,iron:5,calcium:102,vitc:6,vitd:0,b12:0,potassium:515,magnesium:86,zinc:1.2},
Mushroom:{cal:22,protein:3.1,carbs:3.3,fat:.3,fiber:1,iron:.5,calcium:3,vitc:2,vitd:1,b12:0,potassium:318,magnesium:9,zinc:.5},
SweetPotato:{cal:86,protein:1.6,carbs:20,fat:.1,fiber:3,iron:.6,calcium:30,vitc:3,vitd:0,b12:0,potassium:337,magnesium:25,zinc:.3},
Cucumber:{cal:15,protein:.6,carbs:3.6,fat:.1,fiber:.5,iron:.3,calcium:16,vitc:3,vitd:0,b12:0,potassium:147,magnesium:13,zinc:.2},

Tomato:{cal:18,protein:.9,carbs:3.9,fat:.2,fiber:1.2,iron:.3,calcium:10,vitc:14,vitd:0,b12:0,potassium:237,magnesium:11,zinc:.2},
Onion:{cal:40,protein:1.1,carbs:9.3,fat:.1,fiber:1.7,iron:.2,calcium:23,vitc:7,vitd:0,b12:0,potassium:146,magnesium:10,zinc:.2},
Mango:{cal:60,protein:.8,carbs:15,fat:.4,fiber:1.6,iron:.2,calcium:11,vitc:36,vitd:0,b12:0,potassium:168,magnesium:10,zinc:.1},
Papaya:{cal:43,protein:.5,carbs:11,fat:.3,fiber:1.7,iron:.3,calcium:20,vitc:60,vitd:0,b12:0,potassium:182,magnesium:21,zinc:.1},
Guava:{cal:68,protein:2.6,carbs:14,fat:1,fiber:5,iron:.3,calcium:18,vitc:228,vitd:0,b12:0,potassium:417,magnesium:22,zinc:.2},

Avocado:{cal:160,protein:2,carbs:9,fat:15,fiber:7,iron:.6,calcium:12,vitc:10,vitd:0,b12:0,potassium:485,magnesium:29,zinc:.6},
Lentils:{cal:116,protein:9,carbs:20,fat:.4,fiber:8,iron:3.3,calcium:19,vitc:1,vitd:0,b12:0,potassium:369,magnesium:36,zinc:1.3},
Quinoa:{cal:120,protein:4.4,carbs:21,fat:1.9,fiber:2.8,iron:1.5,calcium:17,vitc:0,vitd:0,b12:0,potassium:172,magnesium:64,zinc:1},
BrownRice:{cal:111,protein:2.6,carbs:23,fat:.9,fiber:1.8,iron:.4,calcium:10,vitc:0,vitd:0,b12:0,potassium:43,magnesium:44,zinc:.6},
GreenPeas:{cal:81,protein:5.4,carbs:14,fat:.4,fiber:5,iron:1.5,calcium:25,vitc:40,vitd:0,b12:0,potassium:244,magnesium:33,zinc:1.2},

Cauliflower:{cal:25,protein:1.9,carbs:5,fat:.3,fiber:2,iron:.4,calcium:22,vitc:48,vitd:0,b12:0,potassium:299,magnesium:15,zinc:.3},
Beetroot:{cal:43,protein:1.6,carbs:10,fat:.2,fiber:2.8,iron:.8,calcium:16,vitc:5,vitd:0,b12:0,potassium:325,magnesium:23,zinc:.3},
Yogurt:{cal:59,protein:10,carbs:3.6,fat:.4,fiber:0,iron:.1,calcium:110,vitc:0,vitd:0,b12:.8,potassium:141,magnesium:11,zinc:.5},
Cheese:{cal:402,protein:25,carbs:1.3,fat:33,fiber:0,iron:.7,calcium:721,vitc:0,vitd:0,b12:1.5,potassium:98,magnesium:28,zinc:3},
Turkey:{cal:189,protein:29,carbs:0,fat:7,fiber:0,iron:1.4,calcium:11,vitc:0,vitd:0,b12:1,potassium:239,magnesium:28,zinc:2}

};

let log=[];

Object.keys(foods).forEach(f=>{
food.innerHTML += `<option>${f}</option>`;
});

const macroChart=new Chart(document.getElementById("macroChart"),{
type:"doughnut",
data:{labels:["Protein","Carbs","Fat"],datasets:[{data:[0,0,0]}]}
});

const microChart=new Chart(document.getElementById("microChart"),{
type:"bar",
data:{
labels:["Iron","Calcium","Vit C","Vit D","B12","Potassium"],
datasets:[{label:"% Target",data:[0,0,0,0,0,0]}]
}
});

function addFood(){
log.push({food:food.value,qty:+qty.value});
render();
}

function render(){

let t={cal:0,protein:0,carbs:0,fat:0,fiber:0,iron:0,calcium:0,vitc:0,vitd:0,b12:0,potassium:0};

foodTable.innerHTML="";

log.forEach((e,i)=>{

const f=foods[e.food];
const m=e.qty/100;

Object.keys(t).forEach(k=>{
if(f[k]!==undefined)t[k]+=f[k]*m;
});

foodTable.innerHTML+=`
<tr>
<td>${e.food}</td>
<td>${e.qty}</td>
<td>${(f.cal*m).toFixed(0)}</td>
<td>${(f.protein*m).toFixed(1)}</td>
<td><button onclick="log.splice(${i},1);render()">Remove</button></td>
</tr>`;
});

macroChart.data.datasets[0].data=[t.protein,t.carbs,t.fat];
macroChart.update();

microChart.data.datasets[0].data=[
(t.iron/17)*100,
(t.calcium/1000)*100,
(t.vitc/90)*100,
(t.vitd/15)*100,
(t.b12/2.4)*100,
(t.potassium/3500)*100
];
microChart.update();

nutrientTable.innerHTML=`
<tr><td>Calories</td><td>${t.cal.toFixed(1)}</td><td>Calculated</td><td>-</td></tr>
<tr><td>Protein</td><td>${t.protein.toFixed(1)}</td><td>75</td><td>${((t.protein/75)*100).toFixed(0)}%</td></tr>
<tr><td>Iron</td><td>${t.iron.toFixed(1)}</td><td>17</td><td>${((t.iron/17)*100).toFixed(0)}%</td></tr>
<tr><td>Calcium</td><td>${t.calcium.toFixed(1)}</td><td>1000</td><td>${((t.calcium/1000)*100).toFixed(0)}%</td></tr>
<tr><td>Vitamin C</td><td>${t.vitc.toFixed(1)}</td><td>90</td><td>${((t.vitc/90)*100).toFixed(0)}%</td></tr>
<tr><td>Vitamin D</td><td>${t.vitd.toFixed(1)}</td><td>15</td><td>${((t.vitd/15)*100).toFixed(0)}%</td></tr>
<tr><td>Vitamin B12</td><td>${t.b12.toFixed(1)}</td><td>2.4</td><td>${((t.b12/2.4)*100).toFixed(0)}%</td></tr>
`;

let risks=[];

if(t.protein<50) risks.push("⚠️ Protein deficiency risk");
if(t.iron<10) risks.push("⚠️ Iron deficiency risk");
if(t.calcium<700) risks.push("⚠️ Bone health support needed");
if(t.vitd<8) risks.push("⚠️ Vitamin D deficiency risk");
if(t.fat>100) risks.push("⚠️ High fat intake");

riskAnalysis.innerHTML=risks.length?risks.map(r=>`<div class='badge'>${r}</div>`).join(""):"Low nutritional risk";

recommendations.innerHTML="";

if(t.protein<75) recommendations.innerHTML += "<div class='badge'>Increase protein foods</div>";
if(t.vitc<90) recommendations.innerHTML += "<div class='badge'>Add guava, orange, papaya</div>";
if(t.iron<17) recommendations.innerHTML += "<div class='badge'>Add spinach, lentils, chana</div>";
if(t.calcium<1000) recommendations.innerHTML += "<div class='badge'>Add milk, curd, paneer</div>";

mealPlanner.innerHTML=`
<b>Day 1</b><br>
Breakfast: Oats + Milk + Banana<br>
Lunch: Rice + Dal + Spinach<br>
Dinner: Roti + Paneer + Curd
<hr>
<b>Day 2</b><br>
Breakfast: Poha + Apple<br>
Lunch: Brown Rice + Rajma + Salad<br>
Dinner: Dosa + Chana + Yogurt
`;
}

document.getElementById("csvUpload").addEventListener("change",e=>{
const file=e.target.files[0];
if(!file) return;

const reader=new FileReader();
reader.onload=x=>{
const rows=x.target.result.split("\n");
rows.forEach(r=>{
const [foodName,q]=r.split(",");
if(foods[foodName]){
log.push({food:foodName,qty:Number(q)||100});
}
});
render();
};
reader.readAsText(file);
});

render();

</script>
</body>
</html>

### Screenshots of result image
# Image 1
<img width="1536" height="1024" alt="1000224988" src="https://github.com/user-attachments/assets/babec078-c59a-4dc1-ae7a-e679544eeead" />

# Image 2
<img width="1536" height="1024" alt="1000224989" src="https://github.com/user-attachments/assets/4d5206a6-91be-4d43-b46c-35f38228b2d2" />



### 💡 Key Learnings

✅ Start with a focused MVP before adding complexity

✅ Build products in layers:

* Core Functionality
* User Experience
* Intelligence Layer
* Analytics & Insights

✅ Users value actionable insights more than raw data

✅ Features like risk analysis, meal planning, and recommendations significantly increase product value

✅ Trust elements such as nutrition sources and disclaimers improve credibility

✅ Prompt refinement can dramatically improve output quality without changing the underlying technology

✅ AI can accelerate prototyping from weeks to hours when requirements are clearly defined

### Comparison 
## NutriScope Prompt 1 vs Prompt 2 Comparison

| Area                    | Prompt 1 (MVP)                   | Prompt 2 (Enhanced)                                     |
| ----------------------- | -------------------------------- | ------------------------------------------------------- |
| Goal                    | Functional Nutrition Tracker     | Product-Ready Nutrition Intelligence Platform           |
| Food Database           | 20 foods                         | 60 foods (20 + 40 additional)                           |
| Profile Inputs          | Basic demographics               | Same                                                    |
| Food Logging            | Manual entry                     | Manual + CSV Upload                                     |
| Meal Planning           | Not included                     | 2-Day Meal Planner                                      |
| Micronutrients          | Iron, Calcium, Vitamin C, D, B12 | Added Potassium, Magnesium, Zinc + expandable structure |
| Dashboard               | Basic                            | Advanced                                                |
| Charts                  | Single macro chart               | Macro + Micronutrient charts                            |
| Recommendations         | Basic rule-based                 | Context-aware recommendations                           |
| Risk Analysis           | Not included                     | Included                                                |
| Nutrition Sources       | Not included                     | Included                                                |
| Disclaimer              | Not included                     | Included                                                |
| Professional Appeal     | MVP Demo                         | Near SaaS Product Demo                                  |
| LinkedIn Showcase Value | Moderate                         | High                                                    |

---

# What Prompt 1 Did Well

### 1. Strong MVP Scope

Prompt 1 clearly defined:

* Inputs
* Food logging
* Nutrition calculations
* Dashboard
* Recommendations

This helped generate a working application quickly.

### 2. Minimal Complexity

Benefits:

* Faster generation
* Easier debugging
* Cleaner architecture
* Better for initial validation

### 3. Good Product Foundation

Core modules already existed:

* User Profile
* Food Database
* Nutrient Engine
* Dashboard
* Recommendation Engine

These become reusable components later.

---

# Limitations of Prompt 1

### Limited Food Database

20 foods is not enough for realistic use.

Users quickly ask:

* Where is broccoli?
* Where is quinoa?
* Where are nuts?

---

### No Data Import

Real users do not want to manually enter:

* 50 meals
* Weekly logs

CSV support becomes necessary.

---

### Weak Micronutrient Coverage

Only:

* Iron
* Calcium
* Vitamin C
* Vitamin D
* Vitamin B12

Missing:

* Potassium
* Magnesium
* Zinc
* Folate
* Vitamin A
* Vitamin E
* Omega-3

---

### No Risk Assessment

Application reports nutrients but does not answer:

> "What does this mean for my health?"

---

# What Prompt 2 Improved

## 1. Added User Workflow Features

CSV Upload

Moves application from:

Demo → Practical Tool

---

## 2. Expanded Food Intelligence

60 foods provides:

* Better recommendations
* Better nutrient coverage
* More realistic meal plans

---

## 3. Added Risk Layer

Instead of:

> Protein = 40g

Application now says:

> Protein Deficiency Risk

This is more meaningful for users.

---

## 4. Added Meal Planning

Prompt 1 tracked history.

Prompt 2 helps plan the future.

That's a major product shift.

---

## 5. Added Trust Signals

### Nutrition Sources

Users trust applications more when sources are visible.

### Disclaimer

Important for:

* Compliance
* Legal protection
* Professional presentation

---

## 6. Better Visual Storytelling

Prompt 1:

* One chart

Prompt 2:

* Macro chart
* Micronutrient chart
* Risk cards
* Planner
* Recommendations

Feels more premium.

---

# Product Maturity Scale

### Prompt 1

```text
Idea
 ↓
Prototype
 ↓
MVP  ← Prompt 1
```

### Prompt 2

```text
Idea
 ↓
Prototype
 ↓
MVP
 ↓
Beta Product
 ↓
Demo SaaS ← Prompt 2
```

---

# Key Prompt Engineering Learning

## Learning 1: Build in Layers

Best sequence:

```text
Prompt 1
Core Functionality
      ↓
Prompt 2
Enhancements
      ↓
Prompt 3
AI Intelligence
      ↓
Prompt 4
Production Architecture
```

Instead of asking for everything at once.

---

## Learning 2: Features ≠ Product

Prompt 1 contains features.

Prompt 2 starts creating a product experience.

Difference:

```text
Feature = Food Logging

Experience =
Food Logging
+ Analysis
+ Risk Detection
+ Recommendations
+ Planning
```

---

## Learning 3: Insights Are More Valuable Than Data

Users don't want:

```text
Iron = 7mg
```

Users want:

```text
Iron Deficiency Risk
Suggested Foods:
Spinach
Lentils
Chickpeas
```

Prompt 2 moved toward insights.

---

## Learning 4: Trust Matters

Adding:

* Sources
* Disclaimer
* Planner
* Risk analysis

Makes the app look significantly more credible.

---

# Recommended Prompt 3 (Next Evolution)

To make NutriScope portfolio-worthy or startup-grade, add:

### AI Layer

* Meal recommendations using OpenAI
* Personalized coaching
* Smart grocery list generation

### Analytics

* Weekly trends
* Monthly trends
* Deficiency forecasting

### Health Scoring

```text
Nutrition Score: 84/100
Protein Score: 90
Micronutrient Score: 75
Diet Diversity Score: 82
```

### Goals

* Weight Loss
* Weight Gain
* Muscle Building
* Diabetes Friendly
* Heart Healthy

### Export

* PDF Nutrition Reports
* Excel Exports

### Authentication

* User accounts
* Saved history

---

## Overall Assessment

**Prompt 1:** 7.5/10
Good MVP, validates the concept.

**Prompt 2:** 9/10
Looks and feels like a genuine SaaS nutrition platform with stronger UX, analytics, and business value.

**Biggest learning:** Prompt 1 focused on *tracking nutrition*. Prompt 2 evolved into *helping users make nutrition decisions*, which is where most product value is created.


### 🚀 Conclusion

This exercise demonstrated that AI is not just a coding assistant—it can act as a rapid product development partner. Starting with a basic nutrition tracker and progressively enhancing it through structured prompts resulted in a solution that resembles a real-world SaaS platform. The experience reinforced the importance of iterative thinking, clear requirements, and focusing on user outcomes rather than simply adding features.

**From tracking nutrition ➜ to enabling smarter nutrition decisions.**



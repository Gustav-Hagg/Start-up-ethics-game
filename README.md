[startup-ethics-game-playable-app (2).html](https://github.com/user-attachments/files/32006203/startup-ethics-game-playable-app.2.html)
<!doctype html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Startup Ethics: The Entrepreneurial Journey</title>
<style>
:root{
  font-family:Inter,system-ui,-apple-system,sans-serif;
  --bg:#0a0e1a; --card:#141c2e; --card2:#1a2438; --border:#2a3a56;
  --text:#cdd9ee; --muted:#6b7d99; --sky:#38bdf8; --violet:#a78bfa;
  --emerald:#34d399; --amber:#fbbf24; --rose:#f87171;
}
*{margin:0;padding:0;box-sizing:border-box}
body{background:var(--bg);color:var(--text);min-height:100vh}
#app{min-height:100vh}
.container{max-width:720px;margin:0 auto;padding:32px 20px 60px}
.card{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:20px}
.badge{display:inline-block;padding:3px 10px;border-radius:999px;font-size:12px;font-weight:600}
.badge-slate{background:#33415580;color:#cdd9ee}
.badge-violet{background:#a78bfa20;color:var(--violet)}
.badge-amber{background:#fbbf2420;color:var(--amber)}
.badge-sky{background:#38bdf820;color:var(--sky)}
h1{font-size:2.4rem;font-weight:800;color:#fff;letter-spacing:-.02em}
h2{font-size:1.3rem;font-weight:700;color:#fff}
h3{font-size:1rem;font-weight:700;color:#fff}
p{line-height:1.6}
.btn{display:inline-block;padding:11px 24px;border-radius:8px;border:none;font-size:15px;font-weight:600;cursor:pointer;transition:all .15s;font-family:inherit}
.btn-primary{background:var(--sky);color:#fff}
.btn-primary:hover{background:#0ea5e9}
.btn-outline{background:transparent;border:1px solid var(--border);color:var(--muted)}
.btn-outline:hover{border-color:var(--amber);color:var(--amber)}
.btn-opt{display:block;width:100%;text-align:left;background:var(--card2);border:1px solid var(--border);border-radius:10px;padding:16px;cursor:pointer;transition:all .15s;font:inherit;color:var(--text)}
.btn-opt:hover{border-color:#44608a}
.btn-opt.selected{border-color:var(--sky);background:#0c1a30}
.btn-opt.dimmed{opacity:.35}
.fade{animation:fadeIn .3s ease}
@keyframes fadeIn{from{opacity:0;transform:translateX(12px)}to{opacity:1;transform:none}}
.metric-bar{height:8px;border-radius:999px;background:#33415560;overflow:hidden;position:relative}
.metric-fill{height:100%;border-radius:999px;transition:width .5s ease}
.threshold-mark{position:absolute;top:0;bottom:0;width:2px;background:#f8717180}
.impact-chip{font-size:11px;font-weight:600;padding:2px 7px;border-radius:5px}
.pos{background:#34d39920;color:var(--emerald)}
.neg{background:#f8717120;color:var(--rose)}
.zero{background:#6b7d9940;color:var(--muted)}
.q-item{display:flex;gap:8px;padding:5px 0;color:var(--text);font-size:14px;line-height:1.5}
.q-item span:first-child{color:var(--amber);flex-shrink:0}
.section-label{font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:.05em;color:#fbbf2499;margin-bottom:6px}
.teach-box{border:1px solid #fbbf2440;background:#1a1305;border-radius:10px;padding:14px;margin-top:14px}
.decision-row{display:flex;align-items:center;gap:10px;padding:10px 14px;background:var(--card2);border:1px solid var(--border);border-radius:8px;margin-bottom:6px}
.decision-row .pill{width:26px;height:26px;border-radius:50%;background:#33415580;display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:700;flex-shrink:0}
.profile-bar{height:8px;border-radius:999px;background:#33415560;overflow:hidden;flex:1}
.profile-fill{height:100%;border-radius:999px}
</style>
</head>
<body>
<div id="app"></div>
<script>
// ─── Data model (mirrors the Python dataclasses) ──────────
const METRICS=[
  {key:"ES",full:"Economic Sustainability",desc:"Financial viability & competitiveness",color:"#38bdf8"},
  {key:"SR",full:"Social Responsibility",desc:"Stakeholder wellbeing & equity",color:"#a78bfa"},
  {key:"EI",full:"Environmental Impact",desc:"Ecological footprint & conservation",color:"#34d399"},
];

const SCENARIOS=[
  {id:1,phase:1,phaseName:"Ideation & Foundation",title:"Product Development",
   prompt:"Your AI-powered productivity tool could save companies up to $2M a year, but may displace 30-40% of routine roles, hitting workers aged 45-55 hardest.",
   story:"Your team can re-engineer the algorithm to augment humans rather than replace them, though that reduces efficiency and market appeal.",
   options:[
     {id:"A",label:"Modify the product to augment rather than replace workers",detail:"Protect jobs at the cost of efficiency",es:-10,sr:15,ei:5,framework:"deontological",feedback:"You honored a duty to the workers most vulnerable to disruption. Efficiency is lower, but you built a product with people inside the loop."},
     {id:"B",label:"Proceed with the original design to maximize efficiency",detail:"Maximize profit, accept displacement",es:20,sr:-15,ei:-5,framework:"teleological",feedback:"You prioritized the greatest economic gain for the greatest number of customers. The human cost of displacement is externalized to society."}
   ],
   teaching:{objective:"Recognize the tension between maximizing efficiency/profit and protecting vulnerable workers affected by technological disruption.",
     discussion:["Is a company responsible for the downstream job losses its product causes?","How might the displaced 45-55 age group be supported? Whose duty is it?","Does augmenting rather than replacing meaningfully change the ethical outcome?","If the augmented version fails commercially, was the ethical choice still right?"],
     frameworks:"Option A leans deontological: a duty to avoid foreseeable harm to individuals. Option B leans teleological: aggregate economic benefit outweighs localized harm."}},
  {id:2,phase:1,phaseName:"Ideation & Foundation",title:"Funding Choice",
   prompt:"A top VC offers $10M (24 months runway) but has a history of funding controversial mining and deforestation. You have only 6 months of runway left.",
   story:"Their network could turn you into a unicorn. Other investors have shown only moderate interest.",
   options:[
     {id:"A",label:"Accept the funding to accelerate growth and change from within",detail:"Take the money, influence from inside",es:25,sr:-5,ei:-10,framework:"teleological",feedback:"You bet that the ends justify the means. Reputation risk is real."},
     {id:"B",label:"Decline the investment and seek alternative funding",detail:"Refuse on principle, stay independent",es:-15,sr:10,ei:15,framework:"deontological",feedback:"You refused to benefit from environmental harm, regardless of the growth cost. Principles over expedience."}
   ],
   teaching:{objective:"Evaluate whether accepting tainted funding can be justified by the positive change a startup might create from within.",
     discussion:["Can taking harmful money to do good be a legitimate strategy, or is it self-deception?","What is the reputational cost to a young company?","Is there a middle path - conditional acceptance or governance terms?","How does power asymmetry between investor and founder affect influence claims?"],
     frameworks:"Option A applies teleological reasoning: the ends may justify tainted means. Option B is deontological: benefiting from environmental destruction is wrong regardless of outcomes."}},
  {id:3,phase:2,phaseName:"Growth & Scaling",title:"Manufacturing Decision",
   prompt:"Local manufacturing costs $89/unit; overseas costs $31/unit but the facility faces criticism for long hours and poor ventilation. Lower cost reaches 5x more price-sensitive customers.",
   story:"Local means community jobs, quality control, lower transport emissions. Overseas means accessibility for many more small businesses.",
   options:[
     {id:"A",label:"Choose local manufacturing",detail:"Higher cost, local jobs, clean transport",es:-20,sr:20,ei:15,framework:"deontological",feedback:"You accepted higher costs to protect workers and your community. Fewer customers can afford the product, but those who make it are treated well."},
     {id:"B",label:"Choose overseas manufacturing",detail:"Lower cost, broader reach, lax oversight",es:30,sr:-15,ei:-20,framework:"teleological",feedback:"You maximized reach and profit for the greatest number of customers, but shifted the human and environmental burden offshore."}
   ],
   teaching:{objective:"Weigh the trade-off between broad market accessibility and the labor/environmental conditions that enable low costs.",
     discussion:["Does reaching 5x more customers morally outweigh the conditions at the overseas facility?","What does 'passed basic audits' actually guarantee? Who sets the audit standards?","Is there a responsibility to improve overseas conditions rather than just avoid them?","How should transport emissions factor into the decision?"],
     frameworks:"Option A is deontological: a duty to workers and community regardless of cost. Option B is teleological: greater aggregate access is weighed against outsourced harm."}},
  {id:4,phase:2,phaseName:"Growth & Scaling",title:"Data Privacy",
   prompt:"Advertising firms offer big contracts for anonymized workplace data. This could cut your price 40% and reach smaller businesses. Your customers named privacy as a top concern.",
   story:"Your privacy policy allows sharing with consent, but consent flows are often rubber-stamped. The data could also aid research institutions.",
   options:[
     {id:"A",label:"Implement data monetization",detail:"New revenue, cheaper product, privacy risk",es:25,sr:-20,ei:-10,framework:"teleological",feedback:"You weighed the aggregate benefit against eroding the very trust customers asked you to protect."},
     {id:"B",label:"Maintain strict privacy standards",detail:"Keep the promise, miss the revenue",es:-15,sr:25,ei:5,framework:"deontological",feedback:"You treated data privacy as a duty, not a negotiable trade-off. Trust grows, but the price stays higher for the customers you wanted to help."}
   ],
   teaching:{objective:"Examine consent, anonymization, and whether privacy is a negotiable value or a fundamental right.",
     discussion:["Is anonymized data truly harmless? What re-identification risks exist?","Does user consent in a privacy policy reflect genuine informed consent, or legal cover?","Is cheaper access for small businesses a sufficient justification for monetizing behavioral data?","Could the research-institution benefit path change the ethical calculus?"],
     frameworks:"Option A is teleological: aggregate access for many is weighed against erosion of an expressed value. Option B is deontological: privacy is treated as a duty grounded in the promise made to customers."}},
  {id:5,phase:3,phaseName:"Market Leadership",title:"Competition Response",
   prompt:"Your competitor grabs 35% market share in 3 months using guaranteed results via unauthorized access to client systems. Your ethical stance has cost you 20% share. 3 major customers may switch.",
   story:"The pressure is real: clients now demand similar guarantees, and your sales team is feeling the squeeze.",
   options:[
     {id:"A",label:"Maintain ethical practices and educate customers",detail:"Hold the line, teach the market",es:-25,sr:30,ei:10,framework:"deontological",feedback:"You refused to win by deception, even at significant cost. By educating customers you may reshape what the market rewards."},
     {id:"B",label:"Match competitor tactics to maintain market share",detail:"Play their game to survive",es:15,sr:-25,ei:-15,framework:"teleological",feedback:"You rationalized that staying in business justified bending the rules. Each compromise makes the next easier."}
   ],
   teaching:{objective:"Confront competitive pressure to compromise ethics and the slippery slope of normalized misconduct.",
     discussion:["Is unauthorized access clearly illegal, or genuinely a gray area?","Can educating customers realistically win against a competitor offering guaranteed results?","What responsibility does an ethical company have to customers it loses to a rival?","Where is the line between adapting to survive and abandoning your values?"],
     frameworks:"Option A is deontological: deception and unauthorized access are wrong regardless of competitive cost. Option B is teleological: preserving the company is weighed against the harm of the tactic."}},
  {id:6,phase:4,phaseName:"Legacy Building",title:"Exit Strategy",
   prompt:"After 5 years, a sustainable cooperative offers $50M and will keep your ethics, workforce, and commitments. A conglomerate offers $120M but will fold your tech into aggressive automation and poor environmental practices. 200 employees and many clients are affected.",
   story:"This final decision tests whether financial success can be balanced with social and environmental responsibility, and what your legacy will be.",
   options:[
     {id:"A",label:"Accept the conglomerate offer",detail:"Higher payout, values at risk",es:40,sr:-20,ei:-30,framework:"teleological",feedback:"You captured the maximum financial outcome. The technology you built may now accelerate harm you once refused to enable."},
     {id:"B",label:"Accept the sustainable business offer",detail:"Lower payout, values preserved",es:-30,sr:35,ei:25,framework:"deontological",feedback:"You let your legacy be defined by your values, not your valuation. The people and planet you protected are your enduring return."}
   ],
   teaching:{objective:"Reflect on the founder's legacy and whether past ethical choices are undone or cemented by the exit.",
     discussion:["Does the founder owe more to employees, clients, and the mission, or to their own financial outcome?","Can the conglomerate's integration undo five years of ethical practice? Is that risk acceptable?","Is the $70M difference a fair price for your values, or an impossible one to refuse?","How does this scenario map onto real-world acquisitions of ethically-positioned startups?"],
     frameworks:"Option A is teleological: maximum financial return is the outcome to optimize. Option B is deontological: the duty to the people, planet, and commitments you built endures beyond ownership."}}
];

const START={ES:50,SR:50,EI:50};
const MIN_T=30;

// ─── State ────────────────────────────────────────────────
let state={phase:"intro",index:0,scores:Object.assign({},START),history:[],completed:false};

// ─── Helpers ──────────────────────────────────────────────
function clampVal(n){return Math.max(0,Math.min(100,n));}
function sign(n){return n>0?"+"+n:""+n;}
function toneFor(v){return v<MIN_T?"danger":v<50?"warn":"ok";}
function barColor(t,m){return t==="danger"?"#f87171":t==="warn"?"#fbbf24":m.color;}

// ─── Renderers ────────────────────────────────────────────
const app=document.getElementById("app");

function metricRow(m,val,delta){
  const tone=toneFor(val);
  const bc=barColor(tone,m);
  let deltaHtml="";
  if(delta!==undefined&&delta!==0){
    deltaHtml='<span style="margin-left:4px;color:'+(delta>0?"#34d399":"#f87171")+'">'+sign(delta)+'</span>';
  }
  let warn= tone==="danger"?'<span style="font-size:10px;color:#f87171;font-weight:600">Below 30</span>':'';
  return '<div style="display:flex;flex-direction:column;gap:5px">'+
    '<div style="display:flex;justify-content:space-between;font-size:13px">'+
      '<span style="font-weight:600;color:#cdd9ee">'+m.full+'</span>'+
      '<span style="font-weight:700;color:'+bc+';font-variant-numeric:tabular-nums">'+val+deltaHtml+'</span>'+
    '</div>'+
    '<div class="metric-bar">'+
      '<div class="metric-fill" style="width:'+val+'%;background:'+bc+'"></div>'+
      '<div class="threshold-mark" style="left:'+MIN_T+'%"></div>'+
    '</div>'+
    '<div style="display:flex;justify-content:space-between;font-size:10px;color:#6b7d99">'+
      '<span>'+m.desc+'</span>'+warn+
    '</div></div>';
}

function render(){
  if(state.phase==="intro")return renderIntro();
  if(state.phase==="playing")return renderGame();
  if(state.phase==="ended")return renderEnd();
}

// ─── Intro screen ──────────────────────────────────────────
function renderIntro(){
  let metricCards="";
  for(const m of METRICS){
    metricCards+='<div class="card" style="border-color:#2a3a56">'+
      '<div style="display:flex;align-items:center;gap:8px"><span style="width:12px;height:12px;border-radius:50%;background:'+m.color+'"></span><span style="font-size:14px;font-weight:600;color:#e2e8f0">'+m.full+'</span></div>'+
      '<p style="font-size:12px;color:#6b7d99;margin-top:6px">'+m.desc+'</p>'+
      '<p style="font-size:12px;color:#6b7d99;margin-top:6px">Starts at <b style="color:#cdd9ee">50</b> · Min to operate: <b style="color:#f87171">30</b></p></div>';
  }
  app.innerHTML='<div class="container fade">'+
    '<span class="badge badge-sky">Interactive Decision Game</span>'+
    '<h1 style="margin-top:14px">Startup Ethics</h1>'+
    '<p style="font-size:18px;font-weight:500;color:#38bdf8;margin-top:4px">The Entrepreneurial Journey</p>'+
    '<p style="color:#94a8c4;margin-top:16px">Step into the role of a startup founder navigating ethical challenges across four stages of business development. Every decision shapes three metrics — and your company\'s right to keep operating.</p>'+
    '<div style="display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-top:24px">'+metricCards+'</div>'+
    '<h2 style="margin-top:28px;font-size:18px">Two ethical lenses guide each choice</h2>'+
    '<div style="display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-top:10px">'+
      '<div class="card" style="border-color:#a78bfa40;background:#1a1530"><h3 style="color:#a78bfa;font-size:14px">Deontological Ethics</h3><p style="font-size:12px;color:#8395b0;margin-top:6px;line-height:1.5">Actions are right or wrong in themselves. Focus on duty, universal principles, individual dignity, and the means — not the ends.</p></div>'+
      '<div class="card" style="border-color:#fbbf2440;background:#1a1305"><h3 style="color:#fbbf24;font-size:14px">Teleological Ethics</h3><p style="font-size:12px;color:#8395b0;margin-top:6px;line-height:1.5">Judge actions by their outcomes. Greatest good for the greatest number, cost-benefit, ripple effects — the ends can justify the means.</p></div>'+
    '</div>'+
    '<p style="font-size:14px;color:#6b7d99;margin-top:24px">The game has <b style="color:#cdd9ee">'+SCENARIOS.length+' scenarios</b> across 4 phases. If any metric drops below 30, your company can no longer operate — choose carefully.</p>'+
    '<button class="btn btn-primary" style="margin-top:20px" onclick="startGame()">Begin the journey →</button>'+
    '<div style="margin-top:16px"><button class="btn btn-outline" onclick="toggleIntroTeach()" id="introTeachBtn">📋 Instructor overview ▸</button><div id="introTeach" style="display:none;margin-top:12px"></div></div>'+
  '</div>';
}

function toggleIntroTeach(){
  const panel=document.getElementById("introTeach");
  const btn=document.getElementById("introTeachBtn");
  if(panel.style.display==="none"){
    let outcomes=["Distinguish deontological (duty-based) from teleological (outcome-based) ethical reasoning.","Apply two ethical frameworks to realistic startup decisions across four business phases.","Evaluate trade-offs between economic, social, and environmental sustainability.","Reflect on how competitive pressure and financial incentives erode ethical commitments."];
    let moments=["Scenarios 1-2: founding choices set values before pressure appears.","Scenarios 3-4: scaling creates new stakeholders and temptations.","Scenario 5: survival pressure tests whether values are real or aspirational.","Scenario 6: the exit is where past commitments are most cheaply abandoned."];
    panel.style.display="block";
    panel.innerHTML='<div class="card" style="border-color:#fbbf2440;background:#1a1305">'+
      '<div style="display:flex;align-items:center;gap:8px"><span style="font-size:18px">📋</span><h3 style="color:#fbbf24;font-size:14px">How to use this game in class</h3></div>'+
      '<p class="section-label" style="margin-top:14px">Learning outcomes</p>'+
      '<ul style="list-style:none">'+outcomes.map(function(o){return '<li class="q-item"><span>›</span><span>'+o+'</span></li>'}).join("")+'</ul>'+
      '<p class="section-label" style="margin-top:14px">Suggested format</p>'+
      '<p style="font-size:14px;color:#94a8c4">Play individually or in small groups. After each scenario, pause for 3-5 minutes of discussion using the on-screen teaching notes (toggle 📋 during play). Compare choices and reasoning across groups. At the end, debrief using the ethical profile and decision log.</p>'+
      '<p class="section-label" style="margin-top:14px">Key teaching moments</p>'+
      '<ul style="list-style:none">'+moments.map(function(o){return '<li class="q-item"><span>›</span><span>'+o+'</span></li>'}).join("")+'</ul>'+
      '<div style="border:1px solid #fbbf2430;background:#1a1505;border-radius:8px;padding:10px;margin-top:14px"><p class="section-label">Note on the fail condition</p><p style="font-size:14px;color:#94a8c4;margin-top:4px">A metric below 30 ends the game early. This mirrors real consequences: a company that ignores any single dimension of sustainability long enough ceases to be viable. Use a mid-game failure as a discussion point, not a punishment.</p></div>'+
    '</div>';
    btn.innerHTML="📋 Instructor overview ▾";
  }else{
    panel.style.display="none";
    btn.innerHTML="📋 Instructor overview ▸";
  }
}

// ─── Game screen ───────────────────────────────────────────
let gameTeachingOpen=false;
let pendingOption=null;

function renderGame(){
  const sc=SCENARIOS[state.index];
  gameTeachingOpen=false;
  pendingOption=null;
  let metricHtml="";
  for(const m of METRICS){metricHtml+=metricRow(m,state.scores[m.key]);}
  let optHtml="";
  for(const opt of sc.options){
    let chips="";
    for(const m of METRICS){const v=opt[m.key.toLowerCase()];chips+='<span class="impact-chip '+(v>0?"pos":v<0?"neg":"zero")+'">'+m.key+" "+sign(v)+'</span>';}
    optHtml+='<div class="btn-opt" id="opt-'+opt.id+'" onclick="selectOption(\''+opt.id+'\')">'+
      '<div style="display:flex;align-items:center;gap:8px"><span style="width:28px;height:28px;border-radius:50%;background:#33415580;display:flex;align-items:center;justify-content:center;font-size:14px;font-weight:700;flex-shrink:0">'+opt.id+'</span></div>'+
      '<h3 style="font-size:14px;font-weight:600;color:#e2e8f0;margin-top:10px">'+opt.label+'</h3>'+
      '<p style="font-size:12px;color:#6b7d99;margin-top:3px">'+opt.detail+'</p>'+
      '<div style="display:flex;flex-wrap:wrap;gap:5px;margin-top:10px">'+chips+'</div>'+
      '<div id="fb-'+opt.id+'" style="display:none;margin-top:10px;border-top:1px solid #38bdf840;padding-top:10px;font-size:13px;line-height:1.5;color:#7dd3fc"></div></div>';
  }
  app.innerHTML='<div class="container fade">'+
    '<div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:14px;flex-wrap:wrap;gap:8px">'+
      '<span class="badge badge-slate">Phase '+sc.phase+' · '+sc.phaseName+'</span>'+
      '<div style="display:flex;align-items:center;gap:8px"><span style="font-size:12px;color:#6b7d99">Scenario '+(state.index+1)+' of '+SCENARIOS.length+'</span><button class="btn btn-outline" style="padding:5px 12px;font-size:13px" onclick="toggleGameTeach()" id="gameTeachBtn">📋 Teaching notes ▸</button></div>'+
    '</div>'+
    '<div class="card" style="margin-bottom:16px">'+metricHtml+'</div>'+
    '<div class="card"><h2 style="font-size:20px">'+sc.title+'</h2><p style="color:#94a8c4;margin-top:10px;line-height:1.6">'+sc.prompt+'</p><p style="font-size:14px;font-style:italic;color:#6b7d99;margin-top:8px">'+sc.story+'</p></div>'+
    '<div id="gameTeach" style="display:none"></div>'+
    '<div style="display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-top:14px">'+optHtml+'</div>'+
    '<div id="pendingMsg" style="display:none;text-align:center;font-size:13px;color:#6b7d99;margin-top:14px">Applying your decision…</div>'+
  '</div>';
}

function toggleGameTeach(){
  const panel=document.getElementById("gameTeach");
  const btn=document.getElementById("gameTeachBtn");
  const sc=SCENARIOS[state.index];
  gameTeachingOpen=!gameTeachingOpen;
  if(gameTeachingOpen){
    panel.style.display="block";
    panel.innerHTML='<div class="teach-box"><div style="display:flex;align-items:center;gap:8px"><span style="font-size:18px">📋</span><h3 style="color:#fbbf24;font-size:14px">Teaching notes — '+sc.title+'</h3></div>'+
      '<p class="section-label" style="margin-top:12px">Learning objective</p><p style="font-size:14px;color:#94a8c4">'+sc.teaching.objective+'</p>'+
      '<p class="section-label" style="margin-top:12px">Discussion questions</p><ul style="list-style:none">'+sc.teaching.discussion.map(function(q){return '<li class="q-item"><span>›</span><span>'+q+'</span></li>'}).join("")+'</ul>'+
      '<div style="border:1px solid #fbbf2430;background:#1a1505;border-radius:8px;padding:10px;margin-top:12px"><p class="section-label">Framework analysis</p><p style="font-size:14px;color:#94a8c4;margin-top:4px">'+sc.teaching.frameworks+'</p></div></div>';
    btn.innerHTML="📋 Teaching notes ▾";
  }else{
    panel.style.display="none";
    btn.innerHTML="📋 Teaching notes ▸";
  }
}

function selectOption(id){
  if(pendingOption)return;
  pendingOption=id;
  const sc=SCENARIOS[state.index];
  const opt=sc.options.find(function(o){return o.id===id;});
  if(!opt)return;
  document.getElementById("opt-"+id).classList.add("selected");
  document.getElementById("fb-"+id).style.display="block";
  document.getElementById("fb-"+id).textContent=opt.feedback;
  const other=sc.options.find(function(o){return o.id!==id;});
  if(other)document.getElementById("opt-"+other.id).classList.add("dimmed");
  document.getElementById("pendingMsg").style.display="block";
  setTimeout(function(){applyChoice(opt);},1500);
}

function applyChoice(opt){
  const sc=SCENARIOS[state.index];
  state.scores.ES=clampVal(state.scores.ES+opt.es);
  state.scores.SR=clampVal(state.scores.SR+opt.sr);
  state.scores.EI=clampVal(state.scores.EI+opt.ei);
  state.history.push({scenario:sc,option:opt});
  const failed=state.scores.ES<MIN_T||state.scores.SR<MIN_T||state.scores.EI<MIN_T;
  if(failed||state.index+1>=SCENARIOS.length){
    state.completed=!failed;
    state.phase="ended";
    render();
  }else{
    state.index++;
    render();
  }
}

// ─── End screen ────────────────────────────────────────────
let endTeachingOpen=false;

function renderEnd(){
  let metricHtml="";
  for(const m of METRICS){metricHtml+=metricRow(m,state.scores[m.key]);}
  const avg=(state.scores.ES+state.scores.SR+state.scores.EI)/3;
  let verdict,tone;
  if(!state.completed){verdict="Operations suspended";tone="#f87171";}
  else if(avg>=65){verdict="Ethical unicorn — rare balance achieved";tone="#34d399";}
  else if(avg>=50){verdict="Sustainable operator — solid, improvable";tone="#38bdf8";}
  else{verdict="Survivor — but at a cost";tone="#fbbf24";}
  const deonto=state.history.filter(function(h){return h.option.framework==="deontological";}).length;
  const teleo=state.history.filter(function(h){return h.option.framework==="teleological";}).length;
  const total=state.history.length||1;
  let profile;
  if(deonto>teleo)profile="You leaned on duty and principles, even when costly. You weighed the means as carefully as the ends.";
  else if(teleo>deonto)profile="You leaned on outcomes — the greatest good for the greatest number. Watch for when the ends quietly stop justifying themselves.";
  else profile="You balanced principle and outcome, adapting each decision to its context. This flexibility is a strength — and a responsibility.";
  let decLog="";
  for(const h of state.history){
    decLog+='<div class="decision-row"><span class="pill">'+h.option.id+'</span><div style="flex:1;min-width:0"><p style="font-size:13px;font-weight:600;color:#cdd9ee">'+h.scenario.title+'</p><p style="font-size:12px;color:#6b7d99;white-space:nowrap;overflow:hidden;text-overflow:ellipsis">'+h.option.label+'</p></div></div>';
  }
  let scenarioReview="";
  for(const s of SCENARIOS){
    const chosen=state.history.find(function(h){return h.scenario.id===s.id;});
    let choseBadge=chosen?'<span class="badge badge-slate" style="margin-left:auto">Chose '+chosen.option.id+'</span>':"";
    scenarioReview+='<div class="card" style="border-color:#fbbf2440;background:#1a1305;margin-bottom:10px"><div style="display:flex;align-items:center;gap:8px"><span class="badge badge-slate">Phase '+s.phase+'</span><h3 style="color:#fbbf24;font-size:14px">'+s.title+'</h3>'+choseBadge+'</div><p style="font-size:14px;color:#94a8c4;margin-top:8px"><span style="font-weight:600;color:#fbbf2499">Objective: </span>'+s.teaching.objective+'</p><ul style="list-style:none;margin-top:8px">'+s.teaching.discussion.map(function(q){return '<li class="q-item"><span>›</span><span>'+q+'</span></li>';}).join("")+'</ul></div>';
  }
  app.innerHTML='<div class="container fade">'+
    '<h1 style="font-size:28px">'+(state.completed?"Journey complete":"Game over")+'</h1>'+
    '<p style="font-size:18px;font-weight:600;color:'+tone+';margin-top:4px">'+verdict+'</p>'+
    (state.completed?'':'<p style="font-size:14px;color:#6b7d99;margin-top:10px">One of your metrics fell below the minimum threshold of 30. Your company can no longer operate. Reflect on which trade-offs led here.</p>')+
    '<div class="card" style="margin-top:20px"><div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:16px">'+metricHtml+'</div></div>'+
    '<h2 style="margin-top:24px;font-size:18px">Your ethical profile</h2>'+
    '<div class="card" style="margin-top:10px"><div style="display:flex;align-items:center;gap:10px;font-size:14px"><span style="font-weight:600;color:#a78bfa">Deontological '+deonto+'</span><div class="profile-bar"><div class="profile-fill" style="width:'+(deonto/total*100)+'%;background:#a78bfa"></div></div><span style="font-weight:600;color:#fbbf24">Teleological '+teleo+'</span></div><p style="font-size:13px;color:#8395b0;margin-top:10px;line-height:1.5">'+profile+'</p></div>'+
    '<h2 style="margin-top:24px;font-size:18px">Your decisions</h2><div style="margin-top:10px">'+decLog+'</div>'+
    '<div style="margin-top:20px"><button class="btn btn-outline" onclick="toggleEndTeach()" id="endTeachBtn">📋 Review all teaching notes ▸</button><div id="endTeach" style="display:none;margin-top:12px">'+scenarioReview+'</div></div>'+
    '<button class="btn btn-primary" style="margin-top:24px" onclick="restart()">↺ Play again</button>'+
  '</div>';
  endTeachingOpen=false;
}

function toggleEndTeach(){
  const panel=document.getElementById("endTeach");
  const btn=document.getElementById("endTeachBtn");
  endTeachingOpen=!endTeachingOpen;
  panel.style.display=endTeachingOpen?"block":"none";
  btn.innerHTML="📋 Review all teaching notes "+(endTeachingOpen?"▾":"▸");
}

// ─── State transitions ─────────────────────────────────────
function startGame(){
  state.scores=Object.assign({},START);
  state.history=[];
  state.index=0;
  state.completed=false;
  state.phase="playing";
  render();
}
function restart(){startGame();}

// ─── Boot ─────────────────────────────────────────────────
render();
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>منصة الفهم القرائي</title>
  <style>
    :root{
      --bg1:#0ea5e9; --bg2:#22c55e; --card:#ffffff;
      --text:#0f172a; --muted:#64748b; --primary:#2563eb;
      --good:#16a34a; --bad:#dc2626; --shadow:0 10px 30px rgba(0,0,0,.12);
      --radius:18px;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family: system-ui, -apple-system, "Segoe UI", Tahoma, Arial;
      color:var(--text);
      background: linear-gradient(135deg, var(--bg1), var(--bg2));
      min-height:100vh;
      display:flex;
      align-items:center;
      justify-content:center;
      padding:18px;
    }
    .app{width:min(920px, 100%);}
    header{
      display:flex; gap:12px; align-items:center; justify-content:space-between;
      color:white; margin-bottom:14px;
    }
    .brand{display:flex; gap:10px; align-items:center}
    .logo{
      width:44px;height:44px;border-radius:14px;
      background: rgba(255,255,255,.18);
      display:grid;place-items:center;
      box-shadow: var(--shadow);
      backdrop-filter: blur(6px);
      font-size:22px;
    }
    .title{line-height:1.2}
    .title h1{margin:0;font-size:20px}
    .title p{margin:2px 0 0;opacity:.9;font-size:13px}
    .pill{
      display:flex; gap:10px; align-items:center;
      background: rgba(255,255,255,.16);
      padding:10px 12px;border-radius:999px;
      backdrop-filter: blur(6px);
      box-shadow: var(--shadow);
      font-size:13px;
    }
    .pill b{font-size:14px}
    .grid{
      display:grid;
      grid-template-columns: 1.1fr .9fr;
      gap:14px;
    }
    @media (max-width: 820px){ .grid{grid-template-columns:1fr;} }
    .card{
      background: var(--card);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      padding:16px;
    }
    .card h2{margin:0 0 10px;font-size:18px}
    .muted{color:var(--muted);font-size:13px;margin-top:6px}
    .levels{display:flex;flex-wrap:wrap;gap:10px;margin-top:8px}
    .lvl{
      border:1px solid #e2e8f0;
      border-radius:14px;
      padding:10px 12px;
      cursor:pointer;
      user-select:none;
      transition:.15s;
      display:flex; gap:8px; align-items:center;
      background:#fff;
    }
    .lvl:hover{transform:translateY(-1px)}
    .lvl.active{border-color: rgba(37,99,235,.4); box-shadow:0 6px 16px rgba(37,99,235,.12)}
    .tag{font-size:12px;color:var(--primary);background:rgba(37,99,235,.08);padding:4px 8px;border-radius:999px}
    .btn{
      border:0; border-radius:14px;
      padding:12px 14px;
      cursor:pointer;
      font-weight:700;
      box-shadow: var(--shadow);
      transition:.15s;
    }
    .btn:active{transform:scale(.98)}
    .btn.primary{background:var(--primary);color:white}
    .btn.ghost{background:#f1f5f9;color:#0f172a;box-shadow:none}
    .row{display:flex;gap:10px;flex-wrap:wrap}
    .qbox{
      border:1px solid #e2e8f0;border-radius:16px;
      padding:14px;margin-top:12px;
      background: #fafafa;
    }
    .story{
      background: #0b1220;
      color:#e5e7eb;
      border-radius:16px;
      padding:14px;
      line-height:1.9;
      font-size:15px;
      box-shadow: inset 0 0 0 1px rgba(255,255,255,.06);
    }
    .question{margin:10px 0 6px;font-weight:800}
    .choices{display:grid;gap:10px;margin-top:8px}
    .choice{
      border:1px solid #e2e8f0;
      border-radius:14px;
      padding:12px;
      cursor:pointer;
      background:white;
      transition:.12s;
      text-align:right;
    }
    .choice:hover{border-color:rgba(37,99,235,.35)}
    .choice.correct{border-color:rgba(22,163,74,.45); background:rgba(22,163,74,.08)}
    .choice.wrong{border-color:rgba(220,38,38,.45); background:rgba(220,38,38,.08)}
    .bar{
      height:12px; background:#e2e8f0; border-radius:999px; overflow:hidden;
      margin-top:10px;
    }
    .fill{height:100%; width:0%; background: var(--primary); transition:.35s}
    .kpis{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-top:10px}
    .kpi{background:#f8fafc;border:1px solid #e2e8f0;border-radius:16px;padding:10px}
    .kpi b{display:block;font-size:18px}
    .kpi span{font-size:12px;color:var(--muted)}
    .foot{margin-top:12px;font-size:12px;color:rgba(255,255,255,.9);text-align:center}
  </style>
</head>

<body>
  <div class="app">
    <header>
      <div class="brand">
        <div class="logo">📚</div>
        <div class="title">
          <h1>منصة الفهم القرائي</h1>
          <p>اختر مستوى، اقرأ النص، ثم أجب لتحصل على نقاطك 🎯</p>
        </div>
      </div>
      <div class="pill">
        <div>⭐ النقاط: <b id="score">0</b></div>
        <div>✅ الصحيح: <b id="ok">0</b></div>
        <div>❌ الخطأ: <b id="bad">0</b></div>
      </div>
    </header>

    <div class="grid">
      <div class="card">
        <h2>1) اختر مستوى الفهم</h2>
        <div class="levels" id="levels"></div>
        <div class="muted">المستويات: حرفي، استنتاجي، نقدي، تذوقي، إبداعي.</div>

        <div class="qbox">
          <div class="story" id="story"></div>

          <div class="question" id="qtext"></div>
          <div class="choices" id="choices"></div>

          <div class="row" style="margin-top:12px">
            <button class="btn primary" id="nextBtn">سؤال جديد ➜</button>
            <button class="btn ghost" id="resetBtn">إعادة من البداية</button>
          </div>

          <div class="bar"><div class="fill" id="progress"></div></div>
          <div class="muted" id="hint"></div>
        </div>
      </div>

      <div class="card">
        <h2>2) لوحة التحفيز</h2>
        <div class="muted">هدف اليوم: ركّز على قراءة الفقرة مرتين قبل الإجابة.</div>

        <div class="kpis">
          <div class="kpi"><b id="lvlName">—</b><span>المستوى الحالي</span></div>
          <div class="kpi"><b id="streak">0</b><span>سلسلة إجابات صحيحة</span></div>
          <div class="kpi"><b id="qNum">1</b><span>رقم السؤال</span></div>
        </div>

        <div class="qbox" style="margin-top:12px">
          <b>🏅 تحدّي صغير</b>
          <div class="muted" id="challenge">احصل على 3 إجابات صحيحة متتالية لتفتح "نص جديد".</div>
        </div>

        <div class="qbox" style="margin-top:12px">
          <b>💡 تلميح تربوي</b>
          <div class="muted" id="tip">اقرأ العنوان، ثم ابحث عن الفكرة العامة، ثم التفاصيل.</div>
        </div>
      </div>
    </div>

    <div class="foot">صُممت للمتعلمين — بسيطة، ممتعة، وتعمل على الجوال ✅</div>
  </div>

<script>
  const $ = (id)=>document.getElementById(id);

  const levels = [
    { id:"literal",   name:"حرفي",   tag:"ماذا قال النص؟", tip:"ابحث عن كلمة أو جملة صريحة داخل النص." },
    { id:"infer",     name:"استنتاجي", tag:"ماذا نفهم؟",  tip:"اربط بين جملتين لتستنتج معنى غير مباشر." },
    { id:"critical",  name:"نقدي",   tag:"هل أوافق؟ ولماذا؟", tip:"قيّم الفكرة: منطقها/دليلها/مناسبتها." },
    { id:"aesthetic", name:"تذوقي",  tag:"جمال اللغة",   tip:"انتبه للتشبيه/الصور/المشاعر في الكلمات." },
    { id:"creative",  name:"إبداعي", tag:"ماذا لو؟",     tip:"تخيل نهاية أخرى أو عنوانًا مختلفًا." },
  ];

  const texts = [
    {
      title:"رحلة إلى المكتبة",
      body:"خرج سالم مع والده إلى المكتبة القريبة. رأى رفوفًا مليئة بالقصص، فاختار كتابًا عن البحر. جلس يقرأ بهدوء، ثم دوّن ثلاث فوائد تعلمها. في طريق العودة قال لوالده: أصبحت القراءة مغامرة!"
    },
    {
      title:"حديقة المدرسة",
      body:"في صباح جميل، لاحظت المعلمة أن الحديقة تحتاج عناية. تعاون الطلاب في تنظيفها وسقي النباتات. وبعد أسبوع ظهرت أزهار جديدة. فرح الجميع لأن العمل الجماعي صنع فرقًا واضحًا."
    }
  ];

  const bank = {
    literal: [
      (t)=>({
        q:`ما عنوان النص؟`,
        choices:[t.title, "المدينة الكبيرة", "مغامرة في الصحراء"],
        a:0
      }),
      (t)=>({
        q:`ماذا اختار سالم في المكتبة؟`,
        choices:["كتاب عن البحر","كرة قدم","قلم جديد"],
        a:0, only:"رحلة إلى المكتبة"
      }),
      (t)=>({
        q:`ماذا فعل الطلاب في الحديقة؟`,
        choices:["نظفوها وسقوا النباتات","كسروا الأغصان","تركوا المكان كما هو"],
        a:0, only:"حديقة المدرسة"
      })
    ],
    infer: [
      (t)=>({
        q:`لماذا قال سالم: "أصبحت القراءة مغامرة"؟`,
        choices:["لأنه اكتشف متعة ومعرفة جديدة","لأنه ضاع الطريق","لأنه تعب من القراءة"],
        a:0, only:"رحلة إلى المكتبة"
      }),
      (t)=>({
        q:`ماذا نستنتج من ظهور الأزهار بعد أسبوع؟`,
        choices:["العناية المستمرة تؤتي ثمارها","الماء يفسد النباتات","الحديقة لا تتغير"],
        a:0, only:"حديقة المدرسة"
      })
    ],
    critical: [
      (t)=>({
        q:`أي رأي هو الأقرب للصواب؟`,
        choices:["تدوين الفوائد يساعد على تثبيت الفهم","القراءة مضيعة للوقت","لا حاجة للتعاون في المدرسة"],
        a:0
      })
    ],
    aesthetic: [
      (t)=>({
        q:`أي عبارة تحمل شعورًا إيجابيًا واضحًا؟`,
        choices:["أصبحت القراءة مغامرة","تحتاج عناية","ظهرَت أزهار"],
        a:0, only:"رحلة إلى المكتبة"
      }),
      (t)=>({
        q:`ما الكلمة التي توحي بجمال المشهد؟`,
        choices:["صباح جميل","تحتاج","واضح"],
        a:0, only:"حديقة المدرسة"
      })
    ],
    creative: [
      (t)=>({
        q:`اختر عنوانًا جديدًا مناسبًا للنص:`,
        choices:["خطوة نحو المعرفة","يوم بلا هدف","الضوضاء الكبيرة"],
        a:0
      }),
      (t)=>({
        q:`ماذا يمكن أن يحدث لو استمر الطلاب بالعناية شهرًا؟`,
        choices:["تصبح الحديقة أجمل وتكثر الأزهار","تختفي النباتات فورًا","لا يحدث أي تغيير"],
        a:0
      })
    ]
  };

  const state = {
    levelId: "literal",
    textIndex: 0,
    score: 0,
    ok: 0,
    bad: 0,
    streak: 0,
    qNum: 1,
    locked: false,
    lastCorrect: null
  };

  function currentText(){ return texts[state.textIndex]; }

  function pickQuestion(){
    const lvl = state.levelId;
    const t = currentText();
    let pool = bank[lvl].slice();

    // فلترة أسئلة "only" بحسب النص
    pool = pool.filter(fn=>{
      const q = fn(t);
      return !q.only || q.only === t.title;
    });

    // إذا كانت المجموعة فارغة لأي سبب، خذ سؤال عام
    if(pool.length === 0) pool = bank[lvl];

    const fn = pool[Math.floor(Math.random()*pool.length)];
    return fn(t);
  }

  let currentQ = null;

  function renderLevels(){
    const box = $("levels");
    box.innerHTML = "";
    levels.forEach(l=>{
      const el = document.createElement("div");
      el.className = "lvl" + (l.id===state.levelId ? " active":"");
      el.innerHTML = `<span class="tag">${l.tag}</span> <b>${l.name}</b>`;
      el.onclick = ()=>{
        state.levelId = l.id;
        state.qNum = 1;
        state.streak = 0;
        state.locked = false;
        $("lvlName").textContent = l.name;
        $("tip").textContent = l.tip;
        document.querySelectorAll(".lvl").forEach(x=>x.classList.remove("active"));
        el.classList.add("active");
        newQuestion(true);
      };
      box.appendChild(el);
    });
    const cur = levels.find(x=>x.id===state.levelId);
    $("lvlName").textContent = cur.name;
    $("tip").textContent = cur.tip;
  }

  function renderStory(){
    const t = currentText();
    $("story").innerHTML = `<b style="color:#93c5fd">📌 ${t.title}</b><br>${t.body}`;
  }

  function renderStats(){
    $("score").textContent = state.score;
    $("ok").textContent = state.ok;
    $("bad").textContent = state.bad;
    $("streak").textContent = state.streak;
    $("qNum").textContent = state.qNum;
    $("progress").style.width = Math.min(100, (state.qNum-1)*10) + "%";
  }

  function newQuestion(resetHint=false){
    state.locked = false;
    currentQ = pickQuestion();
    renderStory();
    $("qtext").textContent = `❓ ${currentQ.q}`;
    const c = $("choices");
    c.innerHTML = "";
    currentQ.choices.forEach((txt, idx)=>{
      const b = document.createElement("button");
      b.className = "choice";
      b.textContent = txt;
      b.onclick = ()=>answer(idx, b);
      c.appendChild(b);
    });

    const lvl = levels.find(x=>x.id===state.levelId);
    $("hint").textContent = resetHint ? `💡 تلميح: ${lvl.tip}` : $("hint").textContent;
    renderStats();
  }

  function answer(idx, btn){
    if(state.locked) return;
    state.locked = true;

    const buttons = Array.from(document.querySelectorAll(".choice"));
    buttons.forEach((b, i)=>{
      if(i===currentQ.a) b.classList.add("correct");
    });

    if(idx === currentQ.a){
      btn.classList.add("correct");
      state.ok += 1;
      state.score += 10;
      state.streak += 1;
      $("hint").textContent = "✅ أحسنت! إجابة صحيحة. +10 نقاط";
      if(state.streak >= 3){
        $("challenge").textContent = "🎉 ممتاز! افتُتح لك نص جديد. انتقلنا للنص التالي.";
        state.textIndex = (state.textIndex + 1) % texts.length;
        state.streak = 0;
      } else {
        $("challenge").textContent = `🏅 تبقى ${3-state.streak} للوصول إلى 3 إجابات صحيحة متتالية.`;
      }
    } else {
      btn.classList.add("wrong");
      state.bad += 1;
      state.streak = 0;
      $("hint").textContent = "❌ ليست الصحيحة. اقرأ الفقرة مرة أخرى ثم جرّب سؤالًا جديدًا.";
      $("challenge").textContent = "🏅 حاول تكوين سلسلة جديدة من الإجابات الصحيحة.";
    }

    renderStats();
  }

  $("nextBtn").addEventListener("click", ()=>{
    state.qNum += 1;
    newQuestion();
  });

  $("resetBtn").addEventListener("click", ()=>{
    state.score = 0; state.ok = 0; state.bad = 0;
    state.streak = 0; state.qNum = 1; state.textIndex = 0;
    $("challenge").textContent = "احصل على 3 إجابات صحيحة متتالية لتفتح \"نص جديد\".";
    newQuestion(true);
  });

  // init
  renderLevels();
  newQuestion(true);
</script>
</body>
</html>

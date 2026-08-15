# emr
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="color-scheme" content="light" />
  <title>隨身電子病歷｜Personal Medical Passport</title>
  <style>
    :root{
      --bg:#f4f9ff;
      --surface:#ffffff;
      --surface-2:#eef7ff;
      --primary:#1267d8;
      --primary-2:#2f8ff5;
      --primary-3:#dcebff;
      --ink:#12304e;
      --muted:#60758a;
      --line:#d7e7f7;
      --danger:#c93c4d;
      --warning:#8a5b00;
      --ok:#167b59;
      --shadow:0 16px 44px rgba(34, 92, 145, .12);
      --radius:22px;
    }

    *{box-sizing:border-box}
    html{scroll-behavior:smooth}
    body{
      margin:0;
      font-family:
        Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont,
        "Segoe UI", "Noto Sans TC", "Noto Sans CJK TC", "PingFang TC",
        "Hiragino Sans", "Apple SD Gothic Neo", Arial, sans-serif;
      color:var(--ink);
      background:
        radial-gradient(circle at 9% 0%, rgba(47,143,245,.10), transparent 30%),
        radial-gradient(circle at 92% 12%, rgba(18,103,216,.08), transparent 26%),
        var(--bg);
      line-height:1.62;
    }

    button, select, input{font:inherit}

    .shell{max-width:1180px;margin:auto;padding:24px}
    .topbar{
      position:sticky; top:12px; z-index:20;
      display:flex; gap:14px; align-items:center; justify-content:space-between;
      background:rgba(255,255,255,.88);
      backdrop-filter:blur(16px);
      -webkit-backdrop-filter:blur(16px);
      border:1px solid rgba(201,222,242,.9);
      border-radius:18px;
      padding:12px 14px;
      box-shadow:0 10px 28px rgba(34,92,145,.10);
      margin-bottom:20px;
    }

    .brand{display:flex;gap:11px;align-items:center;min-width:0}
    .brand-mark{
      width:40px;height:40px;border-radius:12px;
      display:grid;place-items:center;color:#fff;font-weight:900;font-size:21px;
      background:linear-gradient(145deg,var(--primary),#4ca6ff);
      box-shadow:0 8px 20px rgba(18,103,216,.25);
      flex:0 0 auto;
    }
    .brand-title{font-weight:850;letter-spacing:.01em;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
    .brand-sub{font-size:12px;color:var(--muted);margin-top:-2px}

    .toolbar{display:flex;gap:8px;align-items:center;flex-wrap:wrap;justify-content:flex-end}
    .btn, .lang-select{
      border:1px solid var(--line);
      background:var(--surface);
      color:var(--ink);
      border-radius:12px;
      padding:9px 11px;
      cursor:pointer;
      transition:.18s ease;
    }
    .btn:hover,.lang-select:hover{border-color:#a8cef3;transform:translateY(-1px)}
    .btn.primary{background:var(--primary);border-color:var(--primary);color:#fff}
    .btn.soft{background:var(--surface-2)}
    .btn.danger{color:var(--danger)}
    .btn:focus,.lang-select:focus,[contenteditable="true"]:focus{
      outline:3px solid rgba(47,143,245,.18);outline-offset:2px
    }

    .hero{
      position:relative;overflow:hidden;
      border-radius:30px;
      padding:38px;
      background:linear-gradient(135deg,#0e5fc7 0%,#2689f0 55%,#7fc0ff 100%);
      color:#fff;
      box-shadow:var(--shadow);
      margin-bottom:22px;
    }
    .hero:after{
      content:"";
      position:absolute; width:330px;height:330px;border-radius:50%;
      right:-100px;top:-130px;
      background:rgba(255,255,255,.13);
      box-shadow:-120px 210px 0 rgba(255,255,255,.08);
    }
    .hero-grid{display:grid;grid-template-columns:1.65fr 1fr;gap:24px;position:relative;z-index:1}
    .eyebrow{font-size:13px;font-weight:800;letter-spacing:.14em;text-transform:uppercase;opacity:.82}
    .hero h1{font-size:clamp(30px,5vw,54px);line-height:1.05;margin:10px 0 16px;letter-spacing:-.03em}
    .hero p{margin:0;max-width:720px;opacity:.9}
    .hero-card{
      align-self:end;
      border:1px solid rgba(255,255,255,.28);
      background:rgba(255,255,255,.14);
      border-radius:20px;
      padding:18px;
      backdrop-filter:blur(8px);
    }
    .hero-card strong{display:block;font-size:13px;opacity:.82;margin-bottom:4px}
    .hero-card .emergency-name{font-size:23px;font-weight:850}
    .hero-card .mini-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:15px}
    .mini{
      border-radius:14px;padding:10px 12px;background:rgba(255,255,255,.13)
    }
    .mini span{display:block;font-size:11px;opacity:.76}
    .mini b{font-size:15px}

    .notice{
      background:#fff8e7;
      border:1px solid #f1dda3;
      color:#6e5100;
      border-radius:16px;
      padding:12px 15px;
      margin-bottom:20px;
      font-size:14px;
    }

    .layout{display:grid;grid-template-columns:280px 1fr;gap:22px}
    .sidebar{position:sticky;top:92px;align-self:start}
    .nav-card,.card{
      background:var(--surface);
      border:1px solid var(--line);
      border-radius:var(--radius);
      box-shadow:0 8px 30px rgba(34,92,145,.07);
    }
    .nav-card{padding:14px}
    .nav-card a{
      display:flex;align-items:center;gap:10px;
      padding:10px 11px;margin:2px 0;border-radius:11px;
      color:var(--ink);text-decoration:none;font-size:14px;font-weight:700;
    }
    .nav-card a:hover{background:var(--surface-2);color:var(--primary)}
    .nav-dot{width:8px;height:8px;border-radius:50%;background:#8fc6fb;flex:0 0 auto}

    main{display:flex;flex-direction:column;gap:18px}
    .card{padding:24px}
    .section-title{
      display:flex;align-items:center;justify-content:space-between;gap:15px;
      margin-bottom:16px;
    }
    .title-wrap{display:flex;gap:12px;align-items:center}
    .icon{
      width:42px;height:42px;display:grid;place-items:center;border-radius:13px;
      background:linear-gradient(145deg,#e4f2ff,#f7fbff);
      border:1px solid #d3e8fb;font-size:21px;
    }
    h2{margin:0;font-size:21px;letter-spacing:-.01em}
    .section-note{font-size:12px;color:var(--muted)}

    .grid-2{display:grid;grid-template-columns:1fr 1fr;gap:14px}
    .grid-3{display:grid;grid-template-columns:repeat(3,1fr);gap:14px}
    .field{
      border:1px solid var(--line);
      border-radius:15px;
      padding:12px 13px;
      background:linear-gradient(180deg,#fff,#fbfdff);
      min-height:73px;
    }
    .field label{
      display:block;
      color:var(--muted);
      font-size:11px;
      font-weight:800;
      letter-spacing:.06em;
      text-transform:uppercase;
      margin-bottom:4px;
    }
    .editable{
      min-height:24px;
      border-radius:7px;
      padding:2px 4px;
      margin:-2px -4px;
      white-space:pre-wrap;
    }
    .editable:empty:before{
      content:attr(data-placeholder);
      color:#94a7b7;
      font-weight:500;
    }

    .medical-list{display:flex;flex-direction:column;gap:10px}
    .record{
      display:grid;grid-template-columns:130px 1fr;gap:14px;
      padding:13px 0;border-bottom:1px dashed var(--line);
    }
    .record:last-child{border-bottom:none;padding-bottom:0}
    .record-time{font-size:13px;color:var(--primary);font-weight:800}
    .record-body strong{display:block;margin-bottom:2px}
    .record-body .editable{color:#36536e}

    .pill-row{display:flex;gap:8px;flex-wrap:wrap;margin-top:8px}
    .pill{
      display:inline-flex;align-items:center;gap:6px;
      padding:7px 10px;border-radius:999px;
      background:var(--surface-2);border:1px solid var(--line);
      color:#285f91;font-size:13px;font-weight:750;
    }
    .pill.red{background:#fff1f3;border-color:#f5cbd1;color:#a32f42}
    .pill.green{background:#edfbf5;border-color:#ccebdd;color:#157454}

    .emergency{
      border-color:#b9d8f7;
      background:linear-gradient(145deg,#f7fbff,#eef7ff);
    }
    .emergency-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:10px}
    .em-item{padding:12px;border-radius:14px;background:#fff;border:1px solid var(--line)}
    .em-item span{font-size:11px;color:var(--muted);font-weight:800;display:block}
    .em-item b{font-size:15px}

    footer{
      text-align:center;color:var(--muted);font-size:12px;padding:26px 10px 46px;
    }

    .save-state{font-size:12px;color:var(--muted);min-width:62px;text-align:center}
    .save-state.ok{color:var(--ok)}

    @media(max-width:900px){
      .layout{grid-template-columns:1fr}
      .sidebar{display:none}
      .hero-grid{grid-template-columns:1fr}
      .hero{padding:28px}
      .emergency-grid{grid-template-columns:1fr 1fr}
    }
    @media(max-width:620px){
      .shell{padding:12px}
      .topbar{top:6px;border-radius:15px;padding:9px}
      .brand-sub{display:none}
      .brand-title{font-size:14px}
      .btn .wide{display:none}
      .hero{padding:24px;border-radius:22px}
      .grid-2,.grid-3,.emergency-grid{grid-template-columns:1fr}
      .card{padding:18px;border-radius:18px}
      .record{grid-template-columns:1fr;gap:3px}
    }

    @media print{
      body{background:#fff}
      .shell{max-width:none;padding:0}
      .topbar,.sidebar,.notice,.no-print{display:none!important}
      .hero{box-shadow:none;border-radius:0;break-after:avoid}
      .layout{display:block}
      .card{box-shadow:none;break-inside:avoid;margin-bottom:12px}
      main{gap:12px}
      [contenteditable="true"]{outline:none}
    }
  </style>
</head>
<body>
  <div class="shell">
    <header class="topbar">
      <div class="brand">
        <div class="brand-mark">✚</div>
        <div>
          <div class="brand-title" data-i18n="brandTitle">隨身電子病歷</div>
          <div class="brand-sub" data-i18n="brandSub">Personal Medical Passport</div>
        </div>
      </div>
      <div class="toolbar">
        <span id="saveState" class="save-state" data-i18n="saved">已儲存</span>
        <select id="language" class="lang-select" aria-label="Language">
          <option value="zh-Hant">繁體中文</option>
          <option value="en">English</option>
          <option value="ja">日本語</option>
          <option value="ko">한국어</option>
          <option value="vi">Tiếng Việt</option>
        </select>
        <button class="btn soft" id="exportBtn" type="button"><span class="wide" data-i18n="export">匯出</span> JSON</button>
        <button class="btn soft" id="importBtn" type="button" data-i18n="import">匯入</button>
        <button class="btn primary" id="printBtn" type="button" data-i18n="print">列印 / PDF</button>
        <input id="importFile" type="file" accept=".json,application/json" hidden />
      </div>
    </header>

    <section class="hero">
      <div class="hero-grid">
        <div>
          <div class="eyebrow" data-i18n="eyebrow">Medical Passport · Offline First</div>
          <h1 data-i18n="heroTitle">我的隨身電子病歷</h1>
          <p data-i18n="heroDesc">將重要醫療資訊整理成一個可離線開啟、可切換語言、可直接列印的靜態網頁。所有欄位都可點擊修改，資料只儲存在目前瀏覽器。</p>
        </div>
        <div class="hero-card">
          <strong data-i18n="emergencyIdentity">緊急識別</strong>
          <div class="emergency-name editable" contenteditable="true" data-key="fullName" data-placeholder="姓名 / Name"></div>
          <div class="mini-grid">
            <div class="mini"><span data-i18n="bloodType">血型</span><b class="editable" contenteditable="true" data-key="bloodType" data-placeholder="未填寫"></b></div>
            <div class="mini"><span data-i18n="birthDate">出生日期</span><b class="editable" contenteditable="true" data-key="birthDate" data-placeholder="YYYY-MM-DD"></b></div>
            <div class="mini"><span data-i18n="allergyShort">嚴重過敏</span><b class="editable" contenteditable="true" data-key="allergyBrief" data-placeholder="無 / 未知"></b></div>
            <div class="mini"><span data-i18n="contactShort">緊急聯絡</span><b class="editable" contenteditable="true" data-key="emergencyPhone" data-placeholder="+886 ..."></b></div>
          </div>
        </div>
      </div>
    </section>

    <div class="notice" data-i18n="privacyNotice">
      隱私提醒：這是個人醫療資訊檔案。請只在你信任的裝置上填寫；不要把含完整病歷的檔案公開上傳。此頁不取代醫院正式病歷或醫師診斷。
    </div>

    <div class="layout">
      <aside class="sidebar">
        <nav class="nav-card">
          <a href="#emergency"><span class="nav-dot"></span><span data-i18n="navEmergency">緊急摘要</span></a>
          <a href="#profile"><span class="nav-dot"></span><span data-i18n="navProfile">個人資料</span></a>
          <a href="#conditions"><span class="nav-dot"></span><span data-i18n="navConditions">疾病史</span></a>
          <a href="#medications"><span class="nav-dot"></span><span data-i18n="navMedications">用藥史</span></a>
          <a href="#allergies"><span class="nav-dot"></span><span data-i18n="navAllergies">過敏與不良反應</span></a>
          <a href="#surgeries"><span class="nav-dot"></span><span data-i18n="navSurgeries">手術 / 住院史</span></a>
          <a href="#family"><span class="nav-dot"></span><span data-i18n="navFamily">家族史</span></a>
          <a href="#immunization"><span class="nav-dot"></span><span data-i18n="navImmunization">疫苗史</span></a>
          <a href="#tests"><span class="nav-dot"></span><span data-i18n="navTests">檢查與影像</span></a>
          <a href="#contacts"><span class="nav-dot"></span><span data-i18n="navContacts">醫療聯絡</span></a>
          <a href="#notes"><span class="nav-dot"></span><span data-i18n="navNotes">其他備註</span></a>
        </nav>
      </aside>

      <main>
        <section class="card emergency" id="emergency">
          <div class="section-title">
            <div class="title-wrap"><div class="icon">🚑</div><div><h2 data-i18n="emergencyTitle">緊急醫療摘要</h2><div class="section-note" data-i18n="emergencyNote">給急診、海外就醫或無法完整說明病史時快速閱讀</div></div></div>
          </div>
          <div class="emergency-grid">
            <div class="em-item"><span data-i18n="bloodType">血型</span><b class="editable" contenteditable="true" data-key="bloodType" data-placeholder="未填寫"></b></div>
            <div class="em-item"><span data-i18n="allergyShort">嚴重過敏</span><b class="editable" contenteditable="true" data-key="allergyBrief" data-placeholder="無 / 未知"></b></div>
            <div class="em-item"><span data-i18n="criticalCondition">重要疾病</span><b class="editable" contenteditable="true" data-key="criticalCondition" data-placeholder="無 / 未填寫"></b></div>
            <div class="em-item"><span data-i18n="currentMeds">目前用藥</span><b class="editable" contenteditable="true" data-key="currentMeds" data-placeholder="無 / 未填寫"></b></div>
          </div>
        </section>

        <section class="card" id="profile">
          <div class="section-title">
            <div class="title-wrap"><div class="icon">👤</div><div><h2 data-i18n="profileTitle">個人資料與基本健康資訊</h2><div class="section-note" data-i18n="clickEdit">點擊文字即可編輯</div></div></div>
          </div>
          <div class="grid-3">
            <div class="field"><label data-i18n="fullName">姓名</label><div class="editable" contenteditable="true" data-key="fullName" data-placeholder="未填寫"></div></div>
            <div class="field"><label data-i18n="birthDate">出生日期</label><div class="editable" contenteditable="true" data-key="birthDate" data-placeholder="YYYY-MM-DD"></div></div>
            <div class="field"><label data-i18n="sex">生理性別</label><div class="editable" contenteditable="true" data-key="sex" data-placeholder="未填寫"></div></div>
            <div class="field"><label data-i18n="nationality">國籍</label><div class="editable" contenteditable="true" data-key="nationality" data-placeholder="未填寫"></div></div>
            <div class="field"><label data-i18n="idNumber">護照 / 身分識別</label><div class="editable" contenteditable="true" data-key="idNumber" data-placeholder="可選填；注意隱私"></div></div>
            <div class="field"><label data-i18n="bloodType">血型</label><div class="editable" contenteditable="true" data-key="bloodType" data-placeholder="未填寫"></div></div>
            <div class="field"><label data-i18n="height">身高</label><div class="editable" contenteditable="true" data-key="height" data-placeholder="cm"></div></div>
            <div class="field"><label data-i18n="weight">體重</label><div class="editable" contenteditable="true" data-key="weight" data-placeholder="kg"></div></div>
            <div class="field"><label data-i18n="primaryLanguage">主要語言</label><div class="editable" contenteditable="true" data-key="primaryLanguage" data-placeholder="例如：繁體中文"></div></div>
          </div>
        </section>

        <section class="card" id="conditions">
          <div class="section-title">
            <div class="title-wrap"><div class="icon">🫀</div><div><h2 data-i18n="conditionsTitle">疾病史 / 既往病史</h2><div class="section-note" data-i18n="conditionsNote">慢性病、重大疾病、感染症、精神健康、重要受傷等</div></div></div>
          </div>
          <div class="medical-list">
            <div class="record"><div class="record-time editable" contenteditable="true" data-key="condition1Date" data-placeholder="年份 / 日期"></div><div class="record-body"><strong class="editable" contenteditable="true" data-key="condition1Name" data-placeholder="疾病 / 診斷名稱"></strong><div class="editable" contenteditable="true" data-key="condition1Detail" data-placeholder="診斷醫院、目前狀態、重要檢驗值或注意事項"></div></div></div>
            <div class="record"><div class="record-time editable" contenteditable="true" data-key="condition2Date" data-placeholder="年份 / 日期"></div><div class="record-body"><strong class="editable" contenteditable="true" data-key="condition2Name" data-placeholder="疾病 / 診斷名稱"></strong><div class="editable" contenteditable="true" data-key="condition2Detail" data-placeholder="補充說明"></div></div></div>
            <div class="record"><div class="record-time editable" contenteditable="true" data-key="condition3Date" data-placeholder="年份 / 日期"></div><div class="record-body"><strong class="editable" contenteditable="true" data-key="condition3Name" data-placeholder="疾病 / 診斷名稱"></strong><div class="editable" contenteditable="true" data-key="condition3Detail" data-placeholder="補充說明"></div></div></div>
          </div>
        </section>

        <section class="card" id="medications">
          <div class="section-title">
            <div class="title-wrap"><div class="icon">💊</div><div><h2 data-i18n="medicationsTitle">用藥史</h2><div class="section-note" data-i18n="medicationsNote">處方藥、成藥、長期藥物與曾因副作用停用的藥</div></div></div>
          </div>
          <div class="grid-2">
            <div class="field"><label data-i18n="currentMeds">目前用藥</label><div class="editable" contenteditable="true" data-key="currentMeds" data-placeholder="藥名｜劑量｜頻率｜用途"></div></div>
            <div class="field"><label data-i18n="pastMeds">過去重要用藥</label><div class="editable" contenteditable="true" data-key="pastMeds" data-placeholder="藥名｜使用期間｜停藥原因"></div></div>
            <div class="field"><label data-i18n="supplements">保健品 / 補充品</label><div class="editable" contenteditable="true" data-key="supplements" data-placeholder="維生素、草藥、營養補充品等"></div></div>
            <div class="field"><label data-i18n="pharmacy">常用藥局 / 處方來源</label><div class="editable" contenteditable="true" data-key="pharmacy" data-placeholder="選填"></div></div>
          </div>
        </section>

        <section class="card" id="allergies">
          <div class="section-title">
            <div class="title-wrap"><div class="icon">⚠️</div><div><h2 data-i18n="allergiesTitle">過敏與藥物不良反應</h2><div class="section-note" data-i18n="allergiesNote">食物、藥物、昆蟲、乳膠、顯影劑與其他過敏原</div></div></div>
          </div>
          <div class="grid-2">
            <div class="field"><label data-i18n="drugAllergy">藥物過敏</label><div class="editable" contenteditable="true" data-key="drugAllergy" data-placeholder="藥名｜反應｜嚴重程度"></div></div>
            <div class="field"><label data-i18n="foodAllergy">食物 / 其他過敏</label><div class="editable" contenteditable="true" data-key="foodAllergy" data-placeholder="過敏原｜反應"></div></div>
            <div class="field"><label data-i18n="adverseReaction">非過敏性不良反應</label><div class="editable" contenteditable="true" data-key="adverseReaction" data-placeholder="例如：某藥造成暈眩、腸胃不適"></div></div>
            <div class="field"><label data-i18n="anaphylaxisPlan">嚴重過敏處置</label><div class="editable" contenteditable="true" data-key="anaphylaxisPlan" data-placeholder="是否攜帶腎上腺素筆 / 醫囑"></div></div>
          </div>
        </section>

        <section class="card" id="surgeries">
          <div class="section-title">
            <div class="title-wrap"><div class="icon">🏥</div><div><h2 data-i18n="surgeriesTitle">手術、住院與重大處置史</h2><div class="section-note" data-i18n="surgeriesNote">含手術、麻醉、住院、急診、骨折固定、輸血等</div></div></div>
          </div>
          <div class="medical-list">
            <div class="record"><div class="record-time editable" contenteditable="true" data-key="surgery1Date" data-placeholder="日期"></div><div class="record-body"><strong class="editable" contenteditable="true" data-key="surgery1Name" data-placeholder="手術 / 住院原因"></strong><div class="editable" contenteditable="true" data-key="surgery1Detail" data-placeholder="醫院、術式、麻醉、併發症、輸血等"></div></div></div>
            <div class="record"><div class="record-time editable" contenteditable="true" data-key="surgery2Date" data-placeholder="日期"></div><div class="record-body"><strong class="editable" contenteditable="true" data-key="surgery2Name" data-placeholder="手術 / 住院原因"></strong><div class="editable" contenteditable="true" data-key="surgery2Detail" data-placeholder="補充說明"></div></div></div>
          </div>
        </section>

        <section class="card" id="family">
          <div class="section-title">
            <div class="title-wrap"><div class="icon">🧬</div><div><h2 data-i18n="familyTitle">家族病史</h2><div class="section-note" data-i18n="familyNote">尤其記錄一等親的遺傳性疾病、癌症、心血管與代謝疾病</div></div></div>
          </div>
          <div class="grid-2">
            <div class="field"><label data-i18n="fatherSide">父系</label><div class="editable" contenteditable="true" data-key="fatherFamily" data-placeholder="疾病｜親屬關係｜發病年齡"></div></div>
            <div class="field"><label data-i18n="motherSide">母系</label><div class="editable" contenteditable="true" data-key="motherFamily" data-placeholder="疾病｜親屬關係｜發病年齡"></div></div>
            <div class="field"><label data-i18n="siblings">兄弟姊妹</label><div class="editable" contenteditable="true" data-key="siblingFamily" data-placeholder="重要疾病史"></div></div>
            <div class="field"><label data-i18n="genetic">已知遺傳疾病 / 基因檢測</label><div class="editable" contenteditable="true" data-key="geneticHistory" data-placeholder="若無可填「無已知」"></div></div>
          </div>
        </section>

        <section class="card" id="immunization">
          <div class="section-title">
            <div class="title-wrap"><div class="icon">💉</div><div><h2 data-i18n="immunizationTitle">疫苗與感染史</h2><div class="section-note" data-i18n="immunizationNote">常規疫苗、流感、COVID-19、旅遊疫苗與重要感染症</div></div></div>
          </div>
          <div class="grid-2">
            <div class="field"><label data-i18n="vaccines">重要疫苗</label><div class="editable" contenteditable="true" data-key="vaccines" data-placeholder="疫苗｜日期｜劑次"></div></div>
            <div class="field"><label data-i18n="infectionHistory">重要感染史</label><div class="editable" contenteditable="true" data-key="infectionHistory" data-placeholder="疾病｜日期｜是否完全康復"></div></div>
          </div>
        </section>

        <section class="card" id="tests">
          <div class="section-title">
            <div class="title-wrap"><div class="icon">🧪</div><div><h2 data-i18n="testsTitle">重要檢查、影像與檢驗結果</h2><div class="section-note" data-i18n="testsNote">只放會影響後續醫療判斷的重要結果，不必把每次健檢都塞進來</div></div></div>
          </div>
          <div class="medical-list">
            <div class="record"><div class="record-time editable" contenteditable="true" data-key="test1Date" data-placeholder="日期"></div><div class="record-body"><strong class="editable" contenteditable="true" data-key="test1Name" data-placeholder="檢查名稱"></strong><div class="editable" contenteditable="true" data-key="test1Detail" data-placeholder="重要結果 / 結論"></div></div></div>
            <div class="record"><div class="record-time editable" contenteditable="true" data-key="test2Date" data-placeholder="日期"></div><div class="record-body"><strong class="editable" contenteditable="true" data-key="test2Name" data-placeholder="檢查名稱"></strong><div class="editable" contenteditable="true" data-key="test2Detail" data-placeholder="重要結果 / 結論"></div></div></div>
          </div>
        </section>

        <section class="card" id="contacts">
          <div class="section-title">
            <div class="title-wrap"><div class="icon">📞</div><div><h2 data-i18n="contactsTitle">緊急與醫療聯絡資訊</h2><div class="section-note" data-i18n="contactsNote">海外就醫時特別有用</div></div></div>
          </div>
          <div class="grid-2">
            <div class="field"><label data-i18n="emergencyContact">緊急聯絡人</label><div class="editable" contenteditable="true" data-key="emergencyContact" data-placeholder="姓名｜關係｜電話"></div></div>
            <div class="field"><label data-i18n="emergencyPhone">緊急電話</label><div class="editable" contenteditable="true" data-key="emergencyPhone" data-placeholder="+886 ..."></div></div>
            <div class="field"><label data-i18n="primaryDoctor">主要醫師 / 診所</label><div class="editable" contenteditable="true" data-key="primaryDoctor" data-placeholder="姓名｜科別｜醫院｜電話"></div></div>
            <div class="field"><label data-i18n="insurance">保險資訊</label><div class="editable" contenteditable="true" data-key="insurance" data-placeholder="海外旅平險 / 保險公司 / 緊急聯絡方式"></div></div>
          </div>
        </section>

        <section class="card" id="notes">
          <div class="section-title">
            <div class="title-wrap"><div class="icon">📝</div><div><h2 data-i18n="notesTitle">其他可能被忘記、但值得記錄的資訊</h2><div class="section-note" data-i18n="notesNote">生活史、醫療偏好、輔具、溝通需求與其他重要背景</div></div></div>
          </div>
          <div class="grid-2">
            <div class="field"><label data-i18n="lifestyle">生活史</label><div class="editable" contenteditable="true" data-key="lifestyle" data-placeholder="吸菸 / 飲酒 / 咖啡因 / 運動 / 睡眠；無則可寫無"></div></div>
            <div class="field"><label data-i18n="injuries">重大外傷 / 運動傷害</label><div class="editable" contenteditable="true" data-key="injuries" data-placeholder="骨折、腦震盪、韌帶傷等"></div></div>
            <div class="field"><label data-i18n="devices">植入物 / 輔具 / 醫療器材</label><div class="editable" contenteditable="true" data-key="devices" data-placeholder="例如：牙套、植入物、助聽器；若有 MRI 限制請註明"></div></div>
            <div class="field"><label data-i18n="dentalVision">牙科 / 視力 / 聽力</label><div class="editable" contenteditable="true" data-key="dentalVision" data-placeholder="重要治療、矯正、視力或聽力問題"></div></div>
            <div class="field"><label data-i18n="mentalHealth">心理 / 精神健康</label><div class="editable" contenteditable="true" data-key="mentalHealth" data-placeholder="僅填需要讓醫療人員知道的資訊"></div></div>
            <div class="field"><label data-i18n="communication">溝通與醫療需求</label><div class="editable" contenteditable="true" data-key="communication" data-placeholder="語言、聽力、無障礙、注射/抽血特殊需求等"></div></div>
            <div class="field"><label data-i18n="travel">旅行與地區相關</label><div class="editable" contenteditable="true" data-key="travel" data-placeholder="長期居住地、近期特殊旅遊、海外就醫需知"></div></div>
            <div class="field"><label data-i18n="otherNotes">其他重要備註</label><div class="editable" contenteditable="true" data-key="otherNotes" data-placeholder="任何你希望醫療人員優先知道的事"></div></div>
          </div>
        </section>
      </main>
    </div>

    <footer>
      <span data-i18n="footer">Static Medical Passport · 本機儲存 · 無伺服器 · 可離線使用</span>
    </footer>
  </div>

  <script>
    const I18N = {
      "zh-Hant": {
        brandTitle:"隨身電子病歷", brandSub:"Personal Medical Passport",
        saved:"已儲存", saving:"儲存中…", export:"匯出", import:"匯入", print:"列印 / PDF",
        eyebrow:"Medical Passport · Offline First", heroTitle:"我的隨身電子病歷",
        heroDesc:"將重要醫療資訊整理成一個可離線開啟、可切換語言、可直接列印的靜態網頁。所有欄位都可點擊修改，資料只儲存在目前瀏覽器。",
        emergencyIdentity:"緊急識別", bloodType:"血型", birthDate:"出生日期", allergyShort:"嚴重過敏", contactShort:"緊急聯絡",
        privacyNotice:"隱私提醒：這是個人醫療資訊檔案。請只在你信任的裝置上填寫；不要把含完整病歷的檔案公開上傳。此頁不取代醫院正式病歷或醫師診斷。",
        navEmergency:"緊急摘要",navProfile:"個人資料",navConditions:"疾病史",navMedications:"用藥史",navAllergies:"過敏與不良反應",
        navSurgeries:"手術 / 住院史",navFamily:"家族史",navImmunization:"疫苗史",navTests:"檢查與影像",navContacts:"醫療聯絡",navNotes:"其他備註",
        emergencyTitle:"緊急醫療摘要", emergencyNote:"給急診、海外就醫或無法完整說明病史時快速閱讀", criticalCondition:"重要疾病", currentMeds:"目前用藥",
        profileTitle:"個人資料與基本健康資訊", clickEdit:"點擊文字即可編輯", fullName:"姓名", sex:"生理性別", nationality:"國籍",
        idNumber:"護照 / 身分識別", height:"身高", weight:"體重", primaryLanguage:"主要語言",
        conditionsTitle:"疾病史 / 既往病史", conditionsNote:"慢性病、重大疾病、感染症、精神健康、重要受傷等",
        medicationsTitle:"用藥史", medicationsNote:"處方藥、成藥、長期藥物與曾因副作用停用的藥", pastMeds:"過去重要用藥", supplements:"保健品 / 補充品", pharmacy:"常用藥局 / 處方來源",
        allergiesTitle:"過敏與藥物不良反應", allergiesNote:"食物、藥物、昆蟲、乳膠、顯影劑與其他過敏原", drugAllergy:"藥物過敏", foodAllergy:"食物 / 其他過敏",
        adverseReaction:"非過敏性不良反應", anaphylaxisPlan:"嚴重過敏處置",
        surgeriesTitle:"手術、住院與重大處置史", surgeriesNote:"含手術、麻醉、住院、急診、骨折固定、輸血等",
        familyTitle:"家族病史", familyNote:"尤其記錄一等親的遺傳性疾病、癌症、心血管與代謝疾病", fatherSide:"父系", motherSide:"母系", siblings:"兄弟姊妹", genetic:"已知遺傳疾病 / 基因檢測",
        immunizationTitle:"疫苗與感染史", immunizationNote:"常規疫苗、流感、COVID-19、旅遊疫苗與重要感染症", vaccines:"重要疫苗", infectionHistory:"重要感染史",
        testsTitle:"重要檢查、影像與檢驗結果", testsNote:"只放會影響後續醫療判斷的重要結果，不必把每次健檢都塞進來",
        contactsTitle:"緊急與醫療聯絡資訊", contactsNote:"海外就醫時特別有用", emergencyContact:"緊急聯絡人", emergencyPhone:"緊急電話", primaryDoctor:"主要醫師 / 診所", insurance:"保險資訊",
        notesTitle:"其他可能被忘記、但值得記錄的資訊", notesNote:"生活史、醫療偏好、輔具、溝通需求與其他重要背景",
        lifestyle:"生活史", injuries:"重大外傷 / 運動傷害", devices:"植入物 / 輔具 / 醫療器材", dentalVision:"牙科 / 視力 / 聽力", mentalHealth:"心理 / 精神健康",
        communication:"溝通與醫療需求", travel:"旅行與地區相關", otherNotes:"其他重要備註",
        footer:"Static Medical Passport · 本機儲存 · 無伺服器 · 可離線使用"
      },
      en: {
        brandTitle:"Medical Passport",brandSub:"Personal Medical Record",saved:"Saved",saving:"Saving…",export:"Export",import:"Import",print:"Print / PDF",
        eyebrow:"Medical Passport · Offline First",heroTitle:"My Personal Medical Passport",
        heroDesc:"A portable, offline medical record with language switching and print support. Click any field to edit it; data is stored only in this browser.",
        emergencyIdentity:"Emergency ID",bloodType:"Blood type",birthDate:"Date of birth",allergyShort:"Severe allergies",contactShort:"Emergency contact",
        privacyNotice:"Privacy: this file contains personal medical information. Use it only on trusted devices and do not publicly upload a completed copy. It does not replace an official medical record or a clinician's diagnosis.",
        navEmergency:"Emergency summary",navProfile:"Profile",navConditions:"Medical history",navMedications:"Medications",navAllergies:"Allergies / reactions",navSurgeries:"Surgery / hospitalizations",navFamily:"Family history",navImmunization:"Vaccines",navTests:"Tests / imaging",navContacts:"Medical contacts",navNotes:"Other notes",
        emergencyTitle:"Emergency Medical Summary",emergencyNote:"For emergency care, overseas treatment, or when you cannot explain your full history",criticalCondition:"Critical conditions",currentMeds:"Current medications",
        profileTitle:"Personal & Basic Health Information",clickEdit:"Click text to edit",fullName:"Full name",sex:"Biological sex",nationality:"Nationality",idNumber:"Passport / ID",height:"Height",weight:"Weight",primaryLanguage:"Primary language",
        conditionsTitle:"Medical / Past Medical History",conditionsNote:"Chronic disease, major illness, infection, mental health, major injuries, etc.",
        medicationsTitle:"Medication History",medicationsNote:"Prescription, OTC, long-term medications, and medications stopped for adverse effects",pastMeds:"Important past medications",supplements:"Supplements",pharmacy:"Pharmacy / prescription source",
        allergiesTitle:"Allergies & Adverse Drug Reactions",allergiesNote:"Food, drugs, insects, latex, contrast agents, and other allergens",drugAllergy:"Drug allergies",foodAllergy:"Food / other allergies",adverseReaction:"Non-allergic adverse reactions",anaphylaxisPlan:"Severe allergy plan",
        surgeriesTitle:"Surgery, Hospitalization & Major Procedures",surgeriesNote:"Including surgery, anesthesia, hospital admission, ER visits, fracture fixation, transfusion, etc.",
        familyTitle:"Family Medical History",familyNote:"Especially first-degree relatives: hereditary disease, cancer, cardiovascular and metabolic disease",fatherSide:"Paternal side",motherSide:"Maternal side",siblings:"Siblings",genetic:"Known hereditary disease / genetic testing",
        immunizationTitle:"Vaccination & Infection History",immunizationNote:"Routine vaccines, influenza, COVID-19, travel vaccines and important infections",vaccines:"Key vaccinations",infectionHistory:"Important infections",
        testsTitle:"Important Tests, Imaging & Lab Results",testsNote:"Keep only results that may influence future medical decisions",contactsTitle:"Emergency & Medical Contacts",contactsNote:"Especially useful during overseas care",
        emergencyContact:"Emergency contact",emergencyPhone:"Emergency phone",primaryDoctor:"Primary doctor / clinic",insurance:"Insurance information",
        notesTitle:"Other Important Information",notesNote:"Lifestyle, care preferences, devices, communication needs, and other context",lifestyle:"Lifestyle history",injuries:"Major injuries / sports injuries",devices:"Implants / aids / medical devices",dentalVision:"Dental / vision / hearing",mentalHealth:"Mental health",communication:"Communication & care needs",travel:"Travel / regional information",otherNotes:"Other important notes",
        footer:"Static Medical Passport · Local storage · No server · Offline-ready"
      },
      ja: {
        brandTitle:"携帯電子カルテ",brandSub:"Personal Medical Passport",saved:"保存済み",saving:"保存中…",export:"書き出し",import:"読み込み",print:"印刷 / PDF",
        eyebrow:"Medical Passport · Offline First",heroTitle:"私の携帯電子カルテ",heroDesc:"重要な医療情報を、オフラインで閲覧・言語切替・印刷できる静的ページにまとめます。各項目はクリックして編集でき、データはこのブラウザ内だけに保存されます。",
        emergencyIdentity:"緊急識別",bloodType:"血液型",birthDate:"生年月日",allergyShort:"重度アレルギー",contactShort:"緊急連絡先",
        privacyNotice:"プライバシー：個人の医療情報を含みます。信頼できる端末でのみ使用し、入力済みファイルを公開しないでください。正式な診療記録や医師の診断に代わるものではありません。",
        navEmergency:"緊急サマリー",navProfile:"基本情報",navConditions:"既往歴",navMedications:"服薬歴",navAllergies:"アレルギー",navSurgeries:"手術・入院歴",navFamily:"家族歴",navImmunization:"予防接種",navTests:"検査・画像",navContacts:"医療連絡先",navNotes:"その他",
        emergencyTitle:"緊急医療サマリー",emergencyNote:"救急・海外受診・病歴を十分に説明できない状況での確認用",criticalCondition:"重要疾患",currentMeds:"現在の薬",
        profileTitle:"個人情報・基本健康情報",clickEdit:"文字をクリックして編集",fullName:"氏名",sex:"生物学的性別",nationality:"国籍",idNumber:"パスポート / ID",height:"身長",weight:"体重",primaryLanguage:"主な言語",
        conditionsTitle:"病歴 / 既往歴",conditionsNote:"慢性疾患、重大疾患、感染症、精神・心理、重大外傷など",
        medicationsTitle:"服薬歴",medicationsNote:"処方薬、市販薬、長期薬、重い副作用で中止した薬",pastMeds:"過去の重要な薬",supplements:"サプリメント",pharmacy:"利用薬局 / 処方元",
        allergiesTitle:"アレルギー・薬物有害反応",allergiesNote:"食物、薬剤、昆虫、ラテックス、造影剤など",drugAllergy:"薬物アレルギー",foodAllergy:"食物 / その他",adverseReaction:"非アレルギー性副作用",anaphylaxisPlan:"重症アレルギー対応",
        surgeriesTitle:"手術・入院・主要処置歴",surgeriesNote:"手術、麻酔、入院、救急、骨折固定、輸血など",
        familyTitle:"家族歴",familyNote:"特に一等親の遺伝性疾患、がん、心血管・代謝疾患",fatherSide:"父方",motherSide:"母方",siblings:"兄弟姉妹",genetic:"遺伝性疾患 / 遺伝子検査",
        immunizationTitle:"予防接種・感染歴",immunizationNote:"定期接種、インフルエンザ、COVID-19、渡航ワクチンなど",vaccines:"主なワクチン",infectionHistory:"重要な感染歴",
        testsTitle:"重要な検査・画像・検査値",testsNote:"今後の診療判断に影響する重要結果のみ",contactsTitle:"緊急・医療連絡先",contactsNote:"海外受診時に特に有用",
        emergencyContact:"緊急連絡先",emergencyPhone:"緊急電話",primaryDoctor:"主治医 / クリニック",insurance:"保険情報",
        notesTitle:"その他の重要情報",notesNote:"生活歴、医療上の希望、医療機器、コミュニケーション等",lifestyle:"生活歴",injuries:"重大外傷 / スポーツ傷害",devices:"インプラント / 補助具",dentalVision:"歯科 / 視力 / 聴力",mentalHealth:"メンタルヘルス",communication:"コミュニケーション / 医療上の要望",travel:"渡航・地域情報",otherNotes:"その他の重要事項",
        footer:"Static Medical Passport · ローカル保存 · サーバー不要 · オフライン対応"
      },
      ko: {
        brandTitle:"휴대용 전자 의료기록",brandSub:"Personal Medical Passport",saved:"저장됨",saving:"저장 중…",export:"내보내기",import:"가져오기",print:"인쇄 / PDF",
        eyebrow:"Medical Passport · Offline First",heroTitle:"나의 휴대용 전자 의료기록",heroDesc:"중요한 의료 정보를 오프라인 열람, 언어 전환, 인쇄가 가능한 정적 페이지로 정리합니다. 각 항목을 클릭해 수정할 수 있고 데이터는 현재 브라우저에만 저장됩니다.",
        emergencyIdentity:"응급 식별",bloodType:"혈액형",birthDate:"생년월일",allergyShort:"중증 알레르기",contactShort:"응급 연락처",
        privacyNotice:"개인정보: 이 파일에는 개인 의료정보가 포함됩니다. 신뢰할 수 있는 기기에서만 사용하고 작성된 파일을 공개 업로드하지 마세요. 공식 의무기록이나 의사의 진단을 대체하지 않습니다.",
        navEmergency:"응급 요약",navProfile:"개인 정보",navConditions:"병력",navMedications:"약물력",navAllergies:"알레르기 / 이상반응",navSurgeries:"수술 / 입원력",navFamily:"가족력",navImmunization:"예방접종",navTests:"검사 / 영상",navContacts:"의료 연락처",navNotes:"기타",
        emergencyTitle:"응급 의료 요약",emergencyNote:"응급실·해외 진료·전체 병력을 설명하기 어려운 상황에서 사용",criticalCondition:"중요 질환",currentMeds:"현재 복용약",
        profileTitle:"개인 및 기본 건강 정보",clickEdit:"텍스트를 클릭해 수정",fullName:"이름",sex:"생물학적 성별",nationality:"국적",idNumber:"여권 / 신분증",height:"키",weight:"체중",primaryLanguage:"주 사용 언어",
        conditionsTitle:"질병력 / 과거력",conditionsNote:"만성질환, 중대한 질병, 감염, 정신건강, 주요 부상 등",
        medicationsTitle:"약물력",medicationsNote:"처방약, 일반약, 장기 복용약, 부작용으로 중단한 약",pastMeds:"과거 주요 약물",supplements:"건강보조제",pharmacy:"약국 / 처방 기관",
        allergiesTitle:"알레르기 및 약물 이상반응",allergiesNote:"음식, 약물, 곤충, 라텍스, 조영제 및 기타 알레르겐",drugAllergy:"약물 알레르기",foodAllergy:"음식 / 기타 알레르기",adverseReaction:"비알레르기성 이상반응",anaphylaxisPlan:"중증 알레르기 대처",
        surgeriesTitle:"수술·입원·주요 처치력",surgeriesNote:"수술, 마취, 입원, 응급실, 골절 고정, 수혈 등",
        familyTitle:"가족 병력",familyNote:"특히 1촌의 유전질환, 암, 심혈관·대사질환",fatherSide:"부계",motherSide:"모계",siblings:"형제자매",genetic:"유전질환 / 유전자 검사",
        immunizationTitle:"예방접종 및 감염력",immunizationNote:"정기 예방접종, 독감, COVID-19, 여행 백신 등",vaccines:"주요 예방접종",infectionHistory:"주요 감염력",
        testsTitle:"중요 검사·영상·검사 결과",testsNote:"향후 진료 판단에 영향을 줄 중요 결과만 기록",contactsTitle:"응급 및 의료 연락처",contactsNote:"해외 진료 시 특히 유용",
        emergencyContact:"응급 연락처",emergencyPhone:"응급 전화",primaryDoctor:"주치의 / 병원",insurance:"보험 정보",
        notesTitle:"기타 중요한 정보",notesNote:"생활습관, 진료 선호, 의료기기, 의사소통 요구 등",lifestyle:"생활습관",injuries:"중증 외상 / 스포츠 부상",devices:"삽입물 / 보조기기",dentalVision:"치과 / 시력 / 청력",mentalHealth:"정신건강",communication:"의사소통 / 진료 요구",travel:"여행 / 지역 관련 정보",otherNotes:"기타 중요 메모",
        footer:"Static Medical Passport · 로컬 저장 · 서버 없음 · 오프라인 사용"
      },
      vi: {
        brandTitle:"Hồ sơ y tế điện tử cá nhân",brandSub:"Personal Medical Passport",saved:"Đã lưu",saving:"Đang lưu…",export:"Xuất",import:"Nhập",print:"In / PDF",
        eyebrow:"Medical Passport · Offline First",heroTitle:"Hồ sơ y tế cá nhân của tôi",heroDesc:"Tổng hợp thông tin y tế quan trọng trong một trang tĩnh có thể mở ngoại tuyến, đổi ngôn ngữ và in trực tiếp. Nhấp vào từng mục để chỉnh sửa; dữ liệu chỉ được lưu trong trình duyệt này.",
        emergencyIdentity:"Nhận diện khẩn cấp",bloodType:"Nhóm máu",birthDate:"Ngày sinh",allergyShort:"Dị ứng nặng",contactShort:"Liên hệ khẩn cấp",
        privacyNotice:"Quyền riêng tư: tệp này chứa thông tin y tế cá nhân. Chỉ sử dụng trên thiết bị đáng tin cậy và không tải công khai bản đã điền. Trang này không thay thế hồ sơ y tế chính thức hay chẩn đoán của bác sĩ.",
        navEmergency:"Tóm tắt khẩn cấp",navProfile:"Thông tin cá nhân",navConditions:"Tiền sử bệnh",navMedications:"Thuốc",navAllergies:"Dị ứng / phản ứng",navSurgeries:"Phẫu thuật / nhập viện",navFamily:"Tiền sử gia đình",navImmunization:"Vắc-xin",navTests:"Xét nghiệm / hình ảnh",navContacts:"Liên hệ y tế",navNotes:"Ghi chú khác",
        emergencyTitle:"Tóm tắt y tế khẩn cấp",emergencyNote:"Dùng khi cấp cứu, khám ở nước ngoài hoặc không thể trình bày đầy đủ bệnh sử",criticalCondition:"Bệnh quan trọng",currentMeds:"Thuốc hiện tại",
        profileTitle:"Thông tin cá nhân & sức khỏe cơ bản",clickEdit:"Nhấp vào văn bản để chỉnh sửa",fullName:"Họ tên",sex:"Giới tính sinh học",nationality:"Quốc tịch",idNumber:"Hộ chiếu / ID",height:"Chiều cao",weight:"Cân nặng",primaryLanguage:"Ngôn ngữ chính",
        conditionsTitle:"Tiền sử bệnh / bệnh trước đây",conditionsNote:"Bệnh mạn tính, bệnh nặng, nhiễm trùng, sức khỏe tâm thần, chấn thương lớn, v.v.",
        medicationsTitle:"Lịch sử dùng thuốc",medicationsNote:"Thuốc kê đơn, OTC, thuốc dài hạn và thuốc đã ngừng do tác dụng phụ",pastMeds:"Thuốc quan trọng trước đây",supplements:"Thực phẩm bổ sung",pharmacy:"Nhà thuốc / nguồn kê đơn",
        allergiesTitle:"Dị ứng & phản ứng bất lợi do thuốc",allergiesNote:"Thức ăn, thuốc, côn trùng, latex, thuốc cản quang và dị nguyên khác",drugAllergy:"Dị ứng thuốc",foodAllergy:"Dị ứng thức ăn / khác",adverseReaction:"Phản ứng bất lợi không do dị ứng",anaphylaxisPlan:"Kế hoạch xử trí dị ứng nặng",
        surgeriesTitle:"Phẫu thuật, nhập viện & thủ thuật lớn",surgeriesNote:"Bao gồm phẫu thuật, gây mê, nhập viện, cấp cứu, cố định gãy xương, truyền máu, v.v.",
        familyTitle:"Tiền sử bệnh gia đình",familyNote:"Đặc biệt người thân bậc một: bệnh di truyền, ung thư, tim mạch và chuyển hóa",fatherSide:"Bên nội",motherSide:"Bên ngoại",siblings:"Anh chị em",genetic:"Bệnh di truyền / xét nghiệm gen",
        immunizationTitle:"Tiêm chủng & tiền sử nhiễm trùng",immunizationNote:"Vắc-xin định kỳ, cúm, COVID-19, vắc-xin du lịch và nhiễm trùng quan trọng",vaccines:"Vắc-xin quan trọng",infectionHistory:"Nhiễm trùng quan trọng",
        testsTitle:"Xét nghiệm, hình ảnh & kết quả quan trọng",testsNote:"Chỉ ghi kết quả có thể ảnh hưởng đến quyết định y tế sau này",contactsTitle:"Liên hệ khẩn cấp & y tế",contactsNote:"Đặc biệt hữu ích khi khám ở nước ngoài",
        emergencyContact:"Người liên hệ khẩn cấp",emergencyPhone:"Số điện thoại khẩn cấp",primaryDoctor:"Bác sĩ / phòng khám chính",insurance:"Thông tin bảo hiểm",
        notesTitle:"Thông tin quan trọng khác",notesNote:"Lối sống, nhu cầu chăm sóc, thiết bị y tế, giao tiếp và bối cảnh khác",lifestyle:"Lối sống",injuries:"Chấn thương lớn / thể thao",devices:"Thiết bị cấy ghép / hỗ trợ",dentalVision:"Răng / thị lực / thính lực",mentalHealth:"Sức khỏe tâm thần",communication:"Nhu cầu giao tiếp / chăm sóc",travel:"Thông tin du lịch / khu vực",otherNotes:"Ghi chú quan trọng khác",
        footer:"Static Medical Passport · Lưu cục bộ · Không máy chủ · Dùng ngoại tuyến"
      }
    };

    const STORAGE_KEY = "medical-passport-v1";
    const langSelect = document.getElementById("language");
    const saveState = document.getElementById("saveState");

    function applyLanguage(lang){
      const dict = I18N[lang] || I18N["zh-Hant"];
      document.documentElement.lang = lang;
      document.querySelectorAll("[data-i18n]").forEach(el=>{
        const key = el.dataset.i18n;
        if(dict[key]) el.textContent = dict[key];
      });
      localStorage.setItem("medical-passport-language", lang);
    }

    function collectData(){
      const data = {};
      document.querySelectorAll("[data-key]").forEach(el=>{
        const key = el.dataset.key;
        const val = el.innerText.trim();
        if(val !== "") data[key] = val;
      });
      return data;
    }

    function renderData(data){
      document.querySelectorAll("[data-key]").forEach(el=>{
        const key = el.dataset.key;
        el.innerText = data[key] || "";
      });
    }

    let saveTimer = null;
    function save(){
      clearTimeout(saveTimer);
      const lang = langSelect.value;
      const dict = I18N[lang] || I18N["zh-Hant"];
      saveState.textContent = dict.saving || "Saving…";
      saveState.classList.remove("ok");
      saveTimer = setTimeout(()=>{
        localStorage.setItem(STORAGE_KEY, JSON.stringify(collectData()));
        saveState.textContent = dict.saved || "Saved";
        saveState.classList.add("ok");
      }, 250);
    }

    document.querySelectorAll('[contenteditable="true"]').forEach(el=>{
      el.addEventListener("input", ()=>{
        const key = el.dataset.key;
        if(key){
          document.querySelectorAll(`[data-key="${CSS.escape(key)}"]`).forEach(other=>{
            if(other !== el && other.innerText !== el.innerText) other.innerText = el.innerText;
          });
        }
        save();
      });
      el.addEventListener("paste", e=>{
        e.preventDefault();
        const text = (e.clipboardData || window.clipboardData).getData("text/plain");
        document.execCommand("insertText", false, text);
      });
    });

    langSelect.addEventListener("change", ()=>applyLanguage(langSelect.value));
    document.getElementById("printBtn").addEventListener("click", ()=>window.print());

    document.getElementById("exportBtn").addEventListener("click", ()=>{
      const payload = {
        format:"medical-passport-v1",
        exportedAt:new Date().toISOString(),
        language:langSelect.value,
        data:collectData()
      };
      const blob = new Blob([JSON.stringify(payload,null,2)], {type:"application/json"});
      const url = URL.createObjectURL(blob);
      const a = document.createElement("a");
      a.href=url;
      a.download="medical-passport-backup.json";
      a.click();
      setTimeout(()=>URL.revokeObjectURL(url),1000);
    });

    const importFile = document.getElementById("importFile");
    document.getElementById("importBtn").addEventListener("click", ()=>importFile.click());
    importFile.addEventListener("change", async ()=>{
      const file = importFile.files?.[0];
      if(!file) return;
      try{
        const payload = JSON.parse(await file.text());
        const data = payload.data || payload;
        renderData(data);
        if(payload.language && I18N[payload.language]){
          langSelect.value = payload.language;
          applyLanguage(payload.language);
        }
        localStorage.setItem(STORAGE_KEY, JSON.stringify(collectData()));
        alert("Import completed.");
      }catch(err){
        alert("Invalid JSON file.");
      }finally{
        importFile.value="";
      }
    });

    const savedData = localStorage.getItem(STORAGE_KEY);
    if(savedData){
      try{ renderData(JSON.parse(savedData)); }catch(e){}
    }
    const savedLang = localStorage.getItem("medical-passport-language") || "zh-Hant";
    langSelect.value = I18N[savedLang] ? savedLang : "zh-Hant";
    applyLanguage(langSelect.value);
    saveState.classList.add("ok");
  </script>
</body>
</html>

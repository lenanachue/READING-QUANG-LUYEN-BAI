<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Reading Comprehension - Tổng hợp</title>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      min-height: 100vh;
      background: linear-gradient(180deg, #dceefb 0%, #eaf6fd 40%, #f0f9ff 100%);
      font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
      position: relative;
      overflow-x: hidden;
    }

    @keyframes bubbleUp {
      0%   { transform: translateY(0) scale(1); opacity: 0.4; }
      50%  { opacity: 0.6; }
      100% { transform: translateY(-100vh) scale(1.3); opacity: 0; }
    }
    @keyframes waveFloat {
      0%, 100% { transform: translateY(0px); }
      50%       { transform: translateY(-6px); }
    }
    button:hover { filter: brightness(1.05); }

    /* Bubbles */
    #bubbles {
      position: fixed; top: 0; left: 0; right: 0; bottom: 0;
      pointer-events: none; overflow: hidden; z-index: 0;
    }
    .bubble {
      position: absolute;
      border-radius: 50%;
      background: rgba(255,255,255,0.2);
    }

    /* Header */
    #header {
      background: linear-gradient(135deg, #2e86c1 0%, #5dade2 50%, #85c1e9 100%);
      padding: 28px 20px 20px;
      text-align: center;
      position: relative;
      overflow: hidden;
      z-index: 1;
    }
    #header .wave-bottom {
      position: absolute; bottom: -2px; left: 0; right: 0; height: 20px;
    }
    #header .wave-bottom svg { width: 100%; height: 100%; display: block; }
    #header-icon { animation: waveFloat 3s ease-in-out infinite; font-size: 36px; margin-bottom: 4px; }
    #header h1 {
      color: #fff; font-size: 22px; font-weight: 800;
      letter-spacing: 0.5px; text-shadow: 0 2px 8px rgba(0,0,0,0.15);
      margin-bottom: 4px;
    }
    #header p { color: rgba(255,255,255,0.85); font-size: 13px; }

    /* Tabs */
    #tabs {
      display: flex; gap: 0; padding: 12px 16px 0;
      position: relative; z-index: 1; overflow-x: auto;
    }
    .tab-btn {
      flex: 1; min-width: 80px; padding: 10px 8px;
      border: none; border-bottom: 3px solid transparent;
      background: transparent; color: #7fb3d3; font-weight: 500;
      font-size: 13px; cursor: pointer;
      border-radius: 10px 10px 0 0; transition: all 0.2s ease;
    }
    .tab-btn.active {
      border-bottom-color: #2e86c1;
      background: rgba(93,173,226,0.12);
      color: #1a5276; font-weight: 700;
    }

    /* Content */
    #content {
      padding: 16px 16px 40px;
      max-width: 720px; margin: 0 auto;
      position: relative; z-index: 1;
    }
    .tab-panel { display: none; }
    .tab-panel.active { display: block; }

    /* Theory cards */
    .theory-card {
      background: #fff; border-radius: 14px; padding: 16px 18px;
      margin-bottom: 12px; border: 1px solid #cce5f6;
      box-shadow: 0 2px 8px rgba(93,173,226,0.08);
    }
    .theory-card-header {
      display: flex; align-items: center; gap: 10px; margin-bottom: 6px;
    }
    .theory-card-header span { font-size: 22px; }
    .theory-card-header strong { color: #1a5276; font-size: 14.5px; }
    .theory-card p { margin: 0 0 6px; color: #34495e; font-size: 13.5px; line-height: 1.5; }
    .theory-example {
      background: #eaf6fd; border-radius: 8px; padding: 6px 12px;
      font-size: 12.5px; color: #2e86c1; font-style: italic;
    }

    .tips-box {
      background: linear-gradient(135deg, #e8f4fd, #d1ecf9);
      border-radius: 14px; padding: 18px 20px; margin-top: 20px;
      border: 1px solid #b8dff5;
    }
    .tips-box h3 { margin: 0 0 10px; color: #1a5276; font-size: 15px; }
    .tip-item {
      display: flex; align-items: flex-start; gap: 8px;
      margin-bottom: 8px; font-size: 13.5px; color: #2c3e50; line-height: 1.5;
    }
    .tip-item .wave-icon { color: #5dade2; font-weight: 700; flex-shrink: 0; }

    /* Analysis cards (phân tích dạng bài - mở, không chấm điểm) */
    .analysis-card {
      background: #fff; border-radius: 14px; padding: 16px 18px;
      margin-bottom: 12px; border: 1px solid #cce5f6;
      box-shadow: 0 2px 8px rgba(93,173,226,0.08);
    }
    .analysis-card h4 { color: #1a5276; font-size: 14.5px; margin-bottom: 8px; }
    .analysis-card .dang-bai { font-size: 13.5px; color: #34495e; margin-bottom: 10px; line-height: 1.6; }
    .analysis-card .cach-lam-title { font-size: 13px; font-weight: 700; color: #2e86c1; margin-bottom: 6px; }
    .cach-lam-list { list-style: none; }
    .cach-lam-list li {
      font-size: 13px; color: #2c3e50; margin-bottom: 6px; padding-left: 20px;
      position: relative; line-height: 1.55;
    }
    .cach-lam-list li::before { content: "🌊"; position: absolute; left: 0; top: 0; font-size: 11px; }

    .hint-table { width: 100%; border-collapse: collapse; margin-top: 10px; font-size: 12.5px; }
    .hint-table th, .hint-table td { border: 1px solid #cce5f6; padding: 8px 10px; text-align: left; color: #2c3e50; }
    .hint-table th { background: #eaf6fd; color: #1a5276; font-weight: 700; }

    .sub-header {
      display: flex; align-items: center; gap: 8px;
      margin: 22px 0 12px; color: #1a5276; font-size: 16px; font-weight: 800;
    }
    .sub-header:first-of-type { margin-top: 4px; }

    .section-divider {
      margin: 18px 0 14px; padding-top: 14px; border-top: 2px dashed #b8dff5;
      color: #1a5276; font-size: 14.5px; font-weight: 700;
    }

    /* Passage */
    .passage-box {
      background: linear-gradient(135deg, #e8f4fd 0%, #d1ecf9 100%);
      border-radius: 16px; padding: 24px 28px; margin-bottom: 24px;
      border: 1px solid #b8dff5; position: relative; overflow: hidden;
    }
    .passage-box .deco { position: absolute; top: 10px; right: 16px; font-size: 28px; opacity: 0.3; }
    .passage-box h3 { margin: 0 0 14px; color: #1a5276; font-size: 18px; font-weight: 700; }
    .passage-box p {
      margin: 0; color: #2c3e50; font-size: 14.5px; line-height: 1.8;
      white-space: pre-line; text-align: justify;
    }
    .blank {
      display: inline-block; background: #d4edfc; color: #1a5276;
      font-weight: 800; padding: 1px 8px; border-radius: 6px; margin: 0 1px;
    }
    .inline-select {
      display: inline-block; background: #fff; color: #1a5276;
      font-weight: 700; font-size: 13px; padding: 2px 6px;
      border: 1.5px solid #5dade2; border-radius: 6px; margin: 0 2px;
      cursor: pointer; max-width: 165px; vertical-align: middle;
    }
    .inline-select.correct { border-color: #81c995; background: #e8fdf1; color: #1a5276; }
    .inline-select.wrong   { border-color: #e88e8e; background: #fde8e8; }
    .inline-select:disabled { cursor: default; opacity: 0.95; }
    .cloze-instruction { font-size: 13px; color: #5b7d9a; margin-bottom: 10px; }

    /* Question card */
    .q-card {
      background: #fff; border-radius: 14px; padding: 18px 22px;
      margin-bottom: 16px; border: 1.5px solid #cce5f6; transition: all 0.3s ease;
    }
    .q-card.correct { background: #e8fdf1; border-color: #81c995; }
    .q-card.wrong   { background: #fde8e8; border-color: #e88e8e; }

    .q-header { display: flex; align-items: flex-start; gap: 10px; margin-bottom: 12px; }
    .q-num {
      background: #5dade2; color: #fff; border-radius: 8px;
      padding: 2px 10px; font-size: 12px; font-weight: 700; flex-shrink: 0;
    }
    .q-num.correct { background: #81c995; }
    .q-num.wrong   { background: #e88e8e; }
    .q-type {
      font-size: 11px; background: #eaf2f8; border-radius: 6px;
      padding: 2px 8px; color: #5b7d9a; font-weight: 600; flex-shrink: 0;
    }
    .q-text { margin: 0 0 12px; color: #2c3e50; font-size: 14px; font-weight: 600; line-height: 1.5; }

    .options { display: grid; gap: 8px; }
    .opt-btn {
      background: #f7fbfe; border: 1.5px solid #e0eef7; border-radius: 10px;
      padding: 10px 14px; text-align: left; cursor: pointer; font-size: 13.5px;
      color: #2c3e50; font-weight: 400; transition: all 0.2s ease;
      outline: none; line-height: 1.4; width: 100%;
    }
    .opt-btn.selected  { background: #d4edfc; border-color: #5dade2; font-weight: 600; }
    .opt-btn.is-answer { background: #d4edda; border-color: #81c995; font-weight: 700; }
    .opt-btn.is-wrong  { background: #f8d7da; border-color: #e88e8e; font-weight: 600; }
    .opt-btn:disabled  { cursor: default; }

    .explanation {
      margin-top: 12px; padding: 10px 14px; border-radius: 10px;
      font-size: 13px; color: #34495e; line-height: 1.6;
    }
    .explanation.correct { background: rgba(129,201,149,0.12); }
    .explanation.wrong   { background: rgba(232,142,142,0.12); }

    /* Score box */
    .score-box {
      background: linear-gradient(135deg, #d1ecf9 0%, #b8dff5 100%);
      border-radius: 16px; padding: 22px 26px; margin-bottom: 16px;
      text-align: center; border: 2px solid #85c1e9;
    }
    .score-emoji { font-size: 32px; margin-bottom: 6px; }
    .score-pct   { font-size: 28px; font-weight: 800; color: #1a5276; margin-bottom: 8px; }
    .score-detail { display: flex; justify-content: center; gap: 24px; font-size: 14px; color: #2c3e50; }

    /* Buttons */
    .btn-row { display: flex; gap: 12px; justify-content: center; }
    .btn-primary {
      background: linear-gradient(135deg, #5dade2, #3498db); color: #fff;
      border: none; border-radius: 12px; padding: 12px 36px;
      font-size: 15px; font-weight: 700; cursor: pointer;
      box-shadow: 0 4px 14px rgba(93,173,226,0.4);
    }
    .btn-reset {
      background: linear-gradient(135deg, #85c1e9, #5dade2); color: #fff;
      border: none; border-radius: 12px; padding: 12px 36px;
      font-size: 15px; font-weight: 700; cursor: pointer;
      box-shadow: 0 4px 14px rgba(93,173,226,0.3);
    }

    /* History */
    .history-header {
      display: flex; justify-content: space-between; align-items: center; margin-bottom: 16px;
    }
    .history-header h2 { color: #1a5276; font-size: 18px; font-weight: 700; }
    .btn-clear {
      background: rgba(231,76,60,0.1); color: #e74c3c;
      border: 1px solid rgba(231,76,60,0.3); border-radius: 8px;
      padding: 6px 14px; font-size: 12px; cursor: pointer; font-weight: 600;
    }
    .summary-grid {
      background: linear-gradient(135deg, #d1ecf9, #b8dff5);
      border-radius: 14px; padding: 16px 20px; margin-bottom: 16px;
      display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 12px; text-align: center;
    }
    .summary-val { font-size: 22px; font-weight: 800; color: #1a5276; }
    .summary-val.green { color: #27ae60; }
    .summary-val.orange { color: #e67e22; }
    .summary-label { font-size: 11px; color: #5b7d9a; }

    .history-entry {
      background: #fff; border-radius: 12px; padding: 14px 18px;
      margin-bottom: 10px; border: 1px solid #cce5f6;
      display: flex; align-items: center; justify-content: space-between;
    }
    .h-passage { font-size: 14px; font-weight: 600; color: #1a5276; margin-bottom: 2px; }
    .h-date    { font-size: 11px; color: #7fb3d3; }
    .h-pct     { font-size: 20px; font-weight: 800; }
    .h-pct.high   { color: #27ae60; }
    .h-pct.mid    { color: #e67e22; }
    .h-pct.low    { color: #e74c3c; }
    .h-breakdown  { font-size: 11px; color: #5b7d9a; text-align: right; }

    .empty-state { text-align: center; padding: 40px; color: #7fb3d3; font-size: 14px; }
    .empty-state .emoji { font-size: 48px; margin-bottom: 12px; }

    h2.section-title { color: #1a5276; font-size: 18px; font-weight: 700; margin: 0 0 6px; }
    p.section-sub    { color: #5b7d9a; font-size: 13px; margin: 0 0 16px; }
  </style>
</head>
<body>

<!-- Bubbles -->
<div id="bubbles"></div>

<!-- Header -->
<div id="header">
  <div class="wave-bottom">
    <svg viewBox="0 0 1200 40" preserveAspectRatio="none">
      <path d="M0,20 Q150,0 300,20 T600,20 T900,20 T1200,20 L1200,40 L0,40 Z" fill="#dceefb"/>
    </svg>
  </div>
  <div id="header-icon">🐋</div>
  <h1>Reading Comprehension</h1>
  <p>Luyện đọc hiểu, tìm lỗi sai & điền từ 🌊</p>
</div>

<!-- Tabs -->
<div id="tabs">
  <button class="tab-btn active" data-tab="theory">📘 Lý thuyết</button>
  <button class="tab-btn" data-tab="ex1">📝 Bài 1</button>
  <button class="tab-btn" data-tab="ex2">✏️ Bài 2</button>
  <button class="tab-btn" data-tab="history">📊 Lịch sử</button>
</div>

<!-- Content -->
<div id="content">

  <!-- THEORY -->
  <div id="tab-theory" class="tab-panel active">
    <h2 class="section-title">🐠 Các dạng câu hỏi đọc hiểu</h2>
    <p class="section-sub">Nắm vững các dạng câu hỏi để làm bài nhanh và chính xác hơn.</p>
    <div id="theory-cards"></div>
    <div class="tips-box">
      <h3>🐚 Mẹo làm bài</h3>
      <div id="tips-list"></div>
    </div>
  </div>

  <!-- BÀI TẬP 1 -->
  <div id="tab-ex1" class="tab-panel">
    <h2 class="section-title">📝 Bài tập 1: Đọc hiểu "Tet Holiday"</h2>
    <p class="section-sub">Gồm 5 câu đọc hiểu (29-33).</p>

    <div class="sub-header">🔍 Phân tích dạng bài & cách làm</div>
    <div id="analysis1-cards"></div>

    <div class="sub-header">✍️ Làm bài</div>
    <div id="ex1-container"></div>
  </div>

  <!-- BÀI TẬP 2 -->
  <div id="tab-ex2" class="tab-panel">
    <h2 class="section-title">✏️ Bài tập 2: Điền từ vào đoạn văn (Cloze test)</h2>
    <p class="section-sub">Đoạn văn "Internet Addiction" có 5 chỗ trống (27-31) — chọn đáp án ngay trong đoạn văn rồi nộp bài.</p>

    <div class="sub-header">🔍 Phân tích các chỗ trống</div>
    <div id="analysis2-cards"></div>

    <div class="sub-header">✍️ Làm bài</div>
    <div id="ex2-container"></div>
  </div>

  <!-- HISTORY -->
  <div id="tab-history" class="tab-panel">
    <div class="history-header">
      <h2>🏆 Lịch sử điểm số</h2>
      <button class="btn-clear" id="btn-clear-history" style="display:none">🗑️ Xóa tất cả</button>
    </div>
    <div id="history-content"></div>
  </div>

</div>

<script>
// ─── DATA: LÝ THUYẾT (giữ nguyên từ file gốc) ─────────────────────────────────

const THEORY = [
  { title: "Ý chính (Main Idea)", icon: "🐋",
    desc: "Xác định chủ đề hoặc ý chính của bài đọc.",
    example: "What is the topic / main idea of this passage?" },
  { title: "Câu hỏi lấy thông tin (Factual)", icon: "🐠",
    desc: "Tìm thông tin cụ thể được nêu trực tiếp trong bài.",
    example: "According to the passage, why did...?" },
  { title: "Câu hỏi từ vựng (Vocabulary)", icon: "🐚",
    desc: "Đoán nghĩa từ dựa vào ngữ cảnh hoặc tìm từ đồng nghĩa.",
    example: 'The word "X" is closest in meaning to...' },
  { title: "Câu hỏi suy diễn (Inference)", icon: "🦀",
    desc: "Suy ra ý nghĩa ẩn từ thông tin trong bài đọc.",
    example: "It can be inferred from the passage that..." },
  { title: "Câu hỏi liên hệ đại từ (Reference)", icon: "🐙",
    desc: 'Xác định đại từ (it, they, these...) thay thế cho từ nào.',
    example: 'The word "it" in line X refers to...' },
  { title: "Mục đích / Thái độ tác giả", icon: "🦈",
    desc: "Hiểu lý do tác giả đề cập hoặc quan điểm của tác giả.",
    example: "Why does the author mention...? / What is the author's opinion?" }
];

const TIPS = [
  "Đọc lướt để nắm nội dung chính trước khi đọc câu hỏi.",
  "Xác định vị trí chứa thông tin trả lời trong bài đọc.",
  "Chú ý từ đồng nghĩa & trái nghĩa khi so sánh đáp án.",
  "Dùng phương pháp loại trừ khi chưa chắc đáp án.",
  "Làm câu dễ trước, quay lại câu khó sau."
];

// ─── DATA: PHÂN TÍCH BÀI TẬP 1 (mở, không chấm điểm) ──────────────────────────

const ANALYSIS1 = [
  {
    icon: "📖",
    title: "Đọc hiểu nội dung (Reading Comprehension) — Câu 29-33",
    dangBai: 'Đây là dạng câu hỏi tìm thông tin chi tiết (factual) được nêu trực tiếp trong bài đọc về ngày Tết. Câu hỏi thường bắt đầu bằng <em>When / What / Who</em> và hỏi về một mốc thời gian hoặc hành động cụ thể.',
    cachLam: [
      "Đọc lướt cả bài 1 lần để nắm trình tự các hoạt động trước/trong/sau Tết.",
      "Gạch chân từ khóa trong câu hỏi (when, what, who...) rồi dò tìm từ khóa tương ứng trong bài.",
      "Chú ý các mốc thời gian: 'some weeks before', 'one or two days before', 'on the New Year's Eve', 'on the New Year morning'.",
      "Với đáp án dạng 'Both A & B' hoặc 'Both B & C', cần đọc kỹ xem bài có thật sự đề cập đủ cả hai ý không, đừng chọn vội."
    ]
  }
];

// ─── DATA: PHÂN TÍCH BÀI TẬP 2 (mở, không chấm điểm) ──────────────────────────

const ANALYSIS2 = [
  {
    icon: "🧩",
    title: "Dạng bài: Điền từ vào đoạn văn (Cloze test) — Câu 27-31",
    dangBai: "Đoạn văn bị 'đục' 5 chỗ trống, mỗi chỗ trống là một câu hỏi trắc nghiệm 4 đáp án. Đề kiểm tra cả ngữ pháp (chia động từ, giới từ, đại từ quan hệ, dạng V-ing/to-V...) và từ vựng trong văn cảnh.",
    cachLam: [
      "Đọc toàn bài một lượt trước để hiểu nội dung chung, đừng vội điền ngay khi gặp chỗ trống đầu tiên.",
      "Xác định loại từ cần điền: động từ chia theo chủ ngữ, giới từ cố định đi với động từ/danh từ (collocation), V-ing hay to-V, hay đại từ quan hệ.",
      "Nhìn vào các từ ngay trước và sau chỗ trống để tìm 'tín hiệu ngữ pháp' (ví dụ chủ ngữ số nhiều, động từ đứng trước cần V-ing theo sau...).",
      "Dùng phương pháp loại trừ: loại các đáp án sai về từ loại trước, sau đó mới xét đến nghĩa."
    ]
  }
];

const HINTS2 = [
  { gap: "(27)", note: 'Chia động từ "to be" phù hợp với chủ ngữ số nhiều đứng sau "There ___ ..."' },
  { gap: "(28)", note: 'Giới từ cố định đi cùng cụm "spend time ___ someone" (dành thời gian với ai)' },
  { gap: "(29)", note: 'Dạng động từ đi sau cấu trúc "spend + thời gian + ___"' },
  { gap: "(30)", note: 'Dạng động từ đi sau "want ___" (muốn làm gì)' },
  { gap: "(31)", note: 'Đại từ quan hệ phù hợp khi thay cho danh từ chỉ người ("People ___ have...")' }
];

// ─── DATA: BÀI TẬP 1 — passage + câu hỏi ──────────────────────────────────────

const EX1 = {
  title: "Tet Holiday in Viet Nam",
  text: `Tet holiday is celebrated on the first day of the Lunar New Year in Viet Nam. Some weeks before the New Year, the Vietnamese clean their houses and paint the walls. New clothes are bought for the occasion. One or two days before the festival, people make Banh chung, which is the traditional cake, and kinds of jam. On the New Year's Eve, the whole family get together for a reunion dinner. Every member of the family should be present during the dinner in which many different kinds of dishes are served. On the New Year morning, the young members of the family pay their respects to the elders. And the children receive lucky money wrapped in red tiny envelopes. Then people go to visit their neighbors, friends and relatives.`,
  questions: [
    { id:29, text:"When is Tet holiday celebrated of the Lunar New Year in Việt Nam?", type:"Đọc hiểu",
      options:["A. the first day","B. the second day","C. the third day","D. All are correct"], answer:0,
      explanation:'Câu đầu bài đọc: "Tet holiday is celebrated on the first day of the Lunar New Year" → đáp án A.' },
    { id:30, text:"What do they do one or two days before the festival?", type:"Đọc hiểu",
      options:["A. buy new clothes","B. make kinds of jam","C. make Banh chung","D. Both B & C"], answer:3,
      explanation:'"One or two days before the festival, people make Banh chung... and kinds of jam" → cả hai việc B và C → đáp án D.' },
    { id:31, text:"What do they do on the New Year's Eve?", type:"Đọc hiểu",
      options:["A. have a reunion dinner","B. visit relatives","C. go to the pagoda","D. make Banh chung"], answer:0,
      explanation:'"On the New Year\'s Eve, the whole family get together for a reunion dinner" → đáp án A.' },
    { id:32, text:"Who receives lucky money?", type:"Đọc hiểu",
      options:["A. young members","B. the children","C. the elders","D. the whole family"], answer:1,
      explanation:'"the children receive lucky money wrapped in red tiny envelopes" → đáp án B.' },
    { id:33, text:"When do they visit their neighbors, friends and relatives?", type:"Đọc hiểu",
      options:["A. on New Year morning","B. at night","C. during the dinner","D. Both A & C"], answer:0,
      explanation:'Câu cuối bài, ngay sau đoạn nói về buổi sáng năm mới: "Then people go to visit their neighbors, friends and relatives" → đáp án A.' }
  ]
};

// ─── DATA: BÀI TẬP 2 — passage (cloze) + câu hỏi ──────────────────────────────

const EX2 = {
  title: "Internet Addiction",
  text: `The Internet is very useful. Online, you can pay your bills, buy clothes, and read the news. There {{27}} many good reasons to spend time online. However, people with an Internet addiction are online too much. They don't spend time {{28}} their friends and family. Instead, they spend their time {{29}} with their Internet friends, people they have never met in real life. Some also play online games all day or night. Some people with Internet addictions even leave their jobs so they can spend even more time online! People with Internet addictions don't just go online to shop, have fun, or do work. People {{31}} have this problem often go online because they want {{30}} from the stress and problems in their lives. Many internet addicts stop caring about their real lives, and focus only on their online lives.`,
  questions: [
    { id:27, gapText:'There ___ many good reasons to spend time online.',
      options:["A. has","B. are","C. have","D. is"], answer:1,
      explanation:'Chủ ngữ thật "many good reasons" là danh từ số nhiều → dùng "are" sau "There". Đáp án B.' },
    { id:28, gapText:'They don\'t spend time ___ their friends and family.',
      options:["A. about","B. with","C. to","D. of"], answer:1,
      explanation:'Cụm cố định "spend time with someone" = dành thời gian với ai đó. Đáp án B.' },
    { id:29, gapText:'they spend their time ___ with their Internet friends',
      options:["A. to chat","B. chat","C. chatting","D. chatted"], answer:2,
      explanation:'Cấu trúc "spend + time + V-ing": "spend time chatting". Đáp án C.' },
    { id:30, gapText:'...because they want ___ from the stress and problems in their lives.',
      options:["A. escapes","B. escapeed","C. escaping","D. to escape"], answer:3,
      explanation:'Động từ "want" được theo sau bởi to-infinitive: "want to escape". Đáp án D.' },
    { id:31, gapText:'People ___ have this problem often go online...',
      options:["A. what","B. who","C. which","D. when"], answer:1,
      explanation:'Cần đại từ quan hệ làm chủ ngữ thay cho danh từ chỉ người "People" → dùng "who". Đáp án B.' }
  ]
};

const PASSAGES = { ex1: EX1 };

// ─── STATE ───────────────────────────────────────────────────────────────────

const quizState = {
  ex1: { selected: {}, submitted: false },
  ex2: { selected: {}, submitted: false }
};

let history = [];

// Load history from localStorage
try {
  const saved = localStorage.getItem("reading-history");
  if (saved) history = JSON.parse(saved);
} catch(e) {}

// ─── BUBBLES ─────────────────────────────────────────────────────────────────

function renderBubbles() {
  const container = document.getElementById("bubbles");
  for (let i = 0; i < 8; i++) {
    const b = document.createElement("div");
    b.className = "bubble";
    b.style.cssText = `
      bottom: -${20 + i * 5}px;
      left: ${5 + i * 12}%;
      width: ${8 + (i % 3) * 6}px;
      height: ${8 + (i % 3) * 6}px;
      animation: bubbleUp ${6 + i * 1.5}s ease-in infinite;
      animation-delay: ${i * 0.8}s;
    `;
    container.appendChild(b);
  }
}

// ─── THEORY ──────────────────────────────────────────────────────────────────

function renderTheory() {
  const cards = document.getElementById("theory-cards");
  cards.innerHTML = THEORY.map(t => `
    <div class="theory-card">
      <div class="theory-card-header">
        <span>${t.icon}</span>
        <strong>${t.title}</strong>
      </div>
      <p>${t.desc}</p>
      <div class="theory-example">Ví dụ: ${t.example}</div>
    </div>
  `).join("");

  const tipsList = document.getElementById("tips-list");
  tipsList.innerHTML = TIPS.map(tip => `
    <div class="tip-item">
      <span class="wave-icon">🌊</span>
      <span>${tip}</span>
    </div>
  `).join("");
}

// ─── ANALYSIS (phân tích dạng bài - mở, không chấm điểm) ──────────────────────

function renderAnalysisCards(containerId, data) {
  const el = document.getElementById(containerId);
  el.innerHTML = data.map(a => `
    <div class="analysis-card">
      <h4>${a.icon} ${a.title}</h4>
      <p class="dang-bai"><strong>Dạng bài:</strong> ${a.dangBai}</p>
      <div class="cach-lam-title">🧭 Cách làm:</div>
      <ul class="cach-lam-list">
        ${a.cachLam.map(c => `<li>${c}</li>`).join("")}
      </ul>
    </div>
  `).join("");
}

function renderAnalysis1() {
  renderAnalysisCards("analysis1-cards", ANALYSIS1);
}

function renderAnalysis2() {
  renderAnalysisCards("analysis2-cards", ANALYSIS2);
  const el = document.getElementById("analysis2-cards");
  el.innerHTML += `
    <div class="analysis-card">
      <h4>🗒️ Gợi ý từng chỗ trống (chưa phải đáp án)</h4>
      <table class="hint-table">
        <tr><th>Chỗ trống</th><th>Điểm cần chú ý</th></tr>
        ${HINTS2.map(h => `<tr><td>${h.gap}</td><td>${h.note}</td></tr>`).join("")}
      </table>
    </div>
  `;
}

// ─── QUIZ ─────────────────────────────────────────────────────────────────────

function renderQuiz(quizId, passage) {
  const container = document.getElementById(quizId + "-container");
  const state = quizState[quizId];

  let html = `
    <div class="passage-box">
      <span class="deco">🐋</span>
      <h3>📖 ${passage.title}</h3>
      <p>${passage.text}</p>
    </div>
  `;

  passage.questions.forEach((q, qIdx) => {
    const sel = state.selected[qIdx];
    const submitted = state.submitted;
    const isCorrect = submitted && sel === q.answer;
    const isWrong   = submitted && sel !== q.answer;

    if (q.sectionBreak) {
      html += `<div class="section-divider">${q.sectionBreak}</div>`;
    }

    html += `
      <div class="q-card ${submitted ? (isCorrect ? 'correct' : 'wrong') : ''}" id="${quizId}-q${qIdx}">
        <div class="q-header">
          <span class="q-num ${submitted ? (isCorrect ? 'correct' : 'wrong') : ''}">
            ${submitted ? (isCorrect ? '✓' : '✗') : 'Q' + q.id}
          </span>
          <span class="q-type">${q.type}</span>
        </div>
        <p class="q-text">${q.text}</p>
        <div class="options">
          ${q.options.map((opt, optIdx) => {
            let cls = "opt-btn";
            if (!submitted && sel === optIdx) cls += " selected";
            if (submitted) {
              if (optIdx === q.answer) cls += " is-answer";
              else if (sel === optIdx) cls += " is-wrong";
            }
            const prefix = submitted
              ? (optIdx === q.answer ? "✅ " : (sel === optIdx ? "❌ " : ""))
              : "";
            return `<button class="${cls}" ${submitted ? 'disabled' : ''}
              onclick="selectOpt('${quizId}', ${qIdx}, ${optIdx})">${prefix}${opt}</button>`;
          }).join("")}
        </div>
        ${submitted ? `
          <div class="explanation ${isCorrect ? 'correct' : 'wrong'}">
            <strong>💡 Giải thích:</strong> ${q.explanation}
          </div>` : ""}
      </div>
    `;
  });

  if (state.submitted) {
    const correct = passage.questions.filter((q, i) => state.selected[i] === q.answer).length;
    const total = passage.questions.length;
    const pct = Math.round((correct / total) * 100);
    const emoji = pct >= 80 ? "🎉" : pct >= 50 ? "👍" : "💪";
    html += `
      <div class="score-box">
        <div class="score-emoji">${emoji}</div>
        <div class="score-pct">${pct}%</div>
        <div class="score-detail">
          <span>✅ Đúng: <strong style="color:#27ae60">${correct}</strong></span>
          <span>❌ Sai: <strong style="color:#e74c3c">${total - correct}</strong></span>
          <span>📝 Tổng: <strong>${total}</strong></span>
        </div>
      </div>
    `;
  }

  html += `
    <div class="btn-row">
      ${!state.submitted
        ? `<button class="btn-primary" onclick="submitQuiz('${quizId}', '${passage.title}', ${passage.questions.length})">🐬 Nộp bài</button>`
        : `<button class="btn-reset" onclick="resetQuiz('${quizId}')">🔄 Làm lại</button>`
      }
    </div>
  `;

  container.innerHTML = html;
}

function selectOpt(quizId, qIdx, optIdx) {
  if (quizState[quizId].submitted) return;
  quizState[quizId].selected[qIdx] = optIdx;
  renderQuiz(quizId, PASSAGES[quizId]);
}

function submitQuiz(quizId, passageTitle, total) {
  const state = quizState[quizId];
  if (Object.keys(state.selected).length < total) {
    alert("Vui lòng trả lời tất cả câu hỏi trước khi nộp bài!");
    return;
  }
  state.submitted = true;
  const passage = PASSAGES[quizId];
  const correct = passage.questions.filter((q, i) => state.selected[i] === q.answer).length;
  saveResult(passageTitle, correct, total);
  renderQuiz(quizId, passage);
}

function resetQuiz(quizId) {
  quizState[quizId] = { selected: {}, submitted: false };
  renderQuiz(quizId, PASSAGES[quizId]);
}

// ─── BÀI TẬP 2: điền trực tiếp vào đoạn văn (inline select) ───────────────────

function renderEx2() {
  const container = document.getElementById("ex2-container");
  const state = quizState.ex2;
  const submitted = state.submitted;

  let bodyHtml = EX2.text.replace(/\{\{(\d+)\}\}/g, (match, idStr) => {
    const id = parseInt(idStr, 10);
    const qIdx = EX2.questions.findIndex(q => q.id === id);
    const q = EX2.questions[qIdx];
    const sel = state.selected[qIdx];
    const isCorrect = submitted && sel === q.answer;
    let cls = "inline-select";
    if (submitted) cls += isCorrect ? " correct" : " wrong";

    let optsHtml = `<option value="" disabled ${sel === undefined ? "selected" : ""}>(${id}) ...</option>`;
    q.options.forEach((opt, optIdx) => {
      optsHtml += `<option value="${optIdx}" ${sel === optIdx ? "selected" : ""}>${opt}</option>`;
    });
    return `<select class="${cls}" ${submitted ? "disabled" : ""} onchange="selectEx2Opt(${qIdx}, this.value)">${optsHtml}</select>`;
  });

  let html = `
    <p class="cloze-instruction">👉 Chọn đáp án đúng ngay tại từng chỗ trống trong đoạn văn dưới đây.</p>
    <div class="passage-box">
      <span class="deco">🐋</span>
      <h3>📖 ${EX2.title}</h3>
      <p>${bodyHtml}</p>
    </div>
  `;

  if (submitted) {
    const correct = EX2.questions.filter((q, i) => state.selected[i] === q.answer).length;
    const total = EX2.questions.length;
    const pct = Math.round((correct / total) * 100);
    const emoji = pct >= 80 ? "🎉" : pct >= 50 ? "👍" : "💪";

    html += EX2.questions.map((q, i) => {
      const ok = state.selected[i] === q.answer;
      return `
        <div class="explanation ${ok ? 'correct' : 'wrong'}">
          <strong>${ok ? '✅' : '❌'} (${q.id}):</strong> ${q.explanation}
        </div>`;
    }).join("");

    html += `
      <div class="score-box">
        <div class="score-emoji">${emoji}</div>
        <div class="score-pct">${pct}%</div>
        <div class="score-detail">
          <span>✅ Đúng: <strong style="color:#27ae60">${correct}</strong></span>
          <span>❌ Sai: <strong style="color:#e74c3c">${total - correct}</strong></span>
          <span>📝 Tổng: <strong>${total}</strong></span>
        </div>
      </div>
    `;
  }

  html += `
    <div class="btn-row">
      ${!submitted
        ? `<button class="btn-primary" onclick="submitEx2()">🐬 Nộp bài</button>`
        : `<button class="btn-reset" onclick="resetEx2()">🔄 Làm lại</button>`
      }
    </div>
  `;

  container.innerHTML = html;
}

function selectEx2Opt(qIdx, value) {
  if (quizState.ex2.submitted) return;
  quizState.ex2.selected[qIdx] = parseInt(value, 10);
  renderEx2();
}

function submitEx2() {
  const state = quizState.ex2;
  if (Object.keys(state.selected).length < EX2.questions.length) {
    alert("Vui lòng chọn đáp án cho tất cả chỗ trống trước khi nộp bài!");
    return;
  }
  state.submitted = true;
  const correct = EX2.questions.filter((q, i) => state.selected[i] === q.answer).length;
  saveResult(EX2.title, correct, EX2.questions.length);
  renderEx2();
}

function resetEx2() {
  quizState.ex2 = { selected: {}, submitted: false };
  renderEx2();
}

// ─── HISTORY ─────────────────────────────────────────────────────────────────

function saveResult(passageTitle, correct, total) {
  const entry = {
    id: Date.now(),
    passage: passageTitle,
    correct,
    total,
    pct: Math.round((correct / total) * 100),
    date: new Date().toLocaleString("vi-VN")
  };
  history = [entry, ...history].slice(0, 50);
  try { localStorage.setItem("reading-history", JSON.stringify(history)); } catch(e) {}
  renderHistory();
}

function renderHistory() {
  const container = document.getElementById("history-content");
  const btnClear  = document.getElementById("btn-clear-history");

  if (history.length === 0) {
    btnClear.style.display = "none";
    container.innerHTML = `
      <div class="empty-state">
        <div class="emoji">🐙</div>
        Chưa có lịch sử. Hãy làm bài để xem điểm số tại đây!
      </div>`;
    return;
  }

  btnClear.style.display = "";
  const avg  = Math.round(history.reduce((a, h) => a + h.pct, 0) / history.length);
  const best = Math.max(...history.map(h => h.pct));

  let html = `
    <div class="summary-grid">
      <div><div class="summary-val">${history.length}</div><div class="summary-label">Lần làm</div></div>
      <div><div class="summary-val green">${avg}%</div><div class="summary-label">TB điểm</div></div>
      <div><div class="summary-val orange">${best}%</div><div class="summary-label">Cao nhất</div></div>
    </div>
  `;

  history.forEach((h, i) => {
    const pctClass = h.pct >= 80 ? "high" : h.pct >= 50 ? "mid" : "low";
    html += `
      <div class="history-entry">
        <div>
          <div class="h-passage">${h.passage}</div>
          <div class="h-date">${h.date}</div>
        </div>
        <div>
          <div class="h-pct ${pctClass}">${h.pct}%</div>
          <div class="h-breakdown">✅${h.correct} ❌${h.total - h.correct}</div>
        </div>
      </div>
    `;
  });

  container.innerHTML = html;
}

function clearHistory() {
  if (!confirm("Bạn có chắc muốn xóa toàn bộ lịch sử điểm?")) return;
  history = [];
  try { localStorage.removeItem("reading-history"); } catch(e) {}
  renderHistory();
}

// ─── TABS ────────────────────────────────────────────────────────────────────

document.querySelectorAll(".tab-btn").forEach(btn => {
  btn.addEventListener("click", () => {
    const key = btn.dataset.tab;
    document.querySelectorAll(".tab-btn").forEach(b => b.classList.remove("active"));
    document.querySelectorAll(".tab-panel").forEach(p => p.classList.remove("active"));
    btn.classList.add("active");
    document.getElementById("tab-" + key).classList.add("active");
    if (key === "history") renderHistory();
  });
});

document.getElementById("btn-clear-history").addEventListener("click", clearHistory);

// ─── INIT ────────────────────────────────────────────────────────────────────

renderBubbles();
renderTheory();
renderAnalysis1();
renderAnalysis2();
renderQuiz("ex1", EX1);
renderEx2();
renderHistory();

// Animate header icon
const MARINE = ["🐋","🐬","🐠","🐟","🦈","🐙","🦑","🦀","🐚","🪸","🐡","🦐"];
const iconEl = document.getElementById("header-icon");
iconEl.textContent = MARINE[Math.floor(Date.now() / 10000) % MARINE.length];
</script>
</body>
</html>

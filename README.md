[mythstories index.html.html](https://github.com/user-attachments/files/25828329/mythstories.index.html.html)
<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>擁愛進步・傷害止步｜迷思破解互動故事</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Noto+Serif+TC:wght@400;600;700&family=Noto+Sans+TC:wght@400;500&display=swap');

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    min-height: 100vh;
    background: #f4f0fb;
    font-family: 'Noto Serif TC', Georgia, serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 28px 16px 48px;
  }

  #app { width: 100%; max-width: 660px; }

  /* Progress */
  .progress-bar-wrap {
    margin-bottom: 24px;
  }
  .progress-meta {
    display: flex;
    justify-content: space-between;
    font-family: 'Noto Sans TC', sans-serif;
    font-size: 12px;
    color: #999;
    letter-spacing: 1px;
    text-transform: uppercase;
    margin-bottom: 8px;
  }
  .progress-track {
    height: 5px;
    background: #e0d8f0;
    border-radius: 3px;
    overflow: hidden;
  }
  .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, #7C5CBF, #FF6B9D);
    border-radius: 3px;
    transition: width 0.5s ease;
  }

  /* Card */
  .card {
    border-radius: 20px;
    overflow: hidden;
    box-shadow: 0 8px 40px rgba(0,0,0,0.10);
    transition: opacity 0.3s ease, transform 0.3s ease;
  }
  .card.fade-out { opacity: 0; transform: translateY(12px); }

  .card-header {
    padding: 20px 30px;
    display: flex;
    align-items: center;
    gap: 14px;
  }
  .story-num {
    width: 38px; height: 38px;
    background: rgba(255,255,255,0.25);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    color: white; font-weight: 700; font-size: 16px;
    font-family: 'Noto Sans TC', sans-serif;
    flex-shrink: 0;
  }
  .story-label {
    color: rgba(255,255,255,0.75);
    font-size: 11px;
    letter-spacing: 1.5px;
    font-family: 'Noto Sans TC', sans-serif;
    text-transform: uppercase;
    margin-bottom: 3px;
  }
  .story-title { color: white; font-weight: 700; font-size: 18px; }

  .card-body { padding: 28px 30px; }

  /* Setup phase */
  .setup-text {
    color: #333; line-height: 1.9; font-size: 16px; margin-bottom: 20px;
  }
  .dialogue-box {
    background: rgba(255,255,255,0.75);
    border-radius: 0 12px 12px 0;
    padding: 14px 18px;
    margin-bottom: 18px;
    font-size: 15px;
    color: #222;
    font-style: italic;
    line-height: 1.8;
    border-left-width: 4px;
    border-left-style: solid;
  }
  .myth-box {
    background: rgba(0,0,0,0.05);
    border-radius: 10px;
    padding: 12px 16px;
    margin-bottom: 28px;
    font-size: 13px;
    color: #666;
    font-family: 'Noto Sans TC', sans-serif;
    line-height: 1.6;
  }

  /* Question phase */
  .question-text {
    color: #222; font-weight: 600; font-size: 17px;
    margin-bottom: 20px; line-height: 1.7;
  }
  .choices { display: flex; flex-direction: column; gap: 11px; margin-bottom: 22px; }
  .choice-btn {
    background: rgba(255,255,255,0.8);
    border: 2px solid rgba(0,0,0,0.08);
    border-radius: 12px;
    padding: 14px 16px;
    cursor: pointer;
    text-align: left;
    font-size: 15px;
    color: #333;
    font-family: 'Noto Serif TC', serif;
    line-height: 1.65;
    display: flex;
    align-items: flex-start;
    gap: 10px;
    transition: border-color 0.2s, background 0.2s;
    width: 100%;
  }
  .choice-btn:hover:not(:disabled) {
    border-color: rgba(0,0,0,0.2);
    background: rgba(255,255,255,0.95);
  }
  .choice-btn:disabled { cursor: default; }
  .choice-btn.correct {
    background: #e8f8ee;
    border-color: #4caf50;
    color: #1b6b2c;
  }
  .choice-btn.wrong {
    background: #fdecea;
    border-color: #e53935;
    color: #8b1a1a;
  }
  .choice-btn.correct-hint {
    background: #e8f8ee;
    border: 2px dashed #4caf50;
  }
  .choice-badge {
    min-width: 24px; height: 24px;
    border-radius: 50%;
    background: rgba(0,0,0,0.1);
    display: flex; align-items: center; justify-content: center;
    color: #666; font-size: 12px;
    font-family: 'Noto Sans TC', sans-serif;
    font-weight: 600;
    flex-shrink: 0;
    margin-top: 1px;
    transition: background 0.2s;
  }
  .choice-btn.correct .choice-badge,
  .choice-btn.correct-hint .choice-badge { background: #4caf50; color: white; }
  .choice-btn.wrong .choice-badge { background: #e53935; color: white; }

  .feedback-box {
    border-radius: 12px;
    padding: 14px 18px;
    margin-bottom: 20px;
    font-size: 14px;
    color: #333;
    line-height: 1.75;
    font-family: 'Noto Sans TC', sans-serif;
    background: rgba(255,255,255,0.85);
    border-left-width: 4px;
    border-left-style: solid;
  }

  /* Result phase */
  .law-box {
    background: rgba(255,255,255,0.8);
    border-radius: 14px;
    padding: 20px 22px;
    margin-bottom: 22px;
  }
  .law-label {
    font-size: 12px;
    color: #888;
    font-family: 'Noto Sans TC', sans-serif;
    letter-spacing: 1px;
    text-transform: uppercase;
    margin-bottom: 8px;
  }
  .law-text { font-size: 15px; color: #2d1b69; line-height: 1.85; }
  .concept-box {
    border-radius: 14px;
    padding: 16px 20px;
    margin-bottom: 28px;
    font-size: 15px;
    color: #222;
    line-height: 1.8;
    border-width: 1.5px;
    border-style: solid;
  }

  /* Done state */
  .done-card {
    background: white;
    border-radius: 20px;
    padding: 48px 36px;
    text-align: center;
    box-shadow: 0 8px 40px rgba(124,92,191,0.12);
  }
  .done-icon { font-size: 56px; margin-bottom: 16px; }
  .done-title { font-size: 24px; color: #2d1b69; margin-bottom: 14px; font-weight: 700; }
  .done-text { color: #555; line-height: 1.9; font-size: 16px; margin-bottom: 24px; }
  .resource-box {
    background: #f3f0ff;
    border-radius: 12px;
    padding: 16px 20px;
    margin-bottom: 28px;
    text-align: left;
    font-size: 14px;
    color: #5a3e9e;
    line-height: 1.8;
    font-family: 'Noto Sans TC', sans-serif;
  }

  /* Button */
  .btn-next {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    color: white;
    border: none;
    border-radius: 50px;
    padding: 13px 30px;
    font-size: 15px;
    cursor: pointer;
    font-family: 'Noto Serif TC', serif;
    float: right;
    transition: opacity 0.2s, transform 0.1s;
  }
  .btn-next:hover { opacity: 0.9; transform: translateX(2px); }
  .btn-next:active { transform: scale(0.97); }
  .btn-restart {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: linear-gradient(135deg, #7C5CBF, #FF6B9D);
    color: white; border: none;
    border-radius: 50px;
    padding: 13px 30px;
    font-size: 15px;
    cursor: pointer;
    font-family: 'Noto Serif TC', serif;
    transition: opacity 0.2s;
  }
  .btn-restart:hover { opacity: 0.9; }

  .clearfix::after { content: ""; display: table; clear: both; }

  .footer-note {
    margin-top: 22px;
    font-size: 12px;
    color: #bbb;
    font-family: 'Noto Sans TC', sans-serif;
    text-align: center;
  }
</style>
</head>
<body>

<div id="app"></div>
<p class="footer-note">均悅版健康教育・第四單元・第 5 章教學輔助工具</p>

<script>
const stories = [
  {
    id: 1,
    title: "情境一：放學後",
    color: "#FF6B9D",
    bg: "linear-gradient(135deg, #fff0f5 0%, #ffe4ef 100%)",
    setup: "阿翔放學騎車回家路上，在等紅燈時，一位陌生女性靠過來捏了他的臉，還說「好可愛喔」就走了。他覺得很不舒服，隔天告訴同學小傑。",
    dialogue: "小傑笑著說：「被女生摸有什麼關係，你應該要高興吧！男生哪有被騷擾的啦。」",
    myth: "「男生不可能被性騷擾，被女生碰是應該開心的事。」",
    question: "小傑的說法哪裡有問題？如果你在場，你會怎麼回應？",
    choices: [
      { text: "「也對啦，男生被女生摸確實沒什麼大不了……」", correct: false, feedback: "這樣的回應讓阿翔覺得自己的不舒服是不合理的。性騷擾不分性別，任何人在未經同意的情況下被觸碰身體，都有權利感到不舒服。" },
      { text: "「不對，不管是誰，在不舒服的情況下被碰就是性騷擾。性騷擾不分性別。」", correct: true, feedback: "✓ 說得對！性騷擾的定義跟受害者是男是女無關，關鍵在於當事人是否感到不舒服、是否出於自願。" },
      { text: "「阿翔，你還好嗎？你的感受是真實的，這不是你的問題。」", correct: true, feedback: "✓ 先讓阿翔知道他的感受是被認可的，非常重要。男性受害者往往因為「男生不該被騷擾」的迷思而更難開口，你的支持很關鍵。" },
    ],
  },
  {
    id: 2,
    title: "情境二：交往中的壓力",
    color: "#7C5CBF",
    bg: "linear-gradient(135deg, #f3f0ff 0%, #e8e0ff 100%)",
    setup: "曉晴和男友交往四個月，男友說想進一步親密接觸，但曉晴說她還沒準備好。",
    dialogue: "男友說：「我們都交往這麼久了，妳不答應就是不愛我。妳難道不在乎我的感受嗎？」",
    myth: "「交往就代表應該要答應對方的性要求。」",
    question: "男友的說法哪裡有問題？以下哪些回應是正確的？",
    choices: [
      { text: "男友說的也有道理，交往這麼久應該體諒他。", correct: false, feedback: "這個想法很危險。愛不等於必須答應一切要求。真正的愛會尊重對方的節奏與界線，而不是用情感施壓。" },
      { text: "男友用情感勒索的方式施壓，曉晴有權利說不，不論交往多久。", correct: true, feedback: "✓ 用「你不答應就是不愛我」來施壓，是一種情感操控。同意必須是自願且當下的，不能被逼出來。" },
      { text: "曉晴可以說：「我現在還沒準備好，這不代表我不愛你，但你這樣說讓我很受傷。」", correct: true, feedback: "✓ 清楚表達自己的感受與界線，同時讓對方理解這樣的說法造成的傷害，是很成熟的溝通方式。" },
    ],
  },
  {
    id: 3,
    title: "情境三：派對之後",
    color: "#E07B39",
    bg: "linear-gradient(135deg, #fff7f0 0%, #ffe8d6 100%)",
    setup: "小愷在朋友派對上喝了酒，意識模糊時被一位認識的學姊帶到房間。隔天他很難受，不確定發生了什麼，告訴了好友阿民。",
    dialogue: "阿民說：「你自己喝那麼多，這種事……而且對方是學姊耶，你確定是她的問題？」",
    myth: "「喝酒是自己的責任，而且被比自己年長或強勢的人侵害就更難說是誰的錯。」",
    question: "阿民的說法對嗎？你應該如何支持小愷？",
    choices: [
      { text: "阿民說得有點道理，喝酒還是要自己小心，而且學姊應該不會故意的。", correct: false, feedback: "這樣的想法會讓小愷覺得是自己的錯，更難開口求助。喝酒不是被侵害的原因，對方的身份（學姊、朋友）也不能成為藉口。" },
      { text: "「不對。小愷喝酒不代表他同意任何事。不管對方是誰，利用他意識模糊就是不對的。」", correct: true, feedback: "✓ 意識模糊的狀態下無法給出有效同意。加害者的身份、年齡或與受害者的關係，都不能成為免責的理由。" },
      { text: "「小愷，你還好嗎？你願意說的，我都在聽。我們可以一起想想怎麼做。」", correct: true, feedback: "✓ 讓受害者感到被相信、不被評判，是最重要的第一步。之後也可以陪他去找輔導老師。" },
    ],
  },
  {
    id: 4,
    title: "情境四：網路上的騷擾",
    color: "#2E8B57",
    bg: "linear-gradient(135deg, #f0fff4 0%, #d4edda 100%)",
    setup: "小恩在社群媒體上收到一位同學不斷傳來的私訊，包含帶有性暗示的留言和要求傳私密照片。小恩覺得很不舒服，告訴了朋友阿柔。",
    dialogue: "阿柔說：「你自己po那麼多自拍，別人才會這樣啊。而且只是傳訊息，沒有真的動手，應該還好吧？」",
    myth: "「在網路上被騷擾不算真的性騷擾，而且是自己先曬照片才引起的。」",
    question: "阿柔的說法哪裡有問題？以下哪些回應是正確的？",
    choices: [
      { text: "阿柔說得有道理，小恩確實應該少po一點自拍。", correct: false, feedback: "這樣的說法把責任推給受害者。在社群媒體上分享照片是正常的行為，不代表同意被騷擾。任何形式的騷擾，責任都在對方。" },
      { text: "「網路騷擾跟實體騷擾一樣嚴重，不舒服就是不舒服。而且po自拍跟被騷擾完全沒有關係。」", correct: true, feedback: "✓ 《性騷擾防治法》明確涵蓋網路騷擾行為。要求傳私密照片屬於性騷擾，可以截圖保存證據並向學校或警方申訴。" },
      { text: "「小恩，你可以先截圖存證，不用回覆他，然後我陪你去跟老師說，好嗎？」", correct: true, feedback: "✓ 陪伴受害者採取行動非常重要。截圖保存證據、封鎖對方、向學校輔導老師或警方申訴，都是可以採取的步驟。" },
    ],
  },
];

let storyIndex = 0;
let phase = "setup"; // setup | question | result | done
let selectedIdx = null;
let revealed = false;

function getProgressPct() {
  if (phase === "done") return 100;
  return ((storyIndex) / stories.length) * 100;
}

function render() {
  const app = document.getElementById("app");
  const story = stories[storyIndex];

  if (phase === "done") {
    app.innerHTML = `
      <div class="progress-bar-wrap">
        <div class="progress-meta"><span>擁愛進步・傷害止步</span><span>✓ 完成</span></div>
        <div class="progress-track"><div class="progress-fill" style="width:100%"></div></div>
      </div>
      <div class="done-card">
        <div class="done-icon">🌸</div>
        <h2 class="done-title">你完成了今天的練習</h2>
        <p class="done-text">
          這些情境不是電影，是很多人真實遭遇過的事。<br>
          你選的每一個答案，代表你在那個當下願意怎麼做。<br><br>
          <strong>不論受害者的穿著、行為、或喝了多少酒——<br>
          錯，都在做出傷害行為的那個人。</strong>
        </p>
        <div class="resource-box">
          <strong>📞 需要幫助嗎？</strong><br>
          • 性騷擾申訴暨諮詢專線：<strong>113</strong>（24小時）<br>
          • 輔導室老師隨時歡迎你
        </div>
        <button class="btn-restart" onclick="restart()">再玩一次</button>
      </div>
    `;
    return;
  }

  let bodyHTML = "";

  if (phase === "setup") {
    bodyHTML = `
      <p class="setup-text">${story.setup}</p>
      <div class="dialogue-box" style="border-left-color:${story.color}">💬 ${story.dialogue}</div>
      <div class="myth-box"><strong>隱藏的迷思：</strong>${story.myth}</div>
      <div class="clearfix">
        <button class="btn-next" style="background:${story.color}" onclick="nextPhase()">
          進入情境 →
        </button>
      </div>
    `;
  } else if (phase === "question") {
    const choicesHTML = story.choices.map((c, i) => {
      let cls = "choice-btn";
      let badge = String.fromCharCode(65 + i);
      if (revealed) {
        if (c.correct && i === selectedIdx) { cls += " correct"; badge = "✓"; }
        else if (!c.correct && i === selectedIdx) { cls += " wrong"; badge = "✗"; }
        else if (c.correct) { cls += " correct-hint"; badge = "✓"; }
      }
      const disabled = revealed ? "disabled" : "";
      return `<button class="${cls}" onclick="selectChoice(${i})" ${disabled}>
        <span class="choice-badge">${badge}</span>
        <span>${c.text}</span>
      </button>`;
    }).join("");

    const feedbackHTML = (revealed && selectedIdx !== null) ? `
      <div class="feedback-box" style="border-left-color:${story.choices[selectedIdx].correct ? '#4caf50' : '#e53935'}">
        ${story.choices[selectedIdx].feedback}
      </div>` : "";

    const isLast = storyIndex >= stories.length - 1;
    const nextBtn = revealed ? `
      <div class="clearfix">
        <button class="btn-next" style="background:${story.color}" onclick="nextPhase()">
          ${isLast ? "完成練習 →" : "下一個情境 →"}
        </button>
      </div>` : "";

    bodyHTML = `
      <p class="question-text">${story.question}</p>
      <div class="choices">${choicesHTML}</div>
      ${feedbackHTML}
      ${nextBtn}
    `;
  }

  app.innerHTML = `
    <div class="progress-bar-wrap">
      <div class="progress-meta">
        <span>擁愛進步・傷害止步</span>
        <span>${storyIndex + 1} / ${stories.length}</span>
      </div>
      <div class="progress-track">
        <div class="progress-fill" style="width:${getProgressPct()}%"></div>
      </div>
    </div>
    <div class="card" id="main-card" style="background:${story.bg}">
      <div class="card-header" style="background:${story.color}">
        <div class="story-num">${story.id}</div>
        <div>
          <div class="story-label">情境故事</div>
          <div class="story-title">${story.title}</div>
        </div>
      </div>
      <div class="card-body">${bodyHTML}</div>
    </div>
  `;
}

function transition(fn) {
  const card = document.getElementById("main-card");
  if (card) card.classList.add("fade-out");
  setTimeout(() => { fn(); render(); }, 280);
}

function nextPhase() {
  if (phase === "setup") {
    transition(() => { phase = "question"; });
  } else if (phase === "question") {
    if (storyIndex < stories.length - 1) {
      transition(() => {
        storyIndex++;
        phase = "setup";
        selectedIdx = null;
        revealed = false;
      });
    } else {
      transition(() => { phase = "done"; });
    }
  }
}

function selectChoice(idx) {
  if (revealed) return;
  selectedIdx = idx;
  revealed = true;
  render();
}

function restart() {
  storyIndex = 0;
  phase = "setup";
  selectedIdx = null;
  revealed = false;
  render();
}

render();
</script>
</body>
</html>

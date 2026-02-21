# FUTARI_SOUSA_TEST
フタリソウサのキャラクターシート作成ツール
<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>フタリソウサ キャラ作成ツール（レベル3雛形）</title>
  <style>
    body { font-family: system-ui, -apple-system, "Hiragino Kaku Gothic ProN", "Noto Sans JP", sans-serif; margin: 16px; line-height: 1.5; }
    h1 { font-size: 20px; margin: 0 0 12px; }
    h2 { font-size: 16px; margin: 20px 0 8px; }
    .row { display: grid; grid-template-columns: 1fr; gap: 10px; }
    @media(min-width: 900px){ .row.two { grid-template-columns: 1fr 1fr; } }
    label { display:block; font-size: 12px; opacity: .85; margin-bottom: 4px; }
    input[type="text"], select, textarea { width: 100%; padding: 10px; border: 1px solid #ccc; border-radius: 10px; font-size: 14px; box-sizing: border-box; }
    textarea { min-height: 90px; }
    .card { border: 1px solid #e0e0e0; border-radius: 14px; padding: 12px; }
    .btnbar { display:flex; flex-wrap:wrap; gap:8px; align-items:center; }
    button { padding: 10px 12px; border: 1px solid #ccc; border-radius: 12px; background: #fff; font-size: 14px; }
    button.primary { border-color: #111; }
    button.small { padding: 6px 10px; font-size: 12px; border-radius: 10px; }
    .pill { display:inline-block; padding: 2px 8px; border:1px solid #ddd; border-radius: 999px; font-size: 12px; margin-left: 6px; }
    .grid3 { display:grid; grid-template-columns: 1fr; gap: 10px; }
    @media(min-width: 900px){ .grid3 { grid-template-columns: 1fr 1fr 1fr; } }
    .muted { font-size: 12px; opacity: .75; }
    details summary { cursor: pointer; }
    .list { padding-left: 18px; margin: 6px 0; }
    .mono { font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, "Noto Sans Mono", monospace; white-space: pre-wrap; background: #fafafa; border:1px solid #eee; border-radius: 12px; padding: 12px; }
  </style>
</head>
<body>
  <h1>フタリソウサ キャラ作成ツール（レベル3：技能＋アクションまで自動）</h1>

  <div class="card">
    <div class="btnbar">
      <button class="primary" id="btnAllRandom">🎲 ぜんぶランダム生成（レベル3）</button>
      <button id="btnReset">🧹 リセット</button>
      <span class="muted">※ 各項目の右の🔁で“その項目だけ”再抽選できます</span>
    </div>
  </div>

  <h2>タブ1：基本</h2>
  <div class="row two">
    <div class="card">
      <div class="btnbar" style="justify-content:space-between;">
        <div style="flex:1;">
          <label>役割</label>
          <select id="role">
            <option value="detective">探偵</option>
            <option value="assistant">助手</option>
          </select>
        </div>
        <button class="small" id="rerollRole" title="この項目だけ再抽選">🔁</button>
      </div>

      <div class="btnbar" style="justify-content:space-between; margin-top:10px;">
        <div style="flex:1;">
          <label>クラス</label>
          <select id="class">
            <!-- 動的 -->
          </select>
        </div>
        <button class="small" id="rerollClass" title="この項目だけ再抽選">🔁</button>
      </div>

      <div class="btnbar" style="justify-content:space-between; margin-top:10px;">
        <div style="flex:1;">
          <label>背景</label>
          <select id="background">
            <!-- 動的 -->
          </select>
        </div>
        <button class="small" id="rerollBackground" title="この項目だけ再抽選">🔁</button>
      </div>

      <div style="margin-top:10px;">
        <label>背景メモ（自由記述）</label>
        <textarea id="bgMemo" placeholder="背景の補足を自由に"></textarea>
      </div>
    </div>

    <div class="card">
      <div class="btnbar" style="justify-content:space-between;">
        <div style="flex:1;">
          <label>名前</label>
          <input id="name" type="text" placeholder="例：佐藤 涼介" />
        </div>
        <button class="small" id="btnNameRand" title="苗字＋名前をランダム生成">🎲苗字＋名前</button>
        <button class="small" id="rerollName" title="この項目だけ再抽選">🔁</button>
      </div>

      <div style="margin-top:10px;" class="btnbar">
        <label style="margin:0;">年齢も生成する</label>
        <input type="checkbox" id="chkAge" />
        <span class="pill" id="agePill">OFF</span>
      </div>

      <div class="btnbar" style="justify-content:space-between; margin-top:10px;">
        <div style="flex:1;">
          <label>年齢</label>
          <input id="age" type="text" placeholder="（基本：相談して決定）" />
        </div>
        <button class="small" id="rerollAge" title="この項目だけ再抽選（チェックON時のみ）">🔁</button>
      </div>

      <details style="margin-top:12px;">
        <summary>偽名表（折りたたみ表示）</summary>
        <p class="muted">※ 偽名は入力は自由。表は参照用。</p>
        <ul class="list" id="aliasList"></ul>
      </details>
    </div>
  </div>

  <h2>タブ3：人物設定（必須）</h2>
  <div class="grid3">
    <div class="card">
      <div class="btnbar" style="justify-content:space-between;">
        <div style="flex:1;">
          <label>身長</label>
          <select id="height"></select>
        </div>
        <button class="small" id="rerollHeight">🔁</button>
      </div>

      <div class="btnbar" style="justify-content:space-between; margin-top:10px;">
        <div style="flex:1;">
          <label>ファッション（目立つもの）</label>
          <select id="fashion"></select>
        </div>
        <button class="small" id="rerollFashion">🔁</button>
      </div>

      <div class="btnbar" style="justify-content:space-between; margin-top:10px;">
        <div style="flex:1;">
          <label>職業</label>
          <select id="job"></select>
        </div>
        <button class="small" id="rerollJob">🔁</button>
      </div>
    </div>

    <div class="card">
      <div class="btnbar" style="justify-content:space-between;">
        <div style="flex:1;">
          <label>好きなもの（重複なし）</label>
          <select id="like"></select>
        </div>
        <button class="small" id="rerollLike">🔁</button>
      </div>

      <div class="btnbar" style="justify-content:space-between; margin-top:10px;">
        <div style="flex:1;">
          <label>嫌いなもの（重複なし）</label>
          <select id="dislike"></select>
        </div>
        <button class="small" id="rerollDislike">🔁</button>
      </div>

      <div id="quirkBlock" style="margin-top:10px;">
        <div class="btnbar" style="justify-content:space-between;">
          <div style="flex:1;">
            <label>異常な癖（探偵のみ）</label>
            <select id="quirk"></select>
          </div>
          <button class="small" id="rerollQuirk">🔁</button>
        </div>
        <p class="muted">※ 探偵のみ。助手のときは非表示。</p>
      </div>
    </div>

    <div class="card">
      <label>人物メモ（自由記述）</label>
      <textarea id="charMemo" placeholder="口調／一人称／見た目の補足など"></textarea>
    </div>
  </div>

  <h2>タブ2：技能・アクション（自動生成＋微調整）</h2>
  <div class="row two">
    <div class="card">
      <div class="btnbar">
        <button class="primary" id="btnRandSkills">🎲 技能をルール通り生成</button>
        <button class="primary" id="btnRandActions">🎲 アクションをルール通り生成</button>
        <button id="btnRandBoth">🎲 技能＋アクション生成</button>
      </div>
      <p class="muted">技能は重複なし／クラス別の取得数に従う。固定技能は自動付与。 :contentReference[oaicite:1]{index=1}</p>
      <div>
        <label>技能一覧（カテゴリ別）</label>
        <div id="skillsView" class="mono"></div>
      </div>
    </div>

    <div class="card">
      <p><b>助手メンタル</b>（助手のみ） :contentReference[oaicite:2]{index=2}</p>
      <div class="btnbar" style="gap:10px;">
        <div style="flex:1;">
          <label>余裕（初期0）</label>
          <input id="yoyuu" type="text" value="0" />
        </div>
        <div style="flex:1;">
          <label>心労（初期0 / 3でロスト）</label>
          <input id="shinrou" type="text" value="0" />
        </div>
      </div>

      <div style="margin-top:12px;">
        <label>アクション一覧</label>
        <div id="actionsView" class="mono"></div>
      </div>

      <div id="guestBlock" style="margin-top:12px;">
        <p><b>ゲスト</b>（助手のみ・任意） :contentReference[oaicite:3]{index=3}</p>
        <div class="btnbar" style="justify-content:space-between;">
          <div style="flex:1;">
            <label>ゲスト名</label>
            <input id="guestName" type="text" placeholder="例：星野 七海" />
          </div>
          <button class="small" id="rerollGuestName">🔁</button>
        </div>
        <div class="btnbar" style="justify-content:space-between; margin-top:10px;">
          <div style="flex:1;">
            <label>ゲスト技能</label>
            <select id="guestSkill"></select>
          </div>
          <button class="small" id="rerollGuestSkill">🔁</button>
        </div>
        <div class="btnbar" style="justify-content:space-between; margin-top:10px;">
          <div style="flex:1;">
            <label>ゲスト関係</label>
            <select id="guestRel"></select>
          </div>
          <button class="small" id="rerollGuestRel">🔁</button>
        </div>
      </div>
    </div>
  </div>

  <h2>出力（ココフォリア用テキスト例）</h2>
  <div class="card">
    <div class="btnbar">
      <button class="primary" id="btnBuildOutput">🧾 出力を更新</button>
      <button id="btnCopy">📋 コピー</button>
    </div>
    <div id="output" class="mono" style="margin-top:10px;"></div>
  </div>

<script>
/** ========= 乱数ユーティリティ ========= */
function randInt(min, max){ // inclusive
  return Math.floor(Math.random()*(max-min+1))+min;
}
function pick(arr){
  return arr[randInt(0, arr.length-1)];
}
function pickUnique(arr, usedSet){
  const candidates = arr.filter(x => !usedSet.has(x));
  if(candidates.length === 0) return null;
  const v = pick(candidates);
  usedSet.add(v);
  return v;
}
function shuffle(arr){
  const a = [...arr];
  for(let i=a.length-1;i>0;i--){
    const j = Math.floor(Math.random()*(i+1));
    [a[i], a[j]] = [a[j], a[i]];
  }
  return a;
}

/** ========= データ（メモ準拠） ========= */
const ROLE = {
  detective: { label: "探偵", classes: ["運命の血統","天性の才能","マニア"] },
  assistant: { label: "助手", classes: ["正義の人","情熱の人","巻き込まれの人"] },
};

const BACKGROUNDS = {
  "運命の血統": [
    "名探偵の先祖（真）","名探偵の先祖（想）","親が世界的探偵","街の名探偵","推理作家","育ての親",
    "堕ちた名探偵","大悪人の血","隠された血筋","クローン"
  ],
  "天性の才能": [
    "超エリート","瞬間記憶能力","知識の泉","スパルタ教育","既に名探偵","憧れの背中",
    "ライバル","かつての名探偵","孤立した名探偵","人工名探偵"
  ],
  "マニア": [
    "サスペンスマニア","死体マニア","科学マニア","いわゆるオタク","人間マニア","書物マニア",
    "オカルトマニア","探偵マニア","暴走する知識欲","正義のマニア"
  ],
  "正義の人": ["お人よし","許せない","納得したい","利用している","頼れる協力者","正義の同志"],
  "情熱の人": ["能力にほれ込んだ","人柄にほれ込んだ","一目惚れ","ウマが合った","対立","放っておけない"],
  "巻き込まれの人": ["一方的に気に入られた","リアクション要員","過去のツケ","必要な人材","親しい人","偶然の積み重ね"],
};

const SKILLS = {
  洞察: ["嘘","変化","外見","物理","現場","天気"],
  鑑識: ["交通","情報","指紋","科学","法医学","生物"],
  人間: ["社交","家事","噂話","説得","流行","ビジネス"],
  肉体: ["捕縛","防御","根性","体力","突破","追跡"],
};

// 固定技能（クラス別）
const FIXED_SKILLS = {
  "正義の人": ["説得","突破"],
  "情熱の人": ["社交","根性"],
  "巻き込まれの人": ["防御"],
};

// 取得数ルール（メモ準拠） :contentReference[oaicite:4]{index=4}
const SKILL_RULES = {
  "運命の血統": { 洞察: 2, 鑑識: 2, 人間: 0, 肉体: 0, free: 2 },
  "天性の才能": { 洞察: 2, 鑑識: 3, 人間: 0, 肉体: 0, free: 1 },
  "マニア":     { 洞察: 2, 鑑識: 2, 人間: 1, 肉体: 0, free: 1 },
  "正義の人":   { 洞察: 0, 鑑識: 0, 人間: 2, 肉体: 0, free: 1 },
  "情熱の人":   { 洞察: 0, 鑑識: 0, 人間: 2, 肉体: 0, free: 1 },
  "巻き込まれの人": { 洞察: 0, 鑑識: 0, 人間: 2, 肉体: 2, free: 0 },
};

// アクション：最低限（メモ準拠） :contentReference[oaicite:5]{index=5}
const BASE_ACTIONS = {
  detective: [{
    name:"フタリソウサ", type:"補助", cost:"なし",
    text:"捜査フェイズのシーン終了時。互いの感情を1つ強い感情にして次のシーンをフタリソウサシーンに変更。"
  }],
  assistant: [{
    name:"食らいつく", type:"補助", cost:"1",
    text:"判定後。パートナーへの感情を1つ強い感情にして振り直し（十面体化可）。"
  }],
};

const CLASS_ACTIONS = {
  "運命の血統": [{ name:"血の直感", type:"補助", cost:"1", text:"判定後。使用したサイコロの目をすべて4に変更。" }],
  "天性の才能": [{ name:"当然知っている", type:"補助", cost:"なし", text:"いつでも。好きな技能1つ修得（セッション終了で消失）。1セッション2回まで。" }],
  "マニア": [{ name:"膨大なデータベース", type:"補助", cost:"2", text:"重要でないキーワード獲得時。さらに重要でないキーワード1つ。1セッション1回まで。" }],
  "正義の人": [{ name:"気合を入れる", type:"常駐", cost:"なし", text:"初動捜査の判定時、有利を得る。" }],
  "情熱の人": [{ name:"見直す", type:"補助", cost:"なし", text:"捜査フェイズ中、探偵の判定に4以上があれば使用。探偵への感情1つ獲得。1セッション1回。" }],
  "巻き込まれの人": [{ name:"こうなるとわかってた", type:"常駐", cost:"なし", text:"たまり場で余裕獲得時、獲得余裕+1。" }],
};

// 名前表（抜粋ではなく、あなたのメモそのままを配列化するのが理想）
// ここでは動作確認のため、先頭〜中盤を中心に入れてあります（必要なら全部入れた版に差し替えるよ）
const SURNAME = [
  "佐藤","前田","小島","柴田","秋山","渡辺","鈴木","木村","佐々木","山崎","森","田中","長谷川","太田","西村","伊藤",
  "上田","藤原","小林","大西","高橋","皇","安藤","村上","石田","関","荒井","小鳥遊","中川","星野","榎本","飯田","四季",
  "杉本","馬場","広瀬","那須","岩田","早川","東雲","水野","世界","暁","天野","堀","宇田川","西山","角田","鏡","鎌田",
  "小倉","岡","坂田","鳳","大川","武井","小笠原","芥","萩野","手塚","槐","臼井","巽",
  "シュルツ","ミュラー","シュナイダー","マイヤー","ウェーバー","ホフマン","トーマ","ベルナール","トマ","プティ","デュラン",
  "シュ","リュウ","チョウ","シュウ","ポポフ","モロゾフ","イワノフ","キム","イ","パク",
  "モリアーティ","ホームズ","ワトスン","ハドソン","レストレード","アドラー","ターナー","バスカヴィル"
];

const GIVEN = [
  "涼介","ひより","空","琴音","竜","さくら","智也","美也","大和","美月","優","杏","快人","彩音","大翔","美羽","瑛太","真央",
  "楓真","百花","仁","美優","幹太","みずき","陽向","菜月","隼","優菜","歩夢","優衣","瑠偉","乃愛","悠希","こころ","陽斗",
  "莉子","聖也","雪乃","太陽","玲奈","龍之介","美咲","翔太朗","和奏","隼人","雅","樹","愛奈","湊","ひなた","陽翔","花音",
  "伊織","心春","蒼真","凜","花","悠真","心愛","善","芽衣","岳","菫","慶","蘭","右京","雄大","萌","駿","千尋","陸","楓",
  "七海","蓮","未来","薫","真理子","直人","優花","貴大","海斗","桃子","拓海","佳奈","亮","彩香","里奈","匠","亜美","翼",
  "フェリックス","アニカ","ミア","ソフィア","ルカス","ハンナ","フィン","レナ","レオ","クロエ","エヴァ","イヴァン","ジェームズ",
  "ルーシー","ジョン","マイクロフト","モード","アーサー","メリー","セバスチャン","サラ","アイリーン"
];

const ALIAS_TABLE = [
  "好きな酒の名前","好きな色の名前","好きな動物の名前","好きな惑星の名前","好きな映画の名前","好きなお菓子の名前",
  "好きな小説の名前","好きな星座の名前","好きな作家の名前","好きな刃物の名前","好きな銃器の名前",
  "来ているファッションの名前","付けているアクセサリーの名前","好きな料理の名前",
  "ただの通りすがり","番号で呼ばれている","探偵／助手","アンノウン","通称『便利屋』","不明"
];

const HEIGHT_TABLE = [
  "非常に高い","高め","平均的","低め","非常に低い","パートナーより少し高い","パートナーより少し低い"
];

const FASHION_TABLE = [
  "高級志向","スーツ","カジュアルウェア","フォーマルウェア","スポーツウェア","リーズナブル","サングラス","Yシャツ","Tシャツ",
  "ネックレス","帽子","ミリタリー風","ピアス","ジャージ","エクステ","和風","指輪","チョーカー","サンダル","ジャンパー",
  "インパネスコート","白衣","グローブ","パイプ","チョッキ","和服","カラフルな色使い","パートナーと同じ","ファッションにこだわりがない"
];

const LIKE_DISLIKE_TABLE = [
  "死体","犬","猫","サスペンス","物語","アイドル","犯罪","オカルト","健康","ジャンクフード","高級な食事","ファッション","権力",
  "名誉","友情","おやつ","地元","家族","警察","音楽","銃","謎","探偵","パートナー","パートナーの好きなもの",
  "パートナーの嫌いなもの","特になし","チェスや将棋などボードゲーム","人間","知らないこと"
];

const JOB_TABLE = [
  "パートナーと同じ","フリーター","学生（優秀）","学生（普通）","学生（不真面目）","教師・講師","会社員","主夫・主婦","自営業",
  "ディレッタント","刑事（新人）","刑事（エリート）","公務員","探偵助手","探偵（有名）","探偵（普通）","探偵（不人気）",
  "無職","研究者","作家"
];

const QUIRK_TABLE = [
  "猛烈に感謝の言葉を述べる","皮肉ばかりを言ってしまう","相手の言葉を肯定してから否定する","ニヤニヤ笑いながら謝る",
  "相手の言葉を聞かずに自分だけ喋る","「こうは考えられないでしょうか」","「それとも、何か隠していることでも？」",
  "「妙ですね」","「だいたいわかりました」","「黙っていろ」",
  "勝手に捜査対象の鞄や引き出しを空ける","警察の捜査に割り込む","捜査のためにハッキングや不法侵入を行う",
  "許可されていないところに立ち入る","証拠品を許可なく解体する","捜査対象を騙して情報を聞き出す",
  "寝食を忘れて捜査して急に倒れる","事件の相関図を壁や床に書き始める","事件の話を止められない",
  "パートナーを置いて先に行ってしまう","パートナーに事件クイズを出題する","パートナーに懇切丁寧に事件を説明する"
];

const GUEST_REL = [
  "昔のバディ","友人","親友","顔見知り","戦友","腐れ縁","過去に何かあった","いとこ","友達の友達","遠い親戚","近所の人",
  "迷惑をかけた","師匠","ネットで知り合った","偶然知り合った","前に一度だけあった","パートナーのことで相談された",
  "パートナーについて質問された","幼馴染","パートナーを追っている","一方的に知られている"
];

/** ========= 状態 ========= */
const state = {
  skills: [],   // {cat, name, fixed:boolean}
  actions: [],  // {name,type,cost,text}
};

/** ========= DOM ========= */
const el = (id)=>document.getElementById(id);
const roleEl = el("role");
const classEl = el("class");
const bgEl = el("background");
const quirkBlockEl = el("quirkBlock");
const guestBlockEl = el("guestBlock");
const ageChkEl = el("chkAge");
const agePillEl = el("agePill");

function fillSelect(selectEl, items){
  selectEl.innerHTML = "";
  for(const it of items){
    const opt = document.createElement("option");
    opt.value = it;
    opt.textContent = it;
    selectEl.appendChild(opt);
  }
}
function setVisible(node, show){
  node.style.display = show ? "" : "none";
}

/** ========= 初期化 ========= */
function init(){
  // alias table
  const ul = el("aliasList");
  ul.innerHTML = "";
  for(const a of ALIAS_TABLE){
    const li = document.createElement("li");
    li.textContent = a;
    ul.appendChild(li);
  }

  fillSelect(el("height"), HEIGHT_TABLE);
  fillSelect(el("fashion"), FASHION_TABLE);
  fillSelect(el("job"), JOB_TABLE);
  fillSelect(el("quirk"), QUIRK_TABLE);
  fillSelect(el("like"), LIKE_DISLIKE_TABLE);
  fillSelect(el("dislike"), LIKE_DISLIKE_TABLE);

  // guest
  fillSelect(el("guestRel"), GUEST_REL);
  // guestSkill: 全技能を列挙
  const allSkills = Object.entries(SKILLS).flatMap(([cat, arr]) => arr.map(s => `${cat}:${s}`));
  fillSelect(el("guestSkill"), allSkills);

  syncClassOptions();
  syncBackgroundOptions();
  applyRoleVisibility();
  updateAgePill();
  renderSkills();
  renderActions();
  buildOutput();
}

function syncClassOptions(){
  const role = roleEl.value;
  fillSelect(classEl, ROLE[role].classes);
}
function syncBackgroundOptions(){
  const cls = classEl.value;
  fillSelect(bgEl, BACKGROUNDS[cls] ?? []);
}
function applyRoleVisibility(){
  const role = roleEl.value;
  const isDet = role === "detective";
  setVisible(quirkBlockEl, isDet);
  setVisible(guestBlockEl, !isDet);
  // 助手メンタル欄（入力自体は残してよいが、表示を切替）
  setVisible(el("yoyuu").closest(".btnbar"), !isDet);
  setVisible(el("shinrou").closest(".btnbar"), !isDet);
}

function updateAgePill(){
  agePillEl.textContent = ageChkEl.checked ? "ON" : "OFF";
}

/** ========= ランダム生成（フィールド単位） ========= */
function genName(){
  el("name").value = `${pick(SURNAME)} ${pick(GIVEN)}`;
}
function genAge(){
  if(!ageChkEl.checked) return; // チェック時のみ
  // 年齢は相談が基本なので、軽めのレンジ（10〜60）にしておく。必要なら変える。
  el("age").value = String(randInt(10, 60));
}
function genRole(){
  roleEl.value = pick(["detective","assistant"]);
  syncClassOptions();
  syncBackgroundOptions();
  applyRoleVisibility();
}
function genClass(){
  const role = roleEl.value;
  classEl.value = pick(ROLE[role].classes);
  syncBackgroundOptions();
}
function genBackground(){
  const cls = classEl.value;
  const arr = BACKGROUNDS[cls] ?? [];
  if(arr.length) bgEl.value = pick(arr);
}
function genHeight(){ el("height").value = pick(HEIGHT_TABLE); }
function genFashion(){ el("fashion").value = pick(FASHION_TABLE); }
function genJob(){ el("job").value = pick(JOB_TABLE); }
function genQuirk(){ el("quirk").value = pick(QUIRK_TABLE); }
function genLikeDislike(){
  // 同キャラ内で重複しない
  const like = pick(LIKE_DISLIKE_TABLE);
  let dislike = pick(LIKE_DISLIKE_TABLE);
  let guard = 0;
  while(dislike === like && guard < 50){
    dislike = pick(LIKE_DISLIKE_TABLE);
    guard++;
  }
  el("like").value = like;
  el("dislike").value = dislike;
}
function rerollLikeOnly(){
  const dislike = el("dislike").value;
  let like = pick(LIKE_DISLIKE_TABLE);
  let guard = 0;
  while(like === dislike && guard < 50){
    like = pick(LIKE_DISLIKE_TABLE);
    guard++;
  }
  el("like").value = like;
}
function rerollDislikeOnly(){
  const like = el("like").value;
  let dislike = pick(LIKE_DISLIKE_TABLE);
  let guard = 0;
  while(dislike === like && guard < 50){
    dislike = pick(LIKE_DISLIKE_TABLE);
    guard++;
  }
  el("dislike").value = dislike;
}
function genGuestName(){
  el("guestName").value = `${pick(SURNAME)} ${pick(GIVEN)}`;
}
function genGuestSkill(){
  const allSkills = Object.entries(SKILLS).flatMap(([cat, arr]) => arr.map(s => `${cat}:${s}`));
  el("guestSkill").value = pick(allSkills);
}
function genGuestRel(){
  el("guestRel").value = pick(GUEST_REL);
}

/** ========= レベル3：技能生成 ========= */
function generateSkillsByRules(){
  const cls = classEl.value;
  const rule = SKILL_RULES[cls];
  if(!rule){
    state.skills = [];
    renderSkills();
    return;
  }

  const used = new Set();
  const out = [];

  // 1) 固定技能を付与（あれば）
  const fixed = FIXED_SKILLS[cls] ?? [];
  for(const s of fixed){
    // 固定技能はどのカテゴリかを逆引きする
    const cat = Object.keys(SKILLS).find(c => SKILLS[c].includes(s)) ?? "不明";
    if(!used.has(s)){
      used.add(s);
      out.push({cat, name:s, fixed:true});
    }
  }

  // 2) カテゴリ指定分を抽選
  for(const cat of ["洞察","鑑識","人間","肉体"]){
    const need = rule[cat] ?? 0;
    for(let i=0;i<need;i++){
      const v = pickUnique(SKILLS[cat], used);
      if(v === null) break;
      out.push({cat, name:v, fixed:false});
    }
  }

  // 3) free枠：カテゴリをランダムに選んで、重複なしで取得
  const free = rule.free ?? 0;
  const cats = ["洞察","鑑識","人間","肉体"];
  let guard = 0;
  for(let i=0;i<free;i++){
    // freeは「好きなカテゴリから」なので、カテゴリ自体をランダム抽選
    // 取得可能な候補が残っているカテゴリだけを候補にする
    const availableCats = cats.filter(c => SKILLS[c].some(s => !used.has(s)));
    if(availableCats.length === 0) break;
    const cat = pick(availableCats);
    const v = pickUnique(SKILLS[cat], used);
    if(v === null){ i--; guard++; if(guard>20) break; continue; }
    out.push({cat, name:v, fixed:false});
  }

  // 4) 表示用にカテゴリ順→固定優先
  state.skills = out.sort((a,b)=>{
    const order = {洞察:1,鑑識:2,人間:3,肉体:4};
    if(order[a.cat] !== order[b.cat]) return order[a.cat]-order[b.cat];
    if(a.fixed !== b.fixed) return a.fixed ? -1 : 1;
    return a.name.localeCompare(b.name, "ja");
  });

  renderSkills();
}

/** ========= レベル3：アクション生成 ========= */
function generateActionsByRules(){
  const role = roleEl.value;
  const cls = classEl.value;

  const used = new Set();
  const out = [];

  // 1) 基本アクション（探偵/助手）
  for(const a of BASE_ACTIONS[role]){
    if(!used.has(a.name)){
      used.add(a.name);
      out.push(a);
    }
  }

  // 2) クラスアクション（1つ）
  const ca = CLASS_ACTIONS[cls] ?? [];
  for(const a of ca){
    if(!used.has(a.name)){
      used.add(a.name);
      out.push(a);
    }
  }

  state.actions = out;
  renderActions();
}

/** ========= ビュー ========= */
function renderSkills(){
  if(state.skills.length === 0){
    el("skillsView").textContent = "（まだ生成されていません）";
    return;
  }
  const byCat = {};
  for(const s of state.skills){
    byCat[s.cat] ??= [];
    byCat[s.cat].push(s);
  }
  let text = "";
  for(const cat of ["洞察","鑑識","人間","肉体"]){
    if(!byCat[cat]?.length) continue;
    text += `■${cat}\n`;
    for(const s of byCat[cat]){
      text += `- ${s.name}${s.fixed ? "（固定）" : ""}\n`;
    }
    text += "\n";
  }
  el("skillsView").textContent = text.trim();
}
function renderActions(){
  if(state.actions.length === 0){
    el("actionsView").textContent = "（まだ生成されていません）";
    return;
  }
  let text = "";
  for(const a of state.actions){
    text += `■${a.name}\n`;
    text += `  タイプ：${a.type} / コスト：${a.cost}\n`;
    text += `  ${a.text}\n\n`;
  }
  el("actionsView").textContent = text.trim();
}

/** ========= 出力 ========= */
function buildOutput(){
  const role = ROLE[roleEl.value].label;
  const cls = classEl.value;
  const bg = bgEl.value;

  const lines = [];
  lines.push(`【名前】${el("name").value || ""}`);
  lines.push(`【役割】${role}`);
  lines.push(`【クラス】${cls}`);
  lines.push(`【背景】${bg}`);
  if(el("bgMemo").value.trim()) lines.push(`【背景メモ】${el("bgMemo").value.trim()}`);

  if(el("age").value.trim()) lines.push(`【年齢】${el("age").value.trim()}`);
  lines.push(`【身長】${el("height").value}`);
  lines.push(`【ファッション】${el("fashion").value}`);
  lines.push(`【職業】${el("job").value}`);
  lines.push(`【好き】${el("like").value}`);
  lines.push(`【嫌い】${el("dislike").value}`);
  if(roleEl.value === "detective"){
    lines.push(`【異常な癖】${el("quirk").value}`);
  }else{
    lines.push(`【余裕】${el("yoyuu").value}`);
    lines.push(`【心労】${el("shinrou").value}`);
    const gn = el("guestName").value.trim();
    if(gn){
      lines.push(`【ゲスト】${gn}`);
      lines.push(`【ゲスト技能】${el("guestSkill").value}`);
      lines.push(`【ゲスト関係】${el("guestRel").value}`);
    }
  }

  if(el("charMemo").value.trim()) lines.push(`【人物メモ】${el("charMemo").value.trim()}`);

  lines.push("");
  lines.push("【技能】");
  if(state.skills.length){
    const byCat = {};
    for(const s of state.skills){
      byCat[s.cat] ??= [];
      byCat[s.cat].push(s);
    }
    for(const cat of ["洞察","鑑識","人間","肉体"]){
      if(!byCat[cat]?.length) continue;
      lines.push(`・${cat}：${byCat[cat].map(x=>x.name).join("、")}`);
    }
  }else{
    lines.push("（未生成）");
  }

  lines.push("");
  lines.push("【アクション】");
  if(state.actions.length){
    for(const a of state.actions){
      lines.push(`・${a.name}（${a.type}/コスト${a.cost}）`);
    }
  }else{
    lines.push("（未生成）");
  }

  el("output").textContent = lines.join("\n").trim();
}

async function copyOutput(){
  const text = el("output").textContent;
  try{
    await navigator.clipboard.writeText(text);
    alert("コピーしました！");
  }catch(e){
    alert("コピーに失敗しました。iOSでは長押しコピーで対応してください。");
  }
}

/** ========= まとめランダム ========= */
function randomAllLevel3(){
  genRole();
  genClass();
  genBackground();
  genName();
  genAge();
  genHeight();
  genFashion();
  genJob();
  genLikeDislike();
  if(roleEl.value === "detective") genQuirk();
  if(roleEl.value === "assistant"){
    genGuestName();
    genGuestSkill();
    genGuestRel();
    el("yoyuu").value = "0";
    el("shinrou").value = "0";
  }
  generateSkillsByRules();
  generateActionsByRules();
  buildOutput();
}

function resetAll(){
  el("name").value = "";
  el("age").value = "";
  el("bgMemo").value = "";
  el("charMemo").value = "";
  el("yoyuu").value = "0";
  el("shinrou").value = "0";
  el("guestName").value = "";
  state.skills = [];
  state.actions = [];
  renderSkills();
  renderActions();
  buildOutput();
}

/** ========= イベント ========= */
roleEl.addEventListener("change", ()=>{
  syncClassOptions();
  syncBackgroundOptions();
  applyRoleVisibility();
});
classEl.addEventListener("change", ()=>{ syncBackgroundOptions(); });

ageChkEl.addEventListener("change", ()=>{ updateAgePill(); });

el("btnAllRandom").addEventListener("click", randomAllLevel3);
el("btnReset").addEventListener("click", resetAll);

el("btnNameRand").addEventListener("click", ()=>{ genName(); buildOutput(); });
el("rerollName").addEventListener("click", ()=>{ genName(); buildOutput(); });

el("rerollRole").addEventListener("click", ()=>{ genRole(); buildOutput(); });
el("rerollClass").addEventListener("click", ()=>{ genClass(); buildOutput(); });
el("rerollBackground").addEventListener("click", ()=>{ genBackground(); buildOutput(); });

el("rerollAge").addEventListener("click", ()=>{ genAge(); buildOutput(); });

el("rerollHeight").addEventListener("click", ()=>{ genHeight(); buildOutput(); });
el("rerollFashion").addEventListener("click", ()=>{ genFashion(); buildOutput(); });
el("rerollJob").addEventListener("click", ()=>{ genJob(); buildOutput(); });
el("rerollQuirk").addEventListener("click", ()=>{ genQuirk(); buildOutput(); });

el("rerollLike").addEventListener("click", ()=>{ rerollLikeOnly(); buildOutput(); });
el("rerollDislike").addEventListener("click", ()=>{ rerollDislikeOnly(); buildOutput(); });

el("btnRandSkills").addEventListener("click", ()=>{ generateSkillsByRules(); buildOutput(); });
el("btnRandActions").addEventListener("click", ()=>{ generateActionsByRules(); buildOutput(); });
el("btnRandBoth").addEventListener("click", ()=>{ generateSkillsByRules(); generateActionsByRules(); buildOutput(); });

el("rerollGuestName").addEventListener("click", ()=>{ genGuestName(); buildOutput(); });
el("rerollGuestSkill").addEventListener("click", ()=>{ genGuestSkill(); buildOutput(); });
el("rerollGuestRel").addEventListener("click", ()=>{ genGuestRel(); buildOutput(); });

el("btnBuildOutput").addEventListener("click", buildOutput);
el("btnCopy").addEventListener("click", copyOutput);

init();
</script>
</body>
</html>

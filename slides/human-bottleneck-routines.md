---
marp: true
theme: tech-bold
paginate: false
size: 16:9
---

<!-- _class: title compact-title approval-title -->
<!-- _paginate: false -->

# 承認待ちのボトルネックを減らす

<p class="title-date">2026/08/25</p>

---

<!-- _class: lead -->

<span class="label">課題</span>

## あれ、AIより<br>自分の方が働いてない？？

<p class="lead-note">実装してほしいタスクは多いのに、人間の指示待ちで動き出せてないタスクがたくさんあった</p>

---

<!-- _class: lead -->

<span class="label">結論</span>

## 解決にはClaude Code Routinesが<br>有効かもしれない

---

<!-- _class: three-points -->

<span class="label">AIの強み</span>

## AIを活用できているのか？？

<div class="point-row">
  <div>
    <span class="point-number">01</span>
    <h3>知能</h3>
    <p>大量の情報を読み、候補を出し続ける</p>
  </div>
  <div>
    <span class="point-number">02</span>
    <h3>処理速度</h3>
    <p>大量の処理を短時間で進める</p>
  </div>
  <div>
    <span class="point-number">03</span>
    <h3>並列処理</h3>
    <p>複数の調査や実装を同時に進められる</p>
  </div>
</div>

---

<!-- _class: human-parallel -->

## 人間はタスクを並列には扱えない

<div class="parallel-diagram">
  <div class="parallel-caption">
    <span class="parallel-axis">時間 →</span>
  </div>

  <div class="parallel-grid">
    <div class="parallel-task parallel-task-a">タスクA</div>
    <div class="parallel-track">
      <span class="parallel-work task-a">作業</span>
      <span class="parallel-wait">待ち</span>
      <span class="parallel-wait">待ち</span>
      <span class="parallel-work task-a">作業</span>
      <span class="parallel-wait">待ち</span>
      <span class="parallel-wait">待ち</span>
    </div>
    <div class="parallel-task parallel-task-b">タスクB</div>
    <div class="parallel-track">
      <span class="parallel-wait">待ち</span>
      <span class="parallel-work task-b">作業</span>
      <span class="parallel-wait">待ち</span>
      <span class="parallel-wait">待ち</span>
      <span class="parallel-work task-b">作業</span>
      <span class="parallel-wait">待ち</span>
    </div>
    <div class="parallel-task parallel-task-c">タスクC</div>
    <div class="parallel-track">
      <span class="parallel-wait">待ち</span>
      <span class="parallel-wait">待ち</span>
      <span class="parallel-work task-c">作業</span>
      <span class="parallel-wait">待ち</span>
      <span class="parallel-wait">待ち</span>
      <span class="parallel-work task-c">作業</span>
    </div>
  </div>

  <p class="parallel-note">仕事で扱うことの多い言語情報は<br>同じ脳のワーキングメモリを使用するので並列に扱い難い</p>
</div>

---

<!-- _class: waiting-bottleneck -->

## 大抵は長い待ち時間のタスクが多くなる

<div class="waiting-diagram">
  <div class="waiting-task-list">
    <div class="waiting-task-row">
      <div class="waiting-task-name waiting-task-a">タスクA</div>
      <div class="waiting-line">
        <span class="waiting-block waiting-active">人間が作業中</span>
      </div>
    </div>
    <div class="waiting-task-row">
      <div class="waiting-task-name waiting-task-b">タスクB</div>
      <div class="waiting-line">
        <span class="waiting-block waiting-paused">待ち時間</span>
      </div>
    </div>
    <div class="waiting-task-row">
      <div class="waiting-task-name waiting-task-c">タスクC</div>
      <div class="waiting-line">
        <span class="waiting-block waiting-paused">待ち時間</span>
      </div>
    </div>
  </div>
</div>

---

<!-- _class: lead -->

<span class="label">一応人間の強みも</span>

## AIは、与えていない<br>コンテキストを読めない

<p class="lead-note">暗黙知、過去の経緯、組織の事情など、<br>人間は開発周辺のコンテキストを持っている</p>

<p class="note">※直近では<a href="https://zed.dev/blog/introducing-delta">Delta</a>のようなコラボレーションツールも出てきており、ここも変わっていきそう</p>

<!--
[Sources]
- https://zed.dev/blog/introducing-delta
-->

---

<!-- _class: section-dark chapter -->
<!-- _paginate: false -->

# 人間の承認待ちは<br>以前にもあった

---

<!-- _class: lead -->

<span class="label">Auto mode以前</span>

## AIは、人間の承認待ちで<br>しょっちゅう止まっていた

<div class="flow">
  <div>依頼<br><small>人間</small></div>
  <span>→</span>
  <div>実行<br><small>AI</small></div>
  <span>→</span>
  <div>承認<br><small>人間</small></div>
  <span>→</span>
  <div>再開<br><small>AI</small></div>
</div>

<p class="note dark-note">そこで自作Auto modeのようなskillを作った<br>（名前は「アンチヒューマンボトルネック」）</p>

<p class="note compact-note">--dangerously-skip-permissionsという怖い名前のフラグも存在している</p>

---

<!-- _class: lead -->

<span class="label">現在</span>

## 自律性の向上

<p class="lead-note">8/14から<a href="https://claude.com/blog/auto-mode-default-in-claude-code">Auto mode</a>がデフォルトになった</p>

<p class="lead-note">モデルの向上により、<br>自律性と危険コマンドの検出が向上</p>

<!--
[Sources]
- https://claude.com/blog/auto-mode-default-in-claude-code
-->

---

<!-- _class: section-dark chapter -->
<!-- _paginate: false -->

# ここから本題

---

<!-- _class: lead -->

## ルーティンの活用

<p class="lead-note">セッション間での介入が不要になった</p>

<p class="lead-note">Opus 5の登場でFable 5と同等の能力をコストを抑えて使用できるようになった</p>

<p class="lead-note">→<a href="https://code.claude.com/docs/ja/routines">ルーティン</a>を活用し何度も自律的に起動し動かす</p>

<!--
[Sources]
- https://code.claude.com/docs/ja/routines
-->

---

<span class="label">活用に向けた課題</span>

## 一つのリポジトリだけでは、<br>必要な前提が足りない

<div class="two-column">
  <div>
    <h3>情報が分散している</h3>
    <ul>
      <li>OAS</li>
      <li>エージェントskill</li>
      <li>サブモジュール</li>
    </ul>
  </div>
  <div>
    <h3>クラウド実装で起きること</h3>
    <ul>
      <li>前提が足りない</li>
      <li>実装方針がずれる</li>
      <li>人間の手戻りが増える</li>
    </ul>
  </div>
</div>

---

<!-- _class: lead -->

<span class="label">解決策</span>

## バーチャルモノレポで、<br>AIが見る範囲を揃える

<div class="flow">
  <div>複数の<br>リポジトリ</div>
  <span>→</span>
  <div>情報をまとめた<br>仮想的な入口</div>
  <span>→</span>
  <div>コンテキストを<br>渡して実装</div>
</div>

<p class="note dark-note">各リポジトリの情報を、ルーティンが参照できる形にまとめる</p>

---

## 実際に動かしてみて

<div class="two-column">
  <div>
    <h3>うまくいった</h3>
    <p>ロジック修正</p>
    <ul>
      <li>OASを参照できる</li>
      <li>実装方針を具体化しやすい</li>
    </ul>
  </div>
  <div>
    <h3>うまくいかなかった</h3>
    <p>UI修正</p>
    <ul>
      <li>見た目の表現が曖昧</li>
      <li>方針が雑だと結果もずれる<span class="inline-note">（手書きで方針を雑に記載など）</span></li>
    </ul>
  </div>
</div>


---

## ローカルとクラウドの使い分け

<div class="two-column">
  <div>
    <h3>ローカル</h3>
    <p>すぐに動かしたいもの</p>
    <ul>
      <li>動作確認をする</li>
      <li>実装方針を立てる</li>
    </ul>
  </div>
  <div>
    <h3>クラウド</h3>
    <p>すぐに触らなくてよいもの</p>
    <ul>
      <li>優先度が低いタスク</li>
      <li>単純なタスク</li>
    </ul>
  </div>
</div>

---

<!-- _class: summary-slide -->

<span class="label">まとめ</span>

## 課題は解決された？？

<div class="summary-layout">
  <div class="summary-list">
    <div><span>01</span><p>ルーティンによりAIが働いている時間が増えた</p></div>
    <div><span>02</span><p>手探り中だが実装も割といい感じ！？</p></div>
    <div><span>03</span><p>ワークしてPRも結構溜まってきた</p></div>
  </div>
</div>

---

<!-- _class: section-dark chapter -->
<!-- _paginate: false -->

# 次のボトルネックは<br>レビュー！

<p class="note next-bottleneck-note">ここはまた次回以降で</p>

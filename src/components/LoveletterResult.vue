<template>
  <div class="loveletter-result">
    <div class="loveletter-result_main">
      <img src="@/assets/letter_head.gif" alt>
      <div style="display: flex;align-items: stretch">
        <img src="@/assets/letter_left.gif" alt>
        <div class="loveletter-result__message">
          <p v-if="step>1">{{questions.name}} {{titleList[questions.title-1]}}</p>
          <template v-for="(results, questionNumber) in resultsList">
            <p v-if="step > questionNumber+2" :key="questionNumber">
              <template v-for="(result, resultIndex) in results">
                <span
                  :key="result"
                  v-if="questions[`q${questionNumber+2}`] === resultIndex"
                >{{result}}</span>
              </template>
            </p>
          </template>
        </div>
        <img src="@/assets/letter_right02.gif" alt>
      </div>
      <img src="@/assets/letter_foot.gif" alt>
    </div>
    <template v-if="step >= 7">
      <div style="background: #fff;">
        <p class="loveletter-result_build">
          <button type="button" @click="handleClickRestart">もう一度つくる</button>
        </p>
        <p class="loveletter-result_share">
          <input type="text" class="loveletter-result_shareurl" readonly :value="shareUrl">
          <a target="_blank" :href="twitterUrl">つぶやく</a>
        </p>
      </div>
    </template>
  </div>
</template>
<script>
import { stringify } from 'querystring'

export default {
  props: {
    questions: Object,
    step: Number,
    sex: String
  },
  computed: {
    titleList() {
      return ['さま', '様', '殿', 'さん', 'くん', 'ちゃん']
    },
    shareUrl() {
      return `https://dailyportalz.jp/kiji/love-letter-generator?${stringify({
        ...this.questions
      })}`
    },
    twitterUrl() {
      return `https://twitter.com/intent/tweet?text=読書感想文メールジェネレーター&url=${encodeURIComponent(
        this.shareUrl
      )}`
    },
    resultsList() {
      if (this.sex == 'men') {
        return [
          [
            'やあ、いきなり手紙なんてびびるよね。でもちょっと読んで',
            'このまえはおつかれさまでした。ちゃんと帰れましたか？',
            'おせわになっております。',
            'まだ見ぬあなたへ'
          ],
          [
            'なんというか、あなたのことが好きなんです。',
            '好きだ。結婚してほしい、嫌なら結納でもいい。',
            'おまいさんのことがマジ好いちょるけんのう',
            'ぶっちゃけ、好きなんだけど。おまえのこと。'
          ],
          [
            'あなたといっしょにいると幸せな空気が僕をつつみます。',
            'そう。その吸い込まれるような瞳、白魚のような指、そしてうぶ毛が好きだ。',
            'いつも道に迷っているその姿に、めがねを落として探している姿に惹かれます。',
            '人が住めるぐらい大きな冷蔵庫、玄関だけで僕の部屋ぐらいある大きな家、ステキ過ぎます。'
          ],
          [
            'きみを見るだけで血液が沸騰するような気分になります、ほんとに沸騰したら死んじゃうけど',
            '好きだ。きみが北斗星なら僕はホッキョクグマさ。',
            'きみのことが、お、おにぎりぐらい好きなんだな。',
            'シングルベッドはうんざり、僕を独りぼっちのランナーにしないで'
          ],
          [
            '結論は急ぎません。とりあえず、こんどごはんを食べに行きましょう。',
            'つきあってください。楽しいことをたくさんしましょう。',
            '来週日曜日に両親に紹介させてください。午後あけといて。',
            '嫌いにならないでください。でも、遠くからそっと見つめていてほしい。'
          ],
          [
            'では。メールまってます。',
            'あなたのために家一軒用意してまってます。',
            '僕の携帯に連絡ください。ワンギリでもいいですから！',
            'OKならば黄色いハンカチを干しておいてください。'
          ]
        ]
      } else {
        return [
          [
            'あの、迷ったんだけど、手紙を書くことにしました',
            '毎朝あってるのですが、あたしのこと憶えてますか？',
            'お世話様です。きょうは仕事の話じゃないんです。',
            'まだ見ぬあなたへ'
          ],
          [
            'あなたにぞっこん首ったけです。',
            '言ってみれば好きということなのではないかと思います。',
            'あなたの心に、私という花を咲かせたいです。',
            'っていうか、あなたにラブって感じ？'
          ],
          [
            'あなたが転校してきたときから好きでした。',
            '去年のあたしの10大ニュースはあなたに会ったことです。',
            '仕事の鬼のあなたが雨の夜、捨て猫をひろっている姿を見てから好きです。',
            'いつのまにか好きでした。昨日だった気もします。'
          ],
          [
            'あなたのことを考えると胸が締め付けられます',
            'あなたがいないと枕を涙でぬらす夜ばかりです。',
            'あなたへの想いをごまかすために素振り100回する毎日です。',
            'けっこう好きです。けっこう、というか、まあまあ。'
          ],
          [
            'お気軽にお電話ください。',
            'あした、公園で待ってます。きてください。',
            'この手紙に同封のはがきの回答欄に丸をして投函してください。',
            '妹がご自宅に伺いますので結果をことづけてください。'
          ],
          [
            'かしこ',
            'かみのごかごがありますように',
            'ゼッタイ返事ください！キャー！',
            '詳しくはあしたの朝刊をご覧ください。'
          ]
        ]
      }
    }
  },
  methods: {
    handleClickRestart() {
      location.href = location.href.replace(location.search, '')
    }
  }
}
</script>

<style scoped>
img {
  user-select: none;
}

.loveletter-result {
  width: 420px;
  margin: 30px auto;
  background-image: url('../assets/letter_back.gif');
}

.loveletter-result_main {
  font-size: 0;
  max-width: 420px;
}

.loveletter-result__message {
  padding: 16px;
  font-size: 12px;
  flex: 1;
  min-height: 150px;
  max-width: 292px;
}

.loveletter-result__message p:first-child {
  margin-top: 0;
}

.loveletter-result_build {
  text-align: right;
  background: #fff;
  padding: 1em 0 0;
  margin: 0;
}

.loveletter-result_share {
  font-size: 12px;
  background: #fff;
}

.loveletter-result_shareurl {
  width: 100%;
}

.loveletter-result_share {
  display: flex;
  align-items: center;
}

input {
  margin: 4px 10px 4px 0;
  flex: 1;
}
</style>

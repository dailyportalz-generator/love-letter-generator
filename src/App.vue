<template>
  <div id="app">
    <template>
      <!--<span v-if="step < 7"><b>step{{step+1}}</b></span>-->
      <WomenOrMen
              key="sex"
              v-if="step === 0"
              @selectSex="handleSex"
      />
      <InputQuestion
              key="start"
              v-if="step === 1"
              @next="handleStart"
      />

      <SelectQuestions
              key="question2"
              v-if="step === 2"
              v-model="questions.q2"
              @next="handleNext"
              :choices="choicesList[0]"
      />

      <SelectQuestions
              key="question3"
              v-if="step === 3"
              v-model="questions.q3"
              @next="handleNext"
              :choices="choicesList[1]"
      />

      <SelectQuestions
              key="question4"
              v-if="step === 4"
              v-model="questions.q4"
              @next="handleNext"
              :choices="choicesList[2]"
      />

      <SelectQuestions
              key="question5"
              v-if="step === 5"
              v-model="questions.q5"
              @next="handleNext"
              :choices="choicesList[3]"
      />

      <SelectQuestions
              key="question6"
              v-if="step === 6"
              v-model="questions.q6"
              @next="handleNext"
              :choices="choicesList[4]"
      />

      <SelectQuestions
              key="question7"
              v-if="step === 7"
              v-model="questions.q7"
              @next="handleNext"
              :choices="choicesList[5]"
      />
    </template>

    <LoveletterResult
            :step="step"
            :questions="questions"
            :sex="sex"
    />
  </div>
</template>

<script>
import InputQuestion from './components/InputQuestion.vue'
import LoveletterResult from './components/LoveletterResult.vue'
import SelectQuestions from './components/SelectQuestions.vue'
import WomenOrMen from './components/WomenOrMen.vue'
import { parse } from 'querystring'

export default {
  name: 'app',
  data() {
    return {
      step: 0,
      sex: 'men',
      questions: {
        name: '',
        title: 0,
        q2: 0,
        q3: 0,
        q4: 0,
        q5: 0,
        q6: 0,
        q7: 0,
      }
    }
  },
  components: {
    InputQuestion,
    SelectQuestions,
    LoveletterResult,
    WomenOrMen
  },
  mounted() {
    const params = parse(location.search.replace('?', ''))
    const isValid = ['sex','name', 'title', 'q2', 'q3', 'q4', 'q5', 'q6', 'q7'].every((val) => {
      if (!params[val]) {
        return false
      }
      if (val != 'sex' && parseInt(params[val]) < 1) {
        return false
      }
      return true
    })
    if (isValid) {
      const questions = {
        sex: parseInt(params.sex),
        name: params.name,
        title: parseInt(params.title),
        q2: parseInt(params.q2),
        q3: parseInt(params.q3),
        q4: parseInt(params.q4),
        q5: parseInt(params.q5),
        q6: parseInt(params.q6),
        q7: parseInt(params.q7)
      }
      this.questions = questions
      this.step = 7
    }
  },
  methods: {
    handleNext() {
      this.step ++
    },

    handleSex(sex){
      this.sex = sex
      this.handleNext()
    },

    handleStart(startData) {
      this.questions.name = startData.name
      this.questions.title = startData.title
      this.handleNext()
    }
  },
  computed: {
    choicesList() {
      if(this.sex=='men') {
        return [
          ['クラスメート', '何度かあった人', 'お得意先', '知らない人'],
          ['カジュアルに', '順序間違えて', 'どこの国の言葉かわからないけど、なんかそれっぽい感じで', 'キムタク風に'],
          ['無難に', 'ディテールにこだわって', 'しぐさがすき', '資産'],
          ['ユーモアを交えつつ', '詩人のように', '裸の大将のように', 'Ｊポップ感じで'],
          ['手探りな感じ', 'もっとアグレッシブに', '結論から。', '病める僕を見てくれ'],
          ['IT活用', '強引に', '携帯電話で返事がほしい。', '健さんみたいに']
        ]
      }
      else {
        return[
          ['クラスメート', '同じ電車になる人', 'お得意先', '知らない人'],
          ['ストレートに', '遠まわしに', '花の子気どりで', 'ギャルっぽく'],
          ['学生時代から', '去年から', '大人になってから', 'なんとなく'],
          ['本気で', '弱さを見せつつ', 'ストイックに', 'そんなに好きじゃない'],
          ['通販みたいに', '具体的に', '用意周到に', '手下を使って'],
          ['おしとやかに', 'ドラクエの牧師のように', 'かわいい感じで', '大がかりに']
        ]
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 800px;
  margin: 0 auto;
}
</style>

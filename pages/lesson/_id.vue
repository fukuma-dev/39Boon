<template>
  <div class="text-center wrapper">
    <div v-if="!isStart">
      <el-button
        @click="
          start()
          jpSpeech(phrase[num].jp)
        "
      >
        開始しますか？
      </el-button>
    </div>
    <div v-if="isStart">
      <p class="jp-phrase">{{ phrase[num].jp }}</p>
      <el-button
        v-if="!isAnswer"
        @click="
          toAnswer()
          enSpeech(phrase[num].en)
        "
      >
        答え
      </el-button>
      <div v-if="isAnswer">
        <p class="en-phrase">{{ phrase[num].en }}</p>
        <el-button
          @click="
            next()
            jpSpeech(phrase[num].jp)
          "
        >
          次へ
        </el-button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      num: 0,
      isStart: false,
      isAnswer: false
    }
  },
  asyncData({ params }) {
    return {
      phrase: require(`~/assets/json/${params.id}.json`)
    }
  },
  methods: {
    start() {
      this.isStart = true
    },
    next() {
      this.isAnswer = false
      this.num = this.num + 1
    },
    toAnswer() {
      this.isAnswer = true
    },
    jpSpeech(jpText) {
      const ssu = new SpeechSynthesisUtterance()
      ssu.text = jpText
      ssu.lang = 'ja-JP'
      speechSynthesis.speak(ssu)
    },
    enSpeech(enText) {
      const ssu = new SpeechSynthesisUtterance()
      ssu.text = enText
      ssu.lang = 'en-US'
      speechSynthesis.speak(ssu)
    }
  }
}
</script>

<style scoped>
.wrapper {
  margin: 200px 0;
  text-align: center;
}
.jp-phrase {
  font-size: 1.5rem;
}
.en-phrase {
  font-size: 1.5rem;
}
</style>

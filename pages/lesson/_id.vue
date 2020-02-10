<template>
  <div class="text-center wrapper">
    <div v-if="!isStart">
      <el-button
        @click="
          start()
          jpSpeech(phrase[num].jp)
        "
        type="primary"
        class="start-btn"
      >
        トレーニング開始！
      </el-button>
      <p>※ 音が鳴りますのでご注意ください</p>
    </div>
    <div v-if="isStart">
      <el-row>
        <el-progress
          :percentage="num * 10"
          type="dashboard"
          width="120"
        ></el-progress>
      </el-row>
      <div v-if="num < 10">
        <el-row>
          <p class="jp-phrase">{{ phrase[num].jp }}</p>
        </el-row>
      </div>
      <!-- <div v-if="num === 10">
        <p class="jp-phrase">お疲れ様です！</p>
        <el-button @click="end()">
          終了する
        </el-button>
      </div> -->
      <div v-if="isAnswer">
        <p class="en-phrase">{{ phrase[num].en }}</p>
      </div>
      <v-row>
        <el-button
          v-if="!isAnswer"
          @click="
            toAnswer()
            enSpeech(phrase[num].en)
          "
        >
          答え
        </el-button>
        <el-button
          v-if="isAnswer && num < 10"
          @click="
            next()
            jpSpeech(phrase[num].jp)
          "
        >
          次へ
        </el-button>
      </v-row>
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
    end() {
      this.$router.push('/')
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
  margin: 100px 0;
  text-align: center;
}
.start-btn {
  font-size: 20px;
}
.jp-phrase {
  font-size: 1.5rem;
}
.en-phrase {
  font-size: 1.5rem;
}
</style>

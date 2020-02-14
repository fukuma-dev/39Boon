<template>
  <div class="text-center wrapper">
    <!-- トレーニング開始前 -->
    <div v-if="!isStart" class="confirm">
      <p>表示される日本語文を<br />英語に翻訳しよう！</p>
      <el-button
        @click="
          start()
          speech(phrase[num].jp, 'ja-JP')
        "
        type="primary"
        class="start-btn"
      >
        トレーニング開始！
      </el-button>
      <p>※ 音が鳴りますのでご注意ください</p>
    </div>
    <!-- トレーニング開始後 -->
    <div v-if="isStart">
      <el-row>
        <el-progress
          :percentage="progress * limit"
          type="dashboard"
          width="120"
        ></el-progress>
      </el-row>
      <el-row>
        <div class="phrase-text">
          <p v-if="num < limit" class="jp-phrase">{{ phrase[num].jp }}</p>
        </div>
      </el-row>
      <el-row>
        <div class="phrase-text">
          <p v-if="isAnswer" class="en-phrase">{{ phrase[num].en }}</p>
        </div>
      </el-row>
      <!-- ボタン群 -->
      <el-row>
        <div>
          <el-button
            v-if="!isAnswer && progress !== limit"
            @click="
              toAnswer()
              speech(phrase[num].en, 'en-US')
            "
            type="info"
          >
            答えを見る
          </el-button>
          <el-button
            v-if="isAnswer && progress < limit"
            @click="
              next()
              speech(phrase[num].jp, 'ja-JP')
            "
            type="info"
          >
            次のフレーズへ
          </el-button>
          <div v-if="progress === limit">
            <p>お疲れ様でした！</p>
            <el-button @click="end()" type="danger">
              トレーニングを終了する
            </el-button>
          </div>
        </div>
      </el-row>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      num: 0,
      progress: 0,
      limit: 10,
      isStart: false,
      isAnswer: false
    }
  },
  asyncData({ params }) {
    const data = require(`~/assets/json/${params.id}.json`)
    const count = 10
    const t = []
    const r = []
    let l = data.length
    let n = count < l ? count : l
    while (n-- > 0) {
      const i = (Math.random() * l) | 0
      r[n] = t[i] || data[i]
      --l
      t[i] = t[l] || data[l]
    }

    return {
      phrase: r
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
      this.progress = this.progress + 1
    },
    end() {
      this.$router.push('/')
    },
    speech(text, language) {
      speechSynthesis.cancel()
      const ssu = new SpeechSynthesisUtterance()
      ssu.text = text
      ssu.lang = language
      speechSynthesis.speak(ssu)
    }
  }
}
</script>

<style scoped>
.wrapper {
  margin-top: 50px;
  text-align: center;
}
.confirm {
  margin: 200px 0;
}
.start-btn {
  font-size: 20px;
}
.jp-phrase {
  font-size: 1.2rem;
  margin: 0px 10px;
}
.en-phrase {
  font-size: 1.2rem;
  margin: 0px 10px;
}
.phrase-text {
  height: 60px;
  margin: 20px 0;
}
</style>

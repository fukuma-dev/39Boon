<template>
  <div class="hero">
    <el-row>
      <h1 class="hero__title">39Boon!!</h1>
      <p class="hero__description">
        毎日の英作文トレーニングを通して
        <br />
        英語のスピーキング能力を鍛えよう
      </p>
    </el-row>
    <el-row>
      <el-select
        @change="goTraining(value)"
        v-model="value"
        placeholder="トレーニングを選択"
        size="large"
        class="select"
      >
        <el-option
          v-for="item in options"
          :key="item.value"
          :label="item.label"
          :value="item.value"
          style="font-size:16px"
        >
        </el-option>
      </el-select>
    </el-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      options: [
        {
          value: 'eikaiwa',
          label: '日常会話'
        },
        {
          value: 'grammar-present-perfect',
          label: '英文法 - 現在完了'
        },
        {
          value: 'grammar-passiveness',
          label: '英文法 - 受け身'
        },
        {
          value: 'grammar-would',
          label: 'wouldを使いこなそう!'
        }
      ]
    }
  },
  methods: {
    goTraining(command) {
      console.log(command)
      this.$router.push({ path: `train/${command}` })
    }
  }
}
</script>

<style lang="scss">
.hero {
  color: #fff;
  height: 100vh;
  text-align: center;
  background: -moz-linear-gradient(top, #34558b 30%, #ff6f61 100%);
  background: -webkit-linear-gradient(top, #34558b 30%, #ff6f61 100%);
  background: linear-gradient(to bottom, #34558b 30%, #ff6f61 100%);
  &__title {
    font-family: 'Fugaz One';
    margin: 50px 0;
    font-size: 2.5rem;
  }
  &__description {
    font-weight: bold;
    font-family: 'M PLUS Rounded 1c';
    margin: 40px 0;
  }
}
.el-select > .el-input {
  font-size: 16px;
}
</style>

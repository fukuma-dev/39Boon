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
        @change="goLesson(value)"
        v-model="value"
        placeholder="コースを選ぼう！"
        class="select-menu"
      >
        <el-option
          v-for="item in options"
          :key="item.value"
          :label="item.label"
          :value="item.value"
          class="select-options"
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
        }
      ],
      value: ''
    }
  },
  methods: {
    goLesson(value) {
      this.$router.push({ path: `lesson/${value}` })
    }
  }
}
</script>

<style scoped>
.hero {
  height: 100vh;
  text-align: center;
  background: -moz-linear-gradient(top, #34558b 30%, #ff6f61 100%);
  background: -webkit-linear-gradient(top, #34558b 30%, #ff6f61 100%);
  background: linear-gradient(to bottom, #34558b 30%, #ff6f61 100%);
}
.hero__title {
  color: #fff;
  font-family: 'Fugaz One';
  margin: 50px 0;
  font-size: 2.5rem;
}
.hero__description {
  color: #fff;
  font-weight: bold;
  font-family: 'M PLUS Rounded 1c';
  margin: 40px 0;
}
.select-menu {
  color: black;
}
.select-options {
  font-size: 16px;
}
</style>

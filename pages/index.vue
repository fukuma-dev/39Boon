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
      <el-dropdown @command="goTraining">
        <el-button type="success" class="select-btn">
          トレーニングメニューを選択<i
            class="el-icon-arrow-down el-icon--right"
          ></i>
        </el-button>
        <el-dropdown-menu slot="dropdown">
          <el-dropdown-item
            v-for="item in options"
            :key="item.value"
            :command="item.value"
          >
            {{ item.label }}
          </el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
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
    goTraining(command) {
      this.$router.push({ path: `train/${command}` })
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
.select-btn {
  font-size: 16px;
}
</style>

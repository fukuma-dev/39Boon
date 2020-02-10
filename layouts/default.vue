<template>
  <el-container>
    <el-header v-if="$route.name !== 'index'" style="padding: 0px">
      <custom-header />
    </el-header>
    <el-main style="padding: 0px">
      <nuxt />
    </el-main>
  </el-container>
</template>

<script>
export default {
  components: {
    CustomHeader: () => import('~/components/TheHeader.vue')
  }
}
</script>

<style>
body {
  margin: 0px;
}
</style>

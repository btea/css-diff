<script setup lang="ts">
import { ElButton } from 'element-plus'
import { reactive, ref } from 'vue'

const title = ref('ep-node-18-diff')
const diffInfo = reactive({
  left: '',
  right: '',
  result: ''
})
// @ts-expect-error
const dmp = new window.diff_match_patch();
const startDiff = () => {
  const { left, right } = diffInfo
  const diff = dmp.diff_main(left, right)
  const html = dmp.diff_prettyHtml(diff)
  diffInfo.result = html
}
</script>

<template>
  <div class="container">
    <div class="tree-menu">

    </div>
    <div class="content">
      <div class="common">
        <div class="title">{{ title }}</div>
        <el-button type="primary" @click="startDiff">diff</el-button>
      </div>
      <div class="area">
        <div class="left">
          <textarea v-model="diffInfo.left"></textarea>
        </div>
        <div class="right">
          <textarea v-model="diffInfo.right"></textarea>
        </div>
      </div>
      <div class="result">
        <div v-html="diffInfo.result"></div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.container {
  display: flex;
  height: 100vh;
  overflow-y: auto;
  .tree-menu {
    width: 400px;
  }
  .content {
    flex: 1;
  }
  .area {
    display: flex;
    .left, .right {
      flex: 1;
      height: 400px;
      textarea {
        width: 100%;
        height: 100%;
        padding: 10px;
      }
    }
  }
}
</style>

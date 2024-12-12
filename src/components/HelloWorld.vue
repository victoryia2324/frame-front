<template>
  <div class="app-container">
    <div v-for="(value, key) in configDict" :key="key" class="config-item">
      <h2>{{ key }}</h2>
      <div v-if="value.length === 0" class="no-value">没有 {{ key }}</div>
      <el-radio-group v-model="configValue[key]" class="radio-group">
        <el-radio v-for="(name, idx) in value" :key="idx" :label="name" class="radio-button">{{ name }}</el-radio>
      </el-radio-group>
    </div>

    <el-divider class="custom-divider" />

    <el-button @click="clickButton" type="primary" class="run-button">运行</el-button>

    <el-divider class="custom-divider" />

    <div class="result-section">
      <h2>运行结果</h2>
      <div class="running-res">
        <div v-for="(content, idx) in runningOutput" :key="idx">
          <p v-if="content.type == 'string'" class="result-text">{{ content.content }}</p>
          <img v-if="content.type == 'image'" :src="'data:image/jpeg;base64,'+content.content" class="result-image" />
        </div>
      </div>
    </div>
  </div>

  <el-dialog v-model="showConnectInfoWindow" title="连接地址" :show-close="false" custom-class="custom-dialog">
    <el-form label-width="40px">
      <el-form-item label="Url">
        <el-input v-model="connectUrl" />
      </el-form-item>
      <el-form-item label="Port">
        <el-input v-model="connectPort" />
      </el-form-item>
    </el-form>
    <el-button type="primary" @click="onClickConnect" class="connect-button">连接</el-button>
  </el-dialog>
</template>

<script setup lang="ts">
// ... (script 部分保持不变)
</script>

<style scoped>
.app-container {
  background-color: #eef7f2;
  padding: 20px;
}

.config-item {
  margin-bottom: 20px;
}

.no-value {
  color: #a4cab6;
}

.radio-group {
  display: flex;
  flex-direction: column;
}

.radio-button {
  margin: 5px 0;
  background-color: #68b88e;
  border-color: #5dbe8a;
  color: white;
}

.radio-button.is-checked {
  background-color: #3c9566;
  border-color: #579572;
}

.custom-divider {
  margin: 20px 0;
  border-color: #5dbe8a !important;
}

.run-button {
  background-color: #3c9566;
  border-color: #579572;
}

.result-section {
  margin-top: 20px;
}

.running-res {
  text-align: left;
  width: 100%;
  font-size: large;
  margin-top: 10px;
}

.result-text {
  color: #3c9566;
}

.result-image {
  max-width: 100%;
  height: auto;
  margin-top: 10px;
  border: 1px solid #5dbe8a;
}

.custom-dialog {
  background-color: #eef7f2;
}

.connect-button {
  background-color: #3c9566;
  border-color: #579572;
}
</style>
<template>
  <div class="about">
    <h2 class="about-title">Персональные данные</h2>
    <div v-if="data">
      <div class="user-data">{{ data.user.name }}, {{ data.user.age }} лет</div>

      <h3 class="about-title">Дети</h3>
      <div v-for="(child, index) in data.children" :key="index">
        <div v-if="child.name !== ''" class="child-data">{{ child.name }}, {{ child.age }} лет</div>
      </div>
    </div>
    <div v-else>
      <p>Нет данных для отображения</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const data = ref(null)

onMounted(() => {
  const savedData = localStorage.getItem('formData')
  if (savedData) {
    data.value = JSON.parse(savedData)
  }
})
</script>

<style scoped>
.about {
  max-width: 616px;
  width: 100%;
  margin-top: 30px;
}

.about-title {
  font-size: 16px;
  line-height: 24px;
  font-weight: 500;
  margin-bottom: 20px;
}

.user-data {
  font-size: 16px;
  line-height: 24px;
  font-weight: 700;
  margin-bottom: 60px;
}

.child-data {
  background-color: #f1f1f1;
  border-radius: 5px;
  padding: 10px 20px;
  margin-bottom: 20px;
  font-size: 16px;
  line-height: 24px;
  font-weight: 700;
  display: inline-block;
}
</style>

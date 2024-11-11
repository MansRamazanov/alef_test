<template>
  <div class="form-container">
    <div class="form">
      <h2 class="form-title">Персональные данные</h2>
      <div class="input-container">
        <label class="input-label" for="name">Имя</label>
        <input type="text" v-model="user.name" class="input" id="name" />
      </div>
      <div class="input-container">
        <label class="input-label" for="age">Возраст</label>
        <input type="text" v-model.number="user.age" class="input" id="age" />
      </div>
      <div class="children-container">
        <div class="children-header">
          <div>Дети (макс.5)</div>
          <button @click="addChild" :disabled="children.length >= maxChildren" class="add-button">
            <img src="../assets/img/plus.png" alt="Плюс" /> Добавить ребенка
          </button>
        </div>
        <div v-for="(child, index) in children" :key="index" class="children-list">
          <div class="input-container" style="margin-bottom: 0">
            <label class="input-label" for="child_name">Имя</label>
            <input v-model="child.name" class="input" id="child_name" />
          </div>
          <div class="input-container" style="margin-bottom: 0">
            <label class="input-label" for="child_age">Возраст</label>
            <input v-model.number="child.age" type="text" min="0" class="input" id="child_age" />
          </div>

          <button @click="removeChild(index)" class="remove-button">Удалить</button>
        </div>
      </div>

      <button
        @click="saveData"
        class="save-button"
        :disabled="user.name === '' || user.age === null"
      >
        Сохранить
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

interface User {
  name: string
  age: number | null
}

interface Child {
  name: string
  age: number | null
}

const user = ref<User>({ name: '', age: null })

const children = ref<Child[]>([])

const maxChildren = 5

const addChild = (): void => {
  if (children.value.length < maxChildren) {
    children.value.push({ name: '', age: null })
  }
}

const removeChild = (index: number): void => {
  children.value.splice(index, 1)
}

const saveData = (): void => {
  const data = {
    user: user.value,
    children: children.value
  }
  localStorage.setItem('formData', JSON.stringify(data))
  router.push('/about')
}
</script>

<style scoped>
.form {
  margin: 0 auto;
  max-width: 616px;
  padding: 30px 0;
}

.form-title {
  font-size: 16px;
  font-weight: 500;
  line-height: 24px;
  color: #111111;
  padding-bottom: 20px;
}

.input-container {
  display: flex;
  flex-direction: column;
  border: 1px solid #f1f1f1;
  border-radius: 5px;
  padding: 8px 16px;
  margin-bottom: 10px;
  max-width: 620px;
}

.input-label {
  font-size: 13px;
  line-height: 16px;
  color: #1111117a;
}

.input {
  border: none;
  font-size: 14px;
  line-height: 24px;
}

.input:focus-visible {
  outline: none;
}

.children-container {
  margin-top: 33px;
}

.children-list {
  display: flex;
  align-items: center;
  gap: 18px;
  margin-bottom: 10px;
}

.children-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 11px;
  font-size: 16px;
  line-height: 24px;
  font-weight: 500;
}

.add-button {
  color: #01a7fd;
  font-size: 16px;
  line-height: 24px;
  cursor: pointer;
  border: 2px solid #01a7fd;
  border-radius: 30px;
  padding: 10px 20px;
  background-color: transparent;
  display: flex;
  gap: 4px;
}

.remove-button {
  background-color: transparent;
  border: none;
  cursor: pointer;
  color: #01a7fd;
  font-size: 14px;
  line-height: 24px;
  width: 60px;
  height: 24px;
}

.save-button {
  background-color: #01a7fd;
  color: #fff;
  border: none;
  border-radius: 30px;
  padding: 10px 20px;
  font-size: 14px;
  line-height: 24px;
  cursor: pointer;
  margin-top: 30px;
}

.save-button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.add-button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
</style>

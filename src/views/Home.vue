<template>
  <div class="home-container">
    <header class="header">
      <h1>我的日记</h1>
      <button class="cute-button" @click="showNewDiary = true">写新日记</button>
    </header>

    <div class="diary-list">
      <div v-for="(diary, index) in diaries" :key="index" class="diary-card">
        <div class="diary-header">
          <span class="diary-date">{{ diary.date }}</span>
          <div class="diary-actions">
            <button class="edit-btn" @click="editDiary(index)">编辑</button>
            <button class="delete-btn" @click="deleteDiary(index)">删除</button>
          </div>
        </div>
        <p class="diary-content">{{ diary.content }}</p>
      </div>
    </div>

    <!-- 新建/编辑日记弹窗 -->
    <div v-if="showNewDiary" class="modal">
      <div class="modal-content">
        <h2>{{ editingIndex === -1 ? '写新日记' : '编辑日记' }}</h2>
        <textarea
          v-model="currentDiary.content"
          class="diary-textarea"
          placeholder="写下此刻的心情..."
          autocomplete="off"
        ></textarea>
        <div class="modal-buttons">
          <button class="cute-button" @click="saveDiary">保存</button>
          <button class="cancel-button" @click="closeModal">取消</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      diaries: [],
      showNewDiary: false,
      editingIndex: -1,
      currentDiary: {
        content: '',
        date: ''
      }
    }
  },
  created() {
    // 从本地存储加载日记
    const savedDiaries = localStorage.getItem('diaries')
    if (savedDiaries) {
      this.diaries = JSON.parse(savedDiaries)
    }
  },
  methods: {
    saveDiary() {
      if (!this.currentDiary.content.trim()) {
        alert('请输入日记内容')
        return
      }

      const diary = {
        content: this.currentDiary.content,
        date: new Date().toLocaleString()
      }

      if (this.editingIndex === -1) {
        this.diaries.unshift(diary)
      } else {
        this.diaries[this.editingIndex] = diary
      }

      localStorage.setItem('diaries', JSON.stringify(this.diaries))
      this.closeModal()
    },
    editDiary(index) {
      this.editingIndex = index
      this.currentDiary = { ...this.diaries[index] }
      this.showNewDiary = true
    },
    deleteDiary(index) {
      if (confirm('确定要删除这篇日记吗？')) {
        this.diaries.splice(index, 1)
        localStorage.setItem('diaries', JSON.stringify(this.diaries))
      }
    },
    closeModal() {
      this.showNewDiary = false
      this.editingIndex = -1
      this.currentDiary = {
        content: '',
        date: ''
      }
    }
  }
}
</script>

<style scoped>
.home-container {
  min-height: 100vh;
  padding: 20px;
  background-color: var(--background-color);
  padding-bottom: calc(20px + var(--safe-area-inset-bottom));
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  padding: 0 10px;
}

.header h1 {
  color: var(--primary-color);
  font-size: 1.5rem;
  font-weight: 600;
}

.diary-list {
  display: flex;
  flex-direction: column;
  gap: 15px;
  padding: 0 10px;
}

.diary-card {
  background: white;
  border-radius: 15px;
  padding: 15px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.diary-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}

.diary-date {
  color: #666;
  font-size: 0.85rem;
}

.diary-actions {
  display: flex;
  gap: 8px;
}

.edit-btn, .delete-btn {
  padding: 6px 12px;
  border: none;
  border-radius: 15px;
  font-size: 0.85rem;
  color: white;
  -webkit-tap-highlight-color: transparent;
}

.edit-btn {
  background-color: var(--primary-color);
}

.delete-btn {
  background-color: #ff6b6b;
}

.diary-content {
  line-height: 1.6;
  color: var(--text-color);
  font-size: 0.95rem;
  word-break: break-all;
}

.modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  padding: 20px;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 20px;
  width: 100%;
  max-width: 500px;
  max-height: 90vh;
  overflow-y: auto;
}

.modal-content h2 {
  color: var(--primary-color);
  margin-bottom: 15px;
  text-align: center;
  font-size: 1.3rem;
}

.diary-textarea {
  width: 100%;
  height: 200px;
  padding: 15px;
  border: 2px solid var(--primary-color);
  border-radius: 15px;
  resize: none;
  margin-bottom: 15px;
  font-family: inherit;
  font-size: 1rem;
  line-height: 1.5;
  -webkit-appearance: none;
  appearance: none;
}

.modal-buttons {
  display: flex;
  justify-content: center;
  gap: 15px;
}

.cancel-button {
  background-color: #ccc;
  color: white;
  border: none;
  border-radius: 25px;
  padding: 12px 24px;
  font-size: 1rem;
  -webkit-tap-highlight-color: transparent;
}

.cancel-button:active {
  background-color: #999;
}

@media screen and (max-height: 600px) {
  .modal-content {
    padding: 15px;
  }
  
  .diary-textarea {
    height: 150px;
  }
  
  .modal-buttons {
    gap: 10px;
  }
  
  .cute-button, .cancel-button {
    padding: 10px 20px;
  }
}
</style> 
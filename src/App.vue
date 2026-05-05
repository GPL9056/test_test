<template>
  <div class="container">
    <h1>Todo List</h1>

    <div class="input-area">
      <input
        v-model="newTodo"
        @keyup.enter="addTodo"
        placeholder="輸入待辦事項"
      />
      <button @click="addTodo">新增</button>
    </div>

    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <template v-if="editIndex === index">
          <input v-model="editText" />
          <button @click="saveEdit(index)">儲存</button>
        </template>

        <template v-else>
          <span>{{ todo }}</span>

          <div class="btn-group">
            <button @click="startEdit(index)">修改</button>
            <button class="delete" @click="deleteTodo(index)">
              刪除
            </button>
          </div>
        </template>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: [],
      editIndex: null,
      editText: ''
    }
  },

  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push(this.newTodo)
        this.newTodo = ''
      }
    },

    deleteTodo(index) {
      this.todos.splice(index, 1)
    },

    startEdit(index) {
      this.editIndex = index
      this.editText = this.todos[index]
    },

    saveEdit(index) {
      this.todos[index] = this.editText
      this.editIndex = null
      this.editText = ''
    }
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
  background: #f5f7fa;
  font-family: Arial, sans-serif;
}

.container {
  width: 500px;
  margin: 50px auto;
  background: white;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 8px 20px rgba(0,0,0,0.1);
}

h1 {
  text-align: center;
  color: #333;
}

.input-area {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.input-area input {
  flex: 1;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 8px;
}

button {
  padding: 10px 16px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  background: #42b883;
  color: white;
}

button:hover {
  opacity: 0.9;
}

.delete {
  background: #ff4d4f;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  background: #fafafa;
  margin-bottom: 12px;
  padding: 15px;
  border-radius: 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.btn-group {
  display: flex;
  gap: 8px;
}
</style>
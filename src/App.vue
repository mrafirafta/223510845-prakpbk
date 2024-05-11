<template>
  <div id="app">
    <div class="container">
      <h1>Mobil Impian Tahun Depan</h1>
      <form @submit.prevent="addOrUpdateTodo">
        <input type="text" v-model="newTodo.text" placeholder="Masukan Impian anda dong" />
        <button type="submit" class="submit">{{ editingIndex !== null ? 'Update' : 'Tambah' }}</button>
      </form>
      <table>
        <thead>
          <tr>
            <th>Mobil Kamu</th>
            <th>Tukar lagi?</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(todo, index) in todos" :key="index">
            <td>{{ todo.text }}</td>
            <td class="button-cell">
              <button class="edit-btn" @click="editTodo(index)">Edit</button>
              <button class="delete-btn" @click="deleteTodo(index)">Hapus</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      newTodo: { text: '', editing: false },
      todos: [],
      editingIndex: null
    };
  },
  methods: {
    addOrUpdateTodo() {
      if (this.newTodo.text.trim() !== '') {
        if (this.editingIndex !== null) {
          this.todos[this.editingIndex].text = this.newTodo.text;
          this.todos[this.editingIndex].editing = false;
          this.editingIndex = null;
        } else {
          this.todos.push({ text: this.newTodo.text, editing: false });
        }
        this.newTodo.text = '';
      }
    },
    editTodo(index) {
      this.newTodo.text = this.todos[index].text;
      this.newTodo.editing = true;
      this.editingIndex = index;
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    }
  }
};
</script>

<style scoped>

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #f44336;
}

.container {
  max-width: 450px;
  width: 100%;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  background-color: #fff;
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}

form {
  display: flex;
  margin-bottom: 20px;
}

input {
  flex: 1;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-left: 5px;
}

button.submit {
  background-color: #1e90ff;
  color: #fff;
}

button.edit-btn {
  background-color: #1e90ff;
  color: #fff;
}

button.delete-btn {
  background-color: #ff4500;
  color: #fff;
}

button:hover {
  filter: brightness(110%);
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}

.button-cell {
  display: flex;
  justify-content: right;
}

.button-group button {
  margin-left: 5px;
}

button.delete-btn {
  background-color: #f44336;
}

button.delete-btn:hover {
  background-color: #da190b;
}
</style>

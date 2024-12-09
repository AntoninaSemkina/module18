<template>
  <div className="container">
    <textarea
      v-model="itemName"
      class="text-input"
      placeholder="add your new task to ToDoList..."
    ></textarea>
    <button className="add-btn" @click="addItem">Add</button>
    <div className="tasks" v-for="ListItem in todoList" :key="ListItem.id">
      <TodoItem
        :id="ListItem.id"
        :name="ListItem.name"
        :done="ListItem.done"
        :time="ListItem.time"
        :remove="removeItem"
        :favorite="favoriteItem"
      />
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import TodoItem from "./TodoItem.vue";

let itemName = ref();
let counter = 6;

export default {
  name: "TodoList",
  components: { TodoItem },
  data() {
    return {
      todoList: [
        { id: 1, name: "name 1", done: false, time: "2024-12-09 10:15" },
        { id: 2, name: "name 2", done: false, time: "2024-12-09 10:15" },
        { id: 3, name: "name 3", done: false, time: "2024-12-09 10:15" },
        { id: 4, name: "name 4", done: false, time: "2024-12-09 10:15" },
        { id: 5, name: "name 5", done: false, time: "2024-12-09 10:15" },
      ],
      itemName,
    };
  },
  methods: {
    addItem() {
      if (this.itemName.trim() !== "") {
        const currentTime = new Date()
          .toISOString()
          .slice(0, 16)
          .replace("T", " ");
        this.todoList.push({
          id: counter,
          name: this.itemName,
          done: false,
          time: currentTime,
        });
        this.itemName = "";
        counter++;
      }
    },
    removeItem(id) {
      this.todoList = this.todoList.filter((item) => item.id !== id);
    },
    favoriteItem(id) {
      this.todoList = this.todoList.map((item) => {
        if (item.id === id) {
          return { ...item, done: !item.done }; // Изменяем состояние `done`
        }
        return item;
      });
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  margin: auto;
  width: 80%;
}
.tasks {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.add-btn {
  width: 100px;
  height: 40px;
  background: darkgreen;
  color: aliceblue;
  border: 1px solid darkgreen;
  border-radius: 5px;
  cursor: pointer;
  transition: background 0.3s;
  margin: 20px;
}
.text-input {
  width: 100%;
  max-height: 500px;
  padding: 10px;
  border: 1px solid darkgreen;
  border-radius: 5px;
  box-sizing: border-box;
  resize: none;
  overflow-y: auto;
  font-family: inherit;
  font-size: 16px;
  line-height: 1.5;
  white-space: pre-wrap;
  color: darkgreen;
}
</style>

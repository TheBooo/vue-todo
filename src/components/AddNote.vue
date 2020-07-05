<template>
  <div class="container">
    <button class="btn btn-add" @click="handleShowForm">Add note +</button>

    <!-- overlay and form -->
    <div v-if="showForm === true" class="overlay">
      <form v-on:submit.prevent="submitNote" class="overlay-content">
        <input type="text" v-model="title" placeholder="Title" required />
        <input
          v-on:keydown.enter.prevent="addTodo"
          type="text"
          v-model="todo"
          placeholder="Task"
        />
        <button type="button" @click="addTodo" class="btn btn-todo">
          Add task
        </button>
        <div v-if="this.showNotification === true" class="notification">
          {{ this.notification }}
        </div>
        <div class="form-btns-container">
          <button type="submit" class="btn btn-todo">
            Save
          </button>
          <button
            type="button"
            @click="handleShowForm"
            class="btn btn-todo btn-cancel"
          >
            Cancel
          </button>
        </div>

        <!-- preview -->
        <div class="preview">
          <h3 class="preview-title">{{ this.title }}</h3>
          tasks:
          <div v-for="todo in todos" :key="todo.id" class="preview-task">
            {{ todo.title }}
          </div>
        </div>
        <!-- end of preview -->
      </form>
    </div>
    <!-- end of overlay -->
  </div>
</template>

<script>
import { v4 as uuid } from "uuid";
import { mapActions } from "vuex";

export default {
  name: "AddNote",
  data() {
    return {
      showForm: false,
      title: "",
      todo: "",
      notification: "",
      showNotification: false,
      todos: [],
    };
  },
  methods: {
    ...mapActions(["addNote"]),
    handleShowForm() {
      this.showForm = !this.showForm;
      this.title = "";
      this.todos = [];
    },
    //add single todo
    addTodo() {
      // task input empty or whitespaces check
      if (this.todo.trim()) {
        this.todos.push({
          id: uuid(),
          title: this.todo,
          completed: false,
        });

        this.todo = "";
      } else {
        this.notification = "Task can't be empty line";
        this.showNotification = true;
      }
    },
    //save note
    submitNote() {
      //check for whitespaces name
      if (this.title.trim()) {
        const newNote = {
          id: uuid(),
          title: this.title,
          todos: this.todos,
        };
        this.addNote(newNote);
        this.handleShowForm();
      } else {
        this.notification = "Title can't be whitespace";
        this.showNotification = true;
      }
    },
  },
};
</script>

<style scoped>
.btn-add {
  padding: 0.5rem;
  margin-top: 1rem;
  background-color: lightblue;
  border: none;
  font-family: var(--main-cursive-font);
  font-size: 1.4rem;
  font-weight: bold;
  color: var(--main-grey);
}
.btn-add:hover {
  background-color: var(--main-green);
}
.btn-todo {
  font-size: 1.2rem;
  margin: 0.5rem;
  padding: 0.2rem;
  background-color: lightblue;
}
.btn-todo:hover {
  background-color: white;
}
</style>

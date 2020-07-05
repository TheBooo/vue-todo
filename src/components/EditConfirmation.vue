<template>
  <!-- -->
  <div class="overlay">
    <!-- exit confirmation -->
    <div class="overlay-content" v-if="action === 'exit'">
      Are you sure you want to
      {{ action }}?
      <div>
        <router-link to="/">
          <button class="btn btn-control">Confirm</button>
        </router-link>
        <button class="btn btn-control" @click="$emit('cancel')">Cancel</button>
      </div>
    </div>

    <!-- saving confirmation -->
    <div class="overlay-content" v-if="action === 'save changes'">
      Are you sure you want to
      {{ action }}?
      <div>
        <button class="btn btn-control" @click="$emit('save')">Confirm</button>
        <button class="btn btn-control" @click="$emit('cancel')">Cancel</button>
      </div>
    </div>

    <!-- delete note confirmation -->
    <div class="overlay-content" v-if="action === 'delete note'">
      Are you sure you want to
      {{ action }}?
      <div>
        <button class="btn btn-control" @click="$emit('delete')">
          Confirm
        </button>
        <button class="btn btn-control" @click="$emit('cancel')">Cancel</button>
      </div>
    </div>

    <!-- Edit task -->
    <form
      v-on:submit.prevent="$emit('edit-todo', todoTitle)"
      class="overlay-content"
      v-if="action === 'edit todo'"
    >
      <input type="text" v-model="todoTitle" />
      <div>
        <button
          type="button"
          class="btn btn-control"
          @click="$emit('edit-todo', todoTitle)"
        >
          Confirm
        </button>
        <button type="button" class="btn btn-control" @click="$emit('cancel')">
          Cancel
        </button>
      </div>
    </form>

    <!-- Add new task -->
    <form
      v-on:submit.prevent="$emit('add-todo', newTodo)"
      class="overlay-content"
      v-if="action === 'add todo'"
    >
      Add task
      <input type="text" v-model="newTodo" />
      <div>
        <button
          type="button"
          class="btn btn-control"
          @click="$emit('add-todo', newTodo)"
        >
          Add
        </button>
        <button type="button" class="btn btn-control" @click="$emit('cancel')">
          Cancel
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "EditConfirmation",
  props: ["action", "todo"],
  data() {
    return {
      todoTitle: "",
      newTodo: "",
    };
  },
  created() {
    this.todoTitle = this.todo.title;
  },
};
</script>

<style scoped>
.btn-control {
  font-size: 1.2rem;
  margin: 0.5rem;
  padding: 0.2rem;
  background-color: lightblue;
}
</style>

<template>
  <main class="notes-container">
    <!-- displaying notes -->
    <div v-for="note in allNotes" :key="note.id" class="note-container">
      <!-- edit btn-->
      <router-link :to="{ name: 'Edit', params: { id: note.id, note } }">
        <button class="btn btn-note btn-edit"><PlaylistEdit /></button>
      </router-link>
      <!-- title -->
      <h2 class="note-title">{{ note.title }}</h2>
      <!-- delete btn-->
      <button @click="initiateDelete(note)" class="btn btn-note btn-delete">
        <Delete />
      </button>

      <!-- display todos -->
      <div
        v-for="todo in note.todos.slice(0, 4)"
        :key="todo.id"
        v-bind:class="{ 'is-completed': todo.completed }"
      >
        {{ todo.title }}
        <Check v-if="todo.completed === true" />
      </div>
      <div v-if="note.todos.length > 4">...</div>
    </div>

    <!-- confirm delete -->
    <div class="overlay" v-if="this.deleteOverlay === true">
      <div class="overlay-content">
        Are you sure you want to delete {{ this.delNote.title }} note?
        <div>
          <button @click="confirmDelete" class="btn btn-confirm">
            Confirm
          </button>
          <button @click="toggleOverlay" class="btn btn-cancel btn-confirm">
            Cancel
          </button>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import { mapGetters, mapActions } from "vuex";

import PlaylistEdit from "vue-material-design-icons/PlaylistEdit";
import Delete from "vue-material-design-icons/Delete";
import Check from "vue-material-design-icons/Check";

export default {
  name: "Notes",
  computed: mapGetters(["allNotes"]), // get all notes
  components: {
    PlaylistEdit,
    Delete,
    Check,
  },
  data() {
    return {
      deleteOverlay: false,
      delNote: "",
    };
  },
  methods: {
    ...mapActions(["getNotes", "deleteNote"]),
    toggleOverlay() {
      this.deleteOverlay = !this.deleteOverlay;
    },
    //delete confirmation overlay
    initiateDelete(note) {
      this.delNote = note;
      this.toggleOverlay();
    },
    //delete note
    confirmDelete() {
      this.deleteNote(this.delNote.id);
      this.toggleOverlay();
    },
  },
  created() {
    this.getNotes(); // refresh all notes
  },
};
</script>

<style scoped>
.btn-note {
  position: absolute;
  top: 10px;
  background: none;
  border: none;
  color: var(--main-grey);
}
.btn-note:hover {
  color: var(--main-brown);
  transform: scale(1.1);
}
.btn-edit {
  left: 10px;
}
.btn-delete {
  right: 10px;
}
.btn-confirm {
  font-size: 1.2rem;
  margin: 0.5rem;
  padding: 0.2rem;
  background-color: lightblue;
}
</style>

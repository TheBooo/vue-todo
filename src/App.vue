<template>
  <div id="app">
    <div id="nav">
      <Header />
    </div>
    <router-view />
  </div>
</template>

<script>
import Header from "./components/layout/Header";
export default {
  components: {
    Header,
  },
};
</script>

<style>
@import url(https://fonts.googleapis.com/css?family=Waiting+for+the+Sunrise);

:root {
  --main-green: #41b883;
  --main-grey: #34495e;
  --main-brown: #5f3325;
  --main-cursive-font: "Waiting for the Sunrise", cursive;
  --main-border-radius: 0.2rem;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: var(--main-cursive-font);
  line-height: 1.4;
  letter-spacing: 0.1rem;
}
a {
  text-decoration: none;
}
input {
  padding: 1rem;
  margin: 0.2rem;
  font-size: 1.4rem;
  width: 60%;
  border-radius: var(--main-border-radius);
  border: none;
}

.btn {
  transition: all 0.3s ease-in;
  cursor: pointer;
  letter-spacing: 0.1rem;
  border-radius: var(--main-border-radius);
  border: none;
}
.btn-cancel:hover {
  background-color: var(--main-grey) !important;
  color: var(--main-green) !important;
}

.container {
  max-width: 1160px;
  margin: auto;
  display: flex;
  justify-content: center;
  align-items: center;
}
.note-container {
  /* имитация бумажной заметки / paper note imitation */
  background: linear-gradient(rgba(0, 0, 0, 0.1) 1px, transparent 1px),
    rgba(65, 184, 131, 0.4);
  background-size: 100% 2.5rem;
  background-position: 0 2.5rem;
  background-origin: content-box;
  /* - */
  text-align: center;
  font-size: 1.4rem;
  line-height: 1.7;
  padding: 1rem;
  margin: 1rem;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.3);
  border-radius: var(--main-border-radius);
  font-family: "Waiting for the Sunrise", cursive;
  position: relative;
  color: var(--main-grey);
}
.notes-container {
  margin: auto;
  max-width: 1160px;
  overflow: auto;
  padding: 1rem 2rem;
  display: flex;
  font-weight: bold;
  justify-content: center;
  flex-direction: column;
}
.is-completed {
  text-decoration: line-through;
}

/* -- overlay -- */
.overlay {
  position: fixed;
  top: 0;
  right: 0;
  width: 100%;
  height: 100%;
  /*background: rgba(0, 61, 124, 0.9);*/
  background: rgba(0, 43, 54, 0.85);
  z-index: 20;
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.overlay-content {
  z-index: 21;
  background-color: #41b883;
  padding: 1rem;
  width: 90%;
  max-width: 1024px;
  font-size: 1.2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  border-radius: 0.5rem;
  font-family: Arial, Helvetica, sans-serif;
}
</style>

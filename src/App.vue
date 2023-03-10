<script setup lang="ts">
import { ref } from 'vue';
const messageList = ref([])

window.addEventListener('message', (event: MessageEvent) => {
  console.log('iframe消息', event.data);
  messageList.value.push(event.data)


}, false)

const sendMessage = () => {
  window.parent.postMessage(new Date().getTime(), 'http://localhost:8000/cms/decorate')
} 
</script>

<template>
  <div class="container">
    <div class="m-wrapper">
      <button @click="sendMessage">
        发送
      </button>
      <ul>
        <li v-for="(message, index) in messageList" :key="index">
          {{ message.value }}</li>
      </ul>

    </div>

  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  display: flex;
  align-items: center;
  justify-content: center;

  background: #f7f7f7;
}

.m-wrapper {
  background: #fff;
  width: 375px;
  height: 750px;
  border: 1px solid #eee;
  overflow: auto;
}

header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>

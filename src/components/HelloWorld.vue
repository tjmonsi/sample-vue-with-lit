<script setup>
import { ref } from 'vue';
import '@tjmonsi/small-snackbar/small-snackbar.js';

const afterHidden = ref('');
const snackbar = ref(null);

function onSubmit (event) {
  event.preventDefault();
  const { target: form } = event;
  afterHidden.value = '';
  snackbar.value.open(form.text.value || 'No text provided.');
}

function onHide (event) {
  const { detail } = event;
  const { text } = detail;
  afterHidden.value = text;
}
</script>

<template>
  <div class="greetings">
    <h1 class="green"></h1>
    
    <form  @submit="onSubmit">
      <label for="text">Text: </label>
      <input id="text" type="text" name="text">
      <button type="submit">Submit</button>
    </form>

    {{ afterHidden }}

    <small-snackbar ref="snackbar" @hide="onHide"></small-snackbar>

    
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>

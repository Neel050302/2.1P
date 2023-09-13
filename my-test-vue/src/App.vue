<template>
  <!-- 1. Template Syntax -->
  <h2>1. Template Syntax</h2>
  <p>{{ message }}</p>
  <div v-html="rawHtml"></div>
  <div v-bind:id="dynamicId"></div>
  <p>{{ counter + 10 }}</p>

  <!-- 2. Methods -->
  <h2>2. Methods</h2>
  <button @click="incrementCounter">Increment</button>

  <!-- 5. Class and Style Bindings -->
  <h2>5. Class and Style Bindings</h2>
  <div :class="{ active: isActive }">Class Binding</div>
  <div :style="dynamicStyles">Style Binding</div>

  <!-- 6. List Rendering -->
  <h2>6. List Rendering</h2>
  <div v-for="(value, key) in user" :key="key">{{ key }}: {{ value }}</div>
  <div v-for="n in 3" :key="n">{{ n }}</div>
  <template v-for="item in visibleItems" :key="item.id">
    <div>{{ item.text }}</div>
  </template>

  <!-- 7. Event Handling -->
  <h2>7. Event Handling</h2>
  <button @click="sayHello">Say Hello</button>

  <!-- 8. Form Input Bindings -->
  <h2>8. Form Input Bindings</h2>
  <input v-model="message" />
  <input type="checkbox" v-model="isChecked" />
  <input type="radio" v-model="picked" value="One" />
  <input type="radio" v-model="picked" value="Two" />
  <select v-model="selectedOption">
    <option>A</option>
    <option>B</option>
  </select>
  <textarea v-model.trim="feedback"></textarea>

  <!-- ... previous sections ... -->

  <!-- 9. Watchers -->
  <h2>9. Watchers</h2>
  <p>Message for watcher: {{ messageForWatcher }}</p>

  <!-- 10. Components -->
  <h2>10. Components</h2>
  <child-component 
    :some-prop="message" 
    @child-event="handleChildEvent">
    <template #slotContent>
      This is content passed through a slot!
    </template>
  </child-component>

  <!-- 11. Router -->
  <h2>11. Router</h2>
  <router-link to="/">Home</router-link>
  <router-view></router-view>
</template>

<!-- ... rest of the script and styles ... -->

<script setup>
import { ref, computed } from 'vue';
import {  watch } from 'vue';


// 1. Template Syntax
const message = ref("Hello Vue 3!");
const rawHtml = ref("<strong>Strong Text</strong>");
const dynamicId = ref("dynamicID");
const counter = ref(5);

// 2. Methods
const incrementCounter = () => {
  counter.value++;
};

// 3. Reactivity Fundamentals
const isActive = ref(true);
const dynamicStyles = ref({
  color: 'red',
  fontSize: '20px'
});
const user = ref({
  name: 'John Doe',
  age: 25
});
const items = ref([
  { id: 1, text: 'Item 1', visible: true },
  { id: 2, text: 'Item 2', visible: false },
  { id: 3, text: 'Item 3', visible: true }
]);

// 4. Computed Properties
const visibleItems = computed(() => items.value.filter(item => item.visible));

// 7. Event Handling
const sayHello = () => {
  alert('Hello!');
};

// 8. Form Input Bindings
const isChecked = ref(false);
const picked = ref('One');
const selectedOption = ref('A');
const feedback = ref('');

// 9. Watchers
const messageForWatcher = ref("Change me and watch the console!");
watch(messageForWatcher, (newValue, oldValue) => {
  console.log(`messageForWatcher changed from ${oldValue} to ${newValue}`);
});

// 10. Components
// For this example, ensure you have a child-component defined or imported 
// that supports the prop, slot, and event as described above.
// 10. Components (Placeholder - requires component setup)
const handleChildEvent = (payload) => {
  console.log('Received event from child:', payload);
};

</script>

<style scoped>
body {
  font-family: 'Arial', sans-serif;
  color: #333;
  background-color: #f4f4f4;
  line-height: 1.6;
}

button {
  padding: 10px 15px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #2980b9;
}

div {
  padding: 10px;
  margin: 10px 0;
}

div.active {
  background-color: #a3d2f0;
}

input[type="text"],
input[type="radio"],
select,
textarea {
  padding: 10px;
  width: 100%;
  margin-bottom: 10px;
  border: 1px solid #d9d9d9;
  border-radius: 3px;
}

textarea {
  resize: vertical;
  min-height: 100px;
}

router-link {
  display: inline-block;
  margin: 10px;
  padding: 5px 10px;
  background-color: #2c8ad9;
  color: #fff;
  text-decoration: none;
  border-radius: 3px;
}

router-link:hover {
  background-color: #2677a5;
}
</style>

<template>
  <div class="json-lab">
    <h1>🗄️ JSON Data & Vue Directives Lab</h1>

    <section class="lab-section">
      <h2>📚 Working with JSON Arrays</h2>
      <p>Our <code>authors.json</code> contains an array of author objects.</p>

      <h3>Iterating through Arrays</h3>
      <ul>
        <li v-for="author in authors" :key="author.id" class="card">
          {{ author.name }} ({{ author.birthYear }})
        </li>
      </ul>

      <h3>Filtering Arrays</h3>
      <p>Authors born after 1850:</p>
      <ul>
        <li v-for="author in modernAuthors" :key="author.id" class="card">
          {{ author.name }} ({{ author.birthYear }})
        </li>
      </ul>

      <h3>Mapping Arrays</h3>
      <p>Famous works:</p>
      <ul>
        <li v-for="work in allFamousWorks" :key="work" class="card">
          {{ work }}
        </li>
      </ul>

      <h3>Finding in Arrays</h3>
      <p>
        Finding by property: <strong>{{ orwell?.name }}</strong>
      </p>

      <h3>Nested Arrays/Objects</h3>
      <p>
        <strong>{{ austen?.name }}</strong
        >'s works:
      </p>
      <ul>
        <li v-for="work in austen?.famousWorks || []" :key="work.title" class="card">
          {{ work.title }} ({{ work.year }})
        </li>
      </ul>
    </section>

    <section class="lab-section">
      <h2>🏢 Working with JSON Objects</h2>
      <p>Our <code>bookstores.json</code> is a JSON object.</p>

      <h3>Accessing Properties</h3>
      <p>
        Company: <strong>{{ bookstores.name }}</strong>
      </p>
      <p>
        Total Stores: <strong>{{ bookstores.totalStores }}</strong>
      </p>

      <h3>Iterating Object Properties</h3>
      <p>Store Types:</p>
      <ul>
        <li v-for="(count, type) in bookstores.storeTypes" :key="type" class="card">
          {{ type }}: {{ count }} stores
        </li>
      </ul>

      <h3>Nested Objects</h3>
      <p>Opening Hours:</p>
      <ul>
        <li v-for="(time, day) in bookstores.openingHours" :key="day" class="card">
          {{ day }}: {{ time.open }} - {{ time.close }}
        </li>
      </ul>

      <h3>Working with Arrays in Objects</h3>
      <p>
        We operate in: <strong>{{ bookstores.countries.join(', ') }}</strong>
      </p>
      <p>
        Our #1 seller: <strong>{{ bookstores.topSellers[0] }}</strong>
      </p>
    </section>

    <section class="lab-section">
      <h2>v-if & v-else</h2>
      <p>Toggle visibility based on a condition.</p>
      <button @click="showMessage = !showMessage">Toggle Message</button>
      <p v-if="showMessage" class="message success">✨ You're a Vue superstar! ✨</p>
      <p>Click the button to see a message.</p>
    </section>

    <section class="lab-section">
      <h2>Attribute, Class and Style Binding with <code>v-bind</code></h2>
      <p>Highlighting Specific Authors:</p>
    </section>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import authors from '../assets/json/authors.json'
import bookstores from '../assets/json/bookstores.json'

const showMessage = ref(false)

const modernAuthors = computed(() => authors.filter((author) => author.birthYear > 1850))

const allFamousWorks = computed(() =>
  authors.flatMap((author) => author.famousWorks.map((work) => work.title)),
)

const orwell = computed(() => authors.find((author) => author.name === 'George Orwell'))

const austen = computed(() => authors.find((author) => author.name === 'Jane Austen'))
</script>

<style scoped>
.json-lab {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  max-width: 80vw;
  margin: 0 auto;
  padding: 20px;
  background-color: #f4f4f4;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  opacity: 1 !important;
  filter: none !important;
  color: #000 !important;
}

h1,
h2,
h3,
p,
ul,
li {
  opacity: 1 !important;
  filter: none !important;
  color: #000 !important;
}

h1 {
  text-align: center;
}

.lab-section {
  background-color: white;
  padding: 20px;
  margin-bottom: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.message {
  padding: 10px;
  border-radius: 5px;
  margin-top: 10px;
}

.success {
  background-color: #e7faf3;
  color: #42b883;
  border: 1px solid #42b883;
}

code {
  background-color: #e0e0e0;
  padding: 2px 5px;
  border-radius: 4px;
  font-family: 'Courier New', Courier, monospace;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.card {
  background-color: #f0f0f0;
  padding: 10px 16px;
  margin: 6px 0;
  border-radius: 6px;
  font-size: 16px;
  font-weight: 500;
  opacity: 1 !important;
  filter: none !important;
  color: #000 !important;
}
</style>

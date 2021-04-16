<template>
  <section class="container">
    <h1>TODO</h1>
    <p><input v-model="content" type="text" name="content"></p>
    <div>
      <button @click="insert">
        save
      </button>
      <button>find</button>
    </div>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <span>{{ todo.content }}</span>
        <span>{{ todo.created }}</span>
        <span>×</span>
      </li>
    </ul>
  </section>
</template>

<script>
import { mapState } from 'vuex'
export default {
  // eslint-disable-next-line object-shorthand
  data: function () {
    return {
      content: ''
    }
  },
  computed: {
    ...mapState(['todos'])
  },
  methods: {
    // eslint-disable-next-line object-shorthand
    insert: function () {
      this.$store.commit('insert', { content: this.content })
      this.content = ''
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>

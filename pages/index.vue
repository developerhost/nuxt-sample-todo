<template>
  <section class="container">
    <h1>TODO</h1>
    <p><input v-model="content" type="text" name="content" @focus="set_flg"></p>
    <div>
      <button @click="insert">
        save
      </button>

      <button @click="find">
        find
      </button>
    </div>
    <ul>
      <li v-for="(todo, index) in display_todos" :key="index">
        <span>{{ todo.content }}</span>
        <span>{{ todo.created }}</span>
        <span @click="remove(todo)">×</span>
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
      content: '',
      fing_flg: false
    }
  },
  computed: {
    ...mapState(['todos']),
    // eslint-disable-next-line object-shorthand
    // eslint-disable-next-line vue/return-in-computed-property
    display_todos () {
      if (this.fing_flg) {
        const arr = []
        const data = this.todos
        data.forEach((element) => {
          // eslint-disable-next-line eqeqeq
          if (element.content.toLowerCase() == this.content.toLowerCase()) {
            arr.push(element)
          }
        })
        return arr
      } else {
        return this.todos
      }
    }
  },
  methods: {
    // eslint-disable-next-line object-shorthand
    insert: function () {
      this.$store.commit('insert', { content: this.content })
      this.content = ''
    },
    // eslint-disable-next-line object-shorthand
    find: function () {
      this.fing_flg = true
    },
    // eslint-disable-next-line object-shorthand
    set_flg: function () {
      if (this.find_flg) {
        this.find_flg = false
        this.content = ''
      }
    },
    // eslint-disable-next-line object-shorthand
    remove: function (todo) {
      this.$store.commit('remove', todo)
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

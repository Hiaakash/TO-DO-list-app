<template>
  <section class="greeting">
    <slot></slot>
  <h2 class="title">
    What's up, <input v-on:change="setUsername" type="text" v-bind:value="username" placeholder="Your Name?" />
  </h2>

</section>
</template>

<script>
export default {
  name: 'Greetings',
  data () {
    return {
      username: ''
    }
  },
  created () {
    console.log('LOCAL NAME', localStorage.getItem('username'))
    this.username = localStorage.getItem('username') || ''
    console.log('CREATED NAME VAL', this.username)
  },
  methods: {
    setUsername (e) {
      this.username = e.target.value
      localStorage.setItem('username', e.target.value)
    }
  },
  updated () {
    console.log('UPDATE NAME VAL', this.username)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.title > input{
  font-family: 'Noto Sans Mono', monospace;
}
</style>

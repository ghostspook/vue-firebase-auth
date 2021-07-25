<template>
  <div>
    <div v-if=error class="error">{{error.message}}</div>
    <form @submit.prevent="onSubmitClick">
      Login
      <div class="email">
        <input type="email" v-model="email" placeholder="e.g. me@domain.com">
      </div>
      <div class="password">
        <input type="password" v-model="password">
      </div>
      <button type="submit">Register</button>
    </form>
  </div>
</template>

<script>
  import firebase from 'firebase/app'
  import "firebase/auth"

  export default {
    data() {
      return {
        email: '',
        password: '',
        error: ''
      }
    },
    methods: {
      async onSubmitClick() {
        try {
          const user = firebase.auth().signInWithEmailAndPassword(this.email, this.password)
          console.log(user)
          this.$router.push({name: 'Restricted'})
        } catch(err) {
          console.log(err)
        }
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>
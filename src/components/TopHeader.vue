<template>
  <div>
    <span v-if="loggedIn">Logged In</span>
    <span v-else>Logged Out</span>
    <div v-if="loggedIn">
      <button @click="signOut">Log Out</button>
    </div>
  </div>
</template>

<script>
  import firebase from 'firebase/app'
  import "firebase/auth"

  export default {
    data() {
      return {
        loggedIn: false,
      }
    },
    created () {
      firebase.auth().onAuthStateChanged(user => {
        this.loggedIn = !!user
      })
    },
    methods: {
      async signOut() {
        try {
          const data = await firebase.auth().signOut()
          console.log(data)
          this.loggedIn = false
          this.$router.push({name: 'Login'})
        } catch (err) {
          console.log(err)
        }
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>
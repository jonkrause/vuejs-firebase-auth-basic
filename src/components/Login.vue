<template>
  <div class="login">
    <h3>Sign In</h3>
    <input type="text" placeholder="Email" v-model="email"><br>
    <input type="password" placeholder="Password" v-model="password"><br>
    <button @click="login">Log In</button>
    <p>Don't have an account? <router-link to="/signup">Sign Up</router-link></p>
  </div>
</template>

<script>
import firebase from 'firebase'
import axios from 'axios'
export default {
  name: 'login',
  data() {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    login: function() {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
        .then(
          user => {
            this.$store.dispatch('signIn', { email: this.email }).then(() => {
              // this.$store.dispatch('setUser')
              alert('Signed in as ' + this.email)
            })
            this.$router.replace('home')
          },
          err => {
            alert('[ERROR] ' + err.message)
          }
        )
      this.$router.replace('home')
<<<<<<< HEAD
=======
    },
    fbLogin: function() {
      var provider = new firebase.auth.FacebookAuthProvider()
      provider.addScope('user_location')
      provider.addScope('user_hometown')
      provider.addScope('user_birthday')
      firebase.auth().signInWithPopup(provider).then(result => {
        console.log("result: ", result.user.providerData[0])
          var token = result.credential.accessToken
          var user = result.user
          console.log('token: ' + token)
          console.log(user)

          this.$store.dispatch('getFbData', {token: token, user: user})
          this.$router.replace('home')
        })
        .catch(err => {
          console.log(err.code)
          console.log(err.message)
          console.log(err.email)
          console.log(err.credential)
        })
>>>>>>> parent of 6aa1015... working, but uses a setTimeout on home.vue - needs to be fixed
    }
  }
}
</script>

<style scoped>
.login {
  display: block;
}
</style>
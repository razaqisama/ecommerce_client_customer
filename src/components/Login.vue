<template>
    <div class="container mt-2" id="loginPage">
    <div class="row">
      <div class=".col-12 .col-md-8" style="min-width: 640px;">
        <div class="card mb-3">
          <div class="row no-gutters">
            <div class="col-md-5">
              <img src="../assets/login.jpg" class="card-img" alt="Image">
            </div>
            <div class="col-md-7">
              <div class="card-body">
                <h5 class="card-title">Login</h5>
                <form class="form-container" id="loginForm" @submit.prevent="login">
                    <div class="form-group">
                      <label for="emailLoginForm">Email address</label>
                      <input type="email" class="form-control" id="emailLogin" v-model="email" aria-describedby="emailHelp" required>
                      <p class="text-kecil"><small>We'll never share your email with anyone else.</small></p>
                    </div>
                    <div class="form-group">
                      <label for="passwordLoginForm">Password</label>
                      <input type="password" class="form-control" id="passwordLogin" v-model="password" required>
                    </div>
                    <button type="submit" class="btn btn-primary btn-block mt-2">Login</button>
                </form>
                <button @click="changeSign('register')" class="btn btn-primary btn-block mt-2" id="createNewAccount">Create a New Account?</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Swal from 'sweetalert2'
export default {
  name: 'Login',
  data () {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    changeSign (payload) {
      this.$store.commit('changeSign', payload)
    },
    login () {
      const payload = {
        email: this.email,
        password: this.password,
        role: 'customer'
      }
      this.$store.dispatch('login', payload)
        .then((response) => {
          Swal.fire({
            icon: 'success',
            title: 'Welcome!',
            text: 'Login Success'
          })
          this.$store.commit('changeSign', 'loggedIn')
          localStorage.setItem('access_token', response.data.access_token)
          this.$router.push('/')
        })
        .catch((error) => {
          console.log(error)
          Swal.fire({
            icon: 'error',
            title: 'Oppss..',
            text: 'Something went wrong'
          })
        })
    }
  }
}
</script>

<style>

</style>

<template>
  <form class="form-user center border border-secondary p-3 rounded" @submit.prevent="register">
    <div class="form-group">
      <label>Name</label>
      <input type="text" class="form-control" v-model="newUser.name" placeholder="Name" required>
    </div>
    <div class="form-group">
      <label>Email address</label>
      <input type="email" class="form-control" v-model="newUser.email" aria-describedby="emailHelp" placeholder="Email" required>
    </div>
    <div class="form-group">
      <label>Password</label>
      <input type="password" class="form-control" v-model="newUser.password" placeholder="Password" required>
    </div>
    <div class="form-group">
      <p>Already have an account? <b-link :to="{path: '/login'}" href="#" class="login-button" @click="login">Login Here</b-link></p>
    </div>
    <div class="col text-center">
      <button type="submit" class="btn btn-success center">Submit</button>
    </div>
  </form>
</template>

<script>
export default {
  name: 'RegisterForm',
  data () {
    return {
      newUser: {
        name: '',
        email: '',
        password: ''
      }
    }
  },
  methods: {
    login () {
      this.$router.push({ path: '/login' })
    },
    register () {
      this.$store.dispatch('register', this.newUser)
        .then(({ data }) => {
          console.log('masuk register')
          this.$swal({
            type: 'success',
            title: 'Register Success',
            showConfirmButton: false,
            timer: 2000
          })
          this.$router.push({
            path: '/login'
          })
        })
        .catch(err => {
          console.log(err)
          if (!err.response) {
            this.$swal({
              type: 'error',
              title: `Connection to Server Error`,
              showConfirmButton: true
            })
          } else {
            this.$swal({
              type: 'error',
              title: `${err.response.data.message}`,
              showConfirmButton: true
            })
          }
        })
    }
  }
}
</script>

<style scoped>
  .form-user {
    width: 40%;
    border-color: grey;
    border-width: 2px !important;
    -webkit-box-shadow: 10px 10px 11px -3px rgba(107,107,107,1);
    -moz-box-shadow: 10px 10px 11px -3px rgba(107,107,107,1);
    box-shadow: 10px 10px 11px -3px rgba(107,107,107,1);
  }
  .center {
    margin: 0px auto;
  }
</style>

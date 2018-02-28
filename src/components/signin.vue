<template>
  <form>
    <div class="form-group">
      <label for="email">Email</label>
      <input type="email" id="email" class="form-control" v-model="email"/>
    </div>
    <div class="form-group">
      <label for="password">Password</label>
      <input type="password" id="password" class="form-control" v-model="password"/>
    </div>
    <button type="submit" class="btn btn-primary" @click.prevent="onSignin">Sign in</button>
  </form>
</template>

<script>
  import axios from "axios"

  export default {
    data() {
      return {
        email: '',
        password: ''
      }
    },
    methods: {
      onSignin() {
        axios.post('http://192.168.10.10/api/user/signin',
          {email: this.email, password: this.password},
          {headers: {'X-Requested-With': 'XMLHttpRequest'}})
          .then(
            (response) => {
              const token = response.data.token;
              const base64Url = token.split('.')[1];
              const base64 = base64Url.replace('-', '+').replace('_', '/');
              console.log(JSON.parse(window.atob(base64)));
              localStorage.setItem('token', token);
            }
          ).catch(
            (error) => console.log(error)
        );
      }
    }
  }
</script>

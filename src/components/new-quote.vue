<template>
  <form @submit.prevent="onSubmitted">
    <div class="form-group">
      <label for="content">Content</label>
      <input type="text" id="content" class="form-control" v-model="quoteContent"/>
    </div>
    <button type="submit" class="btn btn-primary">Submit</button>
  </form>
</template>

<script>
  import axios from 'axios';

  export default {
    data () {
      return {
        quoteContent: '',
      }
    },
    methods: {
      onSubmitted () {
        const token = localStorage.getItem('token');
        //TODO: Change the url to the real back-end address
        axios.post('http://192.168.10.10/api/quote?token=' + token,
          {content: this.quoteContent})
          .then(
            (response) => {
              console.log(response);
              this.$router.push('/quotes');
            }
          ).catch(
          (error) => console.log(error)
        );
      }
    }
  }
</script>

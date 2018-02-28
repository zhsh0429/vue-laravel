<template>
  <form>
    <div @submit.prevent="onSubmitted" class="form-group">
      <label for="content">Content</label>
      <input type="text" id="content" class="form-control" v-model="quoteContent"/>
      <button type="submit" class="btn btn-primary">Submit</button>
    </div>
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
        //TODO: Change the url to the real back-end address
        axios.post('http://back-end/api/quote',
          {content: this.quoteContent})
          .then(
            (response) => console.log(response)
          ).catch(
          (error) => console.log(error)
        );
      }
    }
  }
</script>

<template>
  <div class="card text-center">
    <div class="card-header">
      {{ qt.content }}
    </div>
    <div class="card-block">
      <div v-if="editing">
        <input type="text" v-model="editValue"/>
        <a href="#" class="card-link" @click="onUpdate">Save</a>
        <a href="#" class="card-link" @click="onCancel">Cancel</a>
      </div>
      <div v-if="!editing">
        <a href="#" class="card-link" @click="onEdit">Edit</a>
        <a href="#" class="card-link" @click="onDelete">Delete</a>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    props: ['qt'],
    data() {
      return {
        editing: false,
        editValue: this.qt.content
      }
    },
    methods: {
      onEdit() {
        this.editing = true;
        this.editValue = this.qt.content
      },
      onCancel() {
        this.editing = false;
      },
      onDelete() {
        this.$emit('quoteDeleted', this.qt.id);
        const token = localStorage.getItem('token');
        //TODO: change the URL
        axios.delete('http://192.168.10.10/api/quote/' + this.qt.id + '?token=' + token)
          .then(
            response => console.log(response)
          )
          .catch(
            error => console.log(error)
          );
      },
      onUpdate() {
        this.editing = false;
        this.qt.content = this.editValue;
        const token = localStorage.getItem('token');
        //TODO: change the URL
        axios.put('http://192.168.10.10/api/quote/' + this.qt.id + '?token=' + token, {content: this.editValue})
          .then(
            response => console.log(response)
          )
          .catch(
            error => console.log(error)
          );
      }
    }
  }
</script>

<style scoped>
  a {
    cursor: pointer;
  }
</style>


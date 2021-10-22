<template>
  <div class="post">
    <h3>{{post.id}}</h3>
    <p> {{post.body}} </p>
    <i @click="onDelete(post.id)">Delete</i>
  </div>
</template>
<script>
export default {
    props : {
        post: {
            required: true
        }
    },
    methods: {
    onDelete(id) {
    console.log(id);
    this.$emit('delete-post', id);
    }
}
    
}
</script>
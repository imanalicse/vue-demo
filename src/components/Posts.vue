<template>
  <ul class="posts">
      <li v-for="post in posts" v-bind:key="post.id">            
            <Post :post="post" @delete-post="deletePost" />
      </li>
  </ul>
</template>
<script>
import Post from '@/components/Post.vue';
export default {
     components: {
        Post
    },    
    data() {
        return {
            posts: [],
            count : 5
        }
    },
    created() {
    },
     mounted() {
        fetch('https://jsonplaceholder.typicode.com/posts', {
            method: 'GET'
        })
        .then(response => response.json())
        .then(data => {
            this.posts = data;
            console.log(data);
        })
        .catch(err => console.log(err.message));
    },
    methods: {
        deletePost(id) {
        console.log('deletePost', id);
            this.posts = this.posts.filter((post) => post.id !== id);
        }
    },
}
</script>
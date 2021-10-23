<template>
  <div v-if="!isAddPost">
    <Button text="Add Post" backgroundColor="#ccc" @btn-click="addPostBtnClick"/>
    <ul class="posts">
        <li v-for="post in posts" v-bind:key="post.id">
              <Post :post="post" @delete-post="deletePost" />
        </li>
    </ul>
  </div>
   <div v-if="isAddPost">
       <AddPost @add-post = "addPost" />
   </div>

</template>
<script>
import Post from '@/components/Post.vue';
import AddPost from '@/components/posts/AddPost.vue'
import Button from './Button.vue';

export default {
     components: {
        Post,
        Button,
        AddPost
    },    
    data() {
        return {
            posts: [],
            isAddPost: false,
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
           this.posts = this.posts.filter((post) => post.id !== id);
        },
        addPostBtnClick() {
          this.isAddPost = true;
        },
        addPost(post) {
          this.isAddPost = false;
          console.log(post);
        }
    },
}
</script>

<style>
#app {
 text-align: left;
}
</style>
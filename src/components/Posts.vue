<template>
  <div v-if="!isAddPost">
    <Button text="Add Post" backgroundColor="#ccc" @btn-click="addPost"/>
    <ul class="posts">
        <li v-for="post in posts" v-bind:key="post.id">
              <Post :post="post" @delete-post="deletePost" />
        </li>
    </ul>
  </div>

  <form v-if="isAddPost" method="post" @submit="savePost">
    <input type="text" placeholder="Post title">
    <div class="">
      <input type="submit" value="Submit">
    </div>
  </form>

</template>
<script>
import Post from '@/components/Post.vue';
import Button from './Button.vue';
export default {
     components: {
        Post,
        Button
    },    
    data() {
        return {
            posts: [],
            isAddPost: false
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
        },
        addPost() {
          this.isAddPost = true;
          console.log("button click - parent");
        },
        savePost() {
          console.log('save post');
          this.isAddPost = false;
          //this.$router.push('/');
        }
    },
}
</script>
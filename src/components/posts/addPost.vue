<template>
    <form method="post" @submit="savePost">
    <div class="form-group">
        <label for="post-title">Title</label>
        <input id="post-title" type="text" name="title" v-model="post.title" placeholder="Post title">
    </div>
    <div class="form-group">
        <label for="post-body">Body</label>
        <textarea id="post-body" name="body" v-model="post.body"></textarea>
    </div>
    <div class="form-group">
        <input type="submit" value="Submit">
    </div>
</form>
</template>
<script>
export default {
    name: 'AddPost',
    data() {
        return {
            post: {
              title: '',
              body: ''
            }
        }
    },
    methods: {
        savePost(e) {
          e.preventDefault();
          if (!this.post.title) {
            alert('Please add title')
            return
          }
          const newPost = this.post;
          this.$emit('add-post', newPost);
          this.post.title = ''
          this.post.body = ''
        }
    },
}
</script>
<template>
  <div>
    <h2>Welcome to Ant Design</h2>
    <div v-for="post in posts" :key="post.id">
      {{ post.id }} - {{ post.title }} - {{ post.author }}
    </div>
    <a-pagination
      v-model:current="current"
      :total="totalPost"
      @change="pageClick"
    />
    <a-row>
      <a-col :span="6" class="bg-color">
        {{ current }}
      </a-col>
      <a-col :span="6">col - 6</a-col>

      <a-col :span="6">col - 6</a-col>
    </a-row>
    <a-button :type="primary" @click="getBottonType">Primary Button</a-button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  components: {},
  data() {
    return {
      primary: "dashed",
      current: 1,
      posts: [],
      postLength: 0,
    };
  },
  computed: {
    totalPost() {
      return this.postLength;
    },
  },
  methods: {
    async pageClick(page) {
      await axios
        .get(`http://localhost:3000/posts?_page=${page}`)
        .then((res) => {
          this.posts = res.data;
        });
    },
    getBottonType(e) {
      console.log(e);
    },
    async getFirstPost() {
      await axios.get("http://localhost:3000/posts?_page=1").then((res) => {
        this.posts = res.data;
        // console.log(res);
        // console.log(this.posts.length);
      });

      await axios.get("http://localhost:3000/posts").then((res) => {
        this.postLength = res.data.length;
      });
    },
  },
  mounted() {
    this.getFirstPost();
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.bg-color {
  background: rgb(0, 0, blue);
}
</style>

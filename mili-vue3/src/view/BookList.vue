<template>
  <div>
    <ul class="book-list">
      <li
        v-for="(book, i) in books"
        class="book-item"
        :style="{ 'margin-right': (i + 1) % 5 == 0 ? 0 : '20px' }"
      >
        <div class="book-item-img">
          <a :href="`/book/${book.id}`" target="_blank">
            <img :src="book.coverURL" />
          </a>
        </div>
        <h3 class="book-item-title">{{ book.name | entity2HTML }}</h3>
        <div class="book-item-producer">{{ book.user.name }}</div>
      </li>
    </ul>
  </div>
</template>

<script>
import htmlUtil from "@/utils/html";
import { getBooks } from "@/utils/apiConfig";

export default {
  name: "BookList",
  data() {
    return {
      books:[]
    };
  },
  created() {
    getBooks()
      .then((res) => {

          this.books=res.data.books

      })
      .catch((err) => {
        console.log(err);
        this.$message.error({ statusCode: 404, message: "Page not found" });
      });
  },
  head() {
    return {
      title: "图书",
    };
  },
  methods: {
    entity2HTML: htmlUtil.entity2HTML,
  },
};
</script>

<style>
@import "../assets/styles/book/list.css";
</style>

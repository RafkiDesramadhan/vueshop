<template>
  <div>
    <!-- template categoires  -->
    <v-container class="mb-0 pa-0 pt-3" grid-list-sm>
      <div class="text-right">
        <v-btn small text to="/categories" class="blue--text">
          All Categories <v-icon>mdi-chevron-right</v-icon>
        </v-btn>
      </div>
      <v-layout wrap>
        <v-flex
          v-for="category in categories"
          :key="'category-' + category.id"
          xs6
        >
          <category-item :category="category"></category-item>
        </v-flex>
      </v-layout>
    </v-container>

    <!-- template books  -->
    <v-container class="mb-0 pa-0 mt-2" grid-list-sm>
      <div class="text-right">
        <v-btn small text to="/books" class="blue--text">
          All Books <v-icon>mdi-chevron-right</v-icon>
        </v-btn>
      </div>
      <v-layout wrap>
        <v-flex v-for="book in books" :key="'book-' + book.id" xs6>
          <book-item :book="book"> </book-item>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
export default {
  name: "Home",
  components: {
    BookItem: () => import("@/components/BookItem.vue"),
    CategoryItem: () => import("@/components/CategoryItem.vue"),
  },
  data: () => ({
    categories: [],
    books: [],
  }),
  created() {
    console.log("get data categories");
    this.axios
      .get("/categories/random/2")
      .then((response) => {
        let { data } = response.data;
        this.categories = data;
      })
      .catch((error) => {
        let { response } = error;
        console.log(response);
      });

    console.log("get data books");
    this.axios
      .get("/books/top/4")
      .then((response) => {
        let { data } = response.data;
        this.books = data;
      })
      .catch((error) => {
        let { response } = error;
        console.log(response);
      });
  },
};
</script>

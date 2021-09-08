<template>
  <div>
    <v-app-bar app color="primary" dark>
      <v-btn icon @click.stop="$router.go(-1)">
        <v-icon>mdi-arrow-left-circle</v-icon>
      </v-btn>
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-badge color="orange" overlap>
          <template v-slot:badge>
            <span>3</span>
          </template>
          <v-icon>mdi-cart</v-icon>
        </v-badge>
      </v-btn>
    </v-app-bar>
    <v-container class="ma-0 pa-0" grid-list-sm>
      <v-subheader> All Books </v-subheader>
      <v-layout wrap>
        <v-flex v-for="book in books" :key="'book-' + book.id" xs6>
          <v-card :to="'/book/' + book.slug">
            <v-img :src="getImage('/books/' + book.cover)" class="white--text">
              <v-card-title class="fill-height align-end" v-text="book.title">
              </v-card-title>
            </v-img>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>

    <template>
      <v-pagination
        v-model="page"
        @input="go"
        :length="lengthPage"
        :total-visible="5"
      >
      </v-pagination>
    </template>
  </div>
</template>

<script>
export default {
  data: () => ({
    books: [],
    page: 0,
    lengthPage: 0,
  }),
  created() {
    this.go();
  },
  methods: {
    go() {
      let url = "/books?page=" + this.page;
      this.axios
        .get(url)
        .then((response) => {
          let { data } = response.data;
          let { meta } = response.data;
          this.books = data;
          this.lengthPage = meta.last_page;
          this.page = meta.current_page;
        })
        .catch((error) => {
          let { responses } = error;
          console.log(responses);
        });
    },
  },
};
</script>

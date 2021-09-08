<template>
  <div>
    <v-app-bar app color="primary" dark>
      <v-btn icon @click.stop="$router.go(-1)">
        <v-icon>mdi-arrow-left-circle</v-icon>
      </v-btn>
      <v-spacer></v-spacer>
      <v-btn icon to="/about">
        <v-badge color="orange" overlap>
          <template v-slot:badge>
            <span>3</span>
          </template>
          <v-icon>mdi-cart</v-icon>
        </v-badge>
      </v-btn>
    </v-app-bar>

    <v-container class="ma-0 pa-0" grid-list-sm>
      <v-subheader> All Category </v-subheader>
    </v-container>
    <v-layout wrap>
      <v-flex
        v-for="category in categories"
        :key="'category-' + category.id"
        xs6
      >
        <v-card :to="'/category/' + category.slug">
          <v-img
            :src="getImage('/categories/' + category.image)"
            class="white--text"
          >
            <v-card-title class="fill-height align-end" v-text="category.name">
            </v-card-title>
          </v-img>
        </v-card>
      </v-flex>
    </v-layout>
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
    categories: [],
    page: 0,
    lengthPage: 0,
  }),
  created() {
    this.go();
  },
  methods: {
    go() {
      let url = "/categories?page=" + this.page;
      this.axios
        .get(url)
        .then((response) => {
          let { data } = response.data;
          let { meta } = response.data;
          this.categories = data;
          this.page = meta.current_page;
          this.lengthPage = meta.last_page;
        })
        .catch((error) => {
          let { responses } = error;
          console.log(responses);
        });
    },
  },
};
</script>

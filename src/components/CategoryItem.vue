<template>
  <div>
    <v-card :to="'/category/' + category.slug">
      <v-img
        :src="getImage('/categories/' + category.image)"
        class="white--text"
      >
        <v-card-title
          class="fill-height align-end"
          v-text="category.name"
        ></v-card-title>
      </v-img>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "category-item",
  props: ["category"],
  data: () => ({}),
};
</script>

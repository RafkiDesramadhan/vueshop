<template>
  <div>
    <v-app-bar app color="primary" dark>
      <v-btn icon @click.stop="$router.go(-1)">
        <v-icon>mdi-arrow-left-circle</v-icon>
      </v-btn>
    </v-app-bar>

    <v-subheader class="text-h5">FORM UPDATE PROFILE</v-subheader>
    <v-form ref="form" lazy-validation>
      <v-text-field label="Name"></v-text-field>
      <v-text-field label="Email"></v-text-field>
      <v-select label="Roles"></v-select>
      <v-textarea label="Address"></v-textarea>
      <v-select label="City"></v-select>
      <v-select label="Province"></v-select>
      <v-text-field label="Phone"></v-text-field>
      <v-file-input
        prepend-icon="mdi-camera"
        label="Avatar Input"
        filled
      ></v-file-input>
    </v-form>
  </div>
</template>

<script>
export default {};
</script>


<template>
  <div>
    <v-app-bar app color="primary" dark>
      <v-btn icon @click.stop="$router.go(-1)">
        <v-icon>mdi-arrow-left-circle</v-icon>
      </v-btn>
    </v-app-bar>
    <v-subheader>Your Profile</v-subheader>
    <v-btn color="purple" class="white--text ml-4" to="/update-profile"
      >Update Profile</v-btn
    >
    <v-card flat>
      <v-container>
        <v-simple-table>
          <tbody>
            <tr v-for="(value, key) in user" :key="key">
              <td>{{ key }}</td>
              <td>{{ value }}</td>
            </tr>
          </tbody>
        </v-simple-table>
      </v-container>
    </v-card>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
export default {
  computed: {
    ...mapGetters({
      user: "auth/user",
    }),
  },
};
</script>

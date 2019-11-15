<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center headline">
        Hi, {{user.first_name}} {{user.last_name}}!
      </div>
      <v-spacer></v-spacer>

      <v-avatar color="blue">
        {{user.initials}}  
        <span class="white--text headline"></span>
      </v-avatar>
    </v-app-bar>

    <v-content>
      <UserProfile :user="user"/>
    </v-content>
  </v-app>
</template>

<script>
import UserProfile from './components/UserProfile';

export default {
  name: 'App',

  components: {
    UserProfile,
  },

  data: () => ({
    // Mock data of logged in user
    user: {
      first_name: "Evert",
      last_name: "Trollip",
      initials: "ET",
      email: "evert.trollip@careerteam.de",
      username: "evert.trollip@careerteam.de",
      password: "encrypted_pass_123",
      company: {
        name: "CAREERTEAM GmbH",
        country: "Germany",
        address: "Am Sandtorkai 48, 20457 Hamburg"
      },
      job_title: "Software Developer",
      activated: 1,
      last_login_at: "2019-07-22T13:40:09Z",
      created_at: "2019-07-22T13:40:09Z",
      updated_at: "2019-08-26T12:19:08Z",
    }
  }),
};
</script>

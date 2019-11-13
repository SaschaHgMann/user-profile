<template>
  <v-container fluid>
    <v-row>
      <v-col cols="8">
        <!-- ------------------------------------------ -->
        <!-- VCard component with primary user details  -->
        <!-- ------------------------------------------ -->
        <v-card>
          <v-card-title>User Profile</v-card-title>
          <v-card-subtitle>Primary Details</v-card-subtitle>
          
          <v-card-text class="text--primary">
            <v-text-field
            outlined
              v-model="user.first_name"
              label="First Name"
            >
            </v-text-field>
            <v-text-field
            outlined
              v-model="user.last_name"
              label="Last Name"
            >
            </v-text-field>
            <v-text-field
            outlined
              v-model="user.email"
              label="Email"
            >
            </v-text-field>
            <v-text-field
            outlined
              v-model="user.username"
              label="Username"
            >
            </v-text-field>
            <v-text-field
            outlined
              v-model="user.password"
              :value="user.password"
              label="Encrypted password"
              :type="showPassword ? 'text' : 'password'"
              :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
              @click:append="showPassword = !showPassword"
            >
            </v-text-field>
          </v-card-text>

          <v-card-actions>
            <!-- Add save function to this button using @click -->
            <v-btn
              outlined
              text
              color="success"
              @click="savePrimaryUserDetails(user.first_name)" 
            >
              Save
            </v-btn>
            <v-spacer></v-spacer>
            <v-btn
              outlined
              color="info"
              text
              @click="changePassword(user.password)" 
            >
              Change password
            </v-btn>
            <!-- Add button to change password -->
            
          </v-card-actions>
        </v-card>
      </v-col>

      <v-col cols="4">
        <!-- ------------------------------------------- -->
        <!-- VCard component with user secondary details -->
        <!-- ------------------------------------------- -->

        <!-- Use the example above to help -->        
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'UserProfile',
  props: ['user'],
  data: () => ({
   
  showPassword: false

  }),
  methods: {
    changePassword(event) {
      this.user.password = event.target.value
      this.$emit('passwordChanged', this.user.password)
    }
  }
};
</script>

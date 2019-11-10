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
              v-model="user.first_name"
              label="First Name"
            >
            </v-text-field>

            <!-- Add the rest of the user details here -->
          </v-card-text>

          <v-card-actions>
            <!-- Add save function to this button using @click -->
            <v-btn
              outlined
              text
            >
              Save
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
  }),
};
</script>

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
              @change="dataGood=true"
              v-model="user.first_name"
              label="First Name"
              
            >
            </v-text-field>
            <v-text-field
              outlined
              @change="dataGood=true"
              v-model="user.last_name"
              label="Last Name"
            >
            </v-text-field>
            <v-text-field
              outlined
              @change="dataGood=true"
              v-model="user.email"
              label="Email"
            >
            </v-text-field>
            <v-text-field
              outlined
              @change="dataGood=true"
              v-model="user.username"
              label="Username"
            >
            </v-text-field>
            <v-text-field
              outlined
              @change="dataGood=true"
              ref="pw"
              v-model="user.password"
              label="Encrypted password"
              :type="showPassword ? 'text' : 'password'"
              :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
              @click:append="showPassword = !showPassword"
            >
            </v-text-field>
          </v-card-text>

          <p v-if="errors.length" class="mx-auto">
            <b>!! Please correct following entry/entries !!</b>
            <ul>
              <li v-for="error in errors" :key="error"> {{error}} </li>
            </ul>
          </p>

          <v-alert v-if="dataSubmitted" type="success" width="96%" class="mx-auto">
            Data saved!
          </v-alert>

          <v-card-actions>
            <v-btn
              :class="{ active: dataGood }"
              v-if="dataGood"
              outlined
              text
              color="success"
              @click="onSavePrimaryUserDetails(user, data)" 
            >
              Save
            </v-btn>
            <v-spacer></v-spacer>
            <v-btn
              outlined
              color="info"
              text
              @click="onChangePassword(user.password)" 
            >
              Change password
            </v-btn>            
          </v-card-actions>
        </v-card>
      </v-col>

      <v-col cols="4">
        <!-- ------------------------------------------- -->
        <!-- VCard component with user secondary details -->
        <!-- ------------------------------------------- -->
        <v-card class="text-center ">
          <v-img 
            src="https://live.staticflickr.com/5463/16876873654_3a15d1cdc4_b.jpg"
            width="200px"
            alt="Profile Image"
            class="mx-auto"
            >
          </v-img>
          <v-card-subtitle>
             {{user.job_title}}
          </v-card-subtitle>
          <hr width="90%" class="mx-auto">
          <p>
          <p>
             {{user.company.name}}
          <br>
              {{user.company.country}}, {{user.company.address}}
          </p>
          <br>
        </v-card>
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
   
  showPassword: false,
  dataSubmitted: false,
  dataGood: false,
  errors:[]

  }),

  methods: {
  
    onSavePrimaryUserDetails() {  
           
      if (this.user.first_name && this.user.last_name && this.user.email &&this.user.username &&
          this.user.password) {
              //this.errors.push('')
              //this.errors.refresh()  
              //setTimeout(function(){ alert("Hello"); }, 1000)          

              this.dataSaved()
     
      }
          
      else {
        if(!this.user.first_name) this.errors.push('Enter first name')
        if(!this.user.last_name) this.errors.push('Enter last name')
        if(!this.user.email) this.errors.push('Enter email')
        if(!this.user.username) this.errors.push('Enter a username')
        if(!this.user.password) this.errors.push('Enter password')
      } 
    },

    onChangePassword() {
      this.clearPassword()
    },
    clearPassword() {
      var self = this;
      self.user.password = '',
      this.$refs.pw.focus()
    },
    dataSaved(){
      this.dataSubmitted = true,
      this.errors = ''
    }

  }
  
};
</script>

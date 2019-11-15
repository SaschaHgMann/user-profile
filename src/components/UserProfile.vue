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
              @focus="onChangeEntry()"
              v-model="user.first_name"
              label="First Name"             
            >
            </v-text-field>
            <!-- tried @change also but prefer @focus due to ux -->
            <v-text-field
              outlined
              @change="onChangeEntry()"           
              v-model="user.last_name"
              label="Last Name"
            >
            </v-text-field>
            <v-text-field
              outlined
              @focus="onChangeEntry()"
              v-model="user.email"
              label="Email"
            >
            </v-text-field>
            <v-text-field
              outlined
              @focus="onChangeEntry()"
              v-model="user.username"
              label="Username"
            >
            </v-text-field>
            <v-text-field
              outlined
              @focus="onChangeEntry()"
              ref="pw"
              v-model="user.password"
              label="Encrypted password"
              :type="showPassword ? 'text' : 'password'"
              :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
              @click:append="showPassword = !showPassword"
            >
            </v-text-field>
          </v-card-text>

          <v-alert v-if="errors.length" type="error" width="96%" class="mx-auto">
            <b>!! Please correct following entry/entries !!</b>
            <ul>
              <li v-for="error in errors" :key="error"> {{error}} </li>
            </ul>
          </v-alert>

          <div class="text-center">
            <v-progress-circular
              v-if="loading"
              indeterminate
              color="primary"
              :size="60"
              :width="5"              
            >
            </v-progress-circular>
          </div>

          <v-alert v-if="dataSubmitted" type="success" width="96%" class="mx-auto">
            Data saved!
          </v-alert>

          <v-card-actions>
            <v-btn
              :class="{ active: dataGood }"
              :disabled="dataSubmitted || loading"
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
          <v-avatar width="200px" height=auto>
          <v-img 
            src="https://live.staticflickr.com/5463/16876873654_3a15d1cdc4_b.jpg"           
            alt="Profile Image"
            class="mx-auto"
            >
          </v-img>
          </v-avatar>
          <v-card-subtitle>
             <b>{{user.job_title}}</b>
          </v-card-subtitle>
          <hr width="90%" class="mx-auto">
        
          <v-card-text>
          <p>
             {{user.company.name}}
          <br>
              {{user.company.country}}, {{user.company.address}}
          </p>
          </v-card-text>
          <br>
        </v-card> 
        <br>
        <v-card class="text-center">
        
          <v-card-subtitle class="text-center" font-size="30px">
            <h2>Primary User Details</h2>
          </v-card-subtitle>
          <v-card-subtitle>
             <b>{{fullName}}</b>
          </v-card-subtitle>
          <v-card-subtitle>
             <p>Username: {{user.username}}</p>
             <p>Email: {{user.email}}</p>
          </v-card-subtitle>          
          <br>
        </v-card>    
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
  dataGood: false,
  loading: false,
  dataSubmitted: false,
  errors:[]
  }),

  methods: {  
    onSavePrimaryUserDetails() {            
      if (this.user.first_name && 
          this.user.last_name && 
          this.user.email &&
          this.user.username &&
          this.user.password) {               
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
      this.$refs.pw.focus(),
      this.dataSubmitted = false    
    },
    dataSaved(){
      this.errors = '',
      this.loading = true,      
      setTimeout(() => {(
        this.dataSubmitted = true, this.loading = false);
      }, 1000);
    },
    onChangeEntry(){
      this.dataGood = true,
      this.dataSubmitted = false
    }

  },
  computed: {
    fullName() {
      return this.user.first_name + ' ' + this.user.last_name
    }
  }
  
};
</script>

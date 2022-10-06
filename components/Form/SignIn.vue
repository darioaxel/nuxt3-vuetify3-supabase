<template>
    <v-card>
      <v-card-title>Formulario SignIn </v-card-title>
      <v-form ref="form" lazy-validation class="ma-2">
        <div class="ma-2">
        <v-text-field v-model="name" :counter="10" :rules="nameRules" label="Name" required></v-text-field>
        <v-text-field v-model="email" :rules="emailRules" label="E-mail" required></v-text-field>
        <v-text-field
            v-model="password"    
            :value="password"
            label="Enter password"
            hint="Your password passed! Password rules are not meant to be broken!"
          ></v-text-field>
           
          
        </div>
        <v-btn color="success" class="mr-4" @click="signUp">
          SignIn
        </v-btn>
        <v-btn color="warning" class="mr-4" @click="reset">
          Reset
        </v-btn>
      </v-form>
    </v-card>
  </template>
  <script setup lang="ts">

    const password = ref('');
    const name = ref('');
    const email = ref('');
    const user = useSupabaseUser();
    const { auth } = useSupabaseClient(); 

    const nameRules = [
        v => !!v || 'Name is required',
        v => (v && v.length <= 10) || 'Name must be less than 10 characters',
      ];
    const emailRules = [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ];
   //ToDo Usar Vuelidate para comprobar todo. 
    const reset = () => {
        name.value = '';
        email.value = '';
    }

    const signUp = async () => {
      const {error} = await auth.signUp(
        {
          email: email.value,
          password: password.value
        })
        if (error) {
          return alert('Something went wrong !')
        } else return alert('Something went wrong !')
    }
  
  </script>
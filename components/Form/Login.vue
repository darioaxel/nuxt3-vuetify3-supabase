<template>
  <v-card>
    <v-card-title>Formulario Login</v-card-title>
    <v-form ref="form"  lazy-validation class="ma-2">
      <div class="ma-2">
      <v-text-field v-model="name" :counter="10" :rules="nameRules" label="Name" required></v-text-field>
      <v-text-field v-model="email" :rules="emailRules" label="E-mail" required></v-text-field>
      </div>
      <v-btn color="success" class="mr-4" @click="login">
        Login
      </v-btn>
      <v-btn color="warning" class="mr-4">
        Reset Form
      </v-btn>
    </v-form>
  </v-card>
</template>

  <script setup lang="ts">

const password = ref('yokozuna');
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
const router = useRouter()
// Login method using providers
console.log(email.value, " ", password.value)
const login = async () => {
  const { error } = await auth.signIn({
          email: email.value,
          password: password.value
        })
  if (error) {
    return alert('Something went wrong !')
  } else
     router.push('/private-page')
}
</script>
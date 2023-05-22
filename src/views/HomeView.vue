<template>
  <div>
    <h2 class="text-center">Login</h2>
    <v-card class="mx-auto" max-width="400">
      <v-card-text>
        <v-form @submit.prevent="login">
          <v-text-field v-model="emailText" label="Email" type="email" ></v-text-field>
          <div v-if="v$.emailText.$error">
            <div class="c-red" v-for="error in v$.emailText.$errors" :key="error.$uid">
              {{error.$message}}
            </div>
          </div>
          <v-text-field v-model="password" label="Password" type="password"></v-text-field>
          <div v-if="v$.password.$error">
            <div class="c-red" v-for="error in v$.password.$errors" :key="error.$uid">
              {{error.$message}}
            </div>
          </div>
          <v-btn type="submit" color="primary">Login</v-btn>
        </v-form>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
import { ref, computed } from 'vue'
import { required, minLength, email } from '@vuelidate/validators'
import { useVuelidate } from '@vuelidate/core'
import { useRouter } from 'vue-router'

export default {
  name: 'LoginView',
  setup() {
    const emailText = ref('')
    const password = ref('')
    const router = useRouter()

    const rules = computed(() => ({
      emailText: {
        required,
        email,
      },
      password: {
        required,
        minLength: minLength(6),
      }
    }))

    const v$ = useVuelidate(rules, { emailText, password })

    const login = () => {
      v$.value.$touch();

      if (!v$.value.$error) {
        router.push('/game');
      }
    };

    return {
      emailText,
      password,
      login,
      v$
    }
  },
};
</script>

<style scoped>
.text-center {
  text-align: center;
}

.mx-auto {
  margin-left: auto;
  margin-right: auto;
}

.v-card {
  padding: 20px;
}

.c-red {
  color: red;
}
</style>


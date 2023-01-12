<template>
  <q-card class="q-pa-lg column no-wrap flex-center" style="min-width: 350px">
    <div class="q-py-lg">
      <q-icon name="account_circle" color="secondary" size="56px" />
      <div class="text-h5 text-center text-secondary">Login</div>
    </div>

    <q-input
      ref="username_input"
      outlined
      class="q-pb-lg login-input"
      color="secondary"
      v-model="username"
      name="Username"
      label="Username"
      lazy-rules
      @keyup.enter="nextInput"
      :rules="[(val) => (val && val.length > 0) || 'Invalid username']"
      key="nextInput"
    />

    <q-input
      outlined
      ref="password_input"
      class="q-pt-sm login-input"
      color="secondary"
      v-model="password"
      name="Password"
      label="Password"
      :type="isPwd ? 'password' : 'text'"
      lazy-rules
      :rules="[(val) => (val && val.length > 0) || 'Invalid password']"
    >
      <template v-slot:append>
        <q-icon
          :name="isPwd ? 'visibility_off' : 'visibility'"
          class="cursor-pointer"
          @click="isPwd = !isPwd"
        />
      </template>
    </q-input>

    <div class="q-py-lg text-center">
      <q-btn label="Submit" @click="submit" color="secondary" />
      <q-btn
        label="Reset"
        @click="reset"
        color="secondary"
        flat
        class="q-ml-sm"
      />
    </div>
  </q-card>
</template>

<script>
import { ref } from 'vue';
import { api } from 'boot/axios';

export default {
  setup() {
    return {
      username: ref(''),
      password: ref(''),
      loading: ref('false'),
      sentRequest: ref('false'),
      isPwd: ref('true'),
    };
  },
  methods: {
    nextInput() {
      this.$refs.password_input.focus();
    },
    async submit() {
      if (
        this.$refs.username_input.validate() &&
        this.$refs.password_input.validate()
      ) {
        let login = { username: this.username, password: this.password };
        api
          .post('/api/tracker/login', login)
          .then((response) => {
            api.defaults.headers.common['Authorization'] =
              'Bearer ' + response.data.token;
            commit('login', {
              token: response.access_token,
              user: response.user_id,
            });
          })
          .catch(() => {
            console.log('Failed to login');
          });
        // toJSON method
      } else {
        console.log('invalid submission');
      }
    },
    reset() {
      this.username = '';
      this.password = '';
      this.$refs.username_input.resetValidation();
      this.$refs.password_input.resetValidation();
    },
  },
};
</script>

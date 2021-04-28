<template>
  <v-container fluid>
    <v-row>
      <v-col cols="12">
        <v-btn
          color="secondary"
          @click="recaptcha"
        >
          Generate Token
        </v-btn>
      </v-col>
      <v-col cols="12">
        <v-textarea
          v-model="token"
          placeholder="Click in generate token to get a new token.."
          disabled
          filled
        ></v-textarea>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Vue from 'vue';
import { VueReCaptcha } from 'vue-recaptcha-v3';

Vue.use(VueReCaptcha, {
  siteKey: process.env.VUE_APP_RECAPTCHA_KEY,
});

export default {
  name: 'Home',
  data() {
    return {
      token: '',
    };
  },
  methods: {
    async recaptcha() {
      // (optional) Wait until recaptcha has been loaded.
      await this.$recaptchaLoaded();

      // Execute reCAPTCHA with action "login".
      this.token = await this.$recaptcha('login');

      // Do stuff with the received token.
    },
  },
};
</script>

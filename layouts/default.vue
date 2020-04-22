<template>
  <v-app class="app">
    <v-overlay v-if="loading" color="#F8F9FA" opacity="1" z-index="9999">
      <div class="loader">
        <scale-loader color="#00A040" />
      </div>
    </v-overlay>
    <v-content>
      <v-container v-if="userAuth" class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="4">
            <LoginForm @func="login"></LoginForm>
          </v-col>
        </v-row>
      </v-container>
      <v-container v-else class="mainpage">
        <v-app-bar fixed app flat src="/bgimg.png">
          <v-toolbar-title>KL通商</v-toolbar-title>
        </v-app-bar>
        <nuxt></nuxt>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import ScaleLoader from "vue-spinner/src/ScaleLoader.vue";
import LoginForm from "../components/LoginForm.vue";

export default {
  components: {
    ScaleLoader,
    LoginForm
  },
  data: function() {
    return {
      loading: true,
      userAuth: true,
    };
  },
  mounted() {
    this.loading = false;
  },
  methods: {
    login(data) {
      this.userAuth = data;
    }
  }
};
</script>
<style scoped>
.app {
  max-width: 1440px;
  margin: 0 auto;
  background-color: inherit !important;
}

.loader {
  height: 200px;
  width: 150px;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translateY(-50%) translateX(-50%);
}

.mainpage{
  margin-top: 0px;
  padding-top: 0px;
}
</style>
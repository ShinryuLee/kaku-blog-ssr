<template>
  <v-app class="app">
    <v-overlay v-if="loading" color="#F8F9FA" opacity="1" z-index="9999">
      <scale-loader class="steal accent-3" />
    </v-overlay>
    <v-content>
      <v-container v-if="userAuth" class="fill-height" fluid>
        <v-row class="ml-0" align="center" justify="center" >
          <v-col cols="12" sm="4" md="6" align="center" justify="center">
            <LoginForm @func="login"></LoginForm>
          </v-col>
        </v-row>
      </v-container>
      <v-container v-else class="mainpage">
        <v-app-bar class="primary" dark fixed app flat >
          <v-toolbar-title>KL通商</v-toolbar-title>
          <v-spacer/>
          <v-btn  v-if="userAuth"  rounded flat outlined @click="login">Login</v-btn>
          <v-btn class="primary" v-else color="primary" rounded flat outlined @click="logout">Logout</v-btn>
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
      userAuth: true
    };
  },
  mounted() {
    this.loading = false;
  },
  methods: {
    logout() {
      this.userAuth = true;
    },
    login(data) {
      this.userAuth = data;
    }
  }
};
</script>
<style lang="scss" scoped>
.app {
  max-width: 100%;
  margin: 0 auto;
  background-color:$gray-4 !important;
}

.loader {
  height: 200px;
  width: 150px;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translateY(-50%) translateX(-50%);
}

.mainpage {
  margin-top: 0px;
  padding-top: 0px;
}
</style>
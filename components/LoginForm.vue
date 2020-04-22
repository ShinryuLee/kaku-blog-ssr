<template>
  <v-card class="elevation-12">
    <v-toolbar src="/bgimg.png" flat>
      <v-toolbar-title>Login</v-toolbar-title>
    </v-toolbar>
    <v-card-text>
      <v-form>
        <v-text-field label="Login" name="login" prepend-icon="mdi-account" type="text" />
        <v-text-field
          id="password"
          label="Password"
          name="password"
          prepend-icon="mdi-lock"
          type="password"
        />
      </v-form>
    </v-card-text>
    <v-card-actions>
      <v-spacer />
      <v-btn color="primary" @click="login">Login</v-btn>
    </v-card-actions>
  </v-card>
</template>
<script>
export default {
  data () {
        return {
            //将msg传递给父组件
          authFlg: true,
        }
    },
     methods:{
         login(){
           this.authFlg = false,
             //func: 是父组件指定的传数据绑定的函数，this.msg:子组件给父组件传递的数据
             this.$emit('func',this.authFlg)
         }
     }
}
</script>
<template>
<!--设置登录界面最大宽度，保证画面不会拉伸太严重-->
  <v-card max-width="700" class="elevation-0" outlined>
    <v-window v-model="step">
      <v-window-item :value="1">
        <v-row class="mx-0 fill-height" justify="center">
          <v-col cols="12" md="7">
            <v-card-text class="mt-2">
              <h1 class="text-center display-1 teal--text text--green-3">Kaku-CRM系统</h1>
              <h4 class="text-center mt-5">请使用邮箱登录或注册</h4>
              <v-form>
                <v-text-field
                  label="Email"
                  name="Email"
                  prepend-icon="email"
                  type="text"
                  color="teal accent-3"
                ></v-text-field>
                <v-text-field
                  id="password"
                  label="Password"
                  name="Password"
                  prepend-icon="lock"
                  type="password"
                  color="teal accent-3"
                ></v-text-field>
              </v-form>
              <h3 class="text-center mt-3">忘记密码?</h3>
            </v-card-text>
            <div class="text-center mt-3">
              <v-btn rounded color="teal accent-4 elevation-0" dark @click="login">登&nbsp;&nbsp;录</v-btn>
            </div>
          </v-col>
          <v-col cols="12" md="5" class="teal accent-4 py-10">
            <v-card-text class="white--text">
              <h2 class="text-center display-0">尊敬的VIP客户</h2>
              <h4 class="text-center mt-5">欢迎注册kaku家客户关系系统</h4>
            </v-card-text>
            <div class="text-center mt-4">
              <v-btn rounded outlined dark @click="step++">注&nbsp;&nbsp;册</v-btn>
            </div>
          </v-col>
        </v-row>
      </v-window-item>
      <v-window-item :value="2">
        <v-row class="mx-0 fill-height" justify="center">
          <v-col cols="12" md="5" class="teal green-3">
            <v-card-text class="white--text mt-2">
              <h2 class="text-center display-0">如果已经拥有账户</h2>
              <h4 class="text-center mt-5">请点击下面按钮直接返回登录界面</h4>
            </v-card-text>
            <div class="text-center mt-4">
              <v-btn rounded outlined dark @click="step--">返回登录</v-btn>
            </div>
          </v-col>
          <v-col col="12" md="7">
            <v-card-text class="mt-2">
              <h1 class="text-center display-1 teal--text text--green-3">注&nbsp;&nbsp;册</h1>
              <h4 class="text-center mt-5">请使用邮箱注册</h4>
              <v-form>
                <v-text-field
                  label="Name"
                  name="Name"
                  prepend-icon="person"
                  type="text"
                  color="teal accent-3"
                />
                <v-text-field
                  label="Email"
                  name="Email"
                  prepend-icon="email"
                  type="text"
                  color="teal accent-3"
                ></v-text-field>
              </v-form>
              <h3 class="text-center mt-3">点击下一步验证邮箱</h3>
            </v-card-text>
            <div class="text-center mt-3">
              <v-btn rounded outlined dark color="teal green-3" @click="step++">下一步</v-btn>
            </div>
          </v-col>
        </v-row>
      </v-window-item>
      <v-window-item :value="3">
        <v-row class="mx-0 fill-height" justify="center">
          <v-col cols="12" md="5" class="teal green-3">
            <v-card-text class="white--text mt-2">
              <h2 class="text-center display-0">如果已经拥有账户</h2>
              <h4 class="text-center mt-5">请点击下面按钮直接返回登录界面</h4>
            </v-card-text>
            <div class="text-center mt-4">
              <v-btn rounded outlined dark @click="step=1">返回登录</v-btn>
            </div>
          </v-col>
          <v-col col="12" md="7">
            <v-card-text class="mt-2">
              <h1 class="text-center display-1 teal--text text--green-3">验&nbsp;&nbsp;证</h1>
              <h4 class="text-center mt-5">请输入验证码</h4>
              <v-form>
                <v-text-field
                  label="OneTimeCode"
                  name="验证码"
                  prepend-icon="code"
                  type="text"
                  color="teal accent-3"
                />
                <v-radio-group v-model="row" row>
                  <template v-slot:label>
                    <div>请选择客户属性</div>
                  </template>
                  <v-radio label="个人" value="1"></v-radio>
                  <v-radio label="法人" value="2"></v-radio>
                </v-radio-group>
              </v-form>
              <h3 class="text-center mt-3">点击下一步输入密码</h3>
            </v-card-text>
            <div class="text-center mt-3">
              <v-btn class="mr-3" rounded outlined dark color="teal green-3" @click="step--">上一步</v-btn>
              <v-btn rounded outlined dark color="teal green-3" @click="step++">下一步</v-btn>
            </div>
          </v-col>
        </v-row>
      </v-window-item>
      <v-window-item :value="4">
        <v-row class="mx-0 fill-height" justify="center">
          <v-col cols="12" md="5" class="teal green-3">
            <v-card-text class="white--text mt-2">
              <h2 class="text-center display-0">如果已经拥有账户</h2>
              <h4 class="text-center mt-5">请点击下面按钮直接返回登录界面</h4>
            </v-card-text>
            <div class="text-center mt-4">
              <v-btn rounded outlined dark @click="step=1">返回登录</v-btn>
            </div>
          </v-col>
          <v-col col="12" md="7">
            <v-card-text class="mt-2">
              <h1 class="text-center display-1 teal--text text--green-3">输入&nbsp;&nbsp;密码</h1>
              <h4 class="text-center mt-5">请输入密码</h4>
              <v-form>
                <v-text-field
                  id="password"
                  label="Password"
                  name="Password"
                  prepend-icon="lock"
                  type="password"
                  color="teal accent-3"
                ></v-text-field>
                <v-text-field
                  id="password"
                  label="Password"
                  name="Password"
                  prepend-icon="lock"
                  type="password"
                  color="teal accent-3"
                ></v-text-field>
              </v-form>
              <h3 class="text-center mt-3">点击下一步输入密码</h3>
            </v-card-text>
            <div class="text-center mt-3">
              <v-btn class="mr-3" rounded outlined dark color="teal green-3" @click="step--">上一步</v-btn>
              <v-btn rounded outlined dark color="teal green-3" @click="step++">注册</v-btn>
            </div>
          </v-col>
        </v-row>
      </v-window-item>
      <v-window-item :value="5">
        <v-row class="mx-0 fill-height" justify="center">
          <v-col cols="12" md="12" class="teal green-3 py-12">
            <v-card-text class="white--text mt-2">
              <h2 class="text-center display-0">账户注册成功！</h2>
              <h4 class="text-center mt-5">请点击下面按钮直接返回登录界面</h4>
            </v-card-text>
            <div class="text-center mt-4">
              <v-btn rounded outlined dark @click="step=1">返回登录</v-btn>
            </div>
          </v-col>
        </v-row>
      </v-window-item>
    </v-window>
  </v-card>
</template>
<script>
export default {
  data() {
    return {
      //将msg传递给父组件
      authFlg: true,
      step: 1,
      registstep: 1,
      row: null
    };
  },
  props: {
    source: String
  },
  methods: {
    login() {
      this.authFlg = false;
      //func: 是父组件指定的传数据绑定的函数，this.msg:子组件给父组件传递的数据
      this.$emit("func", this.authFlg);
    }
  }
};
</script>
<style lang="scss" scoped>
</style>
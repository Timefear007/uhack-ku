<template>
  <div class="text-xs-center">
    <v-dialog v-model="isSignin" width="400">
      <v-card
        v-if="LoginContext === 'Login' && active"
        key="login"
        class="float-card"
      >
        <v-card-title class="headline center-title">LOG IN</v-card-title>
        <v-form>
          <v-container>
            <v-layout wrap row justify-center>
              <v-flex md9>
                <v-text-field
                  v-model="email"
                  label="Email"
                  required
                ></v-text-field>
              </v-flex>
              <v-flex md9>
                <v-text-field
                  v-model="password"
                  type="password"
                  label="Password"
                  required
                ></v-text-field>
              </v-flex>
              <v-flex md9 justify-center>
                <div class="div-center">
                  <v-btn color="primary" @click="onLogin()">Log &nbsp;in</v-btn>
                  <v-btn color="primary" @click="LoginContext = 'Reg'"
                    >Register</v-btn
                  >
                </div>
              </v-flex>
            </v-layout>
          </v-container>
        </v-form>
        <hr class="hr-text" data-content="Or log in with" />
        <div class="signin-alternative">
          <v-btn class="login-btn" round ripple>
            <v-avatar size="32">
              <v-img
                sizes="32"
                :src="require('../../assets/g+.png')"
              ></v-img> </v-avatar
            >&nbsp;&nbsp;&nbsp; Log in with Google&nbsp;
          </v-btn>
          <br />
          <v-btn class="login-btn" round ripple>
            <v-avatar size="32">
              <v-img
                sizes="32"
                :src="require('../../assets/facebook.png')"
              ></v-img> </v-avatar
            >&nbsp; Log in with Facebook
          </v-btn>
        </div>
      </v-card>
      <v-card v-if="LoginContext === 'Reg'" key="reg" class="float-card">
        <v-card-title>Registration form</v-card-title>
        <v-form ref="form">
          <v-container>
            <v-layout wrap row justify-center>
              <v-flex md9>
                <v-text-field
                  v-model="email"
                  type="email"
                  :rules="mailrules"
                  label="Email"
                  required
                ></v-text-field>
              </v-flex>
              <v-flex md9>
                <v-text-field
                  v-model="password"
                  type="password"
                  label="Password"
                  required
                ></v-text-field>
              </v-flex>
              <v-flex md9>
                <v-text-field
                  v-model="passMatch"
                  type="password"
                  :rules="passrules"
                  label="Confirm password"
                  required
                ></v-text-field>
              </v-flex>
              <v-flex md9 class="div-center">
                <v-btn role="submit" @click="submit()">Register</v-btn>
              </v-flex>
            </v-layout>
          </v-container>
        </v-form>
      </v-card>
    </v-dialog>
    <v-btn
      round
      color="#4e5d6b"
      flat="flat"
      @click="
        isSignin = !isSignin;
        active = true;
      "
      >Log in or Sign up</v-btn
    >
  </div>
</template>

<script>
export default {
  props: {
    onLogin: {
      type: Function,
      default: function() {
        return;
      }
    }
  },
  data() {
    return {
      isSignin: false,
      email: "",
      password: "",
      LoginContext: "Login",
      passMatch: "",
      active: false,
      mailrules: [
        v => !!v || "E-mail is required",
        // eslint-disable-next-line
        v => /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(v) || "E-mail must be valid"
      ],
      passrules: [v => (!!v && v) === this.passMatch || "Values do not match"]
    };
  },
  watch: {
    passMatch: "validateField",
    email: "validateField",
    isSignin(v) {
      if (!v && this.LoginContext === "Reg") {
        this.LoginContext = "Login";
        this.active = false;
        this.email = "";
        this.password = "";
        this.passMatch = "";
      }
    }
  },
  methods: {
    validateField() {
      this.$refs.form.validate();
    },
    submit() {
      console.log(this.email, this.password);
      this.active = false;
      this.LoginContext = "Login";
      this.active = false;
      this.email = "";
      this.password = "";
      this.passMatch = "";
      this.isSignin = false;
      alert("success");
    }
  }
};
</script>

<style>
.center-title {
  text-align: center;
  display: block;
}
.signin-alternative {
  text-align: center;
  align-content: center;
}

.hr-text {
  line-height: 1em;
  position: relative;
  outline: 0;
  border: 0;
  color: black;
  text-align: center;
  height: 1.5em;
  opacity: 0.5;
}
.hr-text:before {
  content: "";
  background: linear-gradient(to right, transparent, #818078, transparent);
  position: absolute;
  left: 0;
  top: 50%;
  width: 100%;
  height: 1px;
}
.hr-text:after {
  content: attr(data-content);
  position: relative;
  display: inline-block;
  color: black;
  padding: 0 0.5em;
  line-height: 1.5em;
  color: #818078;
  background-color: #fcfcfa;
}
.float-card {
  border-radius: 8px;
}
.div-center {
  text-align: center;
}
</style>

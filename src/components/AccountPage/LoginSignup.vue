<template>
  <template v-if="loadingState">
    <div className="loading-state">
      Loading...
      <span></span>
      Be patient while backend starts up, it may take up to a minute
    </div>
  </template>
  <template v-else>
    <div className="signup" v-if="signup">
      <h2>Create a new account</h2>
      <form @submit.prevent="createAccountHandler">
        <div className="inputbox">
          <input
            id="email"
            type="email"
            name="email"
            v-model="email"
            required
          />
          <span>Email Address</span>
        </div>
        <div className="inputbox">
          <input
            id="password"
            type="password"
            name="password"
            v-model="password"
            minLength="{10}"
            required
          />
          <span>Password</span>
        </div>
        <input type="submit" value="Signup" id="submit" />
      </form>
    </div>
    <div className="login" v-if="login">
      <h2>Log in to account</h2>
      <form @submit.prevent="loginAccountHandler">
        <div className="inputbox">
          <input
            id="email"
            type="email"
            name="username"
            v-model="email"
            required
          />
          <span>Email Address</span>
        </div>
        <div className="inputbox">
          <input
            id="password"
            type="password"
            name="password"
            v-model="password"
            minLength="{10}"
            required
          />
          <span>Password</span>
        </div>
        <input type="submit" value="Login" id="submit" />
      </form>
    </div>
    <template v-if="message.length > 0">{{ message }}</template>
  </template>
</template>

<script>
export default {
  name: "LoginSignUp",
  props: [
    "login",
    "signup",
    "createAccount",
    "loginAccount",
    "loadingState",
    "message",
  ],
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    loginAccountHandler() {
      this.loginAccount(this.email, this.password)
    },
    createAccountHandler() {
      this.createAccount(this.email, this.password)
    }
  }
};
</script>

<style scoped>
.login-signup {
    width: 50%;
    height: 100%;
    backdrop-filter: blur(1px);
    border-radius: 30px;
}

.login-signup .inputbox {
    position: relative;
    width: auto;
}
.login-signup h2 {
    margin-bottom: 10px;
}
.login-signup .inputbox input {
    width: 100%;
    padding: 10px;
    border-radius: 5px;
    outline: none;
    border: 1px solid black;
    font-size: 1rem;
}
.login-signup .inputbox #email{
    margin-bottom: 15px;
}
.login-signup #submit{
    margin-top: 20px;
    padding: 10px 15px;
    background-color: transparent;
    cursor: pointer;
    border: 2px solid black;
    border-radius: 15px;
    transition: 500ms;
}
.login-signup #submit:hover{
    border: 2px solid var(--color3);
    border-radius: 5px;
}
.login-signup .inputbox span {
    position: absolute;
    left: 0;
    padding: 10px;
    pointer-events: none;
    font-size: 1rem;
    color: var(--color1);
    transition: 0.5s;
}

.login-signup .inputbox input:valid ~span::after {
    content: "👍";
} 
.login-signup .inputbox input:focus ~ span,
.login-signup .inputbox input:valid ~ span{
    color: var(--color3);
    transform: translateX(10px) translateY(-7px);
    font-size: 0.65em;
    padding: 0 10px;
    background-color: white;
    border-left: 4px solid var(--color3);
    border-right: 4px solid var(--color3);
    letter-spacing: 0.2em;
}
.login-signup .inputbox input:focus,
.login-signup .inputbox input:valid {
    border: 2px solid var(--color3);
}
#account-page div .login-signup .loading-state span {
    height: 10px;
    width: 80px;
    display: block;
    background-color: var(--color1);
    animation: loading-span 1s ease-out infinite alternate;
}
@keyframes loading-span {
    from {
        width: 80px;
    }
    to {
        width: 200px;
    }
}
</style>
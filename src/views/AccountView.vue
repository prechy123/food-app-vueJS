<template>
  <template v-if="isAuthenticated"> 
    <SaveAccountCom />
  </template>
  <template v-else>
    <section id="account-page">
      <div>
        <div className="title">
          <h1>Already have an account</h1>
          <div>
            <button @click="handleLogin">
              <span className="first"></span>
              <p>login</p>
            </button>
            <button @click="handleSignup">
              <span className="second"></span>
              <p>Signup</p>
            </button>
          </div>
        </div>
        <div className="login-signup">
          <LoginSignup
            :login="login"
            :signup="signup"
            :createAccount="createAccount"
            :loginAccount="loginAccount"
            :loadingState="loadingState"
            :message="message"
          />
        </div>
      </div>
    </section>
  </template>
</template>

<script>
import LoginSignup from "@/components/AccountPage/LoginSignup.vue";
import axios from "axios";
import SaveAccountCom from '@/components/AccountPage/SaveAccountCom.vue';
export default {
  components: { LoginSignup, SaveAccountCom },
  data() {
    return {
      login: false,
      signup: false,
      isAuthenticated: false,
      tokenData: "",
      loadingState: false,
      message: "",
    };
  },
  methods: {
    handleLogin() {
      this.login = !this.login;
      this.signup = false;
      this.message = "";
    },
    handleSignup() {
      this.signup = !this.signup;
      this.login = false;
      this.message = "";
    },
    createAccount(email, password) {
      const account = {
        email,
        password,
      };
      axios
        .post("https://foodapp-api-41m2.onrender.com/signupAccount", account, {
          withCredentials: true,
        })
        .then((res) => {
          const message = res.data.message;

          if (message === "Email exists") {
            this.loadingState = false;
            this.message = "Account already exist, Login or Try another email";
          }
          if (res.data.token === undefined) {
            return console.log("Undefined");
          }
          localStorage.setItem("token", res.data.token);
          if (localStorage.getItem("token") === res.data.token) {
            this.isAuthenticated = true;
            this.tokenData = res.data.token;
          }
        })
        .catch((err) => {
          console.log(err.message);
        });
    },
    loginAccount(email, password) {
      const account = {
        email,
        password,
      };
      axios
        .post("https://foodapp-api-41m2.onrender.com/loginAccount", account, {
          withCredentials: true,
        })
        .then((res) => {
          const message = res.data.message;
          if (message === "Email does not exist") {
            this.message =
              "Email address does not exist... Try another email address or create a new account";
            this.loadingState = false;
          }
          if (message === "Incorrect password") {
            this.message =
              "Incorrect password entered.... Try another password or Create a new account";
            this.loadingState = false;
          }
          if (res.data.token === undefined) {
            return console.log("Undefined");
          }
          localStorage.setItem("token", res.data.token);

          if (localStorage.getItem("token") === res.data.token) {
            this.isAuthenticated = true;
            this.tokenData = res.data.token;
          }
        })
        .catch((err) => {
          console.log(err.message);
        });
    },
  },
  mounted() {
    const token = localStorage.getItem("token");
    if (token) {
      const tokenData = JSON.parse(atob(token.split(".")[1]));
      //atob is a built-in javascipt used to decodes a base64-encoded string
      const expirationTime = tokenData.exp * 1000;
      if (expirationTime > Date.now()) {
        console.log("Token is still valid");
        this.isAuthenticated = true;
        this.tokenData = token;
      } else {
        console.log("Token has expired");
        this.isAuthenticated = false;
      }
    } else {
      console.log("Token not found");
      this.isAuthenticated = false;
    }
  },
};
</script>

<style scoped>
#account-page {
  width: 100vw;
  width: 100dvw;
  height: calc(100vh - 144px);
  height: calc(100dvh - 144px);
  padding: 20px;
  background-color: var(--color3);
  display: flex;
  align-content: center;
  justify-content: center;
}
#account-page > div {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  height: 100%;
  padding: 30px;
}
#account-page > div > div {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  height: 100%;
  padding: 30px;
}
#account-page > div .title {
  height: 30%;
}
#account-page > div .title h1 {
  font-size: 4rem;
  color: var(--color2);
  white-space: nowrap;
}
#account-page > div .title div {
  display: flex;
  flex-direction: row;
  gap: 30px;
}
#account-page > div .title button {
  padding: 10px 15px;
  background-color: transparent;
  cursor: pointer;
  border: 2px solid var(--color2);
  position: relative;
  border-radius: 15px;
  overflow: hidden;
  transition: 2000ms;
  z-index: 4;
}
#account-page > div .title button .first {
  background-color: #3a1a1a;
  position: absolute;
  top: 0;
  right: 0;
  height: 100%;
  width: 0;
  z-index: 3;
  transition: 1500ms;
}
#account-page > div .title button .second {
  background-color: #3a1a1a;
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 0;
  z-index: 3;
  transition: 1500ms;
}
#account-page > div .title button:hover p {
  position: relative;
  z-index: 7;
  color: var(--color3);
}
#account-page > div .title button:hover span {
  width: 100%;
}
@media screen and (max-width: 674px) {
  #account-page > div .title h1 {
    font-size: 2rem;
  }
  #account-page > div .login-signup {
    width: 80%;
  }
}
@media screen and (max-width: 337px) {
  #account-page > div .title h1 {
    font-size: 1rem;
  }
}
</style>
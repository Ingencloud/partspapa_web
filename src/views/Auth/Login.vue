<template>
  <div class="">
    <div class="flex w-full">
      <div class="left-panel hidden md:block relative">
        <!-- <div class="cta-info">
          this is a test
        </div> -->
        <div class="img_overlay"></div>
        <img src="@/assets/img/hero2.png" class="res-img w-full" alt="" />
      </div>
      <div class="w-full flex place-content-center m-auto p-[65px]">
        <div class="form text-left w-[500]">
          <p class="info text-grey text-base">Welcome back! 👋</p>
          <h1 class="font-bold mb-8 text-md">Login to your account</h1>
          <form @submit.prevent="login" class="my-10" method="POST">
            <div class="form-group flex flex-col">
              <label for="email" class="font-semibold mb-1">Email:</label>
              <input
                type="email"
                class="form-control bg-grey outline-none"
                id="email"
                v-model="email"
                placeholder="Please enter your email"
              />
            </div>
            <div class="form-group flex flex-col">
              <label for="password" class="font-semibold mb-1">Password:</label>
              <input
                type="password"
                class="form-control bg-grey outline-none"
                id="password"
                v-model="password"
                placeholder="Enter Password"
              />
            </div>
            <button
              type="submit"
              name="action"
              class="btn bg-secondary w-full text-white font-bold"
            >
              Login
            </button>
            <a href="" class="text-primary flex">Forgot password?</a>
          </form>
          <div class="line w-full relative">
            <p class="option text-center">or</p>
          </div>
          <p class="info mb-2">Login using</p>
          <!-- google button -->
          <div class="flex justify-center">
            <button class="btn w-full text-grey-dark font-bold g-btn">
              <span class="flex text-center place-content-center">
                <img src="@/assets/img/google-auth.png" class="mr-3" alt="" />
                <p>Google</p>
              </span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { getAPI } from "@/utils/apis/axios";

export default {
  name: "Home",
  data() {
    return {
      img_id: 1,
      email: "",
      password: "",
    };
  },
  methods: {
    // generate random numbers 1 to 3 every 10 seconds
    randomNumber() {
      this.img_id = Math.floor(Math.random() * 2) + 1;
    },

    // trigger random number evry 10 seconds recursively
    randomNumberInterval() {
      setInterval(() => {
        this.randomNumber();
      }, 10000);
    },

    // login user
    login() {
      const data = {
        email: this.email,
        password: this.password,
      };
      getAPI.post("/api-token/", data).then((res) => {
        // if response is successfully logged in
        if (res.status === 200) {
          // store token in local storage
          localStorage.setItem("token", res.data.token);
          // redirect to dashboard
          this.$router.push("/");
        }
      });
    },
  },
  mounted() {
    this.randomNumberInterval();
  },
};
</script>

<style scoped>
.cta-info {
  position: absolute;
  width: 500px;
  height: 200px;
  left: 50%;
  top: 75%;
  transform: translate(-50%, -50%);

  background: rgba(255, 242, 242, 0.3);
  mix-blend-mode: normal;
  backdrop-filter: blur(100px);
  /* Note: backdrop-filter has minimal browser support */

  border-radius: 10px;
  z-index: 10;
}

.img_overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
}

.left-panel {
  width: 100%;
}
.res-img {
  width: 100%;
  height: 100vh;
}

.form {
  width: 420px;
}

.form-group input {
  border: 1px solid #d8d8d8;
  border-radius: 5px;
  padding: 10px;
  margin-bottom: 30px;
  gap: 12px;
}

.line {
  width: 100%;
  height: 1px;
  background-color: #d8d8d8;
  margin: 30px 0;
}

button {
  border-radius: 5px;
  padding: 10px;
  margin-bottom: 20px;
  margin-top: 10px;
}

.option {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: -13px;
  background-color: #fff;
  width: 40px;
}

.btn {
  cursor: pointer;
}

.g-btn {
  box-shadow: 0px 3px 9px 2px rgba(0, 0, 0, 0.1);
  -webkit-box-shadow: 0px 3px 9px 2px rgba(0, 0, 0, 0.1);
  -moz-box-shadow: 0px 3px 9px 2px rgba(0, 0, 0, 0.1);
}
</style>

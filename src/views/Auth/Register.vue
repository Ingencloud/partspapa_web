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
          <p class="info text-grey text-base">Hello There! 👋</p>
          <h1 class="font-bold mb-8 text-md">Create an account</h1>
          <form @submit.prevent="register" class="my-10">
            <div class="form-group flex flex-col">
              <label for="f_name" class="font-semibold mb-1">First Name:</label>
              <input
                type="name"
                class="form-control bg-grey outline-none"
                id="f_name"
                v-model="f_name"
                placeholder="Please enter your First Name"
              />
            </div>
            <div class="form-group flex flex-col">
              <label for="f_name" class="font-semibold mb-1">Last Name:</label>
              <input
                type="name"
                class="form-control bg-grey outline-none"
                id="l_name"
                v-model="l_name"
                placeholder="Please enter your Last Name"
              />
            </div>
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
            <div class="form-group flex flex-col">
              <label for="password" class="font-semibold mb-1"
                >Confirm Password:</label
              >
              <input
                type="password"
                class="form-control bg-grey outline-none"
                id="password"
                v-model="c_password"
                placeholder="Confirm Password"
              />
            </div>
            <button
              type="submit"
              class="btn bg-secondary w-full text-white font-bold"
            >
              Register
            </button>
          </form>
          <p>
            Already have and account?
            <router-link to="/login" tag="a" class="text-primary"
              >Login</router-link
            >
          </p>
          <!-- <div class="line w-full relative">
            <p class="option text-center">or</p>
          </div>
          <p class="info mb-1">Register with</p>
          <div class="flex justify-center">
            <button class="btn w-full text-grey-dark font-bold g-btn">
              <span class="flex text-center place-content-center">
                <img src="@/assets/img/google-auth.png" class="mr-3" alt="" />
                <p>Google</p>
              </span>
            </button>
          </div> -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { getAPI } from "@/utils/apis/axios";
// @ is an alias to /src=
export default {
  name: "Home",
  data() {
    return {
      img_id: 1,
      email: "",
      password: "",
      f_name: "",
      l_name: "",
      c_password: "",
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

    // register user
    register() {
      // check if passwords match
      if (this.password !== this.c_password) {
        alert("Passwords do not match");
        return;
      } else {
        const data = {
          firstname: this.f_name,
          lastname: this.l_name,
          email: this.email,
          password: this.password,
          roles: 'customer'
        };
        getAPI.post("/api/users/register/", data).then((res) => {
          // if status is 20
        });
      }
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

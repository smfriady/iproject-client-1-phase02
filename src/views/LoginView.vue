<script>
import { mapActions } from "pinia";
import { useGlobalStore } from "../stores/globalStore";

import FooterVue from "../components/Footer.vue";
import NavbarVue from "../components/Navbar.vue";
export default {
  name: "LoginVue",
  components: {
    NavbarVue,
    FooterVue,
  },
  data: () => ({
    credential: {
      email: "",
      password: "",
    },
  }),
  methods: {
    ...mapActions(useGlobalStore, ["loginUser", "signInGoogle", "loginGithub"]),
  },
  created() {
    const { code } = this.$route.query;
    if (code) {
      this.loginGithub(code);
    }
  },
};
</script>

<template>
  <NavbarVue />
  <div class="grid grid-cols-1 container mx-auto p-10 gap-5">
    <main class="mx-auto">
      <div class="flex flex-col md:flex-row gap-5">
        <div class="flex justify-between flex-col">
          <div class="text-left">
            <h1 class="text-xl text-center md:text-left text-gray-900 mb-6">
              <span class="font-bold">Continue</span> Study, Finish your
              <span class="font-bold">Goals</span>
            </h1>
          </div>

          <div class="flex flex-col mb-4">
            <GoogleLogin v-bind:callback="signInGoogle" />
          </div>
          <div class="flex flex-col mb-4">
            <a
              href="https://github.com/login/oauth/authorize?client_id=6757ba3f3ba6aa0987e6&redirect_uri=https://iproject-phase02.web.app/login&scope=user:email"
              class="bg-orange-500 hover:bg-orange-400 transition-all duration-200 focus:outline-none shadow-inner text-white px-6 py-3 mt-4 w-full text-center"
            >
              Login via github
            </a>
          </div>
          <form @submit.prevent="loginUser(credential)">
            <div class="flex flex-col mb-4">
              <label htmlFor="email" class="text-lg mb-2">
                Email Address
              </label>
              <input
                v-model="credential.email"
                name="email"
                type="email"
                class="bg-white focus:outline-none border w-full px-4 py-3 border-gray-600 focus:border-teal-500"
                placeholder="Your email address ..."
              />
            </div>

            <div class="flex flex-col mb-4">
              <label htmlFor="password" class="text-lg mb-2">Password </label>
              <input
                v-model="credential.password"
                name="password"
                type="password"
                class="bg-white focus:outline-none border w-full px-4 py-3 border-gray-600 focus:border-teal-500"
                placeholder="Your password ..."
              />
            </div>

            <button
              type="submit"
              class="bg-orange-500 hover:bg-orange-400 transition-all duration-200 focus:outline-none shadow-inner text-white px-6 py-3 mt-4 w-full"
            >
              Masuk
            </button>
          </form>
        </div>
      </div>
    </main>
  </div>
  <FooterVue />
</template>

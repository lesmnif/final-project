<template>
  <div class="flex min-h-screen py-10">
    <div
      class="flex flex-1 flex-col justify-center py-12 px-4 sm:px-6 lg:flex-none lg:px-20 xl:px-24"
    >
      <p class="flex justify-center">
        <img class="h-28 w-auto" src="/Logo.png" alt="Your Company" />
      </p>

      <div class="mx-auto w-full max-w-sm lg:w-96">
        <div>
          <h2
            class="mt-6 text-3xl font-bold tracking-tight text-gray-900 text-center"
          >
            Log In to GID!
          </h2>
          <h1 class="mt-2 text-center">
            Organize your tasks and get stuff done!
          </h1>
        </div>

        <div class="mt-8">
          <p v-if="errorMsg" class=" text-sm font-semibold text-center text-red-500">
              {{ errorMsg }}
            </p>
          <div class="mt-6">
           
            <form @submit.prevent="signIn" class="space-y-6">
              <div>
                <label
                  for="email"
                  class="block text-sm font-medium text-gray-700"
                  >Email address</label
                >
                <div class="mt-1">
                  <input
                    type="email"
                    placeholder="example@mail.com"
                    v-model="email"
                    id="email"
                    class="block w-full appearance-none rounded-md border border-gray-300 px-3 py-2 placeholder-gray-400 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm"
                  />
                </div>
              </div>

              <div class="space-y-1">
                <label
                  for="password"
                  class="block text-sm font-medium text-gray-700"
                  >Password</label
                >
                <div class="mt-1">
                  <input
                    :type="passwordFieldType"
                    onpaste="return false"
                    placeholder="************"
                    v-model="password"
                    id="password"
                    class="block w-full appearance-none rounded-md border border-gray-300 px-3 py-2 placeholder-gray-400 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm"
                  />
                </div>
              </div>
              <div>
                <button
                  type="submit"
                  class="flex w-full justify-center rounded-md border border-transparent bg-indigo-600 py-2 px-4 text-sm font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                >
                  Sign in
                </button>
              </div>
              <div class="text-center text-sm font-semibold">
                Don't have an account ?
                <PersonalRouter :route="route" :buttonText="buttonText" />
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
    <div class="relative hidden sm:block w-0 flex-1">
      <img
        class="absolute inset-0 h-full w-full object-cover rounded-r-xl"
        src="/ImageHero.jpg"
        alt=""
      />
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue"
import PersonalRouter from "./PersonalRouter.vue"
import { supabase } from "../supabase"
import { useRouter } from "vue-router"
import { useUserStore } from "../stores/user"
import { storeToRefs } from "pinia"
import toast from "react-hot-toast"
// Route Variables
const route = "/auth/sign-up"
const buttonText = "Sign up"
// Input Fields
const email = ref("")
const password = ref("")
// Error Message
const errorMsg = ref("")
//Show hide password variables
const passwordFieldType = computed(() =>
  hidePassword.value ? "password" : "text"
)
const hidePassword = ref(true)
// Router to push user once SignedIn to the HomeView
const redirect = useRouter()
// Arrow function to Signin user to supaBase
const signIn = async () => {
  try {
    // calls the user store and send the users info to backend to logIn
    await useUserStore().signIn(email.value, password.value)
    // redirects user to the homeView
    redirect.push({ path: "/" })
  } catch (error) {
    toast.error(error.message)
    // displays error message
    errorMsg.value = `Error: ${error.message}`
    // hides error message
    setTimeout(() => {
      errorMsg.value = null
    }, 5000)
  }
}
</script>

<style></style>

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
            Register to GID!
          </h2>
          <h1 class="mt-2 text-center">
            Organize your tasks and get stuff done!
          </h1>
        </div>

        <div class="mt-8">
          <p v-if="errorMsg" class=" text-sm font-semibold text-center text-red-500">
              {{ errorMsg }}
            </p>
            <p v-if="successMsg" class=" text-sm font-semibold text-center text-green-500">
              {{ successMsg }}
            </p>
          <div class="mt-6">
            <form @submit.prevent="signUp" class="space-y-6">
              <div>
                <label
                  for="email"
                  class="block text-sm font-medium text-gray-700"
                  >Email address</label
                >
                <div class="mt-1">
                  <input
                    type="email"
                    placeholder="dave@wuTangfinancial.com"
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
                    type="password"
                    placeholder="************"
                    v-model="password"
                    id="password"
                    class="block w-full appearance-none rounded-md border border-gray-300 px-3 py-2 placeholder-gray-400 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm"
                  />
                </div>
              </div>
              <div class="space-y-1">
                <label
                  for="password"
                  class="block text-sm font-medium text-gray-700"
                  >Confirm Password</label
                >
                <div class="mt-1">
                  <input
                    type="password"
                    placeholder="************"
                    v-model="confirmPassword"
                    id="confirmPassword"
                    class="block w-full appearance-none rounded-md border border-gray-300 px-3 py-2 placeholder-gray-400 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm"
                  />
                </div>
              </div>
              <div>
                <button
                  type="submit"
                  class="flex w-full justify-center rounded-md border border-transparent bg-indigo-600 py-2 px-4 text-sm font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                >
                  Sign up
                </button>
              </div>
              <div class="text-center text-sm font-semibold">
                Have an account ?
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
import { ref } from "vue"
import { useRouter } from "vue-router"
import PersonalRouter from "./PersonalRouter.vue"
import { useUserStore } from "../stores/user"
import { supabase } from "../supabase";
// Route Variables
const route = "/auth/login"
const buttonText = "Log In"
// Input Fields
const email = ref(null)
const password = ref(null)
const confirmPassword = ref(null)
const errorMsg = ref(null)
const successMsg = ref(null)
// Error Message
// Show hide password variable
// Show hide confrimPassword variable
// Router to push user once SignedUp to Log In
const redirect = useRouter()
// function to SignUp user to supaBase with a timeOut() method for showing the error
async function signUp() {
  if (password.value === confirmPassword.value) {
    try {
      await useUserStore().signUp(email.value, password.value)
      successMsg.value = "Validate your confirm signup link and Log In!"
      setTimeout(() =>{
        redirect.push({ path: "/auth/login" })
      }, 3000)
    } catch (error) {
      console.log("this is my error", error)
      errorMsg.value = error.message
      setTimeout(() => {
        errorMsg.value = null
      }, 5000)
    }
    return
  }
  errorMsg.value = "Passwords do not match"
  setTimeout(() => {
    errorMsg.value = null
  }, 5000)
}
</script>

<style></style>


<template>
  <!--
    This example requires updating your template:

    ```
    <html class="h-full bg-white">
    <body class="h-full">
    ```
  -->
  
    <div class="sm:mx-auto sm:w-full sm:max-w-sm">
      <img class="mx-auto h-10 w-auto" src="https://tailwindui.com/img/logos/mark.svg?color=indigo&shade=600" alt="Your Company" />
      <h2 class="mt-10 text-center text-2xl font-bold leading-9 tracking-tight text-gray-900">Register for free</h2>
    </div>
    <p class="mt-2 text-center text-sm text-gray-600">
        or
        {{''}}
        <router-link :to="{name: 'Login'}" class="font-medium text-indigo-600 hover:text-indigo-500" >
           Already have an account? Sign-in
        </router-link>
      </p>

    <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
      <Alert v-if="Object.keys(errors).length" class="flex-col items-stretch text-sm">
      <div v-for="(field, i) of Object.keys(errors)" :key="i">
        <div v-for="(error, ind) of errors[field] || []" :key="ind">
          * {{ error }}
        </div>
      </div>
    </Alert>
      <form class="space-y-6" @submit="register">
        <div>
          <label for="fullname" class="block text-sm font-medium leading-6 text-gray-900">Full Name</label>
          <div class="mt-2">
            <input id="fullname" name="name" type="text" autocomplete="name" required="" v-model="user.name" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
          </div>
        </div>
        <div>
          <label for="email" class="block text-sm font-medium leading-6 text-gray-900">Email address</label>
          <div class="mt-2">
            <input id="email" name="email" type="email" autocomplete="email" required="" v-model="user.email" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
          </div>
        </div>

        <div>
          <div class="flex items-center justify-between">
            <label for="password" class="block text-sm font-medium leading-6 text-gray-900">Password</label>
            <!-- <div class="text-sm">
              <a href="#" class="font-semibold text-indigo-600 hover:text-indigo-500">Forgot password?</a>
            </div> -->
          </div>
          <div class="mt-2">
            <input id="password" name="password" type="password" autocomplete="current-password" required="" v-model="user.password" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
          </div>
        </div>

        <div>
          <div class="flex items-center justify-between">
            <label for="password_confirmation" class="block text-sm font-medium leading-6 text-gray-900">Confirm Password</label>
            <!-- <div class="text-sm">
              <a href="#" class="font-semibold text-indigo-600 hover:text-indigo-500">Forgot password?</a>
            </div> -->
          </div>
          <div class="mt-2">
            <input id="password_confirmation" name="password_confirmation" type="password" autocomplete="current-password_confirmation" required="" v-model="user.password_confirmation" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
          </div>
        </div>

        <div>
          <button
        type="submit"
        :disabled="loading"
        class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
        :class="{
          'cursor-not-allowed': loading,
          'hover:bg-indigo-500': loading,
        }"
      >
        <span class="absolute left-0 inset-y-0 flex items-center pl-3">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-5 h-5">
  <path stroke-linecap="round" stroke-linejoin="round" d="M16.5 10.5V6.75a4.5 4.5 0 1 0-9 0v3.75m-.75 11.25h10.5a2.25 2.25 0 0 0 2.25-2.25v-6.75a2.25 2.25 0 0 0-2.25-2.25H6.75a2.25 2.25 0 0 0-2.25 2.25v6.75a2.25 2.25 0 0 0 2.25 2.25Z" />
</svg>
        </span>
        <svg
          v-if="loading"
          class="animate-spin -ml-1 mr-3 h-5 w-5 text-white"
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
        >
          <circle
            class="opacity-25"
            cx="12"
            cy="12"
            r="10"
            stroke="currentColor"
            stroke-width="4"
          ></circle>
          <path
            class="opacity-75"
            fill="currentColor"
            d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
          ></path>
        </svg>
        Sign up
      </button>
        </div>
      </form>

      <!-- <p class="mt-10 text-center text-sm text-gray-500">
        Not a member?
        {{ ' ' }}
        <a href="#" class="font-semibold leading-6 text-indigo-600 hover:text-indigo-500">Start a 14 day free trial</a>
      </p> -->
    </div>
  
</template>

<script setup>
import store from '../store/index.js';
import { useRouter } from 'vue-router';
import { ref } from "vue";
import Alert from "../components/Alert.vue";
const loading = ref(false);
const errors = ref({});

const router =useRouter();
const user ={
  name:'',
  email:'',
  password:'',
  password_confirmation:'',
};

function register(ev) {
  ev.preventDefault();
  loading.value = true;
  store
    .dispatch("register", user)
    .then(() => {
      loading.value = false;
      router.push({
        name: "Dashboard",
      });
    })
    .catch((error) => {
      loading.value = false;
      if (error.response.status === 422) {
        errors.value = error.response.data.errors;
      }
    });
}

</script>





<template>
    <div class="sm:mx-auto sm:w-full sm:max-w-sm">
        <img class="mx-auto h-10 w-auto" src="https://tailwindui.com/img/logos/mark.svg?color=indigo&shade=600" alt="Your Company" />
        <h2 class="mt-10 text-center text-2xl font-bold leading-9 tracking-tight text-gray-900">Sign in to your account</h2>
      </div>
  
      <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
        <form class="space-y-6" @submit.prevent="login" method="POST">
          <div v-if="errorMsg" class="py-3 px-5 bg-red-500 text-white rounded flex items-center justify-between">
            {{ errorMsg }}
            <span @click="errorMsg = ''" class="cursor-pointer transition-colors hover:bg-[rgba(0,0,0,0.2)] w-8 h-8 rounded-full flex items-center justify-center">
              X
            </span>
          </div>
          <div>
            <label for="email" class="block text-sm font-medium leading-6 text-gray-900">Email address</label>
            <div class="mt-2">
              <input id="email" name="email" type="email" autocomplete="email" v-model="user.email" required class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
            </div>
          </div>
  
          <div>
            <div class="flex items-center justify-between">
              <label for="password" class="block text-sm font-medium leading-6 text-gray-900">Password</label>
              <div class="text-sm">
                <a href="#" class="font-semibold text-indigo-600 hover:text-indigo-500">Forgot password?</a>
              </div>
            </div>
            <div class="mt-2">
              <input id="password" name="password" type="password" v-model="user.password" autocomplete="current-password" required class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
            </div>
          </div>
  
          <div>
            <button type="submit" class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Sign in</button>
          </div>
        </form>
  
        <p class="mt-10 text-center text-sm text-gray-500">
          Not a member?
          {{ ' ' }}
          <router-link :to="{ name: 'Register' }" class="font-semibold leading-6 text-indigo-600 hover:text-indigo-500">Register now!</router-link>
        </p>
      </div>
  </template>
  
<script setup>
import { useRouter } from 'vue-router';
import store from '../store';
import { ref } from 'vue';

const errorMsg = ref('');

const router = useRouter();

const user = {
  email: '',
  password: ''
}

function login() {
  store.dispatch('login', user)
  .then(() => {
    router.push({
      name: 'Dashboard'
    })
  })
  .catch(err => {
    errorMsg.value = err.response.data.error;
  })
}

</script>

<style scoped>
</style>

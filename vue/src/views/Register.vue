<template>
  <div class="sm:mx-auto sm:w-full sm:max-w-sm">
    <img class="mx-auto h-10 w-auto" src="https://tailwindui.com/img/logos/mark.svg?color=indigo&shade=600"
      alt="Your Company" />
    <h2 class="mt-10 text-center text-2xl font-bold leading-9 tracking-tight text-gray-900">Create your account for free!
    </h2>
  </div>

  <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
    <form class="space-y-6" @submit.prevent="register" method="POST">
      <div>
        <label for="name" class="block text-sm font-medium leading-6 text-gray-900">Name</label>
        <div class="mt-2">
          <input id="name" name="name" type="text" autocomplete="name" required @input="nameError = ''" v-model="user.name"
            class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
          <ul v-if="nameError" class="px-5">
            <li v-for="error in nameError" class="text-red-600 text-sm list-disc">{{ error }}</li>
          </ul>
        </div>
      </div>

      <div>
        <label for="email" class="block text-sm font-medium leading-6 text-gray-900">Email address</label>
        <div class="mt-2">
          <input id="email" name="email" type="email" autocomplete="email" required @input="emailError = ''" v-model="user.email"
            class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
          <ul v-if="emailError" class="px-5">
            <li v-for="error in emailError" class="text-red-600 text-sm list-disc">{{ error }}</li>
          </ul>
        </div>
      </div>

      <div>
        <label for="password" class="block text-sm font-medium leading-6 text-gray-900">Password</label>
        <div class="mt-2">
          <input id="password" name="password" type="password" @input="passwordError = ''" autocomplete="current_password" required
            v-model="user.password"
            class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
          <ul v-if="passwordError" class="px-5">
            <li v-for="error in passwordError" class="text-red-600 text-sm list-disc">{{ error }}</li>
          </ul>
        </div>
      </div>

      <div>
        <label for="password_confirmation" class="block text-sm font-medium leading-6 text-gray-900">Password
          Confirmation</label>
        <div class="mt-2">
          <input id="password_confirmation" name="password_confirmation" type="password"
            autocomplete="current_password_confirmation" required @input="passwordError = ''" v-model="user.password_confirmation"
            class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
          <ul v-if="passwordError" class="px-5">
            <li v-for="error in passwordError" class="text-red-600 text-sm list-disc">{{ error }}</li>
          </ul>
        </div>
      </div>

      <div>
        <button type="submit"
          class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Sign
          Up</button>
      </div>
    </form>

    <p class="mt-10 text-center text-sm text-gray-500">
      Already a member?
      {{ ' ' }}
      <router-link :to="{ name: 'Login' }" class="font-semibold leading-6 text-indigo-600 hover:text-indigo-500">Log
        In!</router-link>
    </p>
  </div>
</template>

<script setup>

import store from '../store';
import { useRouter } from 'vue-router';
import { ref } from 'vue';

const router = useRouter();

const nameError = ref('');
const emailError = ref('');
const passwordError = ref('');

const user = {
  name: '',
  email: '',
  password: '',
  password_confirmation: '',
}

function register() {
  store.dispatch('register', user)
    .then(() => {
      router.push({
        name: 'Dashboard'
      })
    })
    .catch(err => {
      nameError.value = err.response.data.errors.name ?? null;
      emailError.value = err.response.data.errors.email ?? null;
      passwordError.value = err.response.data.errors.password ?? null;
    })
}
</script>

<style scoped></style>
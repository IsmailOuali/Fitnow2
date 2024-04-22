<template>
  <div class="bg-black">
    <nav class="flex justify-between items-center p-5 bg-cyan-700">
      <div>
        <h1 class="font-bold text-gray-50 text-2xl">{{ title }}</h1>
      </div>
      <div class="flex justify-center items-center">
        <router-link to="/progress_list" class="text-gray-50 mx-2">
          Progress list
        </router-link>
        <router-link to="/add_progress" class="text-gray-50 mx-2">
          Add progress
        </router-link>
        <router-link to="/Register" class="text-gray-50 mx-2">
          Register
        </router-link>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  name: "mainHeader",
  props: {
    title: String,
  },
};
</script>

<template>
  <div class="bg-black">
    <h1 class="text-white text-gray-50">Add progress</h1>
  </div>
  <div class="container">
    <div class="flex h-screen bg-yellow-100">
      <div class="m-auto">
        <div>
          <div class="mt-5 bg-orange-200 rounded-lg shadow">
            <div class="flex">
              <div class="flex-1 py-5 pl-5 overflow-hidden">
                <h1 class="inline text-2xl font-semibold leading-none">
                  Add Progress
                </h1>
              </div>
            </div>
            <div
              class="bg-red-700 rounded-2xl px-4 py-2 w-3/4 m-auto my-2"
              v-if="errors.length != 0"
            >
              <ul>
                <li v-for="(error, index) in errors" :key="index">
                  {{ error }}
                </li>
              </ul>
            </div>
            <form class="px-5 pb-5" @submit.prevent="saveProgress">
              <fieldset>
                <input
                  placeholder="title"
                  v-model="Progress.title"
                  class="text-black placeholder-gray-400 w-full px-4 py-2.5 mt-2 text-base transition duration-500 ease-in-out transform border-transparent rounded-lg bg-gray-200 focus:border-blueGray-500 focus:bg-white dark:focus:bg-gray-500 focus:outline-none focus:shadow-outline focus:ring-2 ring-offset-current ring-offset-2 ring-gray-400"
                />
                <div class="flex">
                  <div class="flex-grow w-1/4 pr-2">
                    <input
                      placeholder="weight"
                      v-model="Progress.weight"
                      type="number"
                      class="text-black placeholder-gray-600 w-full px-4 py-2.5 mt-2 text-base transition duration-500 ease-in-out transform border-transparent rounded-lg bg-gray-200 focus:border-blueGray-500 focus:bg-white dark:focus:bg-gray-500 focus:outline-none focus:shadow-outline focus:ring-2 ring-offset-current ring-offset-2 ring-gray-400"
                    />
                  </div>
                  <div class="flex-grow">
                    <input
                      placeholder="size"
                      v-model="Progress.size"
                      type="number"
                      class="text-black placeholder-gray-600 w-full px-4 py-2.5 mt-2 text-base transition duration-500 ease-in-out transform border-transparent rounded-lg bg-gray-200 focus:border-blueGray-500 focus:bg-white dark:focus:bg-gray-500 focus:outline-none focus:shadow-outline focus:ring-2 ring-offset-current ring-offset-2 ring-gray-400"
                    />
                  </div>
                </div>
                <button
                  type="submit"
                  class="bg-orange-600 py-3 px-7 rounded-2xl my-2 hover:bg-orange-400"
                >
                  Add
                </button>
              </fieldset>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "AddProgress",
  data() {
    return {
      Progress: {},
      title: "",
      weight: "",
      size: "",
      errors: [],
    };
  },
  methods: {
    async saveProgress() {
      //   console.log(this.Progress.size);
      this.errors = [];
      if (!this.Progress.title) {
        this.errors.push("title is required");
      }
      if (!this.Progress.weight) {
        this.errors.push("weight is required");
      }
      if (!this.Progress.size) {
        this.errors.push("size is required");
      }
      if (!this.errors.length) {
        var formData = new FormData();

        formData.append("title", this.Progress.title);
        formData.append("weight", this.Progress.weight);
        formData.append("size", this.Progress.size);
        const token = localStorage.getItem("token");
        console.log(token);
        const config = {
          headers: { Authorization: `Bearer ${token}` },
        };
        let url = "http://127.0.0.1:5000/api/progress";
        await axios
          .post(url, formData, config)
          .then((Response) => {
            console.log("naaadeee");
            if (Response.status == 200) {
              alert(Response.data.message);
            }
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },
  },
};
</script>

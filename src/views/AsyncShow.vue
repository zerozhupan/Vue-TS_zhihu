<template>
  <!-- <h2>{{ result }}</h2> -->
  <h2>供suspense组件使用</h2>
  <img :src="result && result.message" />
</template>
<script lang="ts">
import { defineComponent } from "vue";
import axios from "axios";
export default defineComponent({
  name: "AysncShow",
  async setup() {
    const rawData = await axios.get("https://dog.ceo/api/breeds/image/random");
    return {
      result: rawData.data,
    };

    // return new Promise((resolve) => {
    //   setTimeout(() => {
    //     return resolve({
    //       result: "asyncShow",
    //     });
    //   }, 3000);
    // });
  },
});
</script>
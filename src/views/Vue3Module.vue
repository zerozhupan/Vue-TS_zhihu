<template>
  <h2>鼠标移动事件</h2>
  <h3>X: {{ x }}</h3>
  <h3>Y: {{ y }}</h3>
  <div>
    <h2>axios请求图片</h2>
    <h3 v-if="loading">loading...</h3>
    <img v-if="loaded" :src="result.message" />
  </div>
</template>
<script lang="ts">
import { defineComponent, ref, onMounted, onUnmounted } from "vue";
import useMousePosition from "@/hooks/useMouseposition";
import useURLLoader from "@/hooks/useURLLoaders";
export default defineComponent({
  name: "Vue3Module",
  components: {},
  setup() {
    const { x, y } = useMousePosition();

    const { result, loading, error, loaded } = useURLLoader(
      "https://dog.ceo/api/breeds/image/random"
    );
    return {
      x,
      y,
      result,
      loading,
      loaded,
    };
  },
});
</script>
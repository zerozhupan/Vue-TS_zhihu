<template>
  <h2>鼠标移动事件</h2>
  <h3>X: {{ x }}</h3>
  <h3>Y: {{ y }}</h3>
  <div>
    <h2>axios请求图片</h2>
    <h3 v-if="loading">loading...</h3>
    <img v-if="loaded" :src="result.message" />
    <modal />
  </div>
</template>
<script lang="ts">
import { defineComponent, ref, onMounted, onUnmounted, watch } from "vue";
import useMousePosition from "@/hooks/useMouseposition";
import useURLLoader from "@/hooks/useURLLoaders";
import Modal from "@/components/Modal.vue";

interface DogResult {
  message: string;
  status: string;
}
export default defineComponent({
  name: "Vue3Module",
  components: { Modal },
  setup() {
    const { x, y } = useMousePosition();
    const { result, loading, error, loaded } = useURLLoader<DogResult>(
      "https://dog.ceo/api/breeds/image/random"
    );
    watch(result, () => {
      if (result.value) console.log(result.value.message);
    });
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
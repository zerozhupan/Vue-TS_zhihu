<template>
  <h2>鼠标移动事件</h2>
  <h3>X: {{ x }}</h3>
  <h3>Y: {{ y }}</h3>
  <div>
    <h2>axios请求图片</h2>
    <h3 v-if="loading">loading...</h3>
    <img v-if="loaded" :src="result.message" />
  </div>
  <hr />
  <p>{{ error_sus }}</p>
  <suspense>
    <template #default>
      <aysnc-show />
    </template>
    <template #fallback>
      <h2>loading!...</h2>
    </template>
  </suspense>
</template>
<script lang="ts">
import {
  defineComponent,
  ref,
  onMounted,
  onUnmounted,
  watch,
  onErrorCaptured,
} from "vue";
import useMousePosition from "@/hooks/useMouseposition";
import useURLLoader from "@/hooks/useURLLoaders";
import AysncShow from "./AsyncShow.vue";

interface DogResult {
  message: string;
  status: string;
}
export default defineComponent({
  name: "Vue3Module",
  components: { AysncShow },
  setup() {
    // 错误抓取
    let error_sus = ref(null);
    onErrorCaptured((e: any) => {
      error_sus.value = e;
      return true;
    });
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
      error_sus,
    };
  },
});
</script>
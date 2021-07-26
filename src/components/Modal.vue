<template>
  <teleport to="body">
    <div id="center">对话框</div>
  </teleport>
</template>
<script lang="ts">
import { defineComponent, ref, onMounted, onUnmounted, watch } from "vue";

interface DogResult {
  message: string;
  status: string;
}
export default defineComponent({
  name: "Modal",
  components: {},
});
</script>

<style lang="css">
#center {
  height: 200px;
  width: 200px;
  border: 2px solid salmon;
  background-color: #fff;
  position: relative;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
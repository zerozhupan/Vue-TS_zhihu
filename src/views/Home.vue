<template>
  <div>
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <h1>
      使用ref
      <h4>{{ count }}</h4>
      <h4>{{ double }}</h4>
    </h1>
    <button @click="increase">+1</button>
    <h1>
      使用reactive
      <!-- <h2>{{ data.count1 }}</h2> -->
      <h4>{{ count1 }}</h4>
      <h4>{{ double_Rea }}</h4>
    </h1>
    <button @click="increase_Rea">+1</button>
  </div>
  <!-- 数组列表和对象 -->
  <div>
    <ul>
      <li v-for="(item, index) in numbers" :key="index">{{ item }}</li>
    </ul>
  </div>
  <div>
    <h4>观测响应式{{ person.name }}</h4>
  </div>
</template>
<script lang="ts">
import {
  defineComponent,
  ref,
  computed,
  reactive,
  toRefs,
  toRef,
  watch,
} from "vue";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src
interface Dataprops {
  count1: number;
  increase_Rea: () => void;
  double_Rea: number;
  numbers: number[];
  person: {
    name?: string;
  };
}
export default defineComponent({
  name: "Home",
  components: {
    // HelloWorld,
  },
  setup() {
    const count = ref(0);
    // count是一个ref对象（ref对象中包裹着响应式数据），值是存在count.value中的，但是在标签内可以直接使用count，写一些方法处理count的时候要使用count.value
    const increase = () => {
      count.value++;
    };
    const double = computed(() => {
      return count.value * 2;
    });
    // 在computed中，使用data.count1会使类型推断出现问题，data就会被推断成any。最好是写一个interface接口来定义一下data的类型
    const data: Dataprops = reactive({
      count1: 0,
      increase_Rea: () => {
        data.count1++;
      },
      double_Rea: computed(() => data.count1 * 2),
      // 用数组和对象来试一试响应式
      numbers: [1, 2, 3],
      person: {},
    });
    data.numbers[0] = 5; // 可以响应式
    data.numbers.push(6);
    data.person.name = "xcm";

    // watch 的用法
    // 因为data是一个reactive对象，只写data的话，检测出来的值是proxy对象
    // watch(data, (newVal, oldVal) => {
    //   console.log(newVal);
    //   console.log(oldVal);
    // });
    // 使用箭头函数拿到里面的值
    watch(
      () => data.count1,
      (newVal, oldVal) => {
        console.log(newVal);
        console.log(oldVal);
      }
    );

    const refData = toRefs(data);
    // 要return出来
    return {
      count,
      increase,
      double,
      // data,使用data的话，模板中使用要用data.count，data.increse_Rea等等
      // 如何更简单的使用呢？使用toRefs
      ...refData,
    };
  },
});
</script>

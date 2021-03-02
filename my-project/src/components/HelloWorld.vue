<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button
      v-for="(item, index) in girls"
      :key="index"
      @click="selectGirlFun(index)"
    >
      {{item}}
    </button>

  <div v-if="selectGirls == ''">
    您还未进行选择
  </div>
  <div v-if="selectGirls !== ''">
    恭喜您，选择了我们的【{{selectGirls}}】为您服务！
  </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, reactive, toRefs } from 'vue';

export default ({
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  setup() {

    // const girls = ref(["小红", "小黄", "小白"]);
    // const selectGirls = ref("");
    // const selectGirlFun = (index: number) => {
    //   selectGirls.value = girls.value[index];
    // };

    // return {
    //   girls,
    //   selectGirls,
    //   selectGirlFun,
    // };

    const data = reactive({
      girls: ["小红", "小黄", "小白"],
      selectGirls: "",
      selectGirlFun: (index: number) => {
        data.selectGirls = data.girls[index]
      }
    })

    const refData = toRefs(data);

    return {
      ...refData
    }

  }
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

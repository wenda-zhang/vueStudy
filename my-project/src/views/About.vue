<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div>
      {{ time }}
    </div>
    <button @click="showTime">显示时间</button>
    <br />
    <div>
      <img v-if="loaded" :src="result.message" />
    </div>
  </div>
</template>

<script lang="ts">
import { ref } from "vue";
import useUrlAxios from "../hooks/useUrlaxios";

export default {
  name: "about",
  setup() {
    const time = ref("00:00:00");
    const showTime = () => {
      const timeNow = new Date();
      const hour =
        timeNow.getHours() < 10 ? "0" + timeNow.getHours() : timeNow.getHours();
      const minutes =
        timeNow.getMinutes() < 10
          ? "0" + timeNow.getMinutes()
          : timeNow.getMinutes();
      const seconds =
        timeNow.getSeconds() < 10
          ? "0" + timeNow.getSeconds()
          : timeNow.getSeconds();
      time.value = hour + ":" + minutes + ":" + seconds;
      setTimeout(showTime, 1000);
    };
    const { result, loading, loaded } = useUrlAxios(
      "https://dog.ceo/api/breeds/image/random"
    );

    return {
      time,
      showTime,
      result,
      loading,
      loaded,
    };
  },
};

</script>

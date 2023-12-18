<template>
  <div
    class="d-flex justify-content-end flex-wrap align-content-center"
    style="width: 95%; margin: 0 auto; height: 10vh; color: white"
  >
    <div class="d-flex justify-content-end mr-5">
      <div>聯絡我們：</div>
      <div>0999999999</div>
    </div>
    <div class="d-flex justify-content-end">
      <div>賣場連結：</div>
      <div
        class="ml-2 cursor"
        v-for="(item, index) in this.url"
        :key="index"
        @click="renderurl(item.url)"
      >
        {{ item.name }}
      </div>
    </div>

  </div>
</template>
<script>
export default {
  data() {
    return {
      contact: "0999999999",
      url: [
        {
          name: "IG",
          url: "https://www.youtube.com/watch?v=qORaYudQ7Zc&list=PLl_KIqd3w-Anc1-nYIiDbnsw2hdkpSeLh&index=1",
        },
        {
          name: "蝦皮",
          url: "https://www.youtube.com/watch?v=pXhjs-35jSI&list=PLl_KIqd3w-Anc1-nYIiDbnsw2hdkpSeLh&index=2",
        },
        {
          name: "PCHome",
          url: "https://www.youtube.com/watch?v=NnTEZCxhxF4&list=PLl_KIqd3w-Anc1-nYIiDbnsw2hdkpSeLh&index=3",
        },
      ],
    };
  },
  methods: {
    renderurl(url) {
      window.open(url);
    },
  },
  created() {},
};
</script>
<style scoped>
.cursor {
  cursor: pointer;
}
.cursor:hover {
  color: blue;
}
</style> 
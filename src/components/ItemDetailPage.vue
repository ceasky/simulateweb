<template>
  <b-modal ref="my-modal" size="lg" hide-footer hide-header>
    
      <div class="test" style="">
          <div style="min-height: 20rem; background-color: red">image</div>
          <div class="d-flex align-items-center" style="height: 5rem">
            <div class="col-8">商品名稱</div>
            <div class="col-2">商品價格</div>
            <div class="col-2">相關連結</div>
          </div>
          <div class="pl-3">
            <li style="list-style: none; height: 3rem" v-for="i in 5" :key="i">
              123132
            </li>
          </div>
          <div class="d-flex flex-wrap">
            <div
              v-for="i in 10"
              :key="i"
              class="col-4"
              style="background-color: yellow; height: 10rem"
            >
              image
            </div>
          </div>
        </div>

  </b-modal>
</template>
<script>
export default {
  data() {
    return {};
  },
  methods: {},
  created() {},
};
</script>
<style scoped>
</style> 
<template>
  <div
    class="d-flex justify-content-between flex-wrap align-content-center"
    style="width: 95%; margin: 0 auto; height: 10vh"
  >
    <div class="col-2">
      {{ ComName }}
    </div>
    <div class="d-flex justify-content-start col-8">
      <div class="cursor mr-2" v-for="(item, index) in ComType" :key="index">
        {{ item.CategoryName }}
      </div>
    </div>
    <div class="col-2 d-flex justify-content-end">
      <div class="cursor d-flex" style="font-size: 20px">
        <i class="fa-solid fa-magnifying-glass mr-3"></i>
        <i class="fa-brands fa-shopify mr-3"></i>
        <i class="fa-solid fa-user"></i>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    CompanyName: {
      type: String,
    },
    CompanyData: {
      type: Array,
    },
  },
  data() {
    return {
      ComName: "",
      ComType: [],
    };
  },
  methods: {
    //使用api 取得公司資訊
    GetComData() {
      this.ComName = this.CompanyName;
      this.ComType = this.CompanyData;
    },
  },
  created() {
    this.GetComData();
  },
};
</script>
<style scoped>
.cursor {
  cursor: pointer;
}
</style> 
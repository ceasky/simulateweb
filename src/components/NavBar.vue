<template>
  <div
    class="d-flex justify-content-between flex-wrap align-content-center"
    style="width: 95%; margin: 0 auto; height: 10vh; color: white"
  >
    <div class="col-2 d-flex cursor" @click="randerhomepage()">
      {{ CompanyImage }}

      {{ CompanyName }}
    </div>
    <div class="d-flex justify-content-start col-8">
      <!-- <div
        class="cursor mr-2"
        v-for="(item, index) in CompanyCategory"
        :key="index"
      >
        {{ item.CategoryName }}
      </div> -->
      <router-link
        class="routercss cursor mr-2"
        v-for="(item, index) in CompanyCategory"
        :key="index"
        :to="{ name: 'ItemsView', params: { id: item.CategoryId } }"
      >
        {{ item.CategoryName }}
      </router-link>
    </div>
    <div class="col-2 d-flex justify-content-end">
      <div class="cursor d-flex" style="font-size: 20px">
        <i class="fa-solid fa-magnifying-glass mr-3"></i>
        <!-- <i class="fa-brands fa-shopify mr-3"></i> -->
        <i class="fa-solid fa-user"></i>
      </div>
    </div>
  </div>
</template>
<script>
const GetApiData = {
  CompanyName: "公司名稱",
  CompanyImage: "公司logo",
  CompanyCategory: [
    {
      CategoryId: "0",
      CategoryName: "產品類型1",
    },
    {
      CategoryId: "1",
      CategoryName: "產品類型2",
    },
    {
      CategoryId: "2",
      CategoryName: "產品類型3",
    },
    {
      CategoryId: "3",
      CategoryName: "產品類型4",
    },
  ],
};
export default {
  data() {
    return {
      CompanyName: "",
      CompanyImage: "",
      CompanyCategory: [],
    };
  },
  methods: {
    GetCompanyDataApi() {
      this.CompanyName = GetApiData.CompanyName;
      this.CompanyImage = GetApiData.CompanyImage;
      this.CompanyCategory = GetApiData.CompanyCategory;
    },
    randerhomepage(){
        this.$router.push('/')
    }
  },
  created() {
    this.GetCompanyDataApi();
  },
};
</script>
<style scoped>
.cursor {
  cursor: pointer;
}
.routercss{
  color:white;
  text-decoration: none;
}
</style> 
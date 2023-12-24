<template>
  <div
    class="d-flex flex-wrap"
    style="width: 95%; height: 10vh; color: white; align-items: center"
  >
    <div
      class="col-3 d-flex cursor"
      style="align-items: center"
      @click="randerhomepage()"
    >
      <div class="mr-2">
        <img class="logoimage" src="@/assets/company/logo.jpg" alt="圖片描述" />
      </div>
      <div style="font-size: 2rem">
        {{ CompanyName }}
      </div>
    </div>
    <div class="d-flex justify-content-start col-8">
      <router-link
        class="routercss cursor mr-2"
        v-for="(item, index) in Category"
        :key="index"
        :to="{ name: 'ItemsView', params: { id: item.CategoryId } }"
      >
        {{ item.CategoryName }}
      </router-link>
    </div>
    <div class="col-1 d-flex justify-content-end">
      <div class="cursor d-flex justify-content-end" style="font-size: 20px">
        <!-- <i class="fa-solid fa-magnifying-glass mr-3"></i> -->
        <router-link
          class="routercss cursor mr-2"
          :to="{ name: 'ItemsView', params: { id: 'all' } }"
        >
          <i class="fa-solid fa-magnifying-glass mr-3"></i>
        </router-link>
        <!-- <i class="fa-brands fa-shopify mr-3"></i> -->
        <!-- <i class="fa-solid fa-user"></i> -->
      </div>
    </div>
  </div>
</template>
<script>
import commonData from "@/common/companydata.js"; 

export default {
  data() {
    return {
      CompanyName: "",
      CompanyImage: "",
      Category: [],
    };
  },
  methods: {
    GetCompanyDataApi() {
      this.CompanyName = commonData.CompanyName;
      this.CompanyImage = commonData.CompanyImage;
      this.Category = commonData.Category;
    },
    randerhomepage() {
      this.$router.push("/");
    },
  },
  created() {
    this.GetCompanyDataApi();
    console.log("....", commonData);
  },
};
</script>
<style scoped>
.cursor {
  cursor: pointer;
}
/* .cursor :hover {
  color: #fffdd0;
} */
.routercss {
  color: white;
  text-decoration: none;
}
.routercss:hover {
  color: red;
}
.logoimage {
  width: 10vh;
  height: 10vh;
}
</style> 
<template>
  <div
    class="d-flex flex-wrap"
    style="width: 95%; height: 10vh; color: #fffdd0; align-items: center"
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
    <div
      class="d-flex justify-content-start align-items-center col-8 positionr"
    >
      <router-link
        class="routercss cursor categorycss"
        v-for="(item, index) in rendercategory"
        :key="index"
        :to="{ name: 'ItemsView', params: { id: item.CategoryId } }"
      >
        {{ item.CategoryName }}
      </router-link>
      <i class="fa-solid fa-angle-down cursor" @click="openothercategory()"></i>
      <div
        v-show="showothercategory"
        class="positiona"
        @mouseleave="closeothercategory()"
      >
        <li
          v-for="(item, index) in this.othercategory"
          :key="index"
          class="othercategory cursor"
        >
          <router-link
            class="routercss cursor categorycss"
            :to="{ name: 'ItemsView', params: { id: item.CategoryId } }"
          >
            {{ item.CategoryName }}
          </router-link>
        </li>
        <!-- <router-link
          class="routercss cursor categorycss"
          v-for="(item, index) in othercategory"
          :key="index"
          :to="{ name: 'ItemsView', params: { id: item.CategoryId } }"
        >
          {{ item.CategoryName }}
        </router-link> -->
      </div>
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
      rendercategory: [],
      othercategory: [],

      showothercategory: false,
    };
  },
  methods: {
    GetCompanyDataApi() {
      this.CompanyName = commonData.CompanyName;
      this.CompanyImage = commonData.CompanyImage;
      this.Category = commonData.Category;
      this.rendercategory = this.Category.slice(0, 5);
      this.othercategory = this.Category.slice(5, this.Category.length);
      console.log(".ddd..",this.Category)
    },
    randerhomepage() {
      this.$router.push("/");
    },
    openothercategory() {
      this.showothercategory = !this.showothercategory;
    },
    closeothercategory() {
      this.showothercategory = false;
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
.categorycss {
  margin-right: 3rem;
  font-size: 1.2rem;
}
.positionr {
  position: relative;
  height: 100%;
}
.positiona {
  position: absolute;
  background-color: #141414;
  color: white;
  width: 25%;
  padding-left: 1rem;
  top: 100%;
  right: 0;
  padding-bottom: 1rem;
}
.othercategory {
  margin-top: 1rem;
  list-style-type: none;
}
.othercategory:hover {
  color: red;
}
</style> 
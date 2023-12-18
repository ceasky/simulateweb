<template>
  <div
    class="d-flex justify-content-between flex-wrap"
    style="width: 90%; margin: 0 auto"
  >
    <div class="col-2" @mouseleave="CloseHover()">
      {{ ComName }}
    </div>
    <div class="d-flex justify-content-between col-8">
      <div
        class="cursor"
        v-for="(item, index) in ComType"
        :key="index"
        @click="RenderDetailInfo(item.TypeId)"
        @mouseover="RenderDetailInfo(item.TypeId)"
      >
        {{ item.TypeName }}
      </div>
    </div>
    <div class="col-2 d-flex justify-content-between">
      <div class="cursor">
        <i @mouseover="RenderServe()" class="fa-regular fa-circle-question"
          >支援服務</i
        >
      </div>
      <div class="cursor">
        <i @mouseover="RenderSearch()" class="fa-solid fa-magnifying-glass"></i>
      </div>
      <div class="cursor">
        <i class="fa-solid fa-user"></i>
      </div>
    </div>
    <!-- hover顯示 -->
    <!-- detail -->
    <div
      v-show="ShowHoverData == 'ProductDetail'"
      class="col-8 offset-2 cursor"
      @mouseleave="CloseHover()"
    >
      <div>{{ TypeName }}</div>
      <div>
        <li v-for="(item, index) in TypeDetail" :key="index">
          {{ item.Titlename }}
        </li>
      </div>
    </div>
    <!-- 支援服務 -->
    <div
      v-show="ShowHoverData == 'Serve'"
      class="col-8 offset-2"
      @mouseleave="CloseHover()"
    >
      <div>支援服務</div>
      <div>
        <li>社群</li>
        <li>查詢保固</li>
        <li>維修</li>
        <li>聯絡我們</li>
      </div>
    </div>
    <div
      v-show="ShowHoverData == 'Search'"
      class="col-8 offset-2"
      @mouseleave="CloseHover()"
    >
      <div class="searchfiled d-flex">
        <input class="searchinput" type="text" placeholder="搜尋" />
        <button class="searchbutton">
          <i class="fa-solid fa-magnifying-glass"></i>
        </button>
      </div>
      <div>
        <li>產品11</li>
        <li>產品12</li>
        <li>產品13</li>
        <li>產品14</li>
      </div>
    </div>
  </div>
</template>
<script>
const dummyComname = "公司名稱或圖片";
const dummytype = [
  {
    TypeId: "0",
    TypeName: "產品類型1",
    Detail: [
      { Titleid: "0", Titlename: "產品名稱11" },
      { Titleid: "1", Titlename: "產品名稱12" },
      { Titleid: "2", Titlename: "產品名稱13" },
      { Titleid: "3", Titlename: "產品名稱14" },
    ],
  },
  {
    TypeId: "1",
    TypeName: "產品類型2",
    Detail: [
      { Titleid: "0", Titlename: "產品名稱21" },
      { Titleid: "1", Titlename: "產品名稱22" },
      { Titleid: "2", Titlename: "產品名稱23" },
      { Titleid: "3", Titlename: "產品名稱24" },
    ],
  },
  {
    TypeId: "2",
    TypeName: "產品類型3",
    Detail: [
      { Titleid: "0", Titlename: "產品名稱31" },
      { Titleid: "1", Titlename: "產品名稱32" },
      { Titleid: "2", Titlename: "產品名稱33" },
      { Titleid: "3", Titlename: "產品名稱34" },
    ],
  },
  {
    TypeId: "3",
    TypeName: "產品類型4",
    Detail: [
      { Titleid: "0", Titlename: "產品名稱41" },
      { Titleid: "1", Titlename: "產品名稱42" },
      { Titleid: "2", Titlename: "產品名稱43" },
      { Titleid: "3", Titlename: "產品名稱44" },
    ],
  },
  {
    TypeId: "4",
    TypeName: "產品類型5",
    Detail: [
      { Titleid: "0", Titlename: "產品名稱51" },
      { Titleid: "1", Titlename: "產品名稱52" },
      { Titleid: "2", Titlename: "產品名稱53" },
      { Titleid: "3", Titlename: "產品名稱54" },
    ],
  },
  {
    TypeId: "5",
    TypeName: "產品類型6",
    Detail: [
      { Titleid: "0", Titlename: "產品名稱61" },
      { Titleid: "1", Titlename: "產品名稱62" },
      { Titleid: "2", Titlename: "產品名稱63" },
      { Titleid: "3", Titlename: "產品名稱64" },
    ],
  },
];
export default {
  data() {
    return {
      ComName: "",
      ComType: [],

      TypeName: "產品類型1",
      TypeDetail: [
        { Titleid: "0", Titlename: "產品名稱1" },
        { Titleid: "1", Titlename: "產品名稱2" },
        { Titleid: "2", Titlename: "產品名稱3" },
        { Titleid: "3", Titlename: "產品名稱4" },
      ],

      ShowHoverData: "",
    };
  },
  methods: {
    //使用api 取得公司資訊
    GetComData() {
      this.ComName = dummyComname;
      this.ComType = dummytype;
    },
    RenderDetailInfo(TypeId) {
      this.ShowHoverData = "ProductDetail";
      let object = this.ComType.find((item) => item.TypeId == TypeId);
      this.TypeName = object.TypeName;
      this.TypeDetail = object.Detail;
    },
    RenderServe() {
      this.ShowHoverData = "Serve";
      console.log("RenderServe");
    },
    RenderSearch() {
      this.ShowHoverData = "Search";
      console.log("RenderSearch");
    },

    CloseHover() {
      console.log("CloseHover");
      this.ShowHoverData = "";
    },
  },
  created() {
    this.GetComData();
  },
};
</script>
<style scoped>
li {
  list-style-type: none;
}
.cursor {
  cursor: pointer;
}
.searchfiled {
  height: 2rem;
}
.searchinput {
  height: 100%;
  padding-left: 1rem;
  border-style: solid;
  border-width: 1px;
  border-radius: 5rem 0rem 0rem 5rem;
  border-color: #d3d3d3;
}
.searchinput:focus {
  border-color: #1c62b9;
  outline: none;
}
.searchbutton {
  height: 100%;
  padding: 0 1rem;
  border-radius: 0rem 5rem 5rem 0rem;
  border-style: solid;
  border-width: 1px;
  border-color: #d3d3d3;
}
.searchbutton:focus {
  border-color: #1c62b9;
  outline: none;
}
</style> 
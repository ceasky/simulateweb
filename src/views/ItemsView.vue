<template>
  <div id="app" style="min-height: 50vw">
    <div
      class="d-flex flex-column align-items-center"
      style="margin: 0 auto; width: 95%"
    >
      <div style="font-size: 1.5rem">{{ CategoryName }}</div>
      <div class="searchfiled d-flex">
        <input class="searchinput" type="text" placeholder="搜尋" />
        <button class="searchbutton">
          <i class="fa-solid fa-magnifying-glass"></i>
        </button>
      </div>

      <div class="col-12 d-flex mt-2 flex-wrap pt-3" style="height: 8rem">
        <div
          class="ItemCss d-flex justify-content-center align-items-end"
          v-for="(item, index) in Renderlist"
          :key="index"
          style="text-align: center"
        >
          <div>
            {{ item.ContentTitle }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      Categoryid: "",
      CategoryName: "",
      Category: [],
      AllItems: [],
      Renderlist: [],
    };
  },
  methods: {
    GetCategoryContentApi(id) {
      console.log("GetCategoryContentApi");
      let GetApiData = {
        Category: [
          { CategoryName: "產品類型1", CategoryId: "0" },
          { CategoryName: "產品類型2", CategoryId: "1" },
          { CategoryName: "產品類型3", CategoryId: "2" },
          { CategoryName: "產品類型4", CategoryId: "3" },
        ],
        Items: [
          {
            ItemId: "0",
            CategoryId: "0",
            ContentTitle: "產品名稱1",
            ContentImage: "",
          },
          {
            ItemId: "1",
            CategoryId: "0",
            ContentTitle: "產品名稱2",
            ContentImage: "",
          },
          {
            ItemId: "2",
            CategoryId: "0",
            ContentTitle: "產品名稱3",
            ContentImage: "",
          },
          {
            ItemId: "3",
            CategoryId: "0",
            ContentTitle: "產品名稱4",
            ContentImage: "",
          },
          {
            ItemId: "4",
            CategoryId: "0",
            ContentTitle: "產品名稱5",
            ContentImage: "",
          },
          {
            ItemId: "5",
            CategoryId: "0",
            ContentTitle: "產品名稱6",
            ContentImage: "",
          },
          {
            ItemId: "6",
            CategoryId: "1",
            ContentTitle: "產品名稱7",
            ContentImage: "",
          },
          {
            ItemId: "7",
            CategoryId: "1",
            ContentTitle: "產品名稱8",
            ContentImage: "",
          },
          {
            ItemId: "8",
            CategoryId: "2",
            ContentTitle: "產品名稱9",
            ContentImage: "",
          },
          {
            ItemId: "9",
            CategoryId: "3",
            ContentTitle: "產品名稱10",
            ContentImage: "",
          },
          {
            ItemId: "10",
            CategoryId: "3",
            ContentTitle: "產品名稱11",
            ContentImage: "",
          },
          {
            ItemId: "11",
            CategoryId: "3",
            ContentTitle: "產品名稱12",
            ContentImage: "",
          },
          {
            ItemId: "12",
            CategoryId: "0",
            ContentTitle: "產品名稱13",
            ContentImage: "",
          },
          {
            ItemId: "13",
            CategoryId: "0",
            ContentTitle: "產品名稱14",
            ContentImage: "",
          },
          {
            ItemId: "14",
            CategoryId: "0",
            ContentTitle: "產品名稱15",
            ContentImage: "",
          },
          {
            ItemId: "15",
            CategoryId: "0",
            ContentTitle: "產品名稱16",
            ContentImage: "",
          },
          {
            ItemId: "16",
            CategoryId: "0",
            ContentTitle: "產品名稱17",
            ContentImage: "",
          },
        ],
      };

      this.Categoryid = id;
      this.AllItems = GetApiData.Items;
      this.Category = [
        {
          value: "",
          text: "站內查詢",
        },
      ];
      for (var index in GetApiData.Category) {
        let data = GetApiData.Category[index];
        this.Category.push({
          value: data.CategoryId,
          text: data.CategoryName,
        });
      }
      this.RenderItems();
    },
    RenderItems() {
      if (this.Categoryid !== "") {
        console.log("yyyy", this.Categoryid);
        this.Renderlist = this.AllItems.filter(
          (item) => item.CategoryId == this.Categoryid
        );
      } else {
        console.log("nnn11", this.Categoryid);
        this.Renderlist = [...this.AllItems];
      }
      //////////////////
      this.Renderlist = this.Renderlist.concat(this.Renderlist);
      let item = this.Category.find((item) => item.value == this.Categoryid);
      this.CategoryName = item.text;
    },
  },
  // computed: {
  //   CategoryName() {
  //     console.log("this.Categoryid2222", this.Categoryid);
  //     let item = this.Category.find((item) => item.value == this.Categoryid);
  //     return item.text;
  //   },
  // },
  created() {
    const { id } = this.$route.params;
    this.GetCategoryContentApi(id);
  },
  beforeRouteUpdate(to, from, next) {
    const { id } = to.params;
    this.GetCategoryContentApi(id);
    next();
  },
};
</script>
<style scoped>
.ItemCss {
  background-color: red;
  min-width: 20%;
  height: 10rem;
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


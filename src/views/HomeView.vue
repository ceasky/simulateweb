<template>
  <div id="app">
    <div style="height: 30vw; width: 95%; margin: 0 auto"></div>
    <div
      v-for="(category, index) in this.AllItems"
      :key="index"
      class="d-flex flex-wrap mb-3"
      style="background-color: #141414; width: 95%; margin: 0 auto"
    >
      <div class="col-12" style="font-size: 1.5rem; color: white">
        {{ category.CategoryName }}
      </div>
      <div class="col-12 d-flex home-positionR mt-2" style="height: 8rem">
        <button
          class="home-positionA1 home-arrowbutton"
          v-show="category.ShowPage"
          @click="RenderOtherItems(category.CategoryId, 1)"
          style="height: 100%"
        >
          <i class="fa-solid fa-chevron-left"></i>
        </button>
        <div
          class="home-ItemCss d-flex justify-content-center align-items-end"
          v-for="(item, index) in category.RnderItems"
          :key="index"
          @click="RanderItemDetail(category.CategoryId, item.ItemId)"
          style="text-align: center"
        >
          <div>
            {{ item.ContentTitle }}
          </div>
        </div>
        <button
          class="home-positionA2 home-arrowbutton"
          v-show="category.ShowPage"
          @click="RenderOtherItems(category.CategoryId, 2)"
          style="height: 100%"
        >
          <i class="fa-solid fa-chevron-right"></i>
        </button>
      </div>
    </div>
    <!-- <ItemDetailPage  /> -->
    <!-- /////////////////hide-footer//   hide-header///// -->
    <b-modal
      content-class="your-class"
      ref="home-modal"
      size="lg"
      hide-footer
      hide-header
      centered
      body-class="bodyclasscss"
      header-class="my-class"
    >
      <div class="" style="">
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
  </div>
</template>

<script>
// import ItemDetailPage from "./../components/ItemDetailPage";
const GetApiData = {
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

export default {
  components: {
    // ItemDetailPage,
  },
  data() {
    return {
      ApiData: null,
      AllItems: [],
      RenderNumber: 5,

      DetailData: {
        itemid: "",
        categoryid: "",
        price: "",
        contacturl: [
          {
            urlname: "",
            url: "",
          },
          {
            urlname: "",
            url: "",
          },
        ],
        info: [],
        mainimage: "",
        otherimage: [],
      },
    };
  },
  methods: {
    GetCategoryContentApi() {
      this.ApiData = GetApiData;
      this.SetData();
    },
    SetData() {
      for (var index in this.ApiData.Category) {
        let data = this.ApiData.Category[index];
        this.AllItems.push({
          CategoryName: data.CategoryName,
          CategoryId: data.CategoryId,
          Items: [],
          RenderIndex: 0,
          RnderItems: [],
          ShowPage: false,
        });
      }
      for (var idx in this.ApiData.Items) {
        let data = this.ApiData.Items[idx];
        for (var idx2 in this.AllItems) {
          let data2 = this.AllItems[idx2];
          if (data2.CategoryId == data.CategoryId) {
            data2.Items.push(data);
          }
        }
      }
      for (var idx3 in this.AllItems) {
        let data3 = this.AllItems[idx3];
        if (data3.Items.length > this.RenderNumber) {
          data3.ShowPage = true;
          this.RenderOtherItems(data3.CategoryId, 0);
        } else {
          data3.RnderItems = [...data3.Items];
        }
      }
      console.log("this.AllItems", this.AllItems);
    },
    RenderOtherItems(CategoryId, Type) {
      console.log("...222", CategoryId, Type);
      //type == 0 讀取   1 向左    2向右
      let CheckItem = this.AllItems.find(
        (item) => item.CategoryId == CategoryId
      );
      let maxindex = Math.floor(CheckItem.Items.length / this.RenderNumber);
      console.log("index", maxindex);
      if (Type == 1) {
        if (CheckItem.RenderIndex == 0) {
          CheckItem.RenderIndex = maxindex;
        } else {
          CheckItem.RenderIndex = CheckItem.RenderIndex - 1;
        }
      } else if (Type == 2) {
        if (CheckItem.RenderIndex == maxindex) {
          CheckItem.RenderIndex = 0;
        } else {
          CheckItem.RenderIndex = CheckItem.RenderIndex + 1;
        }
      } else {
        CheckItem.RenderIndex = 0;
      }
      CheckItem.RnderItems = CheckItem.Items.slice(
        CheckItem.RenderIndex * this.RenderNumber,
        (CheckItem.RenderIndex + 1) * this.RenderNumber
      );
      if (CheckItem.RnderItems.length !== this.RenderNumber) {
        let array = CheckItem.Items.slice(
          0,
          this.RenderNumber - CheckItem.RnderItems.length
        );
        CheckItem.RnderItems = CheckItem.RnderItems.concat(array);
      }

      console.log("RenderOtherItems", CheckItem);
    },
    RanderItemDetail(CategoryId, ItemId) {
      console.log("RanderItemDetail", CategoryId, ItemId);
      this.$refs["home-modal"].show();
    },
  },
  created() {
    this.GetCategoryContentApi();
  },
};
</script>
<style>
.home-ItemCss {
  background-color: red;
  min-width: 20%;
}
.home-positionR {
  position: relative;
}
.home-positionA1 {
  position: absolute;
  top: 0px;
  left: 15px;
}
.home-positionA2 {
  position: absolute;
  top: 0px;
  right: 15px;
}
.home-arrowbutton {
  background-color: #141414;
  color: white;
  opacity: 0.1;
  border-style: none;
  width: 3rem;
}
.home-arrowbutton:hover {
  background-color: #141414;
  color: white;
  opacity: 0.5;
  border-style: none;
}
.modal-body {
  background-color: #141414 !important;
  padding: 0.5rem;
  color: white;
}
</style>


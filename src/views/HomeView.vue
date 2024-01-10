<template>
  <div id="app">
    <div style="height: 30vw; width: 95%; margin: 0 auto 2rem auto">
      <img
        class="mainimage"
        src="@/assets/company/mainimage.webp"
        alt="圖片描述"
      />
    </div>
    <div
      v-for="(category, index) in this.AllItems"
      :key="index"
      class="d-flex flex-wrap mb-3"
      style="background-color: #141414; width: 95%; margin: 0 auto"
    >
      <div class="col-12" style="font-size: 2.5rem; color: #fffdd0">
        {{ category.CategoryName }}
      </div>
      <div class="col-12 d-flex home-positionR mt-2" style="">
        <button
          class="home-positionA1 home-arrowbutton"
          v-show="category.ShowPage"
          @click="RenderOtherItems(category.CategoryId, 1)"
          style="height: 100%"
        >
          <i class="fa-solid fa-chevron-left"></i>
        </button>
        <div
          class="home-ItemCss"
          v-for="(item, index) in category.RnderItems"
          :key="index"
          @click="RanderItemDetail(item.CategoryId, item.ItemId)"
          style="text-align: center"
        >
          <div>
            <img class="mainimage" :src="item.MainImage" alt="圖片描述" />
          </div>
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
        <div style="height: 30rem; background-color: red">
          <img class="imgcss" :src="DetailData.MainImage" alt="圖片描述" />
        </div>
        <div class="d-flex align-items-center" style="height: 5rem">
          <div class="col-8" style="color: #fffdd0; font-size: 1.5rem">
            {{ DetailData.ContentTitle }}
          </div>
          <div class="col-2">${{ DetailData.Price }}</div>
          <div
            class="col-2 cursor"
            @click="rendercontacturl(DetailData.Contacturl)"
          >
            蝦皮連結
          </div>
        </div>
        <div class="pl-3">
          <li
            class="mb-3"
            style="list-style: none; height: 3rem"
            v-for="(item, index) in DetailData.Info"
            :key="index"
          >
            {{ item }}
          </li>
        </div>
        <div class="d-flex flex-wrap">
          <div
            v-for="(item, index) in DetailData.Otherimage"
            :key="index"
            class="col-4"
            style="padding: 0"
          >
            <img class="imgcss" :src="item" alt="圖片描述" />
          </div>
        </div>
      </div>
    </b-modal>
  </div>
</template>

<script>
import commonData from "@/common/companydata.js";

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
        ItemId: "0",
        CategoryId: "0",
        ContentTitle: "小姐與流氓,小飛象,瑪麗貓原子筆",
        MainImage:
          "https://down-tw.img.susercontent.com/file/tw-11134207-7r98v-llgek43ypxe9e4",
        Otherimage: [
          "https://down-tw.img.susercontent.com/file/tw-11134207-7r98v-llgfju7d2fa97d",
          "https://down-tw.img.susercontent.com/file/tw-11134207-7r98v-llgek43ypxe9e4",
          "https://down-tw.img.susercontent.com/file/tw-11134207-7r991-lmtwclwrikd5b8",
          "https://down-tw.img.susercontent.com/file/tw-11134207-7r98s-lmtwclwrjyqjfe",
          "https://down-tw.img.susercontent.com/file/tw-11134207-7r98s-lmtwclwrzezf21",
        ],
        Contacturl:
          "https://shopee.tw/%E5%B0%8F%E5%A7%90%E8%88%87%E6%B5%81%E6%B0%93-%E5%B0%8F%E9%A3%9B%E8%B1%A1-%E7%91%AA%E9%BA%97%E8%B2%93%E5%8E%9F%E5%AD%90%E7%AD%86%F0%9F%92%9B%E4%B8%80%E7%B5%84%E4%B8%89%E5%85%A5%E3%80%82%E6%97%A5%E6%9C%AC%E8%BF%AA%E5%A3%AB%E5%B0%BC%E4%BB%A3%E8%B3%BC-i.16822809.21689117848?sp_atk=235e7218-4a1b-4b4c-9a5a-f61d4c9151f3&xptdk=235e7218-4a1b-4b4c-9a5a-f61d4c9151f3",
        Price: "350",
        Info: [
          "來來來～買了可愛鉛筆盒也不能錯過各種可愛的筆吧？",
          "小姐與流氓,小飛象,瑪麗貓原子筆💛一組三入 0.5mm，黑色中性墨水圓珠筆 筆身超級精緻漂亮 寫筆記的筆一定也要用最可愛的吧(◍•ᴗ•◍)",
          "米妮,費加洛,黛西 在另一個頁面下單喔！請在nayo 賣場直接搜尋原子筆，找不到可以聊聊私訊我，會貼連結給您♡",
          "熱愛迪士尼小物(⁎⁍̴̛ᴗ⁍̴̛⁎)，歡迎聊聊詢問🔍，100%正版，日本迪士尼代購",
        ],
      },
    };
  },
  methods: {
    GetCategoryContentApi() {
      this.ApiData = commonData;
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
      let object = this.ApiData.Items.find((item) => item.ItemId == ItemId);
      this.DetailData = {...object}
      this.$refs["home-modal"].show();
    },
    rendercontacturl(url) {
      window.open(url);
    },
  },
  created() {
    this.GetCategoryContentApi();
    console.log("....", commonData);
  },
};
</script>
<style>
.home-ItemCss {
  /* background-color: white; */
  width: 20%;
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
.mainimage {
  width: 100%;
  height: 100%;
}
.cursor {
  cursor: pointer;
}
.imgcss {
  height: 100%;
  width: 100%;
}
.cursor:hover{
  color:#fffdd0
}
</style>


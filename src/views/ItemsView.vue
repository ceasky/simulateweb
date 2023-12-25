<template>
  <div id="app" style="min-height: 50vw">
    <div
      class="d-flex flex-column align-items-center"
      style="margin: 0 auto; width: 95%"
    >
      <div style="font-size: 1.5rem">{{ CategoryName }}</div>
      <div class="searchfiled d-flex">
        <input
          class="searchinput"
          type="text"
          placeholder="搜尋"
          v-model="Searchkeyword"
        />
        <button class="searchbutton" @click="searchaction()">
          <i class="fa-solid fa-magnifying-glass"></i>
        </button>
      </div>

      <div class="col-12 d-flex mt-2 flex-wrap pt-3">
        <div
          class="ItemCss"
          v-for="(item, index) in Renderlist"
          :key="index"
          style="text-align: center"
          @click="RanderItemDetail(item.CategoryId, item.ItemId)"
        >
          <div>
            <img class="mainimage" :src="item.MainImage" alt="圖片描述" />
          </div>
          <div>
            {{ item.ContentTitle }}
          </div>
        </div>
      </div>
    </div>

    <!-- //////////////////////// -->
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
  components: {},
  data() {
    return {
      Searchkeyword: "",
      Categoryid: "",
      CategoryName: "",
      Category: [],
      AllItems: [],
      Categorylist: [],
      Renderlist: [],

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
    GetCategoryContentApi(id) {
      this.Categoryid = id;
      this.AllItems = commonData.Items;
      this.Category = [
        {
          value: "all",
          text: "站內查詢",
        },
      ];
      for (var index in commonData.Category) {
        let data = commonData.Category[index];
        this.Category.push({
          value: data.CategoryId,
          text: data.CategoryName,
        });
      }
      this.RenderItems();
    },
    RenderItems() {
      if (this.Categoryid !== "" && this.Categoryid !== "all") {
        console.log("yyyy", this.Categoryid);
        this.Categorylist = this.AllItems.filter(
          (item) => item.CategoryId == this.Categoryid
        );
      } else if (this.Categoryid == "all") {
        console.log("nnn11", this.Categoryid);
        this.Categorylist = [...this.AllItems];
      }

      this.Renderlist = [...this.Categorylist];
      //////////////////
      let item = this.Category.find((item) => item.value == this.Categoryid);
      this.CategoryName = item.text;
    },
    rendercontacturl(url) {
      window.open(url);
    },
    RanderItemDetail(CategoryId, ItemId) {
      console.log("RanderItemDetail", CategoryId, ItemId);
      let object = this.AllItems.find((item) => item.ItemId == ItemId);
      this.DetailData = { ...object };
      this.$refs["home-modal"].show();
    },
    searchaction() {
      if (!this.Searchkeyword) {
        this.Renderlist = [...this.Categorylist];
      } else {
        let searcharray = this.Categorylist.filter((item) =>
          item.ContentTitle.includes(this.Searchkeyword)
        );
        if (searcharray.length == 0) {
          alert("no data");
          this.Renderlist = [...this.Categorylist];
        } else {
          this.Renderlist = searcharray;
        }
      }
    },
  },

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
  width: 20%;
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
.imgcss {
  height: 100%;
  width: 100%;
}
.cursor {
  cursor: pointer;
}
.cursor:hover {
  color: #fffdd0;
}
</style>


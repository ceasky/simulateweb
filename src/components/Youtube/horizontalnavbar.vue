<template>
  <div class="d-flex horizontal align-items-center ml-4 mr-4">
    <div class="d-flex align-items-center content1" style="height: 100%">
      <i class="fa-solid fa-bars mr-3 iconsize"></i>
      <div class="">Youtube</div>
    </div>
    <div class="search d-flex " style="width: 100%">
      <!-- <div :class="!inputfocus?'opacityitem0':'opacityitem1'" class="searchiconc"></div> -->
      <div :class="inputfocus?' searchicono':' searchiconc'" >
        <i v-show="inputfocus" class="fa-solid fa-magnifying-glass ml-3"></i>
      </div>
      <input
        @blur="getfocus(false)"
        @focus="getfocus(true)"
        class="searchinput"
        type="text"
        placeholder="搜尋"
        style="width: 100%"
      />
      <button class="searchbutton">
        <i class="fa-solid fa-magnifying-glass"></i>
      </button>
      <div class="csscenter ml-3">
        <i class="fa-solid fa-microphone mr-5 iconsize iconcolor"></i>
      </div>
    </div>
    <div class="d-flex align-items-center content3">
      <i class="fa-solid fa-magnifying-glass mr-3 iconsize opacityitem"></i>
      <i class="fa-solid fa-upload mr-3 iconsize"></i>
      <i class="fa-solid fa-bell mr-3 iconsize"></i>
      <div class="user">S</div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      inputfocus: false,
    };
  },
  methods: {
    getfocus(type) {
      this.inputfocus = type;
    },
  },
};
</script>
<style scoped>
.horizontal {
  min-height: 60px;
}
.content1 {
  min-width: 170px;
}
.content3 {
  min-width: 225px;
}
.opacityitem{
    opacity: 0;
}

.search {
  height: 40px;
  margin-left:4rem
}
.csscenter {
  display: flex;
  align-items: center;
}
.iconsize {
  font-size: 1.2rem;
  height: 2.5rem;
  width: 2.5rem;
  padding-top: 10px;
  border-radius: 50%;
}
.iconcolor {
  background-color: #f0f0f0;
}
.iconsize:hover {
  background-color: #c6c6c6;
}
.user {
  border-radius: 50%;
  background-color: red;
  height: 2.5rem;
  width: 2.5rem;
  padding-top: 10px;
}

.searchicono {
  border: 1px solid #d3d3d3;
  border-radius: 5rem 0 0 5rem;
  min-width: 50px;
  border-color: #1c62b9 transparent #1c62b9 #1c62b9;
  display: flex;
  align-items: center;
}
.searchiconc {
  margin-left:30px;
  border: 1px solid red;
  border-radius: 5rem 0 0 5rem;
  min-width: 20px;
  border-color: #d3d3d3 transparent #d3d3d3 #d3d3d3;
}
.searchinput {
  border-style: solid;
  border-width: 1px;
  border-color: #d3d3d3 #d3d3d3 #d3d3d3 transparent;

}
.searchinput:focus {
  border-style: solid;
  border-width: 1px;
  border-color: #1c62b9 #1c62b9 #1c62b9 transparent;

  outline: none;
}
.searchbutton {
  padding-top: 1px;
  border-radius: 0rem 5rem 5rem 0rem;
  width: 64px;
  height: 40px;
  border: none;
  border-style: solid;
  border-width: 1px;
  border-color: #d3d3d3 #d3d3d3 #d3d3d3 transparent;
}
.searchbutton:focus {
  border-style: solid;
  border-width: 1px;
  border-color: #d3d3d3 #d3d3d3 #d3d3d3 transparent;

  outline: none;
}
</style> 
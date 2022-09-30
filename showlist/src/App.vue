<template>
  <div id="app">
    <Handle
      :changePopupStatus="changePopupStatus"
      :infos="infos"
      :changeShowInfo="changeShowInfo"
      :delinfo="delinfo"
    />
    <Table
      :infos="infos"
      :delinfo="delinfo"
      :showinfo="showinfo"
      :checkinfo="checkinfo"
      :trdel="trdel"
    />
    <AddPopUp
      :addinfo="addinfo"
      :changePopupStatus="changePopupStatus"
      v-if="popupStatus"
    />
    <DelPopUp v-if="DelPopUpStatus" />
    <paging
      :count="count"
      :pages="pages"
      :nextpage="nextpage"
      :prevpage="prevpage"
    />
  </div>
</template>

<script>
import Handle from "./components/Handle.vue";
import Table from "./components/Table.vue";
import AddPopUp from "./components/AddPopUp.vue";
import DelPopUp from "./components/DelPopUp.vue";
import paging from "./components/paging.vue";
export default {
  name: "App",
  components: {
    Handle,
    Table,
    AddPopUp,
    DelPopUp,
    paging,
  },
  data() {
    return {
      infos: [],
      showinfo: [],
      popupStatus: false,
      DelPopUpStatus: false,
      count: "0",
      pages: "1",
    };
  },
  methods: {
    //添加信息
    addinfo(infoObj) {
      this.infos.unshift(infoObj);
      // this.showinfo.push(infoObj);
      console.log(this.infos);
    },
    //弹窗状态
    changePopupStatus(state) {
      this.popupStatus = state;
    },
    //搜索时匹配的showinfo
    changeShowInfo(arr) {
      this.showinfo = arr;
    },
    //删除窗口
    // changeDelPopupStatus(state) {
    //   this.DelPopUpStatus = state;
    // },
    //根据id改变对应的select状态
    checkinfo(id) {
      this.infos.forEach((item) => {
        if (item.id === id) {
          item.select = !item.select;
        }
      });
    },
    //删除选中的信息
    delinfo() {
      this.infos = this.infos.filter((item) => {
        console.log(1);
        return !item.select;
      });
      this.showinfo = this.infos;
    },
    //tr里面的删除按钮，删除一个对应的tr
    trdel(id) {
      this.infos = this.infos = this.infos.filter((item) => {
        return item.id !== id;
      });
      this.showinfo = this.infos;
    },
    //下一页
    nextpage() {
      this.pages++;
      this.showinfo = this.infos.filter((item, index) => {
        return (
          index >= 5 * (this.pages - 1) && index < 5 * (this.pages - 1) + 5
        );
      });
    },
    //上一页
    prevpage() {
      this.pages--;
      this.showinfo = this.infos.filter((item, index) => {
        return (
          index >= 5 * (this.pages - 1) && index < 5 * (this.pages - 1) + 5
        );
      });
    },
  },
  watch: {
    infos() {
      this.count = this.infos.length;
      this.showinfo = this.infos.filter((item, index) => {
        return (
          index >= 5 * (this.pages - 1) && index < 5 * (this.pages - 1) + 5
        );
      });
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>

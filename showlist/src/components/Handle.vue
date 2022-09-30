<template>
  <div>
    <button @click="showaddpopup">添加</button>
    <button @click="changeinfos">删除</button>
    <input type="text" placeholder="请输入姓名查询" v-model="str" />
    <button @click="search" :disabled="str.length ? false : true">搜索</button>
    <button @click="reset">重置</button>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  props: ["changePopupStatus", "changeShowInfo", "infos", "delinfo"],
  data() {
    return {
      myStatus: this.changePopupStatus,
      str: "",
    };
  },
  methods: {
    showaddpopup() {
      this.changePopupStatus(true);
    },
    search() {
      this.changeShowInfo(this.filarr);
      this.str = "";
    },
    reset() {
      this.str = "";
      this.changeShowInfo(this.filarr);
    },
    changeinfos() {
      this.delinfo();
    },
  },
  computed: {
    filarr() {
      if (this.str) {
        return this.infos.filter((item) => {
          return item.name.indexOf(this.str) !== -1;
        });
      } else {
        return _.cloneDeep(this.infos);
      }
    },
  },
};
</script>
<style scoped>
button {
  border: none;
  display: inline-block;
  width: 70px;
  height: 20px;
  background-color: #999;
  border-radius: 3px;
  margin: 0 5px;
}

button:hover {
  background-color: #bbb;
}

input {
  border: 1px solid #999;
  outline: none;
}
</style>

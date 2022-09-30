<template>
  <div class="popup">
    <div class="tip">请填写信息</div>
    <div class="inp">
      姓名：<input type="text" v-model="info.name" /><br />
      科目：
      <select v-model="info.subject">
        <option value="java">java</option>
        <option value="javascript">javascript</option>
        <option value="mysql">mysql</option></select
      ><br />
      成绩：<input type="text" v-model="info.score" /><br />
    </div>
    <div>
      <button @click="close">取消</button>
      <button @click="add">确定</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["addinfo", "changePopupStatus"],
  data() {
    return {
      info: {
        name: "",
        subject: "",
        score: "",
      },
    };
  },
  methods: {
    //点击添加信息
    add() {
      //校验数据
      if (!this.info.name.trim()) return alert("输入不能为空");
      //让App添加数据
      this.addinfo({ id: +new Date(), select: false, ...this.info });
      //清空表单
      this.info = {
        name: "",
        subject: "",
        score: "",
      };
    },
    //点击取消
    close() {
      console.log(1);
      this.changePopupStatus(false);
    },
  },
};
</script>
<style>
.popup {
  position: absolute;
  padding: 30px 30px;
  right: 0;
  top: 30%;
  background-color: rgba(0, 0, 0, 0.3);
  width: 300px;
  height: 250px;
  border-radius: 10px;
}
.tip {
  font-size: 25px;
}
button {
  width: 60px;
  height: 30px;
}
input {
  margin: 10px 5px;
  height: 20px;
  width: 100px;
  outline: none;
}
.inp select {
  height: 20px;
}
.popup button {
  margin-right: 15px;
}
</style>

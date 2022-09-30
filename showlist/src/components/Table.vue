<template>
  <div class="box">
    <table cellspacing="0">
      <thead>
        <tr>
          <th>请选择</th>
          <th>姓名</th>
          <th>科目</th>
          <th>成绩</th>
          <th>操作</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="info of showinfo" :key="info.id">
          <td>
            <input
              type="checkbox"
              :checked="info.select"
              @change="handleCheck(info.id)"
            />
          </td>
          <td :contentEditable="tdState">{{ info.name }}</td>
          <td :contentEditable="tdState">{{ info.subject }}</td>
          <td :contentEditable="tdState">{{ info.score }}</td>
          <td>
            <a href="javascript:;" @click="del(info.id)">删除</a>
            <a href="javascript:;" @click="changeTdState">{{
              isoperate ? "编辑" : "取消编辑"
            }}</a>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: ["infos", "showinfo", "checkinfo", "trdel"],
  data() {
    return {
      tdState: false,
      isoperate: true,
    };
  },
  methods: {
    handleCheck(id) {
      console.log(id);
      //通知App组件将对应的todo对象的done值取反
      this.checkinfo(id);
    },
    //点击删除按钮删除对应的tr
    del(id) {
      this.trdel(id);
    },
    //点击可以改变单元格输入状态
    changeTdState() {
      this.tdState = !this.tdState;
      this.isoperate = !this.isoperate;
    },
  },
};
</script>

<style>
table {
  width: 500px;
  margin: 50px auto 0;
  border-collapse: collapse;
  text-align: center;
  border: 1px solid #999;
}

td,
th {
  border: 1px solid #999;
}

thead tr {
  height: 40px;
  background-color: #ccc;
}

a {
  display: inline-block;
  margin: 0 5px;
  text-decoration: none;
}

.box {
  width: 500px;
  height: 300px;
}
</style>
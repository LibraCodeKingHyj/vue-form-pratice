<template>
  <div>
    <div>
      <h4>{{ msg }}</h4>
    </div>
    <div>
      <button>确定</button>
      <button>取消</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg: "确定要删除吗？",
      isDel: false,
    };
  },
  methods: {},
};
</script>
<style scoped>
</style>

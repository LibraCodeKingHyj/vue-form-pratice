<template>
  <div class="pages">
    <button @click="prev" :disabled="prebtnstate">上一页</button>
    <span>第{{ pages }}页</span>
    <button @click="next" :disabled="nextbtnstate">下一页</button>
    <span>共{{ count }}条数据</span>
  </div>
</template>

<script>
export default {
  props: ["count", "pages", "nextpage", "prevpage"],
  data() {
    return {
      prebtnstate: true,
      nextbtnstate: true,
    };
  },
  methods: {
    next() {
      this.nextpage();
    },
    prev() {
      this.prevpage();
    },
  },
  watch: {
    count() {
      this.nextbtnstate = this.count > 5 ? true : false;

    },
    pages() {
      this.prebtnstate = this.pages === 1 ? true : false;
    },
  },
};
</script>

<style>
  .pages button{
    margin: 0 15px;
  }
</style>
<template>
  <div>
    <div class="flexBox">
      <div v-for="(cell,index) in dataLists"
        class="flexItem"
        @click="cellSelect(index)"
        :class="{cellCheck: cell.isactive}" :key="index"
      >{{`index:${index} val:${cell.isactive}`}}</div>
    </div>
    <p>{{dataLists}}</p>
  </div>
</template>

<script>
// const datas = new Array(12);
// datas.fill(1);

export default {
  name: "divRecord",
  data() {
    return {
      // dataLists: datas,
      dataLists: Array(12),
      hoge: "hoge"
    };
  },
  created() {
    // this.dataLists = this.dataLists.fill(null).map((_,i) => i+1).map(month => month + '月');
    // TODO: 配列が参照渡しになっているので個別にオブジェクトを生成
    this.dataLists = this.dataLists.fill({ isactive: false, task: "none" });
  },
  methods: {
    cellSelect(index) {
      if (this.dataLists[index].isactive === false) {
          this.dataLists[index].isactive = true;
          this.dataLists[index].task = 'work';
      } else {
        this.dataLists.splice(index, 1);
        this.dataLists.push({ isactive: false, task: 'none' });
      }
    }
  }
};
</script>

<style scoped>
div.flexBox {
  display: flex;
  flex-wrap: wrap;
  width: 100vw;
}

.flexItem {
  background-color: whitesmoke;
  width: 25vw;
  border: solid 1px;
}

.cellCheck {
  background-color: palegreen;
}
</style>
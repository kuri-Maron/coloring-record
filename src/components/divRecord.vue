<template>
  <div>
    <div class="flexBox">
      <div v-for="(cell,index) in dataLists"
        class="flexItem"
        @click="cellSelect(index)"
        :class="{cellCheck: cell.isActive}" :key="index"
      >{{`index:${index} val:${cell.isActive}`}}</div>
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
    // TODO: for文ダサいので、forerchかもっと良きメソッド使う。
    // this.dataLists = this.dataLists.fill({ isactive: false, task: "none" });
    for(let i=0; i<this.dataLists.length; i++){
        this.$set(this.dataLists,i,{isActive: false,task: 'none'})
    }
  },
  methods: {
    cellSelect(index) {
        console.log(index)
        console.log(this.dataLists[index])
      if (this.dataLists[index].isActive === false) {
          this.dataLists[index].isActive = true;
          this.dataLists[index].task = 'work';
      } else {
        this.dataLists.splice(index, 1);
        this.dataLists.push({ isActive: false, task: 'newNone' });
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
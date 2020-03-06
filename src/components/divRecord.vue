<template>
  <div>
    <div class="flexBox">
      <div
        v-for="(cell, index) in dataLists"
        class="flexItem"
        @click="cellSelect(index)"
        :class="{ cellCheck: cell.isActive }"
        :key="index"
      >{{ `index:${index} val:${cell.isActive}` }}</div>
    </div>
    <p>{{ dataLists }}</p>
  </div>
</template>

<script>
import firebase from "firebase";

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
  async created() {
    // TODO: for文ダサいので、forerchかもっと良きメソッド使う。
    for (let i = 0; i < this.dataLists.length; i++) {
      this.$set(this.dataLists, i, { isActive: false, task: "none" });
    }

    const db = firebase.firestore();
    let querySnapshot = await db
      .collection("myRecords")
      .doc("blocksState")
      .collection("blocks")
      .get();
    await querySnapshot.docs.forEach((doc, index) => {
      // console.log("index: ", index, doc.id, " => ", doc.data());
      this.$set(this.dataLists, index, doc.data());
    });

    // TODO: for文を書かない方法を模索中
    // this.dataLists.forEach((item, i, array) => {
    //   // item = {isActive: false,task: 'none'}
    //   item = false;
    //   array[i] = item;
    // });
  },
  async beforeDestroy() {
    const db = firebase.firestore();
    let collectionReference = await db
      .collection("myRecords")
      .doc("blocksState")
      .collection("blocks");
    let querySnapshot = await collectionReference.get();
    for (let i = 0; i < this.dataLists.length; i++) {
      if (querySnapshot.size > i) {
        console.log(querySnapshot.docs[i]);
        collectionReference.doc(querySnapshot.docs[i].id).update(this.dataLists[i]);
      } else {
        collectionReference.add(this.dataLists[i]);
      }
    }
  },
  methods: {
    cellSelect(index) {
      if (this.dataLists[index].isActive === true) {
        this.dataLists.splice(index, 1);
        this.dataLists.push({ isActive: false, task: "none" });
        // TODO: 今後は先のセルをクリックした場合、そこまで一気に色ぬり。
      } else if (index === 0 || this.dataLists[index - 1].isActive === true) {
        this.dataLists[index].isActive = true;
        this.dataLists[index].task = "work";
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

<template>
  <div>
    <table>
      <thead>
        <tr>
          <th>a</th>
          <th>b</th>
          <th>c</th>
          <th>d</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(rows, rowIdx) in tableDatas" :key="rowIdx">
          <td v-for="(data, colIdx) in rows" :key="colIdx">{{ data }}</td>
        </tr>
      </tbody>
    </table>
    <button @click="add">add</button>
    <button @click="sub">sub</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
    };
  },
  methods: {
    add() {
      let item = this.items[this.items.length - 1] + 1;
      this.items.push(item);
    },
    sub() {
      this.items.splice(this.items.length - 1, 1);
    }
  },
  computed: {
    tableDatas() {
      // 列数は固定
      const cols = 4;
      // 行数はデータ数から計算
      const rows = Math.ceil(this.items.length / cols);
      // 行数 x 列数の2次元配列を作成
      const arrays = Array.from(new Array(rows), () => new Array(cols).fill(0));
      // 配列のデータをコピー
      this.items.forEach((item, index) => {
        const rowIdx = Math.floor(index / cols);
        const colIdx = index % cols;
        arrays[rowIdx][colIdx] = item;
      });
      return arrays;
    }
  }
};
</script>
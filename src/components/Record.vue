<template>
  <!-- <table>
        <caption>塗り絵記録</caption>
        <tr v-for="(row,key) in 8" :key="key">
            <td v-for="(n,key) in 4" :key="key">○</td>
        </tr>
  </table>-->
  <div>
      <p>{{recordDatas.length}}</p>
    <table>
      <template v-for="(cell,key) in recordDatas">
        <tr v-if="(index%6===0)" :key="key"></tr>
      </template>
    </table>
  </div>
</template>

<script>
export default {
  name: "Record",
  data() {
    Array(40);
  },
  methods: {
      setCell () {
          this.recordDatas.push(1)
      }
  }
};
</script>
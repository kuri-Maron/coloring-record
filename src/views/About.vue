<template>
  <div class="about">
    <h1>This is an about page</h1>
    <table-record/>
  </div>
</template>

<script>
import tableRecord from '@/components/tableRecord.vue'

export default {
  name: 'About',
  components: {
    tableRecord
  }
}
</script>

<template>
  <div>
    <div class="banner">
      <h1 class="banner-header">Sticky table columns</h1>
    </div>
    <div>
      <div class="sticky-table-columns">
        <sticky-table></sticky-table>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import StickyTable from './StickyTable.vue';

@Component({
  components: { StickyTable }
})
export default class Main extends Vue {
}
</script>

<style>
.u-flex {
  display: flex;
}

.u-gap-small {
  gap: 5px;
}

.u-flex-wrap {
  flex-flow: wrap;
}

.u-txt-truncate {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.banner {
  background-color: #2b6597;
  border-bottom: 1px solid #14578f;
  padding: 20px 15px;
}

.banner-header {
  color: #fff;
  font-size: 2.2rem;
  margin: 0;
}

.sticky-table-columns {
  margin: 25px 20px 20px;
}
</style>

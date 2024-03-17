<template>
  <table>
    <RecycleScroller
      :style="scroller"
      :items="tableList"
      :item-size="25"
      list-class="tbody"
      key-field="id"
    >
      <template #before>
        <thead>
          <tr>
            <th>名前</th>
            <th>メールアドレス</th>
            <th>会社名</th>
            <th>権限1</th>
            <th>権限2</th>
          </tr>
        </thead>
      </template>
      <template v-slot="{ item }">
        <tr>
          <td>{{ item.name }}</td>
          <td>{{ item.email }}</td>
          <td>{{ item.company }}</td>
          <td>{{ item.auth1 }}</td>
          <td>{{ item.auth2 }}</td>
        </tr>
      </template>
    </RecycleScroller>
  </table>
</template>

<script lang="ts">
import { ref, computed } from "vue";
import { RecycleScroller } from "vue-virtual-scroller";
import "vue-virtual-scroller/dist/vue-virtual-scroller.css";

export default {
  components: {
    RecycleScroller,
  },
  setup() {
    const defaultCountListItem = ref(500000);
    const tableList = computed(() => {
      return new Array(defaultCountListItem.value).fill(null).map((item, i) => {
        return {
          id: i,
          name: `name-${i}`,
          email: `email-${i}`,
          company: `company-${i}`,
          auth1: `auth1-${i}`,
          auth2: `auth2-${i}`,
        };
      });
    });

    const scroller = {
      height: "200px",
      width: "700px",
    };

    return {
      tableList,
      scroller,
    };
  },
};
</script>

<style scoped>
th,
td {
  width: 200px;
}
</style>

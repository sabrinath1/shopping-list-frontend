<template>
  <Item></Item>
  <List></List>
</template>

<script lang="ts">
import { defineComponent } from "vue";

import Item from "@/components/Item.vue";
import List from "@/components/List.vue";

export default defineComponent({
  components: {
    Item,
    List,
  },
  data() {
    return {
      name: "Cataline",
    };
  },
});
</script>
<style scoped></style>

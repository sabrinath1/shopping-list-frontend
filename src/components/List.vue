<template>
  <section>
    <h5 class="title">Lista de Compras</h5>
    <ul>
      <li v-for="item in items" :key="item.id">
        <p>{{ item.name }}</p>
        <small>{{ item.quantity }}</small>
        <a class="destroy" @click="destroyItem(item.id)"></a>
      </li>
    </ul>
  </section>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import axios from "@/utils/axios";
import type { Items } from "@/interfaces/commons";

export default defineComponent({
  data() {
    return {
      items: [] as Items[],
    };
  },
  methods: {
    async destroyItem(id: Items["id"]) {
      try {
        await axios.delete(`/items/${id}`);
        const itemIndex = this.items.findIndex((items) => items.id == id);
        this.items.splice(itemIndex, 1);
      } catch (error) {
        console.warn(error);
      }
    },
  },
});
</script>

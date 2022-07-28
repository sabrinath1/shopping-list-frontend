<template>
  <div class="items"></div>
  <div class="container"></div>
  <section>
    <h5 class="title">Novo Item</h5>
    <form @submit.prevent="createItem">
      <input type="text" placeholder="Item" v-model="form.name" />
      <input type="number" placeholder="Quantidade" v-model="form.quantity" />
      <button type="submit">Adicionar</button>
    </form>
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";
interface Items {
  id: string;
  name: string;
  quantity: number;
}

export default defineComponent({
  data() {
    return {
      items: [] as Items[],
      form: {
        name: "",
        quantity: "",
      },
    };
  },
  created() {
    this.fetchItems();
  },
  methods: {
    async fetchItems() {
      try {
        const { data } = await axios.get("/items");
        this.items = data;
      } catch (error) {
        console.warn(error);
      }
    },
    async createItem() {
      try {
        const { data } = await axios.post("/items", this.form);
        this.items.push(data);
        this.form.name = "";
        this.form.quantity = "";
      } catch (error) {
        console.warn(error);
      }
    },
  },
});
</script>

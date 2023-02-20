<template>
 <div class="app">
  <div class="buttons">
    <button class="btn" @click="sortYear()">по году</button>
    <button class="btn" @click="sortPrice()">по цене</button>
  </div>
  <div class="grid">
    <item-handler
      v-for='card in cards'
      v-bind:key='card.id'
      :name='card.name'
      :model='card.model'
      :color='card.color'
      :year='card.year'
      :price='card.price'
      :method="(e) => method(e, card)"
      :deleteCard='() => deleteCard(card)'/>
  </div>
 </div>
</template>

<script lang="ts">
// eslint-disable-next-line import/no-extraneous-dependencies
import axios from 'axios';
import { defineComponent } from 'vue';
import ItemHandler from './components/ItemHandler/ItemHandler.vue';
import { ItemInterface, Cards } from './types';

export default defineComponent({
  components: {
    ItemHandler,
  },
  data() {
    return {
      cards: [] as Cards,
    };
  },
  mounted() {
    axios
      .get('https://test.tspb.su/test-task/vehicles')
      .then((res) => {
        const arr = res.data;
        arr.forEach((item: ItemInterface) => {
          this.cards.push(item);
        });
      });
  },
  methods: {
    sortYear() {
      this.cards.sort((a: ItemInterface, b: ItemInterface) => a.year - b.year);
    },
    sortPrice() {
      this.cards.sort((a: ItemInterface, b: ItemInterface) => a.price - b.price);
    },
    deleteCard(card: ItemInterface) {
      this.cards = this.cards.filter((i : ItemInterface) => i.id !== card.id);
    },
    method(e: any, card: ItemInterface) {
      const form = e.target.parentElement;
      const name = form.querySelector('#name');
      const price = form.querySelector('#price');
      const model = form.querySelector('#model');
      card.price = price.value;
      card.model = model.value;
      card.name = name.value;
    },
  },
});
</script>
<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@400;700;900&family=Prata&display=swap');
html {
  box-sizing: border-box;
  height: 100%;
  scroll-behavior: smooth;
}
*::before,
*::after {
  box-sizing: inherit;
}
* {
  margin: 0;
  box-sizing: border-box;
}
body {
  padding: 0;
  margin: 0;
  display: flex;
  font-family: "Prata";
  flex-direction: column;
  min-height: 100vh;
  font-size: 16px;
  line-height: 1.4;
  color: #000000;
  font-weight: 400;
}
main {
  flex-grow: 1;
}
a {
  text-decoration: none;
  cursor: pointer;
}
footer {
  flex-shrink: 0;
}
button {
  border: none;
  background: transparent;
  cursor: pointer;
}
img {
  max-width: 100%;
  height: auto;
  display: block;
}
ul {
  list-style: none;
  padding: 0;
}
input {
  border: none;
  outline: none;
  padding: 0;
}
.app {
  padding: 10px;
  flex-direction: column;
  gap: 10px;
}
.buttons {
  display: flex;
  gap: 10px;
  margin-bottom: 10px;
}
.btn {
  padding: 10px;
  font-weight: 500;
  border: 1px solid #d9d9d9;

  &:hover {
    background: #d9d9d9;
    color: #FFFFFF;
  }
}
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  gap: 20px;
}
</style>

<template>
  <div class="item">
    <button class="item__button" @click="deleteCard">
      <img src='@/assets/icons/icon-close.svg' alt="close"/>
    </button>
    <form @submit.prevent>
      <label for="name">
      <input class="item__name"
        :placeholder="name"
        :value="name"
        type="text"
        id="name"
        name="name"/>
      </label>
      <div class="item__model">
        <p>модель: </p>
        <label for="model">
        <input
          :placeholder="model"
          :value="model"
          type="text"
          id="model"
          name="model"/>
        </label>
      </div>
      <div class="item__color">цвет: <span>{{color}}</span></div>
      <div class="item__model item__price">
        <p>цена:</p>
        <label for="price">
          <input
            :placeholder="price"
            :value="price"
            type="number"
            id="price"
            name="price"/>
        </label>
      </div>
      <div class="item__year">год: <span>{{year}}</span></div>
      <button class="item__submit" type="submit" @click="method">сабмит</button>
    </form>
  </div>
</template>
<script lang="ts">
export default {
  props: [
    'name', 'model', 'color', 'price', 'year', 'deleteCard', 'method',
  ],
};
</script>
<style scoped lang="scss">
.item {
  display: flex;
  flex-direction: column;
  background: #d9d9d9;
  padding: 10px;
  position: relative;

  &__button {
    background: transparent;
    border: none;
    outline: none;
    position: absolute;
    right: 10px;
    top: 10px;
    cursor: pointer;
  }
  &__submit {
    padding: 5px;
    border: 1px solid #FFFFFF;
    &:hover {
      background: white;
    }
  }
  &__model {
    display: flex;
    gap: 10px;
    input {
      background: transparent;
      font-family: "Prata";
      font-weight: 500;
    }
  }
  &__name {
  font-weight: 600;
  width: 100%;
  text-align: center;
  background: transparent;
  font-weight: "Prata";
  }
  span {
    padding-left: 10px ;
  }
}
</style>

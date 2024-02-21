<template>
  <div>
    <input min="0" type="number" @input="changeAmount($event.target.value)" />
    <div>
      <button @click="convert()">Конвертировать</button>
      <button @click="favourite()" className="fav-but">
        Добавить в Избранное
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    changeAmount: {
      type: Function,
      required: true,
    },
    convert: {
      type: Function,
      required: true,
    },
    favourite: {
      type: Function,
      required: true,
    },
  },
};
</script>

<style scoped>
input {
  margin-top: 100px;
  margin-bottom: 20px;
  font-size: 1.2em;
  position: relative;
  top: -50px;
  outline: none;
  border-radius: 3px;
  padding: 10px 15px;
  border: none;
  background: #fafafa;
  color: #333;
  width: 500px;
}

button {
  position: relative;
  top: -20px;
  padding: 15px 20px;
  color: #fff;
  text-transform: uppercase;
  cursor: pointer;
  background: #786486;
  border: 0;
  border-radius: 3px;
}

button.fav-but {
  margin-left: 20px;
}
</style>

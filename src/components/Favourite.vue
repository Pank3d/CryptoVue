<template>
  <div>
    <h2>Варианты в Избранное</h2>
    <div
      v-for="(el, index) in favs"
      :key="index"
      className="fav"
      @click="getFromFavs(index)"
    >
      <span>
        {{ el.from }}
      </span>
      <span>
        {{ el.to }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    favs: {
      type: Array,
      required: true,
    },
    getFromFavs: {
      type: Function,
      required: true,
    },
  },
};
</script>

<style scoped>
h2 {
  color: #fff;
}

div.fav {
  display: flex;
  justify-content: space-between;
  margin: 10px auto;
  width: 200px;
}

span {
  cursor: pointer;
}
</style>

<template>
  <div id="app" class="bgc-main">
    <div>
      <div>
        <div class="pt-5 pb-5">
          <h1 class="main-title">Random Git Cat</h1>
        </div>
        <div class="bgc-select">
          <div class="pt-3">
            <label class="me-4">Título:</label>
            <input class="border-0 box-input" type="text" v-model="catInput" />
          </div>
          <div class="d-flex justify-content-center mt-2">
            <span class="my-auto me-4">Filtro:</span>
            <select
              v-model="filter"
              class="form-select filter-select"
              aria-label="Default select example"
            >
              <span>Filtro</span>
              <option v-for="(filter, i) in catFilter" :key="i" :value="filter">
                {{ filter }}
              </option>
            </select>
          </div>

          <div class="d-flex justify-content-center mt-2">
            <span class="my-auto me-4">Color:</span>
            <select
              v-model="color"
              class="form-select color-select__option"
              aria-label="Default select example"
            >
              <span>Color</span>
              <option v-for="(color, i) in colorText" :key="i" :value="color">
                {{ color }}
              </option>
            </select>
            <div
              class="color-select"
              :style="{ 'background-color': colorSelect }"
            ></div>
          </div>
          <div class="mt-2 pb-3">
            <label class="me-2">Tamaño:</label>
            <input class="border-0 box-input" v-model="size" type="number" />
          </div>
        </div>
        <div>
          <button @click="getButton" type="button" class="btn btn-cat">
            Obtener mi Gatito
          </button>
        </div>
        <div class="my-3">
          <img :src="catData" alt="" class="mb-3" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      URL: "https://cataas.com/cat/gif/says/",
      catFilter: ["blur", "mono", "sepia", "negative", "paint", "pixel"],
      colorText: ["red", "blue", "green", "yellow", "purple", "white"],
      catData: "",
      catInput: "",
      filter: "",
      color: "",
      size: "",
    };
  },
  created() {
    this.getCat();
  },
  computed: {
    colorSelect() {
      return this.color;
    },
  },
  methods: {
    async getCat() {
      try {
        const res = await fetch(
          this.URL +
            this.catInput +
            "?filter=" +
            this.filter +
            "&color=" +
            this.color +
            "&size=" +
            this.size +
            "&type=or"
        );
        this.catData = res.url;
        console.log(this.catData);
      } catch (error) {
        console.error(error);
      }
    },
    getButton() {
      this.getCat();
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.main-title {
  color: rgb(10, 96, 125);
}
.filter-select {
  width: 202px;
  margin-left: 5px;
}
.color-select__option {
  width: 147px;
  margin-left: 5px;
}
.btn-cat {
  background-color: rgb(5, 127, 167);
  color: white;
  font-size: 20px;
  margin-top: 20px;
  width: 271px;
}
.color-select {
  border-radius: 50%;
  width: 50px;
  margin-left: 10px;
}
.bgc-main {
  background-color: #97e7f5;
}
.bgc-select {
  color: rgb(10, 96, 125);
  background-color: rgb(241, 145, 161);
}
.box-input {
  border-radius: 3px;
  height: 37px;
}
</style>

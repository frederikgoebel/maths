<template>
  <div class="container card">
    <h1>Map scale calculator</h1>
    <form>
      <fieldset class="container">
        <label>Scale</label>
        <div class="inputBar">
          <input type="text" disabled class="scaleInput" value="1:" />
          <input type="number" v-model="scale" value="1000" />
          <button @click.prevent="recalc(scale)">
            <font-awesome-icon icon="sync" />
          </button>
        </div>
      </fieldset>
      <fieldset class="container">
        <label>Map distance</label>
        <div class="inputBar">
          <input type="number" v-model="onMap" value="100" />
          <select v-model="onMapUnit">
            <option value="0.001">mm</option>
            <option selected value="0.01">cm</option>
            <option value="1">m</option>
          </select>
          <button @click.prevent="recalc(onMap)">
            <font-awesome-icon icon="sync" />
          </button>
        </div>
      </fieldset>

      <fieldset class="container">
        <label>Real distance</label>
        <div class="inputBar">
          <input type="number" v-model="inReal" value="1" />
          <select v-model="inRealUnit">
            <option selected value="1000">km</option>
            <option value="1">m</option>
            <option value="0.01">cm</option>
          </select>
          <button @click.prevent="recalc(inReal)">
            <font-awesome-icon icon="sync" />
          </button>
        </div>
      </fieldset>
    </form>
  </div>
</template>

<script>
export default {
  data: () => ({
    scale: 1000,
    onMap: 100,
    inReal: 1,
    onMapUnit: 0.01,
    inRealUnit: 1000,
  }),
  props: {
    msg: String,
  },
  methods: {
    recalc(clickedElem) {
      switch (clickedElem) {
        case this.scale:
          if (this.onMap && this.inReal)
            this.scale =
              (this.inReal * this.inRealUnit) / (this.onMap * this.onMapUnit);
          break;
        case this.onMap:
          if (this.scale && this.inReal)
            this.onMap =
              (this.inReal * this.inRealUnit) / this.scale / this.onMapUnit;
          break;
        case this.inReal:
          if (this.scale && this.onMapUnit)
            this.inReal =
              (this.scale * (this.onMap * this.onMapUnit)) / this.inRealUnit;
          break;
      }
    },
  },
};
</script>


<style>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 1.5rem;
}

.card {
  flex-direction: column;
  padding: 4rem;
  padding-top: 3rem;
  border-radius: 1rem;
  border: 1px solid black;
}

label,
select,
input,
button {
  border-radius: 0;
  font-size: 1.5rem;
  height: 2rem;
  padding: 0.4rem 0.6rem;
  box-sizing: content-box;
  font-family: freight-text-pro;
  color: var(--text-color);
}

h1 {
  margin-top: 0;
  margin-bottom: 3rem;
  font-size: 2rem;
  color: var(--text-color);
}

form {
  display: flex;
  flex-direction: column;
}

input {
  flex: 1;
  margin: 0;
  width: 8em;
  margin-bottom: 0.3em;
  border: 1px solid black;
  padding-left: 0.5em;
  margin-right: 0;
  border-radius: 0.6rem 0 0 0.6rem;
  font-weight: 600;
}

button {
  margin: 0;

  background: white;
  border: 1px solid black;
  cursor: pointer;
  margin-left: 0;
  border-radius: 0 0.6rem 0.6rem 0;
  border-left: none;
  padding-left: 1rem;
  padding-right: 1rem;
  font-size: 1rem;
}

button:focus,
input:focus {
  outline: none;
}

fieldset {
  font-size: 1em;
  padding: 0;
  border-radius: 1em;
  border-width: 0;
  padding: 0.2rem;
}

label {
  width: 14rem;
  text-align: end;
}

select {
  vertical-align: top;
  border: none;
  border-top: 1px solid black;
  border-bottom: 1px solid black;
  border-right: 1px solid black;
  -moz-appearance: none; /* Firefox */
  -webkit-appearance: none; /* Safari and Chrome */
  appearance: none;
  width: 4rem;
}

.scaleInput {
  flex: 0;
  border-right: none;
  background: white;
  width: 1.4rem;
  padding-right: 0;
}

.scaleInput + input {
  border-left: none;
  border-radius: 0;
  padding-left: 0;
}
.inputBar {
  display: flex;
  width: 100%;
}
</style>

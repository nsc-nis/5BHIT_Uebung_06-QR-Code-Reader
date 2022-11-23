<template>
  <h2>The easiest way to create QR Code</h2>
  <h3>Generate a QR-Code and download it</h3>
  <form>
    <input id="textField_url" type="text" />
  </form>
  <div id="colorPicker" style="position: relative">
    <input id="textField_color" type="text" readonly v-model="color" />
    <button
      id="button_color"
      :style="{ background: color }"
      @click="showcolorpicker = showcolorpicker ? false : true"
    >
      &nbsp;
    </button>

    <div
      v-show="showcolorpicker"
      style="position: relative"
      id="colorPickerDiv"
    >
      <ColorPicker
        theme="light"
        :color="color"
        :sucker-hide="false"
        :sucker-canvas="suckerCanvas"
        :sucker-area="suckerArea"
        @changeColor="changeColor"
        @openSucker="openSucker"
      />
    </div>
  </div>
</template>

<script>
import { ColorPicker } from 'vue-color-kit';
import 'vue-color-kit/dist/vue-color-kit.css';
import { ref } from 'vue';

export default {
  name: 'Main',
  components: {
    ColorPicker,
  },
  setup() {
    let color = ref('#FF007B');
    let suckerHide = ref(false);
    let suckerCanvas = null;
    let suckerArea = ref([]);
    let showcolorpicker = ref(true);
    function changeColor(_color) {
      //const { r, g, b, a } = _color.rgba;
      //color.value = `rgba(${r}, ${g}, ${b}, ${a})`;
      color.value = _color.hex;
    }
    function openSucker(isOpen) {
      if (isOpen) {
        // ... canvas be created
        this.suckerCanvas = canvas;
        this.suckerArea = [x1, y1, x2, y2];
      } else {
        this.suckerCanvas && this.suckerCanvas.remove;
      }
    }
    return {
      color,
      suckerHide,
      suckerCanvas,
      suckerArea,
      changeColor,
      showcolorpicker,
      openSucker,
    };
  },
};
</script>

<style scoped>
#textField_url {
  width: 500px;
  height: 30px;
}

#textField_color {
  width: 60px;
  height: 30px;
}

form {
  display: inline;
  margin: 1em;
}

#button_color {
  height: 37px;
  width: 35px;
}

#colorPicker {
  display: inline;
  align: center;
  decoration: none;
}

#colorPickerDiv {
  margin-left: auto;
  position: relative;
  x: 30px;
}

h3 {
  margin: 0 1em 1em 1em;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

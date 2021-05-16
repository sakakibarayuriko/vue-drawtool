<template>
  <h1>DrawTool</h1>
  <div class="draw-area">
    <div id="canvas-area">
      <canvas
        id="myCanvas"
        v-bind:class="{ eraser: canvasMode === 'eraser' }"
        width="640"
        height="640"
        @mousedown="dragStart"
        @mouseup="dragEnd"
        @mouseout="dragEnd"
        @mousemove="draw"
      ></canvas>
    </div>
    <div id="tool-area">
      <input type="radio" id="pen" name="tool" checked="checked" @change="pen" />
      <label for="pen">
        <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 200.008 200"><g transform="translate(-14.955 -264.331)"><path d="M164,264.331,33.768,394.567l50.959,50.959L214.963,315.29ZM20.59,408.165l-4.175,53.46-1.46,1.46,1.36-.1-.117,1.35,1.46-1.459,53.469-4.165Z" transform="translate(0 0)"/></g></svg>
      </label>
      <input type="radio" id="eraser" name="tool" @change="eraser" />
      <label for="eraser">
        <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 199.997 200"><path d="M235.177,4027.791l38.549-38.552,83.632-83.63-77.816-77.818-83.632,83.635-38.549,38.549Zm31.834-45.265L235.735,4013.8l-64.386-64.392,31.274-31.274Z" transform="translate(-157.361 -3827.791)"/></svg> 
      </label>
      <div v-if="canvasMode !== 'eraser'">
        <input type="radio" id="pen-black" name="color" checked="checked" @change="penBlack" />
        <label for="pen-black" class="black"></label>
        <input type="radio" id="pen-red" name="color" @change="penRed" />
        <label for="pen-red" class="red"></label>
        <input type="radio" id="pen-blue" name="color" @change="penBlue" />
        <label for="pen-blue" class="blue"></label>
        <input type="radio" id="pen-yellow" name="color" @change="penYellow" />
        <label for="pen-yellow" class="yellow"></label>
        <input type="radio" id="pen-green" name="color" @change="penGreen" />
        <label for="pen-green" class="green"></label>
      </div>
      <button id="clear" @click="clear"><svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 172.519 200"><path d="M80.123,263.266a7.7,7.7,0,0,0-7.637,7.633v7.629H23.247a7.7,7.7,0,0,0-7.629,7.637v19.848a7.7,7.7,0,0,0,7.629,7.637H180.5a7.7,7.7,0,0,0,7.633-7.637V286.165a7.7,7.7,0,0,0-7.633-7.637H131.268V270.9a7.7,7.7,0,0,0-7.637-7.633Zm0,7.633h43.509v11.454a3.817,3.817,0,0,0,3.817,3.813H180.5v19.848H23.247V286.165H76.3a3.817,3.817,0,0,0,3.82-3.812ZM45,318.228a7.7,7.7,0,0,0-7.637,7.633V455.636A7.7,7.7,0,0,0,45,463.266H158.749a7.7,7.7,0,0,0,7.633-7.629V325.86a7.7,7.7,0,0,0-7.633-7.633Zm0,7.633H158.749V455.636H45Zm20.168,16.032a5.3,5.3,0,0,0-4.746,3.266,9.766,9.766,0,0,0-.918,4.367v78.63a9.734,9.734,0,0,0,.918,4.359,5.3,5.3,0,0,0,4.746,3.27h7.754a5.3,5.3,0,0,0,4.746-3.27,9.736,9.736,0,0,0,.922-4.359v-78.63a9.771,9.771,0,0,0-.922-4.367,5.3,5.3,0,0,0-4.746-3.266Zm32.825,0a5.3,5.3,0,0,0-4.746,3.266,9.766,9.766,0,0,0-.918,4.367v78.63a9.734,9.734,0,0,0,.918,4.359A5.3,5.3,0,0,0,98,435.784h7.754a5.3,5.3,0,0,0,4.746-3.27,9.736,9.736,0,0,0,.922-4.359v-78.63a9.771,9.771,0,0,0-.922-4.367,5.3,5.3,0,0,0-4.746-3.266Zm32.825,0a5.284,5.284,0,0,0-4.738,3.266,9.773,9.773,0,0,0-.926,4.367v78.63a9.74,9.74,0,0,0,.926,4.359,5.287,5.287,0,0,0,4.738,3.27h7.758a5.293,5.293,0,0,0,4.742-3.27,9.736,9.736,0,0,0,.922-4.359v-78.63a9.772,9.772,0,0,0-.922-4.367,5.29,5.29,0,0,0-4.742-3.266Zm-63.677,7.633h3.813v78.63H67.146Zm32.825,0h3.813v78.63H99.971Zm32.825,0h3.813v78.63H132.8Z" transform="translate(-15.617 -263.266)"/></svg></button>
      <button id="download" @click="download"><svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 200 198.182"><path d="M81.457,0V74.5H49.223L100,152.022,150.769,74.5H118.536V0ZM11.124,163.146A11.1,11.1,0,0,0,0,174.269v12.789a11.1,11.1,0,0,0,11.124,11.124H188.876A11.1,11.1,0,0,0,200,187.059V174.269a11.1,11.1,0,0,0-11.124-11.124Z"/></svg></button>
    </div>
  </div>
</template>

<script>
export default {
  name: "DrawTool",
  data() {
    return {
      canvasMode: "pen",
      canvas: null,
      context: null,
      isDrag: false,
    };
  },
  mounted() {
    this.canvas = document.querySelector("#myCanvas");
    this.context = this.canvas.getContext("2d");
    this.pen();
  },
  methods: {
    // 描画
    draw(e) {
      const x = e.layerX;
      const y = e.layerY;
      if (!this.isDrag) {
        return;
      }
      this.context.lineTo(x, y);
      this.context.stroke();
    },
    // 描画開始（mousedown）
    dragStart(e) {
      const x = e.layerX;
      const y = e.layerY;
      this.context.beginPath();
      this.context.lineTo(x, y);
      this.context.stroke();
      this.isDrag = true;
    },
    // 描画終了（mouseup, mouseout）
    dragEnd() {
      this.context.closePath();
      this.isDrag = false;
    },
    // ペンモード
    pen() {
      this.canvasMode = "pen";
      this.context.lineCap = "round";
      this.context.lineJoin = "round";
      this.context.lineWidth = 5;     
      this.penBlack();
    },
    // 消しゴムモード
    eraser() {
      this.canvasMode = "eraser";
      this.context.lineCap = "square";
      this.context.lineJoin = "square";
      this.context.lineWidth = 30;
      this.context.strokeStyle = "#FFFFFF";
    },
    // ペンモード（黒）
    penBlack() {
      this.canvasMode = "penBlack";
      this.context.strokeStyle = "#000000";
    },
    // ペンモード（赤）
    penRed() {
      this.canvasMode = "penRed";
      this.context.strokeStyle = "#e7695d";
    },
    // ペンモード（青）
    penBlue() {
      this.canvasMode = "penBlue";
      this.context.strokeStyle = "#518ceb";
    },
    // ペンモード（黄色）
    penYellow() {
      this.canvasMode = "penYellow";
      this.context.strokeStyle = "#efcc67";
    },
    // ペンモード（緑）
    penGreen() {
      this.canvasMode = "penGreen";
      this.context.strokeStyle = "#7dcb71";
    },
    // クリア
    clear() {
      this.context.clearRect(0, 0, this.canvas.width, this.canvas.height);
    },
    // 画像ダウンロード
    download() {
      const link = document.createElement("a");
      link.href = this.canvas.toDataURL("image/png");
      link.download = "canvas-" + new Date().getTime() + ".png";
      link.click();
    },
  },
};
</script>

<style scoped>
.draw-area {
  display: flex;
  margin: 0 360px;
}
#myCanvas {
  border: 1px solid #000000;
}
.tool-area {
  width: 60px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.black {
  background-color:#000000;
}
.red {
  background-color: #e7695d;
}
.blue {
  background-color: #518ceb;
}
.yellow {
  background-color: #efcc67;
}
.green {
  background-color: #7dcb71;
}
.eraser {
  cursor: url(../assets/image/eraser.png) 15 15, auto;
}
</style>
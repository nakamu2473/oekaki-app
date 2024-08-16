<template>
  <main>
    <p>ここにお絵描き</p>
    <canvas ref="canvas" width="512" height="512"
      style="border: 1px solid #000;"
      @mousedown="startDrawing"
      @mousemove="draw"
      @mouseup="stopDrawing"
      @mouseout="stopDrawing"
    ></canvas>
    <span>...</span>
    <button ref="download">download</button>
    
  </main>
</template>

<script>
export default {
  data: () => {
    return {
      canvas: null,
      ctx: null,

      download: null, 

      isDrawing: false, // マウスが押されているかどうかを追跡
      lastPos: { x: 0, y: 0 }, // 前回の描画位置を保存

      draws:[]
    };
  },
  mounted(){
    this.canvas = this.$refs.canvas;
    this.ctx = this.canvas.getContext('2d');

    this.download = this.$refs.download;
    this.download.addEventListener( "click", this.saveImage );
  },
  methods: {
    // マウスダウン時に描画を開始
    startDrawing(e) {
      this.isDrawing = true;
      this.lastPos = this.getMousePos(e); // 最初の位置を保存
    },
    // マウス移動時に描画
    draw(e) {
      if (!this.isDrawing) return;

      const mousePos = this.getMousePos(e);
      
      // 前回の位置から現在の位置まで線を引く
      this.ctx.beginPath();
      this.ctx.moveTo(this.lastPos.x, this.lastPos.y);
      this.ctx.lineTo(mousePos.x, mousePos.y);
      this.ctx.strokeStyle = "#000000";  // 描画する線の色を設定
      this.ctx.lineWidth = 1;  // 線の太さを設定
      this.ctx.stroke();
      this.ctx.closePath();

      // 描画したデータを保存
      this.draws.push(this.ctx)
      console.log(this.draws)
      localStorage.setItem("draws", JSON.stringify(this.draws))

      // 現在の位置を次回の開始点として保存
      this.lastPos = mousePos;
    },
    // マウスアップ時またはキャンバス外に出たときに描画を終了
    stopDrawing() {
      this.isDrawing = false;
    },
    // マウス位置を取得
    getMousePos(e) {
      const rect = this.$refs.canvas.getBoundingClientRect();
      return {
        x: e.clientX - rect.left,
        y: e.clientY - rect.top,
      };
    },
    // 画像を保存
    saveImage(){
      const link = document.createElement("a");          
      link.href = this.canvas.toDataURL("image/png");
      link.download = "dot.png";
      link.click();
    },

    drawUp() {
            console.log(this.draws)
            this.draws.push(this.note)
            console.log(this.draws)
            localStorage.setItem("draws", JSON.stringify(this.draws))
            console.log(localStorage.getItem("draws"))
    },
  }
}
</script>
<style>
canvas {
  cursor: crosshair;
}
</style>
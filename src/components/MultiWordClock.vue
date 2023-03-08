<template>
  <div class="clock">
    <canvas ref="canvas" width="200" height="200"></canvas>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentDate: new Date(),
      hours: 0,
      minutes: 0,
      seconds: 0,
      radius: 80,
      centerX: 100,
      centerY: 100,
    };
  },
  mounted() {
    setInterval(() => {
      this.currentDate = new Date();
      this.seconds = this.currentDate.getSeconds() * 6;
      this.minutes = (this.currentDate.getMinutes() + this.seconds / 360) * 6;
      this.hours = (this.currentDate.getHours() + this.minutes / 360) * 30;
      this.drawClock();
    }, 1000);
  },
  methods: {
    drawClock() {
      let ctx = this.$refs.canvas.getContext("2d");
      ctx.clearRect(0, 0, 200, 200);
      this.drawCircle(ctx);
      this.drawNumbers(ctx);
      this.drawHourHand(ctx);
      this.drawMinuteHand(ctx);
      this.drawSecondHand(ctx);
    },
    drawCircle(ctx) {
      ctx.beginPath();
      ctx.arc(this.centerX, this.centerY, this.radius, 0, 2 * Math.PI);
      ctx.lineWidth = 10;
      ctx.strokeStyle = "#2c3e50";
      ctx.stroke();
    },
    drawNumbers(ctx) {
      ctx.font = "20px Roboto";
      ctx.fillStyle = "#2c3e50";
      ctx.textAlign = "center";
      ctx.textBaseline = "middle";
      for (let i = 1; i <= 12; i++) {
        let angle = (i * Math.PI) / 6;
        let x = this.centerX + (this.radius - 20) * Math.sin(angle);
        let y = this.centerY - (this.radius - 20) * Math.cos(angle);
        ctx.fillText(i.toString(), x, y);
      }
    },
    drawHourHand(ctx) {
      let angle = (this.hours * Math.PI) / 180;
      let x = this.centerX + 0.5 * this.radius * Math.sin(angle);
      let y = this.centerY - 0.5 * this.radius * Math.cos(angle);
      ctx.beginPath();
      ctx.moveTo(this.centerX, this.centerY);
      ctx.lineTo(x, y);
      ctx.lineWidth = 6;
      ctx.strokeStyle = "#c0392b";
      ctx.stroke();
    },
    drawMinuteHand(ctx) {
      let angle = (this.minutes * Math.PI) / 180;
      let x = this.centerX + 0.7 * this.radius * Math.sin(angle);
      let y = this.centerY - 0.7 * this.radius * Math.cos(angle);
      ctx.beginPath();
      ctx.moveTo(this.centerX, this.centerY);
      ctx.lineTo(x, y);
      ctx.lineWidth = 4;
      ctx.strokeStyle = "#3498db";
      ctx.stroke();
    },
    drawSecondHand(ctx) {
      let angle = (this.seconds * Math.PI) / 180;
      let x = this.centerX + 0.8 * this.radius * Math.sin(angle);
      let y = this.centerY - 0.8 * this.radius * Math.cos(angle);
      ctx.beginPath();
      ctx.moveTo(this.centerX, this.centerY);
      ctx.lineTo(x, y);
      ctx.lineWidth = 2;
      ctx.strokeStyle = "#f1c40f";
      ctx.stroke();
    },
  },
};
</script>


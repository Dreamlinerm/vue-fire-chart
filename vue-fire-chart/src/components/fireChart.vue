<template>
  <div class="flex justify-center w-full">
    <svg viewBox="-100 -10 100 120" version="1.1" xmlns="http://www.w3.org/2000/svg" class="w-full h-full">
      <path v-for="(label, index) in circleOptions" :key="index" :d="getPath(index)" :fill="getColor(index)" />
      <text :style="'font-size:' + fontSize" :fill="textColor" x="-100" y="-5">
        {{ yaxisTitle }}
      </text>
      <text v-for="(label, index) in circleOptions" :key="index" :style="'font-size:' + fontSize" :fill="textColor"
        :x="getWidth(index)" :y="getHight(index) + 5">
        {{ label }}: {{ circleData[index] }}
      </text>
      <line v-for="(label, index) in circleOptions" :key="index" x1="0" x2="-100" :y1="getHight(index)"
        :y2="getHight(index)" :stroke="getColor(index)" stroke-width="0.5" />
    </svg>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "fireChart",
  components: {},
  async mounted() {
    this.maxValue = Math.max(...this.circleData);
    // iphone compatibility set textLength to 100 manually and then reset
    setTimeout(() => {
      document.querySelectorAll("text").forEach((el) => {
        el.removeAttribute("textLength");
      });
    }, 200);
  },
  /**
  * @param{number} circleOptions The labels for the circles
  * @param{number} circleData The height of the circles
  * @param{string} yaxisTitle The title of the y-axis
  * @param{string} textColor The color of the text
  * @param{string} fontSize The font-size of the text
  * @param{Array} colors The colors of the circles
  * @param{boolean} circle If the circles should be circles or ovals
  */
  props: {
    circleOptions: {
      type: Array,
      required: true,
      default: () => ["Braunkohle", "Steinkohle", "Erdgas", "Windkraft"],
    },
    circleData: {
      type: Array,
      required: true,
      default: () => [1137, 853, 381, 10],
    },
    yaxisTitle: {
      type: String,
      required: true,
      default: "Gramm CO₂ je erzeugter kWh",
    },
    textColor: {
      type: String,
      required: false,
      default: "white",
    },
    fontSize: {
      type: String,
      required: false,
      default: "0.3em",
    },
    colors: {
      type: Array,
      required: false,
      default: () => ["#d23227", "#f67d20", "#ffe10c", "#fffffd"],
    },
    circle: {
      type: Boolean,
      required: false,
      default: true,
    },
  },
  data() {
    return {
      maxValue: 0,
    };
  },
  methods: {
    getPath(index) {
      let tmp = "M0 ";
      tmp += this.getHight(index);
      // round
      if (this.circle)
        tmp += "A1 1 0 000 100L0 0";
      // oval
      else tmp += "A1 .5 90 000 100L0 0";
      return tmp;
    },
    getHight(index) {
      return 100 - Math.round((this.circleData[index] / this.maxValue) * 100);
    },
    getWidth(index) {
      if (index != 0 && this.getHight(index) - this.getHight(index - 1) <= 5) {
        return -100 + 30 + "";
      } else {
        return "-100";
      }
    },
    getColor(index) {
      return this.colors[index];
    },
  },
});
</script>

<style>
.flex {
  display: flex;
}

.justify-center {
  justify-content: center;
}

.w-full {
  width: 100%;
}

.h-full {
  height: 100%;
}
</style>

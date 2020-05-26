<template>
  <div>
    <svg>
      <circle
        :cx="circlePos.x"
        :cy="circlePos.y"
        :r="radius"
        fill="none"
        stroke="black"
        stroke-width="1"
      ></circle>
      <line :x1="circlePos.x" :y1="circlePos.y" :x2="minutePos.x" :y2="minutePos.y" stroke="black"></line>
      <line :x1="circlePos.x" :y1="circlePos.y" :x2="hourPos.x" :y2="hourPos.y" stroke="black"></line>
      <template v-if="showHourMarks">
        <template v-for="mark in hourMarks">
          <line
            :key="mark.hour"
            :x1="mark.x1"
            :y1="mark.y1"
            :x2="mark.x2"
            :y2="mark.y2"
            stroke="black"
          ></line>
        </template>
      </template>
      <template v-if="showMinuteMarks">
        <template v-for="mark in minuteMarks">
          <line
            :key="mark.hour"
            :x1="mark.x1"
            :y1="mark.y1"
            :x2="mark.x2"
            :y2="mark.y2"
            stroke="black"
          ></line>
        </template>
      </template>
    </svg>
  </div>
</template>

<script>
export default {
  name: "Clock",
  props: {
    radius: Number,
    minute: Number,
    hour: Number,
    showHourMarks: Boolean,
    showMinuteMarks: Boolean
  },

  methods: {
    findPoint: function(angle, length = this.radius) {
      const cornerRad = ((angle - 90) * Math.PI) / 180;
      const nx = Math.cos(cornerRad) * length + this.circlePos.x;
      const ny = Math.sin(cornerRad) * length + this.circlePos.y;
      return { x: nx, y: ny };
    },
    graduationMarks: function(end, length) {
      return Array.from({ length: end }, (_, i) => i).map(grad => {
        const angle = grad * (360.0 / end);
        const { x: x1, y: y1 } = this.findPoint(angle, this.radius - length);
        const { x: x2, y: y2 } = this.findPoint(angle, this.radius);
        return { grad, x1, y1, x2, y2 };
      });
    }
  },
  computed: {
    circlePos: function() {
      const center = this.radius + 10;
      return { x: center, y: center };
    },
    minutePos: function() {
      const angle = this.minute * 6.0;
      return this.findPoint(angle, this.radius * 0.8);
    },
    hourPos: function() {
      const angle = this.hour * 30.0 + this.minute * 0.5;
      return this.findPoint(angle, this.radius * 0.6);
    },
    hourMarks: function() {
      return this.graduationMarks(12, 5);
    },
    minuteMarks: function() {
      return this.graduationMarks(60, 2);
    }
  }
};
</script>
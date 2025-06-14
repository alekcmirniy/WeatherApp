<template>
  <div class="update-widget">
    <p>🔄 Time until next update:</p>
    <div 
      class="countdown" 
      @mouseenter="showFull = true" 
      @mouseleave="showFull = false"
    >
      <p v-if="date">
        {{ showFull ? fullCountdown(date) : daysCountdown(date) }}
      </p>
    </div>
  </div>
</template>

<script lang="ts">
import { globalUpdateDate } from '../assets/UpdateDate';

export default {
  name: 'UpdateWidget',
  data() {
    return {
      input: globalUpdateDate || '',
      date: null as null | Date,
      showFull: false,
      timer: null as number | null,
    };
  },
  methods: {
    parseDate() {
      const parsed = new Date(this.input);
      if (!isNaN(parsed.getTime())) {
        this.date = parsed;
      } else {
        console.warn('Invalid date:', this.input);
        this.date = null;
      }
    },
    daysCountdown(targetDate: Date) {
      const now = new Date();
      const diff = targetDate.getTime() - now.getTime();
      const days = Math.floor(diff / (1000 * 60 * 60 * 24));
      return `${days} day${days !== 1 ? 's' : ''}`;
    },
    fullCountdown(targetDate: Date) {
      const diff = targetDate.getTime() - new Date().getTime();
      const days = Math.floor(diff / (1000 * 60 * 60 * 24));
      const hours = Math.floor((diff / (1000 * 60 * 60)) % 24);
      const minutes = Math.floor((diff / (1000 * 60)) % 60);
      const seconds = Math.floor((diff / 1000) % 60);
      return `${days}d ${hours}h ${minutes}m ${seconds}s`;
    },
    startTimer() {
      this.timer = window.setInterval(() => {
        this.$forceUpdate();
      }, 1000);
    },
    stopTimer() {
      if (this.timer) {
        clearInterval(this.timer);
        this.timer = null;
      }
    },
  },
  mounted() {
    this.parseDate();
    this.startTimer();
  },
  beforeUnmount() {
    this.stopTimer();
  },
};
</script>

<style scoped lang="scss">
.update-widget {
  background: linear-gradient(135deg, #3a1c71, #d76d77);
  border-radius: 12px;
  padding: 10px 15px;
  width: 160px;
  color: #f3e9d2;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  text-align: center;
  box-shadow: 0 0 8px rgba(215, 109, 119, 0.7);
  user-select: none;

  p { 
    margin: 5px 0;
  }
}

.countdown {
  cursor: default;
  font-weight: 600;
  font-size: 1.1em;
  background: rgba(255, 255, 255, 0.15);
  border-radius: 8px;
  padding: 8px 12px;
  transition: background-color 0.3s ease;

  &:hover {
    background-color: rgba(255, 255, 255, 0.3);
  }
}
</style>

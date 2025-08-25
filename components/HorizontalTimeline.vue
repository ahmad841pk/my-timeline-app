<template>
    <div class="timeline-wrapper">
      <div class="timeline" ref="track">
        <div
          v-for="(it, i) in items"
          :key="i"
          class="timeline-item"
          :class="{ active: i === value }"
          @click="$emit('input', i)"
          :title="it.label"
        >
          <div class="dot" />
          <div class="label">{{ it.label }}</div>
          <div class="meta" v-if="it.date">{{ it.date }}</div>
        </div>
      </div>
  
      <div class="content" v-if="current">
        <h3 class="content-title">{{ current.label }}</h3>
        <p class="content-date" v-if="current.date">{{ current.date }}</p>
        <div class="content-body" v-html="current.content" />
      </div>
  
      <div class="controls">
        <button @click="prev" :disabled="value <= 0">Prev</button>
        <button @click="next" :disabled="value >= items.length - 1">Next</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'HorizontalTimeline',
    props: {
      items: {
        type: Array,
        required: true,
        // [{ label: 'Kickoff', date: '2024-01-12', content: '<b>Started</b>…' }]
      },
      value: { // v-model for active index
        type: Number,
        default: 0
      }
    },
    computed: {
      current() {
        return this.items && this.items[this.value]
      }
    },
    watch: {
      value() {
        this.scrollActiveIntoView()
      }
    },
    mounted() {
      this.scrollActiveIntoView()
    },
    methods: {
      scrollActiveIntoView() {
        this.$nextTick(() => {
          const track = this.$refs.track
          const active = track && track.querySelector('.timeline-item.active')
          if (active && track) {
            const aRect = active.getBoundingClientRect()
            const tRect = track.getBoundingClientRect()
            const offset = active.offsetLeft - (tRect.width - aRect.width) / 2
            track.scrollTo({ left: Math.max(offset, 0), behavior: 'smooth' })
          }
        })
      },
      prev() {
        if (this.value > 0) this.$emit('input', this.value - 1)
      },
      next() {
        if (this.value < this.items.length - 1) this.$emit('input', this.value + 1)
      }
    }
  }
  </script>
  
  <style scoped>
  .timeline-wrapper {
    display: grid;
    grid-template-rows: auto auto auto;
    gap: 16px;
  }
  
  /* Horizontal rail */
  .timeline {
    display: grid;
    grid-auto-flow: column;
    grid-auto-columns: minmax(140px, 1fr);
    align-items: center;
    gap: 24px;
    overflow-x: auto;
    padding: 16px 8px;
    scroll-snap-type: x mandatory;
    border-bottom: 1px solid #e5e7eb;
    position: relative;
  }
  
  /* line under dots */
  .timeline::before {
    content: "";
    position: absolute;
    left: 0; right: 0;
    height: 2px;
    background: #e5e7eb;
    top: 32px; /* aligns with dots */
    z-index: 0;
  }
  
  .timeline-item {
    position: relative;
    scroll-snap-align: center;
    text-align: center;
    cursor: pointer;
    user-select: none;
  }
  
  .dot {
    width: 14px;
    height: 14px;
    border-radius: 50%;
    background: #9ca3af;
    border: 3px solid white;
    box-shadow: 0 0 0 2px #9ca3af;
    margin: 0 auto 8px;
    position: relative;
    z-index: 1;
  }
  
  /* active state */
  .timeline-item.active .dot {
    background: #111827;
    box-shadow: 0 0 0 2px #111827;
  }
  
  .label {
    font-size: 14px;
    font-weight: 600;
    color: #111827;
    white-space: nowrap;
  }
  
  .meta {
    font-size: 12px;
    color: #6b7280;
    margin-top: 2px;
  }
  
  .content {
    border: 1px solid #e5e7eb;
    border-radius: 12px;
    padding: 16px;
  }
  
  .content-title {
    margin: 0 0 4px;
    font-size: 18px;
  }
  
  .content-date {
    margin: 0 0 12px;
    color: #6b7280;
    font-size: 13px;
  }
  
  .controls {
    display: flex;
    gap: 8px;
    justify-content: center;
  }
  
  .controls button {
    padding: 8px 12px;
    border-radius: 8px;
    border: 1px solid #e5e7eb;
    background: white;
    cursor: pointer;
  }
  
  .controls button:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
  </style>
  
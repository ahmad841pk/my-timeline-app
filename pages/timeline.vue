<template>
    <div class="page">
      <h1>Project Timeline (Horizontal)</h1>
      <HorizontalTimeline v-model="active" :items="events" />
  
      <pre class="debug">Active index: {{ active }}</pre>
    </div>
  </template>
  
  <script>
  // If you don't have auto-import (components: true in nuxt.config),
  // import it manually:
  // import HorizontalTimeline from '~/components/HorizontalTimeline.vue'
  export default {
    components: {
      HorizontalTimeline: () => import('~/components/HorizontalTimeline.vue')
    },
    data() {
      return {
        active: 2,
        events: [
          { label: 'Kickoff', date: '2025-01-05', content: 'Scope defined & team formed.' },
          { label: 'Design', date: '2025-02-01', content: 'Wireframes & UI kit ready.' },
          { label: 'MVP', date: '2025-03-10', content: 'Core features implemented.' },
          { label: 'Beta', date: '2025-04-15', content: 'Closed beta and bug fixes.' },
          { label: 'Launch', date: '2025-05-20', content: 'Public release 🚀' }
        ]
      }
    }
  }
  </script>
  
  <style scoped>
  .page {
    max-width: 900px;
    margin: 24px auto;
    padding: 0 16px;
  }
  .debug {
    background: #f9fafb;
    border: 1px dashed #e5e7eb;
    border-radius: 8px;
    padding: 8px;
    margin-top: 16px;
    font-size: 12px;
    color: #6b7280;
  }
  </style>
  
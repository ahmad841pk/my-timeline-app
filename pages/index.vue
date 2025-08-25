<template>
  <div>
    <h1>Timeline Example</h1>
    <vue-timeline>
      <vue-timeline-item
        v-for="(event, i) in events"
        :key="i"
        :title="event.title"
        :subtitle="event.date"
      >
        {{ event.content }}
      </vue-timeline-item>
    </vue-timeline>
  </div>
</template>

<script>
export default {
  data() {
    return {
      events: [
        { title: 'Event 1', date: '2025-08-01', content: 'First timeline event' },
        { title: 'Event 2', date: '2025-08-10', content: 'Second timeline event' }
      ]
    }
  }
}
</script>

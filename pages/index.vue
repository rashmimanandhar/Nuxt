<template>
  <div>
    <h2>Events</h2>

    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'
export default {
  head() {
    return {
      title: 'Event'
    }
  },
  asyncData({ $axios }) {
    return $axios.get('http://localhost:3000/events').then(response => {
      return {
        events: response.data
      }
    })
  },
  components: {
    EventCard
  }
}
</script>

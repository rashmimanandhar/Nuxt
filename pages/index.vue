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
  // asyncData({ $axios, error }) {
  //   //promises and then api call using axios
  //   return $axios
  //     .get('http://localhost:3000/events')
  //     .then(response => {
  //       return {
  //         events: response.data
  //       }
  //     })
  //     .catch(e => {
  //       error({
  //         statusCode: 503,
  //         message:
  //           'Unable to fetch events at this time. API may be down. Check again'
  //       })
  //     })
  // },

  async asyncData({ $axios, error }) {
    try {
      const { data } = await $axios.get('http://localhost:3000/events')
      return {
        events: data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message:
          'Unable to fetch events at this time. API may be down. Check again'
      })
    }
  },
  components: {
    EventCard
  }
}
</script>

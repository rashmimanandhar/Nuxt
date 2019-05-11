<template>
  <div>
    <h1>event {{ id }}</h1>
    <p>{{ event.title }}</p>
  </div>
</template>

<script>
import EventService from '@/services/EventService.js'
export default {
  head() {
    return {
      title: 'Event #' + this.id,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'what you need to know about ' + this.event.title
        }
      ]
    }
  },
  async asyncData({ error, params }) {
    try {
      const { data } = await EventService.getEvent(params.id)
      return {
        event: data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message:
          'Unable to fetch event #' +
          params.id +
          'at this time. API may be down. Check again'
      })
    }
  },
  computed: {
    id() {
      return this.$route.params.id
    }
  }
}
</script>
<!--vbase-->

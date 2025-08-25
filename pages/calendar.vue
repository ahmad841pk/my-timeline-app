<template>
  <div>
    <h1>Company Calendar</h1>
    <AppCalendar />
  </div>
</template>

<script>
export default {
  components: {
    AppCalendar: () => import("~/components/AppCalendar.vue")
  }
}
</script>

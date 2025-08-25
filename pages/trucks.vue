<template>
  <div>
    <h1>Truck Orders Schedule</h1>
    <TruckSchedule />
  </div>
</template>

<script>
export default {
  components: {
    TruckSchedule: () => import("~/components/TruckSchedule.vue")
  }
}
</script>

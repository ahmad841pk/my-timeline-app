<template>
  <FullCalendar :options="calendarOptions" />
</template>

<script>
import FullCalendar from "@fullcalendar/vue";
import resourceTimelinePlugin from "@fullcalendar/resource-timeline";
import interactionPlugin from "@fullcalendar/interaction";

export default {
  name: "TruckSchedule",
  components: { FullCalendar },
  data() {
    return {
      calendarOptions: {
        plugins: [resourceTimelinePlugin, interactionPlugin],
        initialView: "resourceTimelineDay",
        aspectRatio: 2.2,
        resourceAreaHeaderContent: "Trucks",
        resources: [
          { id: "1", title: "Truck 1" },
          { id: "2", title: "Truck 2" },
          { id: "3", title: "Truck 3" },
          { id: "4", title: "Truck 4" }
        ],
        events: [
          { id: "1", resourceId: "1", title: "Order 1", start: "2025-08-25T12:00:00", end: "2025-08-25T14:00:00" },
          { id: "1", resourceId: "1", title: "Order 0", start: "2025-08-25T16:00:00", end: "2025-08-25T18:00:00" },
          { id: "2", resourceId: "1", title: "Order 2", start: "2025-08-25T18:30:00", end: "2025-08-25T20:00:00" },
          { id: "3", resourceId: "2", title: "Order 251", start: "2025-08-25T16:00:00", end: "2025-08-25T18:00:00" },
          { id: "4", resourceId: "2", title: "Order 252", start: "2025-08-25T19:00:00", end: "2025-08-25T21:00:00" },
          { id: "5", resourceId: "3", title: "Order 501", start: "2025-08-25T17:00:00", end: "2025-08-25T19:00:00" },
          { id: "6", resourceId: "4", title: "Order 751", start: "2025-08-25T16:00:00", end: "2025-08-25T18:30:00" }
        ],
        headerToolbar: {
          left: "prev,next today",
          center: "title",
          right: "resourceTimelineDay,resourceTimelineWeek"
        },
        slotDuration: "01:00:00",
        nowIndicator: true,
        editable: false
      }
    };
  }
};
</script>

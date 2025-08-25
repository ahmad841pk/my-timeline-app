<template>
  <FullCalendar :options="calendarOptions" />
</template>

<script>
import FullCalendar from "@fullcalendar/vue";
import dayGridPlugin from "@fullcalendar/daygrid";
import timeGridPlugin from "@fullcalendar/timegrid";
import interactionPlugin from "@fullcalendar/interaction"; // for drag/drop, click

export default {
  name: "AppCalendar",
  components: { FullCalendar },
  data() {
    return {
      calendarOptions: {
        plugins: [dayGridPlugin, timeGridPlugin, interactionPlugin],
        initialView: "dayGridMonth", // month view
        headerToolbar: {
          left: "prev,next today",
          center: "title",
          right: "dayGridMonth,timeGridWeek,timeGridDay"
        },
        selectable: true,
        editable: true,
        events: [
          { title: "Hello World", start: "2025-08-03T10:00:00" , end: "2025-08-05" },
          { title: "Introduction", start: "2025-08-13T10:00:00" , end: "2025-08-16" },
          { title: "Kickoff Meeting", start: "2025-08-26T10:00:00" },
          { title: "Delivery Order 501", start: "2025-08-27", end: "2025-08-29" },
          { title: "Team Lunch", start: "2025-08-30T13:00:00" }
        ],
        dateClick: (info) => {
          alert("Clicked on: " + info.dateStr);
        },
        eventClick: (info) => {
          alert("Event: " + info.event.title);
        }
      }
    };
  }
};
</script>

<style>
/* Optional styling */
.fc {
  max-width: 100%;
  margin: 20px auto;
}
</style>

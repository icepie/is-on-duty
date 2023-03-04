<script lang="ts">
	import Calendar from '@event-calendar/core';
    import TimeGrid from '@event-calendar/time-grid';
	import DayGrid  from '@event-calendar/day-grid';
	import ResourceTimeGrid from '@event-calendar/resource-time-grid';
	import ListGrid from '@event-calendar/list';
	import '@event-calendar/core/index.css';

    let plugins = [TimeGrid,DayGrid,ResourceTimeGrid,ListGrid];
    let options = {
        view: 'dayGridMonth',
        height: '800px',
        headerToolbar: {
            start: 'prev,next today',
            center: 'title',
            end: 'dayGridMonth,listWeek'
        },
        buttonText: function (texts) {
            texts.resourceTimeGridWeek = 'resources';
            return texts;
        },
        resources: [
            {id: 1, title: 'Resource A'},
        ],
        scrollTime: '09:00:00',
        events: createEvents(),
        views: {
            timeGridWeek: {pointer: true},
            resourceTimeGridWeek: {pointer: true}
        },
        dayMaxEvents: true,
		eventStartEditable: true,
        nowIndicator: true,
        selectable: true,
		dragScroll: true,
		locale: "ZH-cn",
		
    };

	function createEvents() {
        let days = [];
        for (let i = 0; i < 7; ++i) {
            let day = new Date();
            let diff = i - day.getDay();
            day.setDate(day.getDate() + diff);
            days[i] = day.getFullYear() + "-" + _pad(day.getMonth()+1) + "-" + _pad(day.getDate());
        }

        return [
            {start: days[2], end: days[3], resourceId: 1, title: "The calendar can display background and regular events", color: "#FE6B64", editable: true},
            {start:days[1], end: days[4], resourceId: 1, title: "An event may span to another day", color: "#B29DD9"},
            {start: days[1], end: days[3], resourceId: 1,title: "Events can be assigned to resources and the calendar has the resources view built-in", color: "#779ECB"},
            {start: days[1], end: days[3], resourceId: 1, title: "", color: "#FE6B64"},
            {start: days[2], end: days[6], resourceId: 1, title: "Overlapping events are positioned properly", color: "#779ECB"},
            {start: days[5], end: days[6], resourceId: 1, titleHTML: "You have complete control over the <i><b>display</b></i> of events…", color: "#779ECB"},
            {start: days[0], end: days[3], resourceId: 1, title: "…and you can drag and drop the events!", color: "#FE6B64"},
            {start: days[0], end: days[3], resourceId: 1, title: "", color: "#B29DD9"},
            {start: days[1], end: days[3], resourceId: 1, title: "All-day events can be displayed at the top", color: "#B29DD9", allDay: true}
        ];
    }

	function _pad(num) {
        let norm = Math.floor(Math.abs(num));
        return (norm < 10 ? '0' : '') + norm;
    }

</script>


<Calendar {plugins} {options} />


<style >

</style>
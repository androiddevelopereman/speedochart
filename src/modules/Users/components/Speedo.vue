<script setup>
import VueSpeedometer from "vue-speedometer";
import data2 from "..//..//..//data2";
import { Tooltip } from "bootstrap";
import { computed } from "vue";
import { onMounted } from "vue";

const { driver_name, last_speed, vehicle_name, vehicle_id } =
  data2.data_for_speedometer;

// onMounted(() => {
//   const tooltipTriggerList = document.querySelectorAll(
//     '[data-bs-toggle="tooltip"]'
//   );
//   const tooltipList = [...tooltipTriggerList].map(
//     (tooltipTriggerEl) => new Tooltip(tooltipTriggerEl)
//   );
// });

const tooltipText = computed(
  () =>
    `<h5>${driver_name}</h5>
  <p>Vehicle: ${vehicle_name}</p>
  <p>Vehicle ID: ${vehicle_id}</p>`
);

setTimeout(() => {
  const tooltipTrigger = document.querySelector(
    '[data-bs-toggle="tooltip"] g.arc'
  );
  const tooltip = new Tooltip(tooltipTrigger, {
    html: true,
    title: tooltipText.value,
  });
}, 1000);
</script>

<template>
  <vue-speedometer
    data-bs-toggle="tooltip"
    :data-bs-title="tooltipText"
    :forceRender="true"
    :maxSegmentLabels="1"
    :maxValue="200"
    :customSegmentStops="[0, 90, 120, 200]"
    :segmentColors="['#00B050', '#FFC000', '#FF0000']"
    needleColor="#5959ac"
    :currentValueText="'Current Value: \${value}'"
    :value="last_speed"
    textColor="${textColor}"
  />
</template>

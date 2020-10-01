<template>
  <div class="gstc-component" ref="gstc"></div>
</template>

<script>
import GSTC from 'gantt-schedule-timeline-calendar';
import 'gantt-schedule-timeline-calendar/dist/style.css';

let state, gstc;

export { GSTC };
export default {
  name: 'GSTC',
  props: ['config'],
  data(){
    return {
      gstc: null,
      state: null
    }
  },
  mounted() {
    this.$refs.gstc.addEventListener('gstc-loaded', () => {
      // gstc is loaded and displayed
    });
    this.state = GSTC.api.stateFromConfig({});
    this.gstc = GSTC({
      element: this.$refs.gstc,
      state,
    });
  },
  beforeUnmount() {
    if (gstc) gstc.destroy();
  },
};
</script>
<style scoped>
.gstc-component {
  margin: 0;
  padding: 0;
}
</style>
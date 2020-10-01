<template>
  <div class="gstc-component" ref="gstc"></div>
</template>

<script>
import GSTC from 'gantt-schedule-timeline-calendar';
import 'gantt-schedule-timeline-calendar/dist/style.css';

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
      state: this.state,
    });
  },
  beforeUnmount() {
    if (this.gstc) this.gstc.destroy();
  },
};
</script>
<style scoped>
.gstc-component {
  margin: 0;
  padding: 0;
}
</style>
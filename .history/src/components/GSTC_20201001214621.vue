<template>
  <div class="gstc-component" ref="gstc"></div>
</template>

<script>
import GSTC from 'gantt-schedule-timeline-calendar';
import 'gantt-schedule-timeline-calendar/dist/style.css';

let gstc, state;

export default {
  name: 'GSTC',
  props: ['config'],
  data(){
    return {
    }
  },
  mounted() {
    this.$refs.gstc.addEventListener('gstc-loaded', () => {
      // gstc is loaded and displayed
    });
    state = GSTC.api.stateFromConfig({
      licenseKey:'',
      list:{
        columns:{
          data:{
            [GSTC.api.GSTCID('id')] :{
              id:GSTC.api.GSTCID('id'),
              data:({row})=>GSTC.api.sourceID(row.id)
            }
          }
        },
        rows:{
          [GSTC.api.GSTCID('1')]:{
            id:GSTC.api.GSTCID('1'),
            label:'Row 1'
          },
          [GSTC.api.GSTCID('2')]:{
            id:GSTC.api.GSTCID('2'),
            label:'Row 2'
          },
          [GSTC.api.GSTCID('3')]:{
            id:GSTC.api.GSTCID('3'),
            label:'Row 3'
          },
          [GSTC.api.GSTCID('4')]:{
            id:GSTC.api.GSTCID('4'),
            label:'Row 4'
          },
        }
      },
      chart:{
        items:{

        }
      }
    });
    gstc = GSTC({
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
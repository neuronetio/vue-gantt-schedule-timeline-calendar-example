<template>
  <div class="gstc-component" ref="gstc"></div>
</template>

<script>
import GSTC from 'gantt-schedule-timeline-calendar';
import 'gantt-schedule-timeline-calendar/dist/style.css';

let gstc, state;

// helper function
function generateItems(){
  const items = {};
  let start = GSTC.api.date().startOf('day').subtract(6,'day');
  for(let i =0;i<10;i++){
    const id = GSTC.api.GSTCID(i.toString());
    start = start.add(1,'day');
    items[id] = {
      id,
      label:`Item ${i}`,
      time:{
        start: start.valueOf(),
        end: start.add(1,'day').endOf('day')
      }
    }
  }
}

export default {
  name: 'GSTC',
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
              width:60,
              data:({row})=>GSTC.api.sourceID(row.id)
            },
            [GSTC.api.GSTCID('label')] :{
              id:GSTC.api.GSTCID('label'),
              width: 200,
              data:'label'
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
        items: generateItems()
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
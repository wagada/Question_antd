<template>
  <div>
    <a-tabs default-active-key="1" @change="callback">
      <a-tab-pane key="1" tab="反馈处理">
          <Process />
      </a-tab-pane>
      <a-tab-pane key="2" tab="处理历史" force-render>
          2
      </a-tab-pane>
    </a-tabs>
  </div>
</template>
<script>
import Process from './components/Process'
export default {
  data() {
    return {};
  },
  methods: {
    callback(key) {
      console.log(key);
    },
  },
  components:{
      Process,
  }
};
</script>
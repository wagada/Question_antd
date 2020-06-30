<template>
  <div>
    <a-tabs default-active-key="1" @change="callback">
      <a-tab-pane key="1" tab="科目分类">
        <Subject />
      </a-tab-pane>
      <a-tab-pane key="2" tab="章节考点分类" force-render>
        <Chapter />
      </a-tab-pane>
      <a-tab-pane key="3" tab="前端分类">
        <Webclass />
      </a-tab-pane>
    </a-tabs>
  </div>
</template>
<script>
import Subject from './subject'
import Chapter from './chapter'
import Webclass from './webclass'
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
    Subject,
    Chapter,
    Webclass,
  }
};
</script>
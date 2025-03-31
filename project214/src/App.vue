<template>
  <div class="container">
    <Sidebar />
    <div :class="['content', { 'content-expanded': isSidebarOpen }]">
    <div class="headd">
    <h1 class="text-center my-4">Web Information</h1>
     </div>
    <StdDetail />
    <CourseList />
  </div>
</div>
</template>

<script>
import StdDetail from "./components/StdDetail.vue";
import CourseList from "./components/CourseList.vue";
import "./assets/global.css";
import Sidebar from "@/components/Sidebar.vue";

export default {
  components: {
    StdDetail,
    CourseList,
    Sidebar,
  },
  data() {
    return {
      isSidebarOpen: false
    };
  },
};
</script>
<style>
.content {
  margin-left: 0;
  transition: margin-left 0.3s;
}

.sidebar.active + .content {
  margin-left: 250px;
}
</style>

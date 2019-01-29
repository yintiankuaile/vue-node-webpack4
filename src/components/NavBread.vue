<template>
  <div class="nav-breadcrumb-wrap">
    <div class="container">
      <nav class="nav-breadcrumb">
        <a href="/">Home</a>
        <!--因为这个导航是随着进入不同页面名字链接是不一样的，所以需要使用插槽-->
        <slot></slot>
      </nav>
    </div>
  </div>
</template>

<script>
    export default {
        name: "NavBread"
    }
</script>

<style scoped>

</style>

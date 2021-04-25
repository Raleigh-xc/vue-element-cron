# vue-element-cron

```
npm install vue-element-cron -S
// or
yarn add vue-element-cron
```


```
<template>
  <div id="app">
    <VueElementCron ref="VueElementCron"/>
  </div>
</template>

<script>
import VueElementCron from 'vue-element-cron'

export default {
  name: 'App',
  components: {
    VueElementCron
  }
}
</script>

<style>
</style>

```

```
// 获取Cron表达式
this.$refs.VueElementCron.getCron()
```
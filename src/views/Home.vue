<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
// import { ipcRenderer } from 'electron'
import HelloWorld from '@/components/HelloWorld.vue' // @ is an alias to /src

export default defineComponent({
  name: 'Home',
  components: {
    HelloWorld
  },
  setup() {
    const ipcRenderer = (window as any).ipcRenderer
    console.log('ipcRenderer', ipcRenderer)
    // 监听主进程发送的消息
    ipcRenderer.on('main-msg', (event: any, arg: string) => {
      console.log(arg) // prints '好的'
    })
    // 给主进程发消息
    ipcRenderer.send('renderer-msg', '帮我创建一个新的页面')
  }
})
</script>

<template>
  <div class="hello">
   
    <cube-button @click="showToast">show toast</cube-button>
    <cube-upload
     
  :action="action"
  :simultaneous-uploads="1"
  @files-added="filesAdded"
  @file-success="filesSuccess"
  @file-removed="fileRemove" />
  <cube-button @click="showAlert">Dialog - type</cube-button>
   <div class="amap-wrapper">
      <el-amap class="amap-box" :vid="'amap-vue'"></el-amap>
    </div>
  </div>
  
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      action:{
        target:'http://yxrjapi.dongdukeji.com/index.php?m=Api&c=Qita&a=img_upload',
        fileName:'img'
      }
    }
  },
  methods: {
    showToast () {
      this.$createToast({
        txt: this.toastTxt
      }).show()
    },
    filesAdded(files) {
      console.log(files)
      let hasIgnore = false
      const maxSize = 1 * 1024 * 1024 // 1M
      for (let k in files) {
        const file = files[k]
        if (file.size > maxSize) {
          file.ignore = true
          hasIgnore = true
        }
      }
      hasIgnore && this.$createToast({
        type: 'warn',
        time: 1000,
        txt: 'You selected >1M files'
      }).show()
    },
    filesSuccess(e){
      console.log(e)
    },
    fileRemove(e){
      console.log(e)
    },
     showAlert() {
      this.$createDialog({
        type: 'alert',
        title: '我是标',
        content: '我是内容',
        icon: 'cubeic-alert'
      }).show()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.amap-wrapper {
  width: 500px;
  height: 500px;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

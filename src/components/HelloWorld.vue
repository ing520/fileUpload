<template>
  <div class="hello">
    <el-row>
      <el-col :span="12">
        <div class="grid-content bg-purple">
          <el-upload
            class="upload-demo"
            action="https://jsonplaceholder.typicode.com/posts/"
            :on-preview="handlePreview"
            :on-remove="handleRemove"
            :on-success="handleSuccess"
            :before-remove="beforeRemove"
            multiple
            :limit="3"
            :on-exceed="handleExceed"
            :file-list="fileList"
          >
            <el-button size="small" type="primary">点击上传</el-button>
          </el-upload>
        </div>
      </el-col>
      <el-col :span="12">
        <div class="grid-content bg-purple-light"></div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data () {
    return {
      fileList: []
    }
  },
  mounted () {
  },
  methods: {
    handleRemove (file, fileList) {
      console.log('handleRemove')
      console.log(file)
      let btns = document.querySelectorAll('button')
      for (var i = 0; i < btns.length; i++) {
        if (btns[i].id === file.name) {
          btns[i].style.display = 'none'
        }
      }
    },
    handlePreview (file) {
      console.log('handlePreview')
      console.log(file)
    },
    handleExceed (files, fileList) {
      this.$message.warning(
        `当前限制选择 3 个文件，本次选择了 ${
          files.length
        } 个文件，共选择了 ${files.length + fileList.length} 个文件`
      )
    },
    beforeRemove (file, fileList) {
      console.log('beforeRemove')
      console.log(file.name)
      return this.$confirm(`确定移除 ${file.name}？`)
    },
    handleSuccess (file, fileList) {
      let ul = document.querySelector('ul')
      let lis = document.querySelectorAll('li')
      console.log(lis)
      for (var i = 0; i < lis.length; i++) {
        lis[i].style.float = 'left'
      }
      var btn = document.createElement('button')
      btn.innerHTML = '下载'
      btn.style.position = 'relative'
      btn.style.top = '-25px'
      btn.style.left = '53px'
      btn.style.float = 'right'
      btn.id = fileList.name
      ul.appendChild(btn)
      var link = document.createElement('a')
      btn.appendChild(link)
      link.download = fileList.name
      link.href = `https://jsonplaceholder.typicode.com/posts/`
      // link.click()
      btn.addEventListener('click', function (e) {
        window.location.href = `https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100`
        console.log(link.href)
      })
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
</style>

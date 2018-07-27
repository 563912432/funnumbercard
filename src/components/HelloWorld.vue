<template>
  <div class="hello">
    <v-header></v-header>
    <div class="content">
      <el-row :gutter="8" style="padding: 5px 8px">
        <el-col :span="12">
          <el-card :body-style="{ padding: '0px' }">
            <div @click="toList('216')">
              <img src="../assets/number.png" class="image">
              <div style="padding:10px;text-align: center;color: #54C3F1;font-size: 18px">
                <span>数字学习</span>
              </div>
            </div>
          </el-card>
        </el-col>
        <el-col :span="12">
          <el-card :body-style="{ padding: '0px' }">
            <div @click="toList('217')">
              <img src="../assets/yunsuan.png" class="image">
              <div style="padding:10px;text-align: center;color: #54C3F1;font-size: 18px">
                <span>运算符号</span>
              </div>
            </div>
          </el-card>
        </el-col>
      </el-row>
      <el-row :gutter="8" style="padding: 5px 8px">
        <el-col :span="12">
          <el-card :body-style="{ padding: '0px' }">
            <div @click="toList('218')">
              <img src="../assets/jihe.png" class="image">
              <div style="padding: 8px 10px;text-align: center;color: #54C3F1;font-size: 18px">
                <span>几何图形</span>
              </div>
            </div>
          </el-card>
        </el-col>
        <el-col :span="12">
          <el-card :body-style="{ padding: '0px' }">
            <div @click="toList('219')">
              <img src="../assets/yanse.png" class="image">
              <div style="padding: 8px 10px;text-align: center;color: #54C3F1;font-size: 18px">
                <span>颜色认知</span>
              </div>
            </div>
          </el-card>
        </el-col>
      </el-row>
    </div>
    <v-footer></v-footer>
  </div>
</template>

<script>
import footer from '@/components/footer'
import header from '@/components/header'

const Host = '/Api/Pinyin/'

export default {
  name: 'HelloWorld',
  components: {
    'v-footer': footer,
    'v-header': header
  },
  data () {
    return {}
  },
  mounted () {
  },
  methods: {
    post (url, data, fn) { // datat应为'a=a1&b=b1'这种字符串格式，在jq里如果data为对象会自动将对象转成这种字符串格式
      let obj = new XMLHttpRequest()
      obj.open('POST', url, true)
      obj.onreadystatechange = function () {
        if (+obj.readyState === 4 && (+obj.status === 200 || +obj.status === 304 || +obj.status === 0)) { // 304未修改
          fn.call(this, JSON.parse(obj.responseText))
        }
      }
      obj.send(data)
    },
    toList (cid) {
      this.$router.push({path: '/list/' + cid})
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .hello {
    flex: 1;
    display: flex;
    flex-direction: column;
  }

  .hello .content {
    flex: 1;
    display: flex;
    flex-direction: column;
    overflow-y: auto;
    overflow-x: hidden;
    z-index: 0;
    color: #000507;
    padding-top: 5px;
  }
  .image {
    width: 80%;
    margin: 5px auto;
    display: block;
  }

</style>

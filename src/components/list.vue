<template>
  <div class="list">
    <v-header></v-header>
    <div class="content" v-loading.body="loading">
      <div class="menu">
        <router-link to="/" class='menu-title'><img src="../assets/back.png" alt="返回"> 返回
        </router-link>
        <span>{{ category }}</span>
        <router-link to="/" class='menu-title'><img src="../assets/home.png" alt="首页"> 首页</router-link>
      </div>
      <div class="wrapper" v-if="$route.params.cid === '216'">
        <el-row :gutter="10">
          <el-col :span="12" v-for="(value, index) in info" :key="value.id" class="w-col">
            <div class="w-content" @click="detail(value.id)">
              <el-card class="box-card"
                       :class="[
                          {'col-1': value.title === '1'},
                          {'col-2': value.title === '2'},
                          {'col-3': value.title === '3'},
                          {'col-4': value.title === '4'},
                          {'col-5': value.title === '5'},
                          {'col-6': value.title === '6'},
                          {'col-7': value.title === '7'},
                          {'col-8': value.title === '8'},
                          {'col-9': value.title === '9'},
                          {'col-10': value.title === '10'},
                        ]"
                 v-html="value.title" :id="value.id" :cid="value.cid">
              </el-card>
            </div>
          </el-col>
        </el-row>
      </div>
      <ul class="wrapper-ul" v-else>
        <li v-for="(item, index) in info" :key="item.id"
            :class="[index % 2 === 0?'white':'blue']"
            :title="item.title"
            @click="detail(item.id)">
          <i class="el-icon-arrow-right" :style="[{fontWeight: 'bold'},{color: index % 2 === 0?'#0082A8':'#fff'}]"></i><span class="space">{{ item.title }}</span>
        </li>
      </ul>
    </div>
    <v-footer></v-footer>
  </div>
</template>
<script>
  import footer from '@/components/footer'
  import header from '@/components/header'

  const Host = '/Api/Pinyin/'
  export default {
    name: 'list',
    components: {
      'v-footer': footer,
      'v-header': header
    },
    data () {
      return {
        category: '',
        cid: '',
        title: '',
        info: '',
        loading: false
      }
    },
    created () {
      let formdata = new FormData()
      formdata.append('cid', this.$route.params.cid)
      this.loading = true
      let url = Host + 'category'
      this.post(url, formdata, res => {
        this.loading = false
        if (res.status) {
          this.category = res.info['category']
          this.info = res.info['list']
        } else {
          console.log(res.info)
        }
      })
    },
    methods: {
      post (url, data, fn) {         // datat应为'a=a1&b=b1'这种字符串格式，在jq里如果data为对象会自动将对象转成这种字符串格式
        let obj = new XMLHttpRequest()
        obj.open('POST', url, true)
        obj.onreadystatechange = function () {
          if (+obj.readyState === 4 && (+obj.status === 200 || +obj.status === 304 || +obj.status === 0)) {  // 304未修改
            fn.call(this, JSON.parse(obj.responseText))
          }
        }
        obj.send(data)
      },
      detail (id) {
        this.$router.push({path: '/d/' + id})
      }
    }
  }
</script>
<style scoped>
  .list {
    flex: 1;
    display: flex;
    flex-direction: column;
  }

  .list .content {
    flex: 1;
    display: flex;
    flex-direction: column;
  }

  .list .content .menu {
    display: flex;
    height: 40px;
    align-items: center;
    justify-content: space-between;
    padding: 0 20px;
    font-size: 15px;
    color: #fff;
    background-color: #54C3F1;
  }

  .list .content .menu .menu-title {
    font-size: 13px;
    color: #fff;
    text-decoration: none;
  }

  .list .content .menu .menu-title img {
    width: 13px;
    height: 13px;
    margin-bottom: -1px;
  }

  .list .content .wrapper {
    flex: 1;
    overflow-y: auto;
    text-align: center;
    padding: 0 15px 10px 15px;
  }

  .list .content .wrapper .w-col {
    padding: 5px 0 0 0;
  }

  .list .content .wrapper .w-content {
    font-size: 35px;
    color: #333333;
    font-weight: 400;
  }

  .list .content .wrapper .w-content .box-card {
    border-color: #fff;
    /*box-shadow: 1px 2px 2px #BEE5F9;*/
    box-shadow: none;
    margin-top: 10px;
    padding: 13px 0;
  }
 .col-1 {
   color: #ea5514;
 }
  .col-2 {
    color: #ce0080;
  }
  .col-3 {
    color: #00a0e9;
  }
  .col-4{
    color: #009944;
  }
  .col-5 {
    color: #920783;
  }
  .col-6 {
    color: #f8b62c;
  }
  .col-7 {
    color: #00a0e9;
  }
  .col-8 {
    color: #abcd03;
  }
  .col-9 {
    color: #e95383;
  }
  .col-10 {
    color: #006795;
  }
  .list .content .wrapper-ul {
    flex: 1;
    overflow-y: auto;
    margin: 0;
    padding: 0;
    color: #000507;
  }

  .list .content .wrapper-ul li {
    padding: 10px;
  }

  .list .content .wrapper-ul .white {
    background-color: #fff;
    margin: 3px;
    border-radius: 3px;
  }

  .list .content .wrapper-ul .blue {
    background-color: #BEE5F9;
    margin: 3px;
    border-radius: 3px;
  }
</style>

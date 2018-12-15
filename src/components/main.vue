<template>
  <div class="douban-header">
    <div class="douban-header-container">
      <div class="douban-search">
        <a class="title">TMDB</a>
        <div class="search-container">
          <el-input placeholder="电影、影人、影院、电视剧" v-model="content">
            <el-button slot="append" icon="el-icon-search" @click="searchMovie"></el-button>
          </el-input>
        </div>

      </div>
    </div>
    <div class="douban-bar">
    
    </div>
    <div class="search-list" v-loading="searchLoading">
    <el-row>
    <el-col :span="8" v-for="(o, index) in 10" :key="o" :offset="index > 0 ? 2 : 0">
     <el-card :body-style="{ padding: '0px' }" shadow="hover">
       <img src="http://element-cn.eleme.io/static/hamburger.50e4091.png" class="image">
       <div style="padding: 14px;">
         <span>好吃的汉堡</span>
         <div class="bottom clearfix">
           <time class="time">{{ currentDate }}</time>
           <el-button type="text" class="button">操作按钮</el-button>
         </div>
       </div>
     </el-card>
    </el-col>


     </el-row>


    </div>
  </div>
</template>

<script>
  export default{
    data () {
      return {
        content: '',
        title: '正在热映',
        barList: [{
          title: '正在热映',
          url: '/'
        }, {
          title: '即将上映',
          url: '/upcoming'
        }, {
          title: 'Top250',
          url: '/top250'
        }],
         currentDate: new Date()
      }
    },
    methods: {
      choiceUrl (title) {
        this.title = title
      },
      searchMovie () {

        this.$router.push({path: '/detail', query: {searchText: this.content}})
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
.time {
    font-size: 13px;
    color: #999;
  }

  .bottom {
    margin-top: 13px;
    line-height: 12px;
  }

  .button {
    padding: 0;
    float: right;
  }

  .image {
    width: 100%;
    display: block;
  }

  .clearfix:before,
  .clearfix:after {
      display: table;
      content: "";
  }

  .clearfix:after {
      clear: both
  }
</style>

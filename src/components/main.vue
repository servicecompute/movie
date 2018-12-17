<template>
  <div class="header">
    <div class="container">
      <div class="search">
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
    <div class="search-list" v-loading="searchLoading" id="list">
    <el-row>
     <el-col :span="8" v-for="item in message" :key="o" :offset="index > 0 ? 2 : 0" class="card" >
     <el-card :body-style="{ padding: '0px' }" shadow="hover" >
       <img src="http://element-cn.eleme.io/static/hamburger.50e4091.png" class="image">
       <div style="padding: 14px;">
         <span>{{item.name}}</span>
         <div class="bottom clearfix">
          <span class="time">{{item.author}}</span>

           <el-button type="text" class="button" @click="getCustomers">详情</el-button>
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
        message:
        [
],
        movies:[],
         currentDate: new Date()
      }
    },
     mounted: function() {
        this.getMovies()
     },
    methods: {
      choiceUrl (title) {
        this.title = title
      },
      searchMovie () {

        this.$router.push({path: '/detail', query: {search: this.content}})
      },
      getMovies: function() {
          this.$http.get("http://localhost:9988/v1/buckets/movie_1/keys/name").then((response) => {

                  this.message=response.body

          },(response) => {
              console.log("sc")

          }).catch(function(response) {
              console.log(response)
          })
      }
    }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card{
   margin-left:80px;
    margin-bottom:80px;
}


a {
  color: #42b983;
}

.container{
 margin-bottom:50px;
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

  .search-list{
   width:100%;
  }
</style>

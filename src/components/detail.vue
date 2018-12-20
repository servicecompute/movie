<template>
    <div class="left-side">
      <div class="main">
        <div class="cover">
          <h1> title </h1>
          <p> year </p>
          <img src="http://element-cn.eleme.io/static/hamburger.50e4091.png" class="image">
        </div>
        <div class="info">
          <dl>
          <dt>导演:</dt>
          <dt>主演:</dt>
          <dt>类型:</dt>
          <dt>制片国家/地区:</dt>
          </dl>
        </div>
        <div class = "content">
          <p>电影简介</p>
        </div>
      </div>
    </div>
</template>
<script>
  export default{
  data () {
    return {
      param:this.$route.params,
      movie:{

      }
    }
  },
  mounted: function() {
    this.getMovies();

  },
  methods:{
  getMovies: function() {
      this.$http.get("/v2/movie/subject/"+this.param).then((response) => {


      },(response) => {
          console.log("error")

      }).catch(function(response) {
          console.log(response)
      })
  }
  }



  }

</script>


<style scoped>
left-side{
  float: left;
  width:590px;
  padding-right: 40px;
    .h1{
      word-break: break-all;
      display: block;
      font-size: 25px;
      font-weight: bold;
      color: #494949;
      padding: 0 0 15px 0;
      .year{
        color: #888;
      }
    }
  }
</style>

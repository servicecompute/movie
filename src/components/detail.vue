<template>
  <div class="container-moving" v-loading="loadingDetail">
    <div class="content">
      <h1>
        <span class="title">{{movieDetail.title}} {{movieDetail.original_title}}</span>
        <span class="year">({{movieDetail.year}})</span>
      </h1>
      <div class="detail clearfix">
        <div class="left-side">
          <div class="actor-list">
            <div class="subject">
              <div class="mainpic">
                <a href="https://movie.douban.com/subject/25900945/photos?type=R"><img class="movieImg" :src="movieDetail.images.medium" alt="" title="点击查看更多海报"></a>
              </div>
              <div class="info">
                <span class="p1">导演: </span><span v-for="item in movieDetail.directors" class="attrs">{{item.name}}</span><br>
                <span class="p1">主演: </span><span v-for="item in movieDetail.casts" class="attrs">{{item.name}}/</span><br>
                <span class="p1">类型: </span><span v-for="item in movieDetail.genres" class="attrs">{{item}}/</span><br>
                <span class="p1">制片国家/地区: </span><span v-for="(item,index) in movieDetail.countries" class="attrs">{{item}}</span><br>
              </div>
            </div>
          </div>
          <div class="summary">
            <p class="summary-title">{{movieDetail.title}}的剧情简介  ·  ·  ·  ·  ·  ·</p>
            <p class="intro">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{{movieDetail.summary}}</p>
          </div>
          <movieComment :title="movieDetail.title"></movieComment>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  export default{
    name: 'moviesDetail',
    data () {
      return {
      }
    },
    mounted () {
      let id = this.$route.query.id
      this.$store.commit('MOVING_ID', {id})
      this.$store.dispatch('getMovieDetail')
    },
    components: {
      'movieComment': (resolve) => {
        require(['./movieComment.vue'], resolve)
      }
    },
    computed: {
      movieDetail () {
        return this.$store.getters.movieDetail
      },
      loadingDetail () {
        return this.$store.getters.loadingDetail
      }
    }
  }
</script>
<style rel="stylesheet/less" lang="less">
  @import "../../../style/base";
  .container-moving{
    width: 950px;
    margin: 30px auto;
    .content{
      min-height: 420px;
      h1{
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
      .detail{
        .left-side{
          float: left;
          width:590px;
          padding-right: 40px;
          .actor-list{
            margin-bottom: 30px;
            .subject{
              width:415px;
              float: left;
              .mainpic{
                margin: 3px 12px 0 0;
                max-width: 155px;
                overflow: hidden;
                text-align: center;
                float: left;
                height: 140px;
                a{
                  img{
                    margin-bottom: 10px;
                    max-width: 100px;
                  }
                }
                .more-pic{
                  text-decoration: none;
                  color: #BBBBBB;
                  font-size: 12px;
                  text-align: center;
                }
              }
              .info{
                float: left;
                max-width: 248px;
                word-wrap: break-word;
                .p1{
                  line-height: 150%;
                  color: #666666;
                }
                .attrs{
                  color: #37a;
                }
              }
            }
          }
          .summary{
            float: left;
            clear: both;
            margin-top: 20px;
            .summary-title{
              color: #007722;
              font-size: 16px;
            }
          }
        }
      }
    }
  }
</style>

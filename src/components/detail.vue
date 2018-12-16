<template>
    <div id="movieDetail">
        <!--ha，我是电影的详情页{{$route.params.id}}-->
      <div class="detail-header" :style="{background:headerColor}">
        <!--<div class="bgImg" :style="ObgImg"></div>-->
        <img class="headerImg" :src="imgLink" alt="">
      </div>
      <div class="info">
        <div class="infos">
          <p class="info-title">{{details.title}}</p>
          <p>
            <span>{{details.year}}</span>
            <span>{{types}}</span>
          </p>
          <p v-show="details.original_title!=details.title">原名：{{details.original_title}}</p>
          <p>上映时间：{{details.year}}</p>
          <p>片长：</p>
        </div>
      </div>
      <div class="story_info">
        <p class="info-top">简介</p>
        <p class="info-content">
          <span>{{details.summary}}</span>
          <span style="color:green;">展开</span>
        </p>
      </div>
      <div class="actor_info">
        <span></span>
        <ul>
          <li>
            <div></div>
          </li>
        </ul>
      </div>
      <loading v-show="isLoading"></loading>
    </div>
</template>

<template>
  <div>
    <div class="hd" id="head">
      <div class="hd-content w">
        <svg class="icon svg-icon" aria-hidden="true">
          <use xlink:href="#icon-daohang"></use>
        </svg>
        <h1>网址导航</h1>
        <div class="sub-navi">
          <ul>
            <li class="sub-navi-cal" @click="changeIsShow">
              <svg class="icon svg-icon" aria-hidden="true">
                <use xlink:href="#icon-rili"></use>
              </svg>
              <p>&nbsp;2021日历</p>
              <svg class="icon svg-icon" aria-hidden="true" v-show="!isShow">
                <use xlink:href="#icon-jiantou_liebiaozhankai"></use>
              </svg>
              <svg class="icon svg-icon" aria-hidden="true" v-show="isShow">
                <use xlink:href="#icon-jiantou_liebiaoshouqi"></use>
              </svg>
              <svg class="icon svg-icon" aria-hidden="true">
                <use xlink:href="#icon-shuxian1"></use>
              </svg>
            </li>
            <li>
              <a href="http://cmd.bfs.cn.fujitsu.com/room/" target="_blank">
                <svg class="icon svg-icon" aria-hidden="true">
                  <use xlink:href="#icon-huiyi1"></use>
                </svg>
                <p>&nbsp;会议室预约</p>
              </a>
              <svg class="icon svg-icon" aria-hidden="true">
                <use xlink:href="#icon-shuxian1"></use>
              </svg>
            </li>
            <li>
              <a
                href="http://cmd.bfs.cn.fujitsu.com/training/training.asp"
                target="_blank"
              >
                <svg class="icon svg-icon" aria-hidden="true">
                  <use xlink:href="#icon-xuexi1"></use>
                </svg>
                <p>&nbsp;勉強会</p>
              </a>
              <svg class="icon svg-icon" aria-hidden="true">
                <use xlink:href="#icon-shuxian1"></use>
              </svg>
            </li>
            <li>
              <a
                href="http://cmd.bfs.cn.fujitsu.com/staff/index.asp"
                target="_blank"
              >
                <svg class="icon svg-icon" aria-hidden="true">
                  <use xlink:href="#icon-yuangong2"></use>
                </svg>
                <p>&nbsp;人员情报</p>
              </a>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <div class="bd-content company w">
      <h3>社内常用</h3>
      <div class="bd-nav w clearfix">
        <ul>
          <li v-for="(item, index) in listCompany">
            <a :href="item.hrefUrl" target="_blank">
              <div class="pic">
                <img :src="item.imgSrc" :title="item.imgTitle" />
              </div>
              <p>{{ item.hrefText }}</p>
            </a>
          </li>
        </ul>
      </div>
    </div>
    <div class="bd-content outside w">
      <h3>常用搜索</h3>
      <div class="bd-nav w clearfix">
        <ul>
          <li v-for="(item, index) in listSearch">
            <a :href="item.hrefUrl" target="_blank">
              <div class="pic">
                <img :src="item.imgSrc" :title="item.imgTitle" />
              </div>
              <p>{{ item.hrefText }}</p>
            </a>
          </li>
        </ul>
      </div>
    </div>
    <div class="bd-content outside w">
      <h3>学习好站</h3>
      <div class="bd-nav w clearfix">
        <ul>
          <li v-for="(item, index) in listStudy">
            <a :href="item.hrefUrl" target="_blank">
              <div class="pic">
                <img :src="item.imgSrc" :title="item.imgTitle" />
              </div>
              <p>{{ item.hrefText }}</p>
            </a>
          </li>
        </ul>
      </div>
    </div>
    <div class="add">
      <span>URL:</span
      ><input type="text" name="" id="" v-model="inputValue.hrefUrl" />
      <span>TITLE:</span
      ><input type="text" name="" id="" v-model="inputValue.hrefText" />
      <span>IMG URL:</span
      ><input
        type="text"
        name=""
        value="images/rencai.png"
        v-model="inputValue.imgSrc"
      /><br /><br />
      <input type="button" @click="add" value="追加" />
    </div>
    <!-- <div class="weather-beijing">
      <div class="weather-content">
        <p>北京</p>
        <ul>
          <li v-for="(item,index) in forecastListBj" :key="item.date" :style="{transitionDelay:index*100+'ms'}">
            </liv-for>
            <div class="info_type"><span class="iconfont">{{ item.type }}</span></div>
            <div class="info_temp">
              <p>{{ item.low}}</p>
              <p>{{ item.high}}</p>
            </div>
            <div class="info_date"> <strong><span>{{ item.date }}</span></strong></div>
          </li>
        </ul>
      </div>
    </div> -->
    <!-- <div class="weather-chongqing">
      <div class="weather-content">
        <p>重庆</p>
        <ul>
          <li v-for="(item,index) in forecastListCq" :key="item.date" :style="{transitionDelay:index*100+'ms'}">
            </liv-for>
            <div class="info_type"><span class="iconfont">{{ item.type }}</span></div>
            <div class="info_temp">
              <p>{{ item.low}}</p>
              <p>{{ item.high}}</p>
            </div>
            <div class="info_date"> <strong><span>{{ item.date }}</span></strong></div>
          </li>
        </ul>
      </div>
      <div class="return-top">
        <a href="#head" target="_self">返回<br />顶部</a>
      </div>
    </div> -->
    <div class="calendar" v-show="isShow"></div>
    <div class="ft"></div>
  </div>
</template>

<script>
export default {
  name: "Index.vue",
  data() {
    return {
      isShow: false,
      city: "武汉",
      forecastListBj: [],
      forecastListCq: [],
      hotCitys: ["北京", "上海", "广州", "深圳"],
      inputValue: { hrefUrl: "", imgSrc: "", imgTitle: "", hrefText: "" },
      listCompany: [
        {
          hrefUrl: "https://edzt.fa.em4.oraclecloud.com/",
          imgSrc: require("../assets/images/rencai.png"),
          imgTitle: "请假，目标",
          hrefText: "人材网",
        },
        {
          hrefUrl: "http://gdconnect.fujitsu.local/SitePages/GDC.aspx",
          imgSrc: require("../assets/images/OneERPslice.png"),
          imgTitle: "时间票填写",
          hrefText: "时间票",
        },
        {
          hrefUrl: "https://exch.g08.fujitsu.local/owa/",
          imgSrc: require("../assets/images/outlook.png"),
          imgTitle: "网页版邮箱",
          hrefText: "网页版邮箱",
        },
        {
          hrefUrl: "http://cmd.bfs.cn.fujitsu.com",
          imgSrc: require("../assets/images/bfs.png"),
          imgTitle: "BFS主页",
          hrefText: "BFS主页",
        },
        {
          hrefUrl:
            "http://glb.bfs.cn.fujitsu.com/onwork/hr/index_download.html",
          imgSrc: require("../assets/images/document.png"),
          imgTitle: "各种表格",
          hrefText: "各种表格下载",
        },
      ],
      listSearch: [
        {
          hrefUrl: "https://www.baidu.com",
          imgSrc: require("../assets/images/baidu.png"),
          imgTitle: "百度",
          hrefText: "百度",
        },
        {
          hrefUrl: "https://www.yahoo.co.jp",
          imgSrc: require("../assets/images/yahoo.png"),
          imgTitle: "日本Yahoo",
          hrefText: "日本Yahoo",
        },
        {
          hrefUrl: "https://dict.hjenglish.com/jp",
          imgSrc: require("../assets/images/hujiang.png"),
          imgTitle: "沪江",
          hrefText: "沪江",
        },
      ],
      listStudy: [
        {
          hrefUrl: "https://www.w3school.com.cn/",
          imgSrc: require("../assets/images/w3cschool.png"),
          imgTitle: "w3school",
          hrefText: "w3school",
        },
        {
          hrefUrl: "https://www.iconfont.cn/",
          imgSrc: require("../assets/images/iconfont.png"),
          imgTitle: "https://www.iconfont.cn/",
          hrefText: "字体图标：iconfont",
        },
      ],
    };
  },
  methods: {
    focusOff: function() {
      this.isShow = false;
    },
    changeIsShow: function() {
      this.isShow = !this.isShow;
    },
    add: function() {
      this.listSearch.push(this.inputValue);
    },
    remove: function(index) {
      console.log("删除");
      console.log(index);
      this.list.splice(index, 1);
    },
    clear: function() {
      this.list = [];
    },
    queryWeather() {
      this.forecastList = [];
      // 北京天气取得
      this.$axios
        .get(`http://wthrcdn.etouch.cn/weather_mini?city=北京`)
        .then((res) => {
          console.log(res);
          this.forecastListBj = res.data.data.forecast;
        })
        .catch((err) => {
          console.log(err);
        })
        .finally(() => {});
      // 重庆天气取得
      this.$axios
        .get(`http://wthrcdn.etouch.cn/weather_mini?city=重庆`)
        .then((res) => {
          console.log(res);
          this.forecastListCq = res.data.data.forecast;
        })
        .catch((err) => {
          console.log(err);
        })
        .finally(() => {});
    },
  },
  created() {
    this.queryWeather();
    console.log("xxx");
  },
};
</script>

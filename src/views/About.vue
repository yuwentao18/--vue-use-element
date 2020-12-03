<template>
  <div>
    <el-row class="nav-top">
      <el-col :xs="0" :span="2" class="nav"></el-col>
      <el-col :xs="24" :span="20" class="nav mainNav">
        <el-row class="navBox">
          <el-col :xs="4" :span="4" class="navBox"></el-col>
          <el-col :xs="16" :sm="2" :md="6" :lg="8"  class="navBox"></el-col>
          <el-col :xs="0" :sm="3" :md="2" :lg="2" class="navBox navtitle" @click.native="changeindex(0)">首页</el-col>
          <el-col :xs="0" :sm="3" :md="2" :lg="2" class="navBox navtitle" @click.native="changeindex(1)">公司简介</el-col>
          <el-col :xs="0" :sm="3" :md="2" :lg="2" class="navBox navtitle" @click.native="changeindex(2)">产品分类</el-col>
          <el-col :xs="0" :sm="3" :md="2" :lg="2" class="navBox navtitle">热门产品</el-col>
          <el-col :xs="0" :sm="3" :md="2" :lg="2" class="navBox navtitle">新闻列表</el-col>
          <el-col :xs="0" :sm="3" :md="2" :lg="2" class="navBox navtitle">联系我们</el-col>
          <el-col :xs="4" :sm="0" :md="0" :lg="0" class="navBox navtitle"></el-col>
        </el-row>
      </el-col>
      <el-col :xs="0" :span="2" class="nav"></el-col>
    </el-row>
    <el-carousel
      :height="innerHeight + 'px'"
      direction="vertical"
      :autoplay="false"
      indicator-position="none"
      ref="carousel"
    >
      <el-carousel-item :key="0">
        <el-row class="imgbox1">
          <el-col :xs="24" :span="24" class="imgbox1">
            <el-image class="imgbox1" :src="require('../assets/img1.jpg')" fit='cover' />
          </el-col>
        </el-row>
      </el-carousel-item>
      <el-carousel-item :key="1">
        <el-row class="imgbox1">
          <el-col :xs="24" :span="24" class="imgbox1">
            <el-image class="imgbox1" :src="require('../assets/img1.jpg')" fit='cover' />
          </el-col>
        </el-row>
      </el-carousel-item>
      <el-carousel-item :key="2">
        <el-row>
          <el-col :xs="24" :span="24"></el-col>
        </el-row>
      </el-carousel-item>
    </el-carousel>
  </div>
</template>
<script>
export default {
  data() {
    return {
      innerHeight: "",
      index: 0,
      timer: "",
      canchange: true,
    };
  },
  mounted() {
    console.log(window.innerHeight);
    this.innerHeight = window.innerHeight;
    window.onresize = () => {
      this.innerHeight = window.innerHeight;
    };
    window.addEventListener("wheel", this.handleScroll, true);
  },
  methods: {
    changeindex(index){
      console.log('进来了')
      this.index=index;
      this.$refs.carousel.setActiveItem(index);
    },
    handleScroll(e) {
      if (this.canchange && e.deltaY > 0) {
        this.canchange = false;
        this.timer = setTimeout(() => {
          this.canchange = true;
        }, 500);
        let addindex = ++this.index;
        console.log(addindex);
        if (addindex > 2) {
          this.index = 2;
        } else {
          setTimeout(() => {
            this.$refs.carousel.setActiveItem(addindex);
          }, 300);
        }
      }
      if (this.canchange && e.deltaY < 0) {
        this.canchange = false;
        this.timer = setTimeout(() => {
          this.canchange = true;
        }, 500);
        let addindex = --this.index;
        if (addindex < 0) {
          this.index = 0;
        } else {
          setTimeout(() => {
            this.$refs.carousel.setActiveItem(addindex);
          }, 300);
        }
      }
      console.log(e, "Jinlail");
    },
  },
};
</script>
<style lang="scss" scoped>
.nav-top {
  width: 100%;
  position: fixed;
  height: 0.8rem;
  background: rgba(0, 0, 0, 0);
  z-index: 100000;
  .nav {
    height: 0.8rem;
  }
  .mainNav {
    
    .navBox{
      height: 0.8rem;
    }
    .navtitle{
      text-align: center;
      line-height: 0.8rem;
      font-size: 0.16rem;
      color: #fff;
      font-weight: normal;
    }
  }
}
.imgbox1 {
  width: 100%;
  height: 100%;
}
.el-carousel__item h3 {
  color: #475669;
  font-size: 14px;
  opacity: 0.75;
  line-height: 200px;
  margin: 0;
}

.el-carousel__item:nth-child(2n) {
  background-color: #99a9bf;
}

.el-carousel__item:nth-child(2n + 1) {
  background-color: #d3dce6;
}
</style>
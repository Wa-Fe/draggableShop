<template>
  <div class="swiper">
    <div class="left" v-if="!setting">
      <!-- 第一种样式 -->
      <div v-if="datalist.type == 1">
        <el-carousel height="260px" :autoplay="datalist.autoplay">
          <el-carousel-item
            v-for="(item, x) in datalist.image"
            :key="x"
            class="swiperitem"
            :style="`background-color:${item.bgcolor}`"
          >
            <el-image
              :style="`width: ${375 - datalist.left}px; height: ${
                260 - datalist.top
              }px;border-radius:${datalist.radius}px;`"
              :src="item.pic"
            ></el-image>
          </el-carousel-item>
        </el-carousel>
      </div>
      <!-- 第二种样式 -->
      <div v-if="data.type == 2">
          <el-carousel height="260px" :autoplay="datalist.autoplay">
          <el-carousel-item
            v-for="(item, x) in datalist.image"
            :key="x"
            class="swiperitem sca8"
          >
            <el-image
               
              :src="item.pic"
            ></el-image>
          </el-carousel-item>
        </el-carousel>
      </div>
    </div>

    <div class="setting" v-if="setting">
      <p>轮播图设置</p>
      <div class="list">
        <div class="setitem-switch">
          <div class="setitem-l">是否开启自动切换</div>
          <div class="setitem-r">
            <el-switch v-model="datalist.autoplay" active-color="#13ce66">
            </el-switch>
          </div>
        </div>
        <div class="setitem-silder">
          <div class="setitem-l">圆角值</div>
          <div class="setitem-r">
            <el-slider v-model="datalist.radius" :max="50"></el-slider>
          </div>
        </div>
        <div class="setitem-silder">
          <div class="setitem-l">左右间距</div>
          <div class="setitem-r">
            <el-slider v-model="datalist.left" :max="50"></el-slider>
          </div>
        </div>
        <div class="setitem-silder">
          <div class="setitem-l">上下间距</div>
          <div class="setitem-r">
            <el-slider v-model="datalist.top" :max="50"></el-slider>
          </div>
        </div>
        <!-- 切换样式 -->
        <!-- <div class="setitem-select">
          <div class="setitem-l">选择样式</div>
          <div class="setitem-r">
            <el-select v-model="data.type" placeholder="请选择">
              <el-option
                v-for="item in options"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              >
              </el-option>
            </el-select>
          </div>
        </div> -->
        <div class="setitem-photo" v-for="(item, y) in datalist.image" :key="y">
          <div class="title">
            <p>图片{{ y + 1 }}</p>
            <div class="delete" v-if="y >= 1" @click="deleteItem(y)">
              <i class="el-icon-delete" color="red"></i>
            </div>
          </div>
          <div class="select-list">
            <div class="list-one">
              <div class="list-one-l">
                <p>选择图片</p>
              </div>
              <div class="list-one-l">
                <el-image
                  style="width: 100px; height: 50px"
                  :src="item.pic"
                ></el-image>
              </div>
            </div>
            <div class="list-two">
              <div class="list-two-l">
                <p>跳转链接</p>
              </div>
              <div class="list-two-r">
                <el-input
                  v-model="item.url"
                  placeholder="请输入链接"
                ></el-input>
              </div>
            </div>
            <div class="list-two">
              <div class="list-two-l">
                <p>背景颜色</p>
              </div>
              <div class="list-two-r">
                <el-input
                  v-model="item.bgcolor"
                  placeholder="请选择或输入颜色"
                ></el-input>
                <el-color-picker v-model="item.bgcolor"></el-color-picker>
              </div>
            </div>
          </div>
        </div>

        <!-- 添加按钮 -->
        <div class="buttongroup" @click="additem">
          <el-button>添加</el-button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  props: {
    data: {
      type: Object,
      default: () => ({}),
    },
    setting: {
      type: Boolean,
      default: false,
    },
  },
  watch:{
    datalist:function(val){
      console.log(val)
    }
  },
  data() {
    return {
      datalist:'',
      options: [
        {
          value: 1,
          label: "第一种样式",
        },
        {
          value: 2,
          label: "第二种样式",
        },
      ],
    };
  },
  created() {},
  mounted() {
    this.datalist = this.data
    // console.log(this.data);
  },
  watch: {},
  computed: {},
  methods: {
    additem: function () {
      console.log(this.data);
      let a = {
        pic: "",
        url: "",
      };
      this.datalist.image.push(a);
    },
    deleteItem: function (index) {
      this.datalist.image.splice(index, 1);
    },
  },
};
</script>
<style lang="scss" scoped>
@import '../static/css/setting.scss';
.swiperitem {
  display: flex;
  align-items: center;
  justify-content: center;
 
}

// .sca8{
//     transform: scale(.8) !important;
// }

</style>

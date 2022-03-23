<template>
  <div class="groupPhoto">
    <div class="groupPhotobox" v-if="!setting">
      <!-- 一张图片 -->
      <div class="type1" v-if="data.type == 1">
        <div
          class="type1box d-f j-c a-c"
          v-for="(item, x) in data.image"
          :key="x"
        >
          <el-image :src="item.pic"></el-image>
        </div>
      </div>
      <!-- 两张图片 -->
      <div class="type2 d-f j-c a-c" v-if="data.type == 2">
        <div
          class="2-l f1 d-f a-c j-c"
          v-for="(item, x) in data.image"
          :key="x"
        >
          <el-image :src="item.pic">
            <div slot="error" class="image-slot">
              <i class="el-icon-picture-outline"></i>
            </div>
          </el-image>
        </div>
      </div>
      <!-- 左一右二 -->
      <div class="type3 d-f a-c" v-if="data.type == 3">
        <div class="3-l f1 d-f a-c j-c">
          <el-image :src="data.image[0].src">
            <div slot="error" class="image-slot">
              <i class="el-icon-picture-outline"></i>
            </div>
          </el-image>
        </div>
        <div class="3-r f1">
          <div class="r-one d-f a-c j-c">
            <el-image :src="data.image[1].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
          </div>
          <div class="r-two d-f a-c j-c">
            <el-image :src="data.image[2].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
          </div>
        </div>
      </div>

      <!-- 左二右一 -->
      <div class="type4 d-f a-c" v-if="data.type == 4">
        <div class="3-r f1">
          <div class="r-one d-f a-c j-c">
            <el-image :src="data.image[0].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
          </div>
          <div class="r-two d-f a-c j-c">
            <el-image :src="data.image[1].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
          </div>
        </div>
        <div class="3-l f1 d-f a-c j-c">
          <el-image :src="data.image[2].src">
            <div slot="error" class="image-slot">
              <i class="el-icon-picture-outline"></i>
            </div>
          </el-image>
        </div>
      </div>
      <!-- 上一下二 -->
      <div class="type5" v-if="data.type == 5">
          <div class="5-one d-f a-c j-c">
               <el-image :src="data.image[0].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
          </div>
          <div class="5-two d-f a-c">
              <div class="two-l f1 d-f a-c j-c">
                   <el-image :src="data.image[1].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
              </div>
              <div class="two-r f1 d-f a-c j-c">
                   <el-image :src="data.image[2].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
              </div>
          </div>
      </div>

      <!-- 上二下一 -->
       <div class="type6" v-if="data.type == 6">
            <div class="5-two d-f a-c">
              <div class="two-l f1 d-f a-c j-c">
                   <el-image :src="data.image[0].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
              </div>
              <div class="two-r f1 d-f a-c j-c">
                   <el-image :src="data.image[1].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
              </div>
          </div>
          <div class="5-one d-f a-c j-c">
               <el-image :src="data.image[2].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
          </div>
         
      </div>
      <!-- 上二下三 -->
      <div class="type7" v-if="data.type == 7">
          <div class="7-one d-f a-c">
              <div class="one-l d-f a-c j-c f1">
                   <el-image :src="data.image[0].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
              </div>
              <div class="one-r d-f a-c j-c f1">
                   <el-image :src="data.image[1].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
              </div>
          </div>
          <div class="7-two d-f a-c">
               <div class="one-l d-f a-c j-c f1">
                    <el-image :src="data.image[2].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
               </div>
               <div class="one-c d-f a-c j-c f1">
                    <el-image :src="data.image[3].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
               </div>
              <div class="one-r d-f a-c j-c f1">
                   <el-image :src="data.image[4].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
              </div>
          </div>
      </div>

      <!-- 上三下二 -->
       <div class="type8" v-if="data.type == 8">
             <div class="7-two d-f a-c">
               <div class="one-l d-f a-c j-c f1">
                    <el-image :src="data.image[0].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
               </div>
               <div class="one-c d-f a-c j-c f1">
                    <el-image :src="data.image[1].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
               </div>
              <div class="one-r d-f a-c j-c f1">
                   <el-image :src="data.image[2].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
              </div>
          </div>
          <div class="7-one d-f a-c">
              <div class="one-l d-f a-c j-c f1">
                   <el-image :src="data.image[3].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
              </div>
              <div class="one-r d-f a-c j-c f1">
                   <el-image :src="data.image[4].src">
              <div slot="error" class="image-slot">
                <i class="el-icon-picture-outline"></i>
              </div>
            </el-image>
              </div>
          </div>
        
      </div>
    </div>

    <div class="setting" v-if="setting">
      <p>图片分组设置</p>
      <div class="setitem-select">
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
      </div>
      <div class="setitem-photo" v-for="(item, y) in data.image" :key="y">
        <div class="title">
          <p>图片{{ y + 1 }}</p>
        </div>
        <div class="select-list">
          <div class="list-one">
            <div class="list-one-l">
              <p>选择图片</p>
            </div>
            <div class="list-one-l">
              <el-image
                style="width: 50px; height: 50px"
                :src="item.pic"
              ></el-image>
            </div>
          </div>
          <div class="list-two">
            <div class="list-two-l">
              <p>跳转链接</p>
            </div>
            <div class="list-two-r">
              <el-input v-model="item.url" placeholder="请输入链接"></el-input>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { Switch } from "element-ui";
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
  data() {
    return {
      options: [
        {
          value: 1,
          label: "一张图片",
        },
        {
          value: 2,
          label: "两张图片",
        },
        {
          value: 3,
          label: "左一右二",
        },
        {
          value: 4,
          label: "左二右一",
        },
        {
          value: 5,
          label: "上一下二",
        },
        {
          value: 6,
          label: "上二下一",
        },
        {
          value: 7,
          label: "上二下三",
        },
        {
          value: 8,
          label: "上三下二",
        },
      ],
      show: true,
      item: "",
    };
  },
  created() {},
  mounted() {},
  watch: {
    "data.type": function (val) {
      if (this.setting) {
        // console.log(val);
        var obj = { pic: "", url: "" };
        let newarr = [];
        let newval;
        switch (this.options[val].label) {
          case "左二右一":
            newval = 3;
            break;
          case "上一下二":
            newval = 3;
            break;
          case "上二下一":
            newval = 3;
            break;
          case "上二下三":
            newval = 5;
            break;
          case "上三下二":
            newval = 5;
            break;

          default:
            newval = val;
            break;
        }
        for (let index = 0; index < newval; index++) {
          newarr.push(obj);
        }
        this.data.image = newarr;
      }
    },
  },
  computed: {},
  methods: {},
};
</script>
<style lang="scss" scoped>
@import "../static/css/setting.scss";


</style>

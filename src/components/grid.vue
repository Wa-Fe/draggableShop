<template>
  <div class="grid">
    <div class="gridbox" v-if="!setting">
      <!-- 第一种样式，每一排4个 -->
      <div v-if="data.type == 1">
        <div class="list" v-for="(item, x) in newList" :key="x">
          <div class="item w25" v-for="(item1, y) in item.list" :key="y" >
            <div class="item-image ">
              <el-image
              class="circle"
                style="width: 60px; height: 60px"
                :src="item1.pic"
              ></el-image>
            </div>
            <div class="item-name">
              {{ item1.name }}
            </div>
          </div>
        </div>
      </div>

       <div v-if="data.type == 2">
        <div class="list" v-for="(item, x) in newList" :key="x">
          <div class="item w20" v-for="(item1, y) in item.list" :key="y" >
            <div class="item-image ">
              <el-image
              class="circle"
                style="width: 50px; height: 50px"
                :src="item1.pic"
              ></el-image>
            </div>
            <div class="item-name">
              {{ item1.name }}
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="setting" v-if="setting">
      <p>宫格设置</p>
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
          <div class="delete" v-if="y >= 1" @click="deleteItem(y)">
            <i class="el-icon-delete" color="red"></i>
          </div>
        </div>
        <div class="select-list">
             <div class="list-two mb10">
            <div class="list-two-l">
              <p>名称</p>
            </div>
            <div class="list-two-r">
              <el-input v-model="item.name" placeholder="请输入名称"></el-input>
            </div>
          </div>
          <div class="list-one">
            <div class="list-one-l">
              <p>选择图片</p>
            </div>
            <div class="list-one-l">
              <el-image
                style="width: 50px; height: 50px; border-radius: 50%"
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

      <!-- 添加按钮 -->
      <div class="buttongroup" @click="additem">
        <el-button>添加</el-button>
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
  data() {
    return {
        options: [
        {
          value: 1,
          label: "每行4个",
        },
        {
          value: 2,
          label: "每行5个",
        },
      ],
    };
  },
  created() {},
  mounted() {
    // this.formatlist();
  },
  watch: {},
  computed: {
    newList: {
      get() {
        var newArr = [];
        this.newList = this.data.image;
        //   第一种样式，每列4个
        if (this.data.type == 1) {
          newArr = this.getNewArray(this.data.image, 8);
          return newArr;
        } else if (this.data.type == 2) {
            newArr = this.getNewArray(this.data.image, 10);
            return newArr;
        }
      },
      set() {},
    },
 
  },
  methods: {
    formatlist: function () {},
    getNewArray(arr, size) {
      let arrNum = Math.ceil(arr.length / size, 10);
      let index = 0; // 定义初始索引
      let resIndex = 0; // 用来保存每次拆分的长度
      var result = [];
      while (index < arrNum) {
        let obj = {};
        obj.list = arr.slice(resIndex, size + resIndex);
        result.push(obj);
        // result[index].list = arr.slice(resIndex, size + resIndex);
        resIndex += size;
        index++;
      }
      return result;
    },

    additem: function () {
      var obj = { pic: "", url: "", name: "名称" };
      this.data.image.push(obj);
    },
    deleteItem: function (index) {
      this.data.image.splice(index, 1);
    },
  },
};
</script>
<style lang="scss" scoped>
@import "../static/css/setting.scss";
.gridbox {
  .list {
    display: flex;
    flex-wrap: wrap;
    padding: 10px 0;
    .item {
    //   width: 25%;
      margin-bottom: 5px;
      .item-image {
        display: flex;
        justify-content: center;
      }
      .item-name {
        margin-top: 5px;
        text-align: center;
        font-size: 14px;
      }
    }
  }
}
.w25{
    width: 25%;
}
.w20{
    width: 20%;
}
</style>

<template>
  <div class="main">
    <div class="left">
      <div class="list">
        <div class="item" v-for="(item, x) in menulist" :key="x">
          <div class="item-one">
            {{ item.name }}
          </div>
          <div class="item-two">
            <draggable
              animation="300"
              v-model="item.list"
              :sort="false"
              class="leftdraggable"
              :clone="clonedata"
              :group="{ name: 'site', pull: 'clone', put: false }"
            >
              <div
                class="item-two-item"
                v-for="(item1, y) in item.list"
                :key="y"
              >
                <div class="item-two-item-label">
                  <i :class="item1.icon"></i>
                </div>
                <div class="item-two-item-name">
                  {{ item1.name }}
                </div>
              </div>
            </draggable>
          </div>
        </div>
      </div>
      <el-button @click="sub">click</el-button>
    </div>

    <div class="center">
      <div class="mobile">
        <draggable
          animation="300"
          v-model="centerlist"
          :group="{ name: 'site', pull: 'clone' }"
          style="height: 100vh"
          ghostClass="activeclass"
          @add="updatalist"
          @choose="changeID"
        >
          <div
            class="item-two-item"
            v-for="(item1, z) in centerlist"
            :key="z"
            :class="{ activeclass: item1.id == showID }"
          >
            <div v-show="item1.show">
              <div class="item-two-item-label">
                <i :class="item1.icon"></i>
              </div>
              <div class="item-two-item-name" >
                {{ item1.name }}
              </div>
            </div>
           
            <div class="swiper" v-if="item1.type == 'swiper'" >
                <div class="delete" v-if="item1.id == showID" @click="deleteItem(z)">
                  <i class="el-icon-delete" color="red"></i>
              </div>
              <Swiper :data="item1.data"></Swiper>
            </div>
            <div class="grid" v-if="item1.type == 'grid'">
               <div class="delete" v-if="item1.id == showID" @click="deleteItem(z)">
                  <i class="el-icon-delete" color="red"></i>
              </div>
              <Grid :data="item1.data"></Grid>
            </div>
            <div class="groupPhoto" v-if="item1.type == 'groupPhoto'">
               <div class="delete" v-if="item1.id == showID" @click="deleteItem(z)">
                  <i class="el-icon-delete" color="red"></i>
              </div>
              <GroupPhoto :data="item1.data"></GroupPhoto>
            </div>
          </div>
        </draggable>
      </div>
    </div>
    <div class="right">
      <div class="list">
        <div class="item" v-for="(item, yy) in centerlist" :key="yy">
          <div v-if="item.type == 'swiper'">
            <Swiper
              :setting="true"
              :data="item.data"
              v-show="item.id == showID"
            ></Swiper>
          </div>
          <div v-if="item.type == 'grid'">
            <Grid
              :setting="true"
              :data="item.data"
              v-show="item.id == showID"
            ></Grid>
          </div>
          <div v-if="item.type == 'groupPhoto'">
            <GroupPhoto
              :setting="true"
              :data="item.data"
              v-show="item.id == showID"
            ></GroupPhoto>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";
import list from "../util/menulist.json";
// 轮播图
import Swiper from "../components/swiper.vue";
import Grid from "../components/grid.vue";
import GroupPhoto from "../components/groupPhoto.vue";
export default {
  components: {
    draggable,
    Swiper,
    Grid,
    GroupPhoto,
  },
  props: {},
  data() {
    return {
      menulist: list.menulist,
      centerlist: [],
      readlist: [],
      showID: 0, //这个字段显示组件创建的时间，也是控制当前组件显示的唯一标识
    };
  },
  created() {},
  mounted() {},
  watch: {},
  computed: {},
  methods: {
    clonedata(e) {
      e.id = this.genID(5);
      return JSON.parse(JSON.stringify(e));
    },
    updatalist: function (e) {
      this.centerlist[e.newIndex].show = false;
      var num = this.count(this.centerlist);
      //超过次数不哟允许添加
      if (num > this.centerlist[e.newIndex].maxnum) {
        this.$message.error("超过最大允许数量");
        this.centerlist.splice(num - 1, 1);
        return;
      }
      this.showID = this.centerlist[e.newIndex].id;
    },
    changeID: function (e) {
      this.showID = this.centerlist[e.oldIndex].id;
    },
    // 统计出现次数
    count(arr) {
      var count = 0;
      arr.forEach((elem) => {
        if (elem.type === elem.type) {
          count++;
        }
      });
      return count;
    },
    //导出
    sub: function () {
      console.log(this.centerlist);
    },
    genID(length) {
      return Number(
        Math.random().toString().substr(3, length) + Date.now()
      ).toString(36);
    },
    deleteItem:function(index){
      this.centerlist.splice(index, 1);
    }
  },
};
</script>
<style lang="scss" scoped>
.main {
  height: 100vh;
  display: flex;
  .left {
    width: 260px;
    // overflow: scroll;
    .list {
      padding: 20px;
    }
    .leftdraggable {
      display: flex;
      flex-wrap: wrap;
      .item-two-item {
        position: relative;
        width: 50%;
        padding: 10px 0;
        cursor: move;
        &:hover {
          background-color: #f5f5f5;
        }
        .item-two-item-label {
          text-align: center;
        }
        .item-two-item-name {
          text-align: center;
        }
      }
    }
  }
  .center {
    flex: 1;
    background: #f2f2f6;
    display: flex;
    justify-content: center;
    padding: 30px 0;
    overflow: scroll;
    .mobile {
      width: 375px;
      background-color: #ffffff;
    }
  }
  .right {
    width: 400px;
    padding: 20px;
    overflow: scroll;
  }
}
.activeclass {
  width: 100%;
  outline: 2px dashed #aad6b0;
  // text-align: center;
}
.swiper,
.grid,
.groupPhoto{
  position: relative;
}
.delete{
  color: red;
  position: absolute;
  top: 5px;
  right: 5px;
  z-index: 99;
  cursor: pointer;
}
</style>

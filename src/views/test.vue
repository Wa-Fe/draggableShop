<template>
  <div>
    <!--使用draggable组件-->
    <div class="main">
      <div class="left">
        <div class="item" v-for="(item, y) in arr1" :key="y">
          <div class="item-title">
            {{ item.name }}
          </div>
          <template>
            <draggable
              v-model="arr1.menuList"
              :group="{ name: 'site', pull: 'clone', put: false }"
              :sort="false"
              animation="300"
              :handle="handle"
              class="draggablebox"
              :move="onMove"
            >
              <div
                class="item-list"
                v-for="item1 in item.menuList"
                :key="item1.id"
              >
                <div class="item-list-item">
                  <div class="icon">
                    <i :class="item1.icon"></i>
                  </div>
                  <div class="name">
                    <p>{{ item1.name }}</p>
                  </div>
                </div>
              </div>
            </draggable>
          </template>
        </div>
      </div>
      <div class="center">
        {{ arr2 }}
        <draggable
          v-model="arr2"
          :group="{ name: 'site', pull: 'clone' }"
          animation="300"
          @add="onAdd"
          class="height"
          v-bind="dragOptions"
          ghostClass="activeclass"
          @start="onStart"
        >
          <!-- <transition-group> -->
          <div class="item-list" v-for="item1 in arr2" :key="item1.id">
            <div class="item-list-item">
              <div class="icon">
                <i :class="item1.icon"></i>
              </div>
              <div class="name">
                <p>{{ item1.name }}</p>
              </div>
            </div>
            <div class="swiper" v-if="item1.type == 'swiper'">
                <p>轮播图</p>
                <el-image
                  style="width: 100px; height: 100px"
                  src="https://dummyimage.com/200x200/87CEFA/fff"
                  ></el-image>
            </div>
          </div>
        </draggable>
      </div>
      <div class="right">
      </div>
    </div>
  </div>
</template>

<script>
//导入draggable组件
import draggable from "vuedraggable";
export default {
  //注册draggable组件
  components: {
    draggable,
  },
  data() {
    return {
      drag: false,
      handle: ".item-list-item",
      //定义要被拖拽对象的数组
      arr1: [
        {
          name: "图文",
          menuList: [
            {
              name: "轮播图",
              icon: "el-icon-picture",
              type: "swiper",
              id:'1'
            },
            {
              name: "轮播图",
              icon: "el-icon-picture",
              type: "swiper",
               id:'2'
            },
          ],
        },
        // { name: "商品", menuList: "" },
        // { name: "活动", menuList: "" },
      ],
      arr2: [],
      dragOptions: {
        disabled: false,
      },
      arr3:[],
      item: {},
      readindex: null,
    };
  },
  methods: {
    //开始拖拽事件
    onStart(e) {
      console.log(e);
    },
    //拖拽结束事件
    onEnd() {},
    onAdd(e) {
      console.log(e);
      // console.log(e.oldIndex);
      // console.log(e.newIndex);
      // this.item = {};
      // this.readindex = null;
    },
    startone(e) {
      // console.log(e);
    },
    change() {
      // console.log("999");
    },
    onMove(e) {
      // this.item = e.draggedContext.element;
      // // console.log(e.relatedContext.index);
      // this.readindex = e.relatedContext.index;
      // console.log(e.relatedContext);
      // console.log(this.readindex);
    },
  },
};
</script>

<style scoped lang="scss">
.main {
  height: 100vh;
  display: flex;
  .left {
    width: 260px;
    border-right: 1px solid #a9a9a9;
    padding: 20px;
    .item {
      .draggablebox {
        display: flex;
      }
      .item-list {
        // margin-top: 20px;
        width: 50%;
        cursor: move;
        padding: 10px 0;
        &:hover {
          background-color: #f5f5f5;
        }
        .item-list-item {
          .icon {
            display: flex;
            justify-content: center;
          }
          .name {
            display: flex;
            justify-content: center;
          }
        }
      }
    }
  }
  .right {
    width: 200px;
    border-left: 1px solid #000000;
  }
  .center {
    background-color: #f5f5f5;
    flex: 1;
    .item {
      .test {
        padding: 20px;
        margin-bottom: 10px;
        background-color: #ffffff;
        border: 1px solid orange;
      }
    }
  }
}
.show {
  background-color: #aad6b0;
  border: 2px dashed #2b9939;
  text-align: center;
  line-height: 50px;
}
.empty {
  height: 200px;
  line-height: 200px;
  text-align: center;
}
.height {
  min-height: 100%;
}

.activeclass {
  // padding: 30px;
  // display: flex;
  width: 100%;
  // justify-content: center;
  border: 2px dashed #aad6b0;
  // > div{
  //   padding: 30px;
  //   text-align: center;
  // }
}
.activeclass > div {
  width: 100%;
}
.chooseclass {
  border: 2px dashed red;
}
.dragClass {
  padding: 0 !important;
}
</style>

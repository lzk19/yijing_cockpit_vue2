<template>
  <div class="main1">
    <div class="main2">
      <div class="dialog-box">
        <div class="boxShdow"></div>
        <img
          src="@/assets/cockpit/greenhouse/弹窗背景.png"
          alt=""
          class="backImg"
        />
        <div class="search-box">
          <span class="search-title">大棚名称</span>
          <!-- <el-form
            :model="queryParams"
            ref="queryRef"
            :inline="true"
            v-show="showSearch"
            class="search-form"
          >
            <el-form-item prop="greenhouseName" >
              <el-input
                v-model="queryParams.greenhouseName"
                placeholder="请输入大棚名称"
                clearable
                @keyup.enter="handleQuery"
                class="search"
                input-style="color:#88c4f3"
              />
            </el-form-item>
          </el-form> -->
          <el-input v-model="greenhouseName"
                    placeholder="请输入大棚名称"
                    clearable
                    class="search"
                    input-style="color:#88c4f3" @keyup.enter.native="handleQuery(greenhouseName)">
          </el-input>
          <el-button class="search-btn" @click="handleQuery(greenhouseName)">
            <span>搜索</span>
          </el-button>
        </div>
        <div class="greenhouse-box">
          <div
            v-for="(item, index) in dialogList1"
            :key="index"
            class="greenhouse-item"
          >
            <span class="greenhouse-name">
              {{ item.name }}
            </span>
            <img :src="item.url" alt="" class="greenhouse-img" />
          </div>
        </div>
      </div>
      <!-- @click="closeDialog" -->
      <img
        src="@/assets/cockpit/greenhouse/弹窗关闭按钮.png"
        alt=""
        class="close-btn"
        @click="dialogClose"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      greenhouseName:'',
      dialogList: [
        {
          name: "蔬菜大棚",
          url: require("../../../../assets/cockpit/示例图片/1.jpg"),
        },
        {
          name: "玉米基地",
          url: require("../../../../assets/cockpit/示例图片/2.jpg"),
        },
        {
          name: "水稻基地",
          url: require("../../../../assets/cockpit/示例图片/3.jpg"),
        },
        {
          name: "茭白基地",
          url: require("../../../../assets/cockpit/示例图片/4.jpg"),
        },
        {
          name: "水果基地",
          url: require("../../../../assets/cockpit/示例图片/5.jpg"),
        },
        {
          name: "榴莲大棚",
          url: require("../../../../assets/cockpit/示例图片/6.jpg"),
        },
        {
          name: "桃形李基地",
          url: require("../../../../assets/cockpit/示例图片/7.jpg"),
        },
        {
          name: "大棚名称",
          url: require("../../../../assets/cockpit/示例图片/8.jpg"),
        },
        {
          name: "芒果大棚",
          url: require("../../../../assets/cockpit/示例图片/9.jpg"),
        },
        {
          name: "小麦基地",
          url: require("../../../../assets/cockpit/示例图片/10.jpg"),
        },
      ],
      dialogList1:[],
    };
  },
  // computed:{
  //   fileList(){
  //     return this.dialogList.filter((val)=>{
  //       return val.name.indexOf(this.greenhouseName) !== -1
  //     })
  //   }
  // },
  methods:{
    handleQuery(keyword){
      this.dialogList1 = this.dialogList.filter((val)=>{
        return val.name.indexOf(keyword) !== -1
      })
    },
    dialogClose(){
      this.$bus.$emit('dialogState',false)
    }
  },
  watch:{
    greenhouseName(val){
      if(!val){
        this.dialogList1 = this.dialogList
      }
    }
  },
  mounted(){
    this.dialogList1 = this.dialogList
  }
};
</script>

<style lang="scss" scoped>
*::-webkit-scrollbar {
  width: 4px;
}

*::-webkit-scrollbar-thumb {
  background: #0bb3ef;
}

*::-webkit-scrollbar-track {
  margin-bottom: 27vh;
  margin-top: 2vh;
  background: #03374a;
}

.main2 {
  width: 58vw;
  height: 68vh;
  position: absolute;
  display: flex;
  left: 50%;
  top: 15%;
  transform: translate(-50%);
  .close-btn {
    height: 4vh;
    width: 2vw;
    margin-top: 5vh;
    margin-left: -4.5vw;
    cursor: pointer;
  }
  .dialog-box {
    width: 100%;
    max-height: 68vh;
    .boxShdow {
      transform: perspective(0.6em) rotateX(-1.8deg);
      transform-origin: top;
      border-radius: 25px;
      height: 11vh;
      width: 54vw;
      position: absolute;
      z-index: 3;
      opacity: 0.5;
      margin-top: 53.6vh;
      margin-left: 2vw;
      background: linear-gradient(
        0deg,
        rgba(1, 16, 38, 1),
        rgba(1, 16, 38, 0.5)
      );
      box-shadow: inset 12vh 0px 12vh 0px #061648;
    }

    .search-box {
      display: flex;
      align-items: center;
      margin-top: -60vh;
      margin-left: 7vw;
      height: 5vh;
      // .search-form {
        .search {
          // margin-top: 3vh;
          width: 17vw;
          height: 5vh;
          margin-left: 1vw;
          border: 1px solid #0bb3ef;
          border-radius: 4px;
        }
      // }
      .search-title {
        font-size: 1vw;
        font-family: Microsoft YaHei;
        font-weight: 400;
        color: #88c4f3;
        line-height: 5vh;
      }

      .search-btn {
        width: 5vw;
        height: 5vh;
        margin-left: 0.5vw;
        background: #0bb3ef;
        font-size: 1vw;
        font-family: Microsoft YaHei;
        font-weight: 400;
        color: #ffffff;
        border-radius: 4px;
        text-align: center;
        border: none;
        span {
          opacity: 0.55;
        }
      }
    }
    .greenhouse-box {
      margin-left: 5vw;
      margin-top: 3vh;
      overflow-y: auto;
      width: 48vw;
      display: flex;
      flex-wrap: wrap;
      height: 43vh;

      .greenhouse-item {
        width: 13.3vw;
        height: 15vh;
        position: relative;
        margin-left: 2vw;
        margin-top: 2vh;
        border: 1px solid #0bb3ef;
        // box-shadow: inset 55px 55px 55px 0px #011026;
        cursor: pointer;
        .greenhouse-name {
          height: 5vh;
          width: 13.1vw;
          font-size: 1vw;
          font-family: Microsoft YaHei;
          font-weight: 400;
          color: #88c4f3;
          position: absolute;
          bottom: 0;
          text-align: center;
          line-height: 5vh;
          background: linear-gradient(
            0deg,
            rgba(1, 16, 38, 1),
            rgba(43, 95, 143, 0.2)
          );
        }
        .greenhouse-img {
          width: 100%;
          height: 100%;
          border-radius: 4px;
        }
      }
    }
    // #061648
    .backImg {
      width: 100%;
      height: 100%;
      position: relative;
      z-index: -1;
    }

    :deep(.el-input__inner) {
      height: 4.7vh;
      opacity: 1;
      background: #444a5f;
      border: none;
      &::placeholder {
        color: #88c4f3;
        font-size: 1vw;
        opacity: 0.55;
      }
    }
  }
}
</style>

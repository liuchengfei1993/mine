<template>
  <div id="home">
    <!-- periodic table moudle -->
    <div class="kLineWrap">{{$t("message.kLine")}}</div>
    <div class="listWrap">
      <!-- latest block list -->
      <ul class="blockList">
          <li class="listHead">
            <div>
              <i class="iconfont icon-dashuju" style="font-size:20px;"></i>
              <span>{{$t("message.block")}}</span>
            </div>
            <button @click="searchAll('block')" class="button">
              {{$t("message.viewall")}}
            </button>
          </li>
          <div>
          <div class="left" >
            <li v-for="(item  , index) of  listnum" :key="index">
              <div class="listsmallleft">
                <div class="leftlist">
                  <div class="dateTime">
                    <div style="color: white; ">{{item.dateTime}}</div>
                  </div>
                </div>
                <div class="rightlist">
                 <span class="_id"><font style="font-weight:bold">ID:</font><font style="color:#999999">{{item._id}}</font></span>
                 <span class="time"><font style="font-weight:bold">{{$t("message.time")}}:</font><font style="color:#999999">{{item.dateTime}}</font></span>
                 <span class="hash"><font style="font-weight:bold">{{$t("message.time")}}:</font><font style="color:#999999">{{item.time}}</font></span>
                </div>
              </div>
            </li>
          </div>
          </div>
      </ul>
      <div style="width:30px;"></div>
      <!-- latest transaction list -->
      <ul class="transactionList">
        <li class="listHead">
          <div>
            <i class="iconfont icon-jiaoyiguanli"></i>
            <span>{{$t("message.transaction")}}</span>
          </div>
            <button class="button" @click="viewAll('hash')">{{$t("message.viewall")}}</button>
        </li>
        <div class="left" >
            <li v-for="(item  , index) of  listnum" :key="index">
              <div class="listsmallleft">
                <div class="leftlist">
                  <div class="dateTime">
                    <div style="color: white; ">{{item.dateTime}}</div>
                  </div>
                </div>
                <div class="rightlist">
                 <span class="_id"><font style="font-weight:bold">ID:</font><font style="color:#999999">{{item._id}}</font></span>
                 <span class="time"><font style="font-weight:bold">{{$t("message.time")}}:</font><font style="color:#999999">{{item.dateTime}}</font></span>
                 <span class="hash"><font style="font-weight:bold">{{$t("message.time")}}:</font><font style="color:#999999">{{item.time}}</font></span>
                </div>
              </div>
            </li>
          </div>
      </ul>
    </div>
  </div>
</template>

<script>
import { getBlocklist } from "../js/fetch";
export default {
  name: "home",
  data() {
    return {
      listnum: []
    };
  },
  created() {
    this.$store.commit("updateContentTitle", "close");
    this.getBlocklists();
  },
  methods: {
    getBlocklists: function() {
      getBlocklist(10)
        .then(data => {
          console.log(data);
          this.listnum = data.data.data;
        })
        .catch(error => {
          this.$message.error(error.msg);
        });
    },
    searchAll(to) {
      this.$store.dispatch("updateCurrentNav", to);
      this.$router.push(`/${to}`);
    },
    viewAll(to) {
      this.$store.dispatch("updateCurrentNav", to);
      this.$router.push(`/${to}`);
    }
  }
};
</script>

<style lang="scss" scoped>
#home {
  height: 100%;
  width: 96%;
  padding: 2%;
  min-height: 510px;
  font-size: 13px;
  color: #464646;
}
.kLineWrap {
  height: 100px;
  line-height: 100px;
  margin-bottom: 20px;
  border-radius: 5px;
  background-color: #fff;
}
.listWrap {
  display: flex;
  align-items: start;
  justify-content: space-between;
  ul {
    list-style: none;
    padding: 0;
    width: 50%;
    border-radius: 1px;
    .listHead {
      display: flex;
      align-items: center;
      justify-content: space-between;
      height: 44px;
      background-color: #fff;
      border-bottom: 3px solid #f8f8f8;
      div {
        margin-left: 16px;
        font-size: 16px;
        font-weight: 400;
        color: #4e4e4e;
        i {
          margin-right: 4px;
        }
      }
    }
    .listsmallleft {
      height: 90px;
      width: 100%;
      border: 1px #ccc;
      background-color: #ffffff;
      margin-top: 2px;
      display: flex;
    }
    .leftlist {
      height: 100%;
      width: 50%;
      display: flex;
      justify-content: center;
      flex-direction: column;
    }
    .dateTime {
      height: 80px;
      width: 140px;
      background-color: #929292;
      margin-left: 10%;
      display: flex;
      justify-content: center;
      flex-direction: column;
    }
    .rightlist {
      height: 100%;
      width: 50%;
      display: flex;
      justify-content: center;
      flex-direction: column;
      text-align: left;
      font-size: 30%;
      line-height: 21px;
      margin-right: 10%;
    }
    .button {
      padding: 4px;
      margin-right: 16px;
      min-width: 65px;
      user-select: none;
      cursor: pointer;
      border: 1px solid #929292;
    }
    .left {
      height: 451px;
      width: 100%;
      overflow-y: scroll;
    }
    .left::-webkit-scrollbar {
      /*隐藏滚轮*/
      display: none;
    }
  }
}
</style>

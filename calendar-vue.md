```
<template>
  <div>
      <button @click="changeType">CHANGE SHOW TYPE</button><br><br>
    <div class="calendar-box">
      <div class="now-box">
        <span @click="changeYear(-1)">&lt;&lt;</span>
        <span @click="changeMonth(-1)">&nbsp;&nbsp;&lt;&nbsp;&nbsp;&nbsp;&nbsp;</span>
        <span>{{year}}-{{month+1>9 ? month+1: '0' + (month+1)}}</span>
        <span @click="changeMonth(1)">&nbsp;&nbsp;&nbsp;&nbsp;&gt;&nbsp;&nbsp;</span>
        <span @click="changeYear(1)">&gt;&gt;</span>
      </div>
      <div class="week-box">
        <span v-for="(item,index) in weekList[calendarType]" :key="index">周{{item}}</span>
      </div>
      <div class="day-box">
        <span
          v-for="(item,index) in dayList"
          :key="index"
          :class="{
            'is-today':item.isToDay,
            'is-nowday':item.isNowDay
          }"
        >{{item.day}}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      calendarType:0,//修改日历样式，0：周一排第一列；1：周日排第一列；
      weekList: {
        0:["一", "二", "三", "四", "五", "六", "日"],
        1:["日","一", "二", "三", "四", "五", "六"]
      },
      dayList: [],
      nowDay: "",
      month:"",
      year:""
    };
  },
  mounted() {
    const time  = new Date();
    this.nowDay = time.getDate();
    this.month = time.getMonth();
    this.year = time.getFullYear();
    this.dayList = this.currentDaySet(time);
  },
  methods: {
    changeType(){
      this.calendarType = this.calendarType === 0 ? 1 : 0;
      const _time = new Date(); 
      _time.setFullYear(this.year);
      _time.setMonth(this.month);
      this.dayList = this.currentDaySet(_time);
    },
    changeYear(d){
      const _time = new Date();
      this.year  = this.year + (d);
      _time.setFullYear(this.year);
      this.dayList = this.currentDaySet(_time);
    },
    changeMonth(d){
      const _time = new Date();
      let m = this.month + (d);
      if(m > 11) this.year ++;  //递增月，跨年
      if(m < 0) { // 递减月，跨年
        this.year --;
        m = 11;
      }
      const M = m % 12;
      this.month = M;
      _time.setFullYear(this.year);
      _time.setMonth(M);
      this.dayList = this.currentDaySet(_time);
    },
    preDaySet(_time) {
      _time.setDate(0);
      const preMonthLastWeek = _time.getDay(); //上个月最后一天是周几
      const preMonthLastDay = _time.getDate(); //上个月遗留多少天
      let list = [];
      for (
        let i = preMonthLastDay;
        i > preMonthLastDay - preMonthLastWeek - this.calendarType;
        i--
      ) {
        list.push({
          day: i
        });
      };
      list.length >=7 && (list.length = 0);
      return list.reverse();
    },
    currentDaySet(_time) {
      _time.setMonth(_time.getMonth() + 1);
      _time.setDate(0); //当前月一共多少天
      const currentMonthLastWeek = _time.getDay(); //当前月最后一天是周几
      const dayTotal = _time.getDate();
      let list = [];
      for (let i = 1; i <= dayTotal; i++) {
        list.push({
          day: i,
          isNowDay: i === this.nowDay,
          isToDay:true
        });
      }

      for (let i = 1; i <= 7 - currentMonthLastWeek - this.calendarType; i++) {
        list.push({
          day: i
        });
      }

      return [...this.preDaySet(_time), ...list];
    }
  }
};
</script>

<style lang='less' scoped>
.calendar-box {
  width: 286px;
  padding: 2px;
  border: 1px solid #ccc;
  font-size: 0;
  span {
    display: inline-block;
    cursor: pointer;
    font-size: 12px;
    text-align: center;
    width: 40px;
    line-height: 40px;
    border-radius: 50%;
    color:#C0C4CC;
  }
  .now-box{
    text-align: center;
    span{
      font-size: 20px;
      color:#303133;
      display: inline;
    }
  }
  .week-box{
    border-bottom: 1px solid #ccc;
    span{
      color:#303133;
    }
  }
  .day-box span:hover {
    background: rgb(160, 207, 255);
  }
  .is-nowday {
    background: rgb(160, 207, 255);
  }
  .is-today{
    color:#303133;
  } 
}
</style>

```

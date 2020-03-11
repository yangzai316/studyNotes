```
<template>
  <div>
    <div class="box">
      <div class="solid-box">
        <p style="width:60px"></p>
        <p v-for="(item,index) in days" :key="index">{{item}}</p>
      </div>
      <table border="0" cellspacing="0" cellpadding="0">
        <tr>
          <th width="60">姓名</th>
          <th
            v-for="(item,index) in days"
            :key="index"
            width="40"
            style="line-height: 36px;"
          >{{item}}</th>
        </tr>
        <tr v-for="(obj,key) in rasks" :key="key">
          <td width="60">{{key}}</td>
          <td :colspan="days" :width="days*40" :style="{height:obj.length*21+'px'}">
            <p
              v-for="(item,index) in obj"
              :key="index"
              :style="{ left: item.left*40+'px',top:item.top*20+index+'px', width:  item.spread *40 + 'px' }"
              :title="`${item.startTime} - ${item.endTime}`"
            >{{item.content}}</p>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      list: {
        zhangsan: [
          {
            content: "1",
            startTime: "2012-11-13 12:00:00",
            endTime: "2012-11-14 23:59:59"
          },
          {
            content: "2",
            startTime: "2012-11-14 00:00:00",
            endTime: "2012-11-16 00:00:00"
          },
          {
            content: "3",
            startTime: "2012-11-16 00:00:00",
            endTime: "2012-12-17 23:59:59"
          }
        ],
        zhangsan2: [
          {
            content: "1",
            startTime: "2012-11-13 12:00:00",
            endTime: "2012-11-14 23:59:59"
          },
          {
            content: "2",
            startTime: "2012-11-14 00:00:00",
            endTime: "2012-11-16 00:00:00"
          },
          {
            content: "3",
            startTime: "2012-11-16 00:00:00",
            endTime: "2012-12-17 23:59:59"
          }
        ]
      }
    };
  },
  computed: {
    days() {
      const _time = new Date();
      _time.setDate(0);
      return _time.getDate();
    },
    rasks() {
      const _ = {};
      for (let key in this.list) {
        _[key] = this.list[key].map((item, index) => {
          const _start = new Date(item.startTime);
          const _end = new Date(item.endTime);
          return {
            ...item,
            left:
              (_start.getHours() * 60 * 60 * 1000 +
                _start.getMinutes() * 60 * 1000 +
                _start.getSeconds() * 10000) /
                (24 * 60 * 60 * 1000) +
              _start.getDate() -
              1,
            spread: (+_end - _start) / (24 * 3600 * 1000),
            top: index
          };
        });
      }
      return _;
    }
  }
};
</script>

<style lang='less' scoped>
.box {
  position: relative;
  .solid-box {
    position: absolute;
    border: 1px solid #ccc;
    font-size: 0;
    height: 100%;
    p {
      vertical-align: top;
      display: inline-block;
      height: 100%;
      width: 40px;
      border-right: 1px dashed #ccc;
      box-sizing: border-box;
      &:last-child {
        border-right: none;
      }
    }
  }
}
table {
  border: 1px solid #ccc;
  border-right: none;
  box-sizing: border-box;
  tr {
    display: block;
  }
  th {
    border-right: 1px solid #ccc;
    border-bottom: 1px solid #ccc;
    &:last-child {
      border-right: none;
    }
  }
  td {
    text-align: center;
    border-bottom: 1px solid #ccc;
    position: relative;
    overflow: hidden;
    p {
      position: absolute;
      background-color: red;
      text-align: left;
      height: 20px;
      padding-left: 10px;
    }
  }
}
</style>

```

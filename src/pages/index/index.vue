<template>
<div class="wrap">
    <article class="banner"><img src="/static/images/banner.png" alt=""></article>

    <article class="notice">
        <div class="fl"><span @click="termPopFun">{{termArr[termIndex]}}</span><span @click="termPopFun">{{gradeArr[gradeIndex]}}</span></div>
        <div class="fr">同一天，满足一类快乐值*1，满足两类快乐值*1.5，满足三类或三类以上快乐值双倍！</div>
    </article>
    
    <ul class="subject_list">
        <!-- <li v-for="(item,idx) in subject">
            <b>{{item.title}}</b>
            <picker :data-current="idx" @change="bindPickerChange" :value="index[idx]" :range="array">
                <view class="picker">{{array[index[idx]]}}</view>
            </picker>
        </li> -->
        <li v-if="subject[0]">
            <b>{{subject[0].title}}</b>
            <picker :data-current="0" @change="bindPickerChange" :value="index0" :range="array.name[0]">
                <view class="picker">{{array.name[0][index0]}}</view>
            </picker>
        </li>
        <li v-if="subject[1]">
            <b>{{subject[1].title}}</b>
            <picker :data-current="1" @change="bindPickerChange" :value="index1" :range="array.name[1]">
                <view class="picker">{{array.name[1][index1]}}</view>
            </picker>
        </li>
        <li v-if="subject[2]">
            <b>{{subject[2].title}}</b>
            <picker :data-current="2" @change="bindPickerChange" :value="index2" :range="array.name[2]">
                <view class="picker">{{array.name[2][index2]}}</view>
            </picker>
        </li>
        <li v-if="subject[3]">
            <b>{{subject[3].title}}</b>
            <picker :data-current="3" @change="bindPickerChange" :value="index3" :range="array.name[3]">
                <view class="picker">{{array.name[3][index3]}}</view>
            </picker>
        </li>
    </ul>
    <footer class="footer" @click="computePrice"><img src="/static/images/sub-btn.png" alt=""></footer>

    <!-- 学期年级弹窗 -->
    <article class="alert term_pop" v-show="termPop">
        <div class="alert_box">
            <h3 class="alert_hd"><img src="/static/images/alert-hd1.png" alt=""></h3>
            <div class="alert_bd">
                <h4>请选择学期</h4> 
                <ul class="screen_box">
                    <li v-for="(item,idx) in termArr" :class="{ on: termAct[idx] }" :key="idx" @click="termFun(idx)">{{item}}</li>
                </ul>
                <h4>请选择年级</h4>
                <ul class="screen_box">
                    <li v-for="(item,idx) in gradeArr" :class="{ on: gradeAct[idx] }" :key="idx" @click="gradeFun(idx)">{{item}}</li>
                </ul>
            </div>
        </div>
    </article>
    <!-- 学期年级弹窗 end -->

    <!-- 计算优惠弹窗 -->
    <article class="alert result_pop" v-show="resultPop">
        <div class="alert_box">
            <h3 class="alert_hd"><img src="/static/images/alert-hd2.png" alt=""></h3>
            <div class="alert_bd">
                <p>初始快乐值<strong>{{computePriceArr.prefPrice}}</strong></p>
                <p>UP快乐值<strong>{{computePriceArr.discount}}</strong></p>
                <p>加倍快乐<strong>{{computePriceArr.origPrice}}</strong></p>
                <p class="red">快乐就完了！！</p>
                <div class="button" @click="resultHide">关闭</div>
            </div>
        </div>
    </article>
    <!-- 计算优惠弹窗 end -->
</div>
</template>

<script>
export default {
  data () {
    return {
      userInfo: {},
      priceData: [
        // 夏季
        [
          // 周一至周五
          [
            {
              title: '水果',
              opt: [
                {name: '西瓜', num: 20, book: 5},
                {name: '杨梅', num: 20, book: 5},
                {name: '荔枝', num: 20, book: 5},
                {name: '苹果', num: 20, book: 5}
              ]
            },
            {
              title: '睡觉',
              opt: [
                {name: '7小时', num: 5, book: 5},
                {name: '8小时', num: 10, book: 5},
                {name: '9小时', num: 20, book: 5},
                {name: '10小时', num: 30, book: 5}
              ]
            },
            {
              title: '运动',
              opt: [
                {name: '游泳', num: 30, book: 5},
                {name: '骑行', num: 40, book: 5},
                {name: '跑步', num: 20, book: 5}

              ]
            }
          ],
          // 周末
          [
            {
              title: '水果',
              opt: [
                {name: '西瓜', num: 20, book: 5},
                {name: '葡萄', num: 20, book: 5},
                {name: '荔枝', num: 20, book: 5},
                {name: '双华李', num: 20, book: 5}
              ]
            },
            {
              title: '睡觉',
              opt: [
                {name: '7小时', num: 5, book: 5},
                {name: '8小时', num: 10, book: 5},
                {name: '9小时', num: 20, book: 5},
                {name: '10小时', num: 30, book: 5}
              ]
            },
            {
              title: '运动',
              opt: [
                {name: '游泳', num: 30, book: 5},
                {name: '骑行', num: 40, book: 5},
                {name: '跑步', num: 20, book: 5}

              ]
            },
            {
              title: '游戏',
              opt: [
                {name: '0.5小时', num: 10, book: 5},
                {name: '1小时', num: 20, book: 5},
                {name: '1.5小时', num: 30, book: 5}

              ]
            }
          ]
        ],
        // 冬季
        [
          
          // 周一至周五
          [
            {
              title: '睡觉',
              opt: [
                {name: '8小时', num: 5, book: 5},
                {name: '9小时', num: 10, book: 5},
                {name: '10小时', num: 20, book: 5},
                {name: '11小时', num: 30, book: 5}
              ]
            },
            {
              title: '水果',
              opt: [
                {name: '香梨', num: 20, book: 5},
                {name: '青枣', num: 20, book: 5},
                {name: '沙田柚', num: 20, book: 5},
                {name: '苹果', num: 20, book: 5}
              ]
            },
            {
              title: '运动',
              opt: [
                {name: '骑行', num: 40, book: 5},
                {name: '跑步', num: 20, book: 5}

              ]
            }
          ],
          // 周末
          [
            {
              title: '睡觉',
              opt: [
                {name: '7小时', num: 5, book: 5},
                {name: '8小时', num: 10, book: 5},
                {name: '9小时', num: 20, book: 5},
                {name: '10小时', num: 30, book: 5}
              ]
            },
            {
              title: '水果',
              opt: [
                {name: '橙子', num: 20, book: 5},
                {name: '葡萄', num: 20, book: 5},
                {name: '柿子', num: 20, book: 5},
                {name: '苹果', num: 20, book: 5}
              ]
            },
            {
              title: '运动',
              opt: [
                {name: '骑行', num: 40, book: 5},
                {name: '跑步', num: 20, book: 5}

              ]
            },
            {
              title: '游戏',
              opt: [
                {name: '0.5小时', num: 10, book: 5},
                {name: '1小时', num: 20, book: 5},
                {name: '1.5小时', num: 30, book: 5}

              ]
            }
          ]
        ]
      ],
      index0: 0,
      index1: 0,
      index2: 0,
      index3: 0,
      termArr: ['夏季', '冬季'],
      gradeArr: ['周一至五', '周末'],
      termIndex: 0,
      gradeIndex: 0,
      termAct: [true, false],
      gradeAct: [true, false, false, false],
      termPop: true,
      priceObj: [
        {
          num: 0,
          book: 0
        },
        {
          num: 0,
          book: 0
        },
        {
          num: 0,
          book: 0
        },
        {
          num: 0,
          book: 0
        },
        {
          num: 0,
          book: 0
        }
      ],
      resultPop: false,
      computePriceArr: {
        // 加倍
        origPrice: 0,
        // 原
        discount: 0,
        // UP
        prefPrice: 0
      }
    }
  },
  computed: {
    subject: {
      get () {
        // console.log(this.priceData[this.termIndex][this.gradeIndex])
        return this.priceData[this.termIndex][this.gradeIndex]
      },
      set (val) {
        console.log(val)
      }
    },
    array: {
      get () {
        let obj = {
          name: [],
          priceArr: [],
          bookArr: []
        }
        let data = this.priceData[this.termIndex][this.gradeIndex]
        data.forEach((item, i) => {
          obj.name.push(['请选择'])
          obj.priceArr.push([])
          obj.bookArr.push([])
          item.opt.forEach((cItem, j) => {
            obj.name[i].push(cItem.name)
            obj.priceArr[i].push(cItem.num)
            obj.bookArr[i].push(cItem.book)
          })
        })
        // console.log(obj)
        return obj
      },
      set (val) {
        console.log(val)
      }
    }
  },

  components: {},

  methods: {
    getUserInfo () {
      // 调用登录接口
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: (res) => {
              this.userInfo = res.userInfo
            }
          })
        }
      })
    },
    clickHandle (msg, ev) {
      console.log('clickHandle:', msg, ev)
    },
    bindPickerChange (e) {
      // console.log('picker发送选择改变，携带值为', e.mp)
      let pickerCur = e.mp.currentTarget.dataset.current.toString()
      this['index' + pickerCur] = e.mp.detail.value
      // if (pickerCur === 0) {
      //   this.index0 = e.mp.detail.value
      // } else if (pickerCur === 1) {
      //   this.index1 = e.mp.detail.value
      // } else if (pickerCur === 2) {
      //   this.index2 = e.mp.detail.value
      // } else {
      //   this.index3 = e.mp.detail.value
      // }
      // 课时费+书本费
      // console.log(this.array)
      let priIdx = parseInt(e.mp.detail.value) - 1
      if (priIdx >= 0) {
        this.priceObj[pickerCur].num = this.array.priceArr[pickerCur][priIdx]
        this.priceObj[pickerCur].book = this.array.bookArr[pickerCur][priIdx]
      } else {
        this.priceObj[pickerCur].num = 0
        this.priceObj[pickerCur].book = 0
      }
      // console.log(this.priceObj)
    },
    // 计算优惠
    computePrice () {
      this.computePriceArr.origPrice = 0
      this.computePriceArr.prefPrice = 0
      this.computePriceArr.discount = 0
      let falg = 0
      let bookPrice = 0
      this.priceObj.forEach((item, i) => {
        if (item.num !== 0) {
          falg++
          // if (falg === 1) {
          //   this.computePriceArr.prefPrice += item.num
          // } else if (falg === 2) {
          //   this.computePriceArr.prefPrice += item.num * 0.7
          // } else if (falg === 3) {
          //   this.computePriceArr.prefPrice += item.num * 0.3
          // } else {
          //   this.computePriceArr.prefPrice += item.num * 0
          // }
          this.computePriceArr.prefPrice += item.num
          this.computePriceArr.origPrice += item.num
          bookPrice += item.book
        }
      })
      console.log(falg)
      this.computePriceArr.origPrice += bookPrice
      this.computePriceArr.prefPrice += bookPrice
      if (falg === 2) {
        this.computePriceArr.origPrice *= 1.5
      } else if (falg >= 3) {
        this.computePriceArr.origPrice *= 2
      }
      this.computePriceArr.discount = this.computePriceArr.origPrice - this.computePriceArr.prefPrice
      // console.log(this.computePriceArr)
      this.resultPop = true
    },
    resultHide () {
      this.resultPop = false
    },
    termFun (i) {
      let that = this
      this.termIndex = i
      this.termAct.forEach(function (item, idx) {
        that.termAct[idx] = false
      })
      that.termAct[i] = true
      this.termPop = false
      this.initResultPop()
      // console.log(this.termAct)
    },
    gradeFun (i) {
      let that = this
      this.gradeIndex = i
      this.gradeAct.forEach(function (item, idx) {
        that.gradeAct[idx] = false
      })
      that.gradeAct[i] = true
      this.termPop = false
      this.initResultPop()
      // console.log(this.gradeAct)
    },
    termPopFun () {
      this.termPop = true
    },
    // 初始化picker默认值，价格
    initResultPop () {
      this.index0 = 0
      this.index1 = 0
      this.index2 = 0
      this.index3 = 0
      this.priceObj = [
        {
          num: 0,
          book: 0
        },
        {
          num: 0,
          book: 0
        },
        {
          num: 0,
          book: 0
        },
        {
          num: 0,
          book: 0
        },
        {
          num: 0,
          book: 0
        }
      ]
    }
  },
  created () {
  // 调用应用实例的方法获取全局数据
    this.getUserInfo()
  }
}
</script>

<style scoped>
.wrap {
    width: 100%;
    min-height: 100vh;
    padding-bottom: 15rpx;
    box-sizing: border-box;
    background: #ff8e6c;
}
.banner img{
    width: 100%; 
    height: 235rpx;/*
    background: url(/static/images/banner.png) no-repeat;背景图片设置成本地的无效
    background-size: 100%;*/
}
.notice{
    display: flex;
    padding: 0 24rpx;
}
.notice>.fl{
    flex: 0 0 auto;
    width: 167rpx;
}
.notice>.fl>span{
    height: 66rpx;
    line-height: 66rpx;
    font-size: 32rpx;
    display: block;
    text-align: center;
    border: 2rpx solid #d86820;
    border-radius: 12rpx;
    background: #fc9a00;
    color: #4f1200;
}
.notice>.fl>span+span{
    margin-top: 10rpx;
}
.notice>.fr{
    flex: 0 0 auto;
    width: 520rpx;
    margin-left: auto;
    font-size: 24rpx;
    background: #ffd79b;
    border: 2rpx solid #555;
    border-radius: 12rpx;
    padding: 24rpx;
    box-sizing: border-box;
    color: #4f1200;
}
.subject_list>li{
    margin: 20rpx 24rpx 0;
    background: #ffd79b;
    border: 2rpx solid #555;
    border-radius: 12rpx;
    height: 120rpx;
    display: -webkit-flex;
    display: flex;
    -webkit-align-items: center;
    align-items: center;
    position: relative;
}
.subject_list>li b {
    width: 120rpx;
    text-align: center;
    flex: 0 0 auto;
    font-size: 38rpx;
    color: #4f1200;
}
.subject_list>li picker{
    margin-right: 24rpx;
    border: 2rpx solid #555;
    flex: 1 1 auto;
    height: 72rpx;
    border-radius: 12rpx;
    background: #fff;
}
.subject_list>li .picker{
    padding-left: 30rpx;
    line-height: 72rpx;
    font-size: 30rpx;
    color: #888;
    font-weight: bold;
}
.footer{
    position: fixed;
    width: 100%;
    left: 0;
    bottom: 0;
}
.footer img{
    width: 100%;
    height: 123rpx;
}
/*弹窗*/
.alert {
    position: fixed;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,.5);
    top: 0;
    left: 0;
    z-index: 999;
}
.alert_box {
    position: absolute;
    width: 90%;
    height: auto;
    min-height: 100rpx;
    background: #ffe88e;
    border: 4rpx solid #555;
    border-radius: 12rpx;
    top: 50%;
    left: 50%;
    -webkit-transform: translate(-50%,-50%);
    transform: translate(-50%,-50%);
    box-sizing: border-box;
    padding: 4rpx;
}
.alert_hd {
    position: absolute;
    width: 100%;
    text-align: center;
    left: 0;
    top: -46rpx;
}
.alert_hd img{
    width: 292rpx; 
    height: 68rpx;
}
.alert_bd {
    background: #fff;
    min-height: 100rpx;
    padding: 30rpx 12rpx 0;
}

.term_pop .alert_box h4 {
    color: #703a00;
    font-size: 26rpx;
}
.term_pop .alert_box .screen_box+h4 {
    border-top: 2rpx dashed #b06615;
    padding-top: 24rpx;
    margin-top: 10rpx;
}
.screen_box {
    display: flex;
    flex-flow: row wrap;
    justify-content: center;
    margin-top: 24rpx;
}
.screen_box>li {
    height: 68rpx;
    width: 300rpx;
    background: #ffe88e;
    line-height: 68rpx;
    color: #320406;
    font-size: 32rpx;
    font-weight: bold;
    text-align: center;
    flex: 0 0 auto;
    margin-bottom: 20rpx;
    border: 4rpx solid #875211;
    border-radius: 6rpx;
    box-sizing: border-box;
}
.screen_box>li:nth-of-type(2n+1) {
    margin-right: 20rpx;
}
.screen_box>li.on {
    background: #ff683a;
    color: #1f0700;
}

.result_pop .alert_bd {
    padding-top: 60rpx;
    padding-bottom: 18rpx;
}
.result_pop .alert_bd>p {
    color: #442301;
    font-weight: bold;
    text-align: center;
    font-size: 30rpx;
}
.result_pop .alert_bd>p strong {
    color: #ff2f2f;
    font-size: 1.7em;
    display: inline;
}
.result_pop .alert_bd>p:nth-of-type(1) {
    font-size: 24rpx;
}
.result_pop .alert_bd>p.red{
  color: #ff2f2f;
    font-size: 1.5em;
}
.alert .button {
    background: #fff;
    margin: 16rpx 12rpx;
    padding: 12rpx;
    font-size: 38rpx;
    text-align: center;
    font-weight: bold;
    background: #ffe88e;
    border: 4rpx solid #824c10;
    color: #360909;
    border-radius: 6rpx;
}
</style>

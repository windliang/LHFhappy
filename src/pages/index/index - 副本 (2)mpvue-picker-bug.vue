<template>
<div class="wrap">
    <article class="banner"><img src="/static/images/banner.png" alt=""></article>

    <article class="notice">
        <div class="fl"><span>2018寒假</span><span>一年级</span></div>
        <div class="fr">同一学期，报读第一科全价，报读第二科七折，报读第三科三折，报读第四科、第五科免费！</div>
    </article>
    
    <ul class="subject_list">
        <li v-for="(item,idx) in subject">
            <b>{{item.title}}</b>
            <picker :data-current="item.key" @change="bindPickerChange(idx, $event)" :value="index[idx]" :range="item.opt">
                <view class="picker">{{text.yi || '未选择'}}</view>
            </picker>
        </li>
        {{text.yi}}
        <!-- <li v-if="subject[0]">
            <b>{{subject[0].title}}</b>
            <picker :data-current="0" @change="bindPickerChange" :value="index0" :range="array[0]">
                <view class="picker">{{array[0][index0]}}</view>
            </picker>
        </li>
        <li v-if="subject[1]">
            <b>{{subject[1].title}}</b>
            <picker :data-current="1" @change="bindPickerChange" :value="index1" :range="array[1]">
                <view class="picker">{{array[1][index1]}}</view>
            </picker>
        </li>
        <li v-if="subject[2]">
            <b>{{subject[2].title}}</b>
            <picker :data-current="2" @change="bindPickerChange" :value="index2" :range="array[2]">
                <view class="picker">{{array[2][index2]}}</view>
            </picker>
        </li>
        <li v-if="subject[3]">
            <b>{{subject[3].title}}</b>
            <picker :data-current="3" @change="bindPickerChange" :value="index3" :range="array[3]">
                <view class="picker">{{array[3][index3]}}</view>
            </picker>
        </li> -->
    </ul>
    <footer class="footer"><img src="/static/images/sub-btn.png" alt=""></footer>

    <!-- 学期年级弹窗 -->
    <article class="alert term_pop">
        <div class="alert_box">
            <h3 class="alert_hd"><img src="/static/images/alert-hd1.png" alt=""></h3>
            <div class="alert_bd">
                <h4>请选择学期</h4> 
                <ul class="screen_box">
                    <li v-for="item in termArr">{{item}}</li>
                </ul>
                <h4>请选择年级</h4>
                <ul class="screen_box">
                    <li v-for="item in gradeArr">{{item}}</li>
                </ul>
            </div>
        </div>
    </article>
    <!-- 学期年级弹窗 end -->

    <!-- 计算优惠弹窗 -->
    <!-- <article class="alert result_pop">
        <div class="alert_box">
            <h3 class="alert_hd"><img src="images/alert-hd2.png" alt=""></h3>
            <div class="alert_bd">
                <p>原价为<strong>0</strong>元</p>
                <p>您可享受<strong>0</strong>元折扣</p>
                <p>优惠后课程总价为<strong>0</strong>元</p>
                <div class="button"><img src="images/btn3.png" alt=""></div>
            </div>
        </div>
    </article> -->
    <!-- 计算优惠弹窗 end -->
</div>
</template>

<script>
export default {
  data () {
    return {
      userInfo: {},
      priceData: [
        // 2018寒假
        [
          // 三年级
          [
            {
              title: '英语',
              opt: [
                {name: '培优', num: 1890, book: 150},
                {name: '精英', num: 1890, book: 150},
                {name: '尖子', num: 1890, book: 150},
                {name: '超常', num: 1890, book: 150}
              ]
            },
            {
              title: '数学',
              opt: [
                {name: '培优', num: 1680, book: 150},
                {name: '尖子', num: 1680, book: 150}
              ]
            },
            {
              title: '语文',
              opt: [
                {name: '精英', num: 1680, book: 150}
              ]
            }
          ],
          // 四年级
          [
            {
              title: '英语',
              opt: [
                {name: '培优', num: 1890, book: 150},
                {name: '精英', num: 1890, book: 150},
                {name: '尖子', num: 1890, book: 150},
                {name: '超常', num: 1890, book: 150}
              ]
            },
            {
              title: '数学',
              opt: [
                {name: '培优', num: 1680, book: 150},
                {name: '尖子', num: 1680, book: 150}
              ]
            },
            {
              title: '语文',
              opt: [
                {name: '精英', num: 1680, book: 150}
              ]
            }
          ],
          // 五年级
          [
            {
              title: '英语',
              opt: [
                {name: '培优', num: 1890, book: 150},
                {name: '精英', num: 1890, book: 150},
                {name: '尖子', num: 1890, book: 150},
                {name: '超常', num: 1890, book: 150}
              ]
            },
            {
              title: '数学',
              opt: [
                {name: '培优', num: 1680, book: 150},
                {name: '尖子', num: 1680, book: 150}
              ]
            },
            {
              title: '语文',
              opt: [
                {name: '精英', num: 1680, book: 150}
              ]
            }
          ],
          // 六年级
          [
            {
              title: '英语',
              opt: [
                {name: '培优', num: 1890, book: 150},
                {name: '精英', num: 1890, book: 150},
                {name: '尖子', num: 1890, book: 150},
                {name: '超常', num: 1890, book: 150}
              ]
            },
            {
              title: '数学',
              opt: [
                {name: '培优', num: 1680, book: 150},
                {name: '尖子', num: 1680, book: 150}
              ]
            },
            {
              title: '语文',
              opt: [
                {name: '精英', num: 1680, book: 150}
              ]
            }
          ]
        ],
        // 2018寒假
        [
          // 三年级
          [
            {
              title: '英语',
              opt: [
                {name: '培优', num: 3840, book: 150},
                {name: '精英', num: 3840, book: 150},
                {name: '尖子', num: 3840, book: 150},
                {name: '超常', num: 3840, book: 150}
              ]
            },
            {
              title: '数学',
              opt: [
                {name: '培优', num: 2680, book: 150},
                {name: '尖子', num: 2680, book: 150}
              ]
            },
            {
              title: '语文',
              opt: [
                {name: '精英', num: 2680, book: 150}
              ]
            }
          ],
          // 四年级
          [
            {
              title: '英语',
              opt: [
                {name: '培优', num: 3840, book: 150},
                {name: '精英', num: 3840, book: 150},
                {name: '尖子', num: 3840, book: 150},
                {name: '超常', num: 3840, book: 150}
              ]
            },
            {
              title: '数学',
              opt: [
                {name: '培优', num: 2680, book: 150},
                {name: '尖子', num: 2680, book: 150}
              ]
            },
            {
              title: '语文',
              opt: [
                {name: '精英', num: 2680, book: 150}
              ]
            }
          ],
          // 五年级
          [
            {
              title: '英语',
              opt: [
                {name: '培优', num: 3840, book: 150},
                {name: '精英', num: 3840, book: 150},
                {name: '尖子', num: 3840, book: 150},
                {name: '超常', num: 3840, book: 150}
              ]
            },
            {
              title: '数学',
              opt: [
                {name: '培优', num: 2680, book: 150},
                {name: '尖子', num: 2680, book: 150}
              ]
            },
            {
              title: '语文',
              opt: [
                {name: '精英', num: 2680, book: 150}
              ]
            }
          ],
          // 六年级
          [
            {
              title: '英语',
              opt: [
                {name: '培优', num: 3840, book: 150},
                {name: '精英', num: 3840, book: 150},
                {name: '尖子', num: 3840, book: 150},
                {name: '超常', num: 3840, book: 150}
              ]
            },
            {
              title: '数学',
              opt: [
                {name: '培优', num: 2680, book: 150},
                {name: '尖子', num: 2680, book: 150}
              ]
            },
            {
              title: '语文',
              opt: [
                {name: '精英', num: 2680, book: 150}
              ]
            }
          ]
        ]
      ],
      array: ['a', 'b', 'c'],
      text: {},
      index: [0, 0, 0],
      index0: '0',
      index1: '0',
      index2: '0',
      index3: '0',
      termArr: ['2018寒假', '2018春季'],
      gradeArr: ['三年级', '四年级', '五年级', '六年级'],
      termIndex: 0,
      gradeIndex: 0,
      subject: [
        {
          title: '水果',
          opt: [1, 2, 3],
          key: 'yi'
        },
        {
          title: '蔬菜',
          opt: ['a', 'b', 'c'],
          key: 'er'
        },
        {
          title: '水果',
          opt: ['一', '二', '三'],
          key: 'san'
        }
      ]
    }
  },
  computed: {
    // subject: {
    //   get () {
    //     console.log(this.priceData[this.termIndex][this.gradeIndex])
    //     return this.priceData[this.termIndex][this.gradeIndex]
    //   },
    //   set (val) {
    //     console.log(val)
    //   }
    // }
    // array: {
    //   get () {
    //     let arr = []
    //     let data = this.priceData[this.termIndex][this.gradeIndex]
    //     data.forEach(function (item, i) {
    //       arr.push([])
    //       // this.index.push(0)
    //       item.opt.forEach(function (cItem, j) {
    //         arr[i].push(cItem.name)
    //       })
    //     })
    //     console.log(arr)
    //     return arr
    //   },
    //   set (val) {
    //     console.log(val)
    //   }
    // }
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
    bindPickerChange (i, e) {
      console.log('picker发送选择改变，携带值为', e.mp)
      // this.setData({
      // if (e.mp.currentTarget.dataset.current === 0) {
      //   this.index0 = e.mp.detail.value
      // } else if (e.mp.currentTarget.dataset.current === 1) {
      //   this.index1 = e.mp.detail.value
      // } else if (e.mp.currentTarget.dataset.current === 2) {
      //   this.index2 = e.mp.detail.value
      // } else {
      //   this.index3 = e.mp.detail.value
      // }
      this.text[e.mp.currentTarget.dataset.current] = e.mp.detail.value
      console.log()
      console.log(this.text.yi)
      // })
    },

    created () {
    // 调用应用实例的方法获取全局数据
      this.getUserInfo()
    }
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
    height: 294rpx;/*
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
    display: none;
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
</style>

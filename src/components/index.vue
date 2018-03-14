<template>
    <div class="container">
        <div class="topbar">
            <p class="title">购物车</p>
            <p class="edit">编辑</p>
        </div>
        <div class="goods1">
            <div class="goods-top">
                <div class="goods-select" @click="selectOne" :class="{selected: one.flag}"></div>
                <div class="logo"></div>
                <p class="seller">Cartier旗舰店</p>
                <p class="discount">优惠券</p>
            </div>
            <div class="goods-content" @touchstart="touchStart($event, 0)" 
                    @touchmove="touchMove($event,0)"
                    @touchend="touchEnd($event,0)" 
                    :style="moveList[0].deleteSlider">
                <div class="goods-select" @click="selectOne" :class="{selected: one.flag}"></div>
                <div class="img">
                    <img :src="imgList[0].src" alt="">
                </div>
                <div class="detail" >
                    <h3>【属龙蛇】阿弥陀佛菩萨冰曜石吊阿弥陀佛菩萨冰曜石吊</h3>
                    <p>黄钻</p>
                    <p><span>￥</span> {{ one.price }}.<span>00</span></p>
                    <div class="addreduce">
                        <div class="img-wrapper" @click="reduce(1)">
                            <img :src="imgList[1].src" alt="">
                        </div>
                        <input type="text" v-model="one.num">
                        <div class="img-wrapper" @click="add(1)">
                            <img :src="imgList[2].src" alt="">
                        </div>
                    </div>
                </div>
                <div class="hidden" ref='remove'>
                    <div>收藏</div>
                    <div>删除</div>
                </div>
            </div>
        </div>
        <div class="goods2">
            <div class="goods-top">
                <div class="goods-select" @click="selectTwo(1)" :class="{selected: twoSelect}"></div>
                <div class="logo"></div>
                <p class="seller">Tiffany上海店</p>
                <p class="discount">优惠券</p>
            </div>
            <div class="activity">
                <p>满减</p>
                <p>购买890元，可减100元，还差50元</p>
            </div>
            <div class="goods-content" @touchstart="touchStart($event, 1)" 
                    @touchmove="touchMove($event,1)"
                    @touchend="touchEnd($event,1)" 
                    :style="moveList[1].deleteSlider">
                <div class="goods-select" @click="selectTwo(2)" :class="{selected: two.flag}"></div>
                <div class="img">
                    <img :src="imgList[0].src" alt="">
                </div>
                <div class="detail special">
                    <h3>【属龙蛇】阿弥陀佛菩萨冰曜石吊阿弥陀佛菩萨冰曜石吊</h3>
                    <p>黄钻</p>
                    <p><span>￥</span> {{ two.price }}.<span>00</span></p>
                    <div class="addreduce">
                        <div class="img-wrapper" @click="reduce(2)">
                            <img :src="imgList[1].src" alt="">
                        </div>
                        <input type="text" v-model="two.num">
                        <div class="img-wrapper" @click="add(2)">
                            <img :src="imgList[2].src" alt="">
                        </div>
                    </div>
                </div>
                <div class="hidden" ref='remove'>
                    <div>收藏</div>
                    <div>删除</div>
                </div>
            </div>
            <div class="goods-content" @touchstart="touchStart($event, 2)" 
                    @touchmove="touchMove($event,2)"
                    @touchend="touchEnd($event,2)" 
                    :style="moveList[2].deleteSlider">
                <div class="goods-select" @click="selectTwo(3)" :class="{selected: three.flag}"></div>
                <div class="img">
                    <img :src="imgList[0].src" alt="">
                </div>
                <div class="detail">
                    <h3>【属龙蛇】阿弥陀佛菩萨冰曜石吊阿弥陀佛菩萨冰曜石吊</h3>
                    <p>黄钻</p>
                    <p><span>￥</span> {{ three.price }}.<span>00</span><span>￥4888</span></p>
                    <div class="addreduce">
                        <div class="img-wrapper" @click="reduce(3)">
                            <img :src="imgList[1].src" alt="">
                        </div>
                        <input type="text" v-model="three.num">
                        <div class="img-wrapper" @click="add(3)">
                            <img :src="imgList[2].src" alt="">
                        </div>
                    </div>
                </div>
                <div class="hidden" ref='remove'>
                    <div>收藏</div>
                    <div>删除</div>
                </div>
            </div>
        </div>
        <div class="balance-wrapper">
            <div class="goods-select" @click="allSelect" :class="{selected: selectAll}"></div>
            <p class="seller" >全选</p>
            <p class="all">合计：<span>￥{{ allPrice }}</span></p>
            <div class="balance">结算（{{ allNum }}）</div>
        </div>
        <nav class="footer">
            <ul>
                <li>
                    <img :src="imgList[3].src" alt="">
                    <p>首页</p>
                </li>
                <li>
                    <img :src="imgList[4].src" alt="">
                    <p>分类</p>
                </li>
                <li>
                    <img :src="imgList[5].src" alt="">
                    <p>购物车</p>
                </li>
                <li>
                    <img :src="imgList[6].src" alt="">
                    <p>我的</p>
                </li>
            </ul>
        </nav>
    </div>
</template>

<script>
export default {
  data() {
    return {
      one: { flag: false, price: 100, num: 1 },
      two: { flag: false, price: 200, num: 1 },
      three: { flag: false, price: 300, num: 1 },
      imgList: [
        { src: require("@/assets/a.png") },
        { src: require("@/assets/-.png") },
        { src: require("@/assets/+.png") },
        { src: require("@/assets/footer1.png") },
        { src: require("@/assets/footer2.png") },
        { src: require("@/assets/footer3.png") },
        { src: require("@/assets/footer4.png") }
      ],
      moveList: [
        {
          startX: 0, //触摸位置
          endX: 0, //结束位置
          moveX: 0, //滑动时的位置
          disX: 0, //移动距离
          deleteSlider: "" //滑动时的效果,使用v-bind:style="deleteSlider"
        },
        {
          startX: 0, //触摸位置
          endX: 0, //结束位置
          moveX: 0, //滑动时的位置
          disX: 0, //移动距离
          deleteSlider: "" //滑动时的效果,使用v-bind:style="deleteSlider"
        },
        {
          startX: 0, //触摸位置
          endX: 0, //结束位置
          moveX: 0, //滑动时的位置
          disX: 0, //移动距离
          deleteSlider: "" //滑动时的效果,使用v-bind:style="deleteSlider"
        }
      ]
    };
  },
  computed: {
    twoSelect() {
      if (this.two.flag === true && this.three.flag === true) {
        return true;
      } else {
        return false;
      }
    },
    selectAll() {
      if (this.one.flag === false || this.twoSelect === false) {
        return false;
      } else {
        return true;
      }
    },
    allNum(){
        let _allNum = 0;
        if(this.one.flag === true) {
            _allNum += this.one.num;
        }
        if(this.two.flag === true) {
            _allNum += this.two.num;
        }
        if(this.three.flag === true) {
            _allNum += this.three.num;
        }

        return _allNum;
    },
    allPrice(){
        let _allPrice = 0;
        if(this.one.flag === true) {
            _allPrice += this.one.price * this.one.num;
        }
        if(this.two.flag === true) {
            _allPrice += this.two.price * this.two.num;
        }
        if(this.three.flag === true) {
            _allPrice += this.three.price * this.three.num;
        }

        return _allPrice;
    }
  },
  methods: {
    selectOne() {
      this.one.flag = !this.one.flag;
    },
    selectTwo(i) {
      if (i === 1) {
        if (this.twoSelect === true) {
          this.two.flag = false;
          this.three.flag = false;
        } else {
          this.two.flag = true;
          this.three.flag = true;
        }
      } else if (i === 2) {
        this.two.flag = !this.two.flag;
      } else if (i === 3) {
        this.three.flag = !this.three.flag;
      }
    },
    allSelect() {
        if(this.one.flag === true && this.two.flag === true && this.three.flag === true) {
            this.one.flag = false;
            this.two.flag = false;
            this.three.flag = false;
        } else {
            this.one.flag = true;
            this.two.flag = true;
            this.three.flag = true;
        }
    },
    add(i) {
        if(i === 1) {
            this.one.num ++;
        } else if(i === 2) {
            this.two.num ++;
        } else if(i === 3) {
            this.three.num ++;
        }
    },
    reduce(i) {
      if(i === 1) {
            if (this.one.num === 1) {
                return;
            }
            this.one.num --;
        } else if(i === 2) {
            if (this.two.num === 1) {
                return;
            }
            this.two.num --;;
        } else if(i === 3) {
            if (this.three.num === 1) {
                return;
            }
            this.three.num --;
        }
    },
    touchStart(ev, i) {
      ev = ev || event;
      //tounches类数组，等于1时表示此时有只有一只手指在触摸屏幕
      if (ev.touches.length == 1) {
        // 记录开始位置
        this.moveList[i].startX = ev.touches[0].clientX;
      }
    },
    touchMove(ev, i) {
      ev = ev || event;
      //获取删除按钮的宽度，此宽度为滑块左滑的最大距离
      let wd = this.$refs.remove.offsetWidth;
      if (ev.touches.length == 1) {
        // 滑动时距离浏览器左侧实时距离
        this.moveList[i].moveX = ev.touches[0].clientX;

        //起始位置减去 实时的滑动的距离，得到手指实时偏移距离
        this.moveList[i].disX =
          this.moveList[i].startX - this.moveList[i].moveX;
        // 如果是向右滑动或者不滑动，不改变滑块的位置
        if (this.moveList[i].disX < 0 || this.moveList[i].disX == 0) {
          this.moveList[i].deleteSlider = "transform:translateX(0px)";
          // 大于0，表示左滑了，此时滑块开始滑动
        } else if (this.disX > 0) {
          //具体滑动距离我取的是 手指偏移距离*5。
          this.moveList[i].deleteSlider =
            "transform:translateX(-" + this.moveList[i].disX * 5 + "px)";

          // 最大也只能等于删除按钮宽度
          if (this.moveList[i].disX * 5 >= wd) {
            this.moveList[i].deleteSlider =
              "transform:translateX(-" + wd + "px)";
          }
        }
      }
    },
    touchEnd(ev, i) {
      ev = ev || event;
      let wd = this.$refs.remove.offsetWidth;
      if (ev.changedTouches.length == 1) {
        let endX = ev.changedTouches[0].clientX;

        this.moveList[i].disX = this.moveList[i].startX - endX;
        //如果距离小于删除按钮一半,强行回到起点

        if (this.moveList[i].disX * 5 < wd / 2) {
          this.moveList[i].deleteSlider = "transform:translateX(0px)";
        } else {
          //大于一半 滑动到最大值
          this.moveList[i].deleteSlider = "transform:translateX(-" + wd + "px)";
        }
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
.container {
    width: 100vw;
    height: 100vh;
    background-color: #F5F5F5;
}

.topbar {
    position: relative;
    height: 88px;
    background-color: #FA425B;
    line-height: 88px;
    border-bottom: 1px solid #FDA1AD; /* no */

    .title {
        height: 100%;
        color: #fff;
        font-size: 36px;
        text-align: center;
    }

    .edit {
        position: absolute;
        top: 0;
        right: 30px;
        height: 88px;
        color: #fff;
        font-size: 30px;
        rga(238, 238, 238);
    }
}

.goods1 {
    background-color: #fff;
    margin-bottom: 20px;
    padding-left: 30px;
    overflow: hidden;

    .goods-top {
        display: flex;
        align-items: center;
        border-bottom: 1px solid rgb(217, 217, 217); /* no */

        .goods-select {
            flex: 0 0 34px;
            width: 34px;
            height: 34px;
            margin: 30px 30px 26px 0;
            background-image: url('./src/assets/1.png');
            background-size: cover;
        }

        .selected {
            background-image: url('./src/assets/2.png');
        }

        .logo {
            flex: 0 0 42px;
            width: 42px;
            height: 38px;
            margin-right: 8px;
            background-image: url('./src/assets/3.png');
            background-size: cover;
        }

        .seller {
            flex: 1;
            color: rgb(102, 102, 102);
            font-size: 28px;
        }

        .discount {
            padding-right: 30px;
            color: rgb(102, 102, 102);
            font-size: 24px;
        }
    }

    .goods-content {
        display: flex;
        align-items: center;
        transition: 0.3s;

        .goods-select {
            flex: 0 0 34px;
            width: 34px;
            height: 34px;
            margin: 30px 30px 26px 0;
            background-image: url('./src/assets/1.png');
            background-size: cover;
        }

        .selected {
            background-image: url('./src/assets/2.png');
        }

        .img {
            flex: 0 0 180px;
            padding: 24px 20px 25px 0;

            img {
                width: 160px;
                height: 160px;
            }
        }

        .detail {
            position: relative;
            flex: 1;
            height: 100%;
            align-self: flex-start;

            h3 {
                width: calc(100vw - 306px);
                margin-top: 30px;
                font-size: 28px;
                text-overflow: ellipsis;
                overflow: hidden;
                white-space: nowrap;
                color: #000;
            }

            p:nth-of-type(1) {
                margin-top: 20px;
                text-indent: 12px;
                color: rgb(102, 102, 102);
            }

            p:nth-of-type(2) {
                margin-top: 30px;
                text-indent: 12px;
                color: rgb(250, 58, 84);
                font-size: 32px;

                span {
                    font-size: 26px;
                }
            }

            .addreduce {
                position: absolute;
                bottom: 0px;
                right: 0px;
                display: flex;
                align-items: center;

                .img-wrapper {
                    flex: 0 0 50px;
                    text-align: center;
                    width: 50px;
                    height: 52px;
                    border: 1px solid; /* no */

                    img {
                        width: 24px;
                    }

                    &:nth-of-type(1) {
                        border-radius: 3px 0 0 3px; /* no */
                        border-color: rgb(205, 205, 205);
                        border-right: none;
                    }

                    &:nth-of-type(2) {
                        border-radius: 0 3px 3px 0; /* no */
                        border-color: rgb(127, 127, 127);
                        border-left: none;

                        img {
                            margin-top: 13px;
                        }
                    }
                }

                input {
                    flex: 0 0 70px;
                    width: 70px;
                    height: 52px;
                    text-align: center;
                    font-size: 26px;
                    color: rgb(51, 51, 51);
                    border: 1px solid rgb(127, 127, 127); /* no */
                }
            }
        }
    }
}

.goods2 {
    background-color: #fff;
    margin-bottom: 20px;
    padding-left: 30px;
    overflow: hidden;

    .goods-top {
        display: flex;
        align-items: center;

        .goods-select {
            flex: 0 0 34px;
            width: 34px;
            height: 34px;
            margin: 30px 30px 26px 0;
            background-image: url('./src/assets/1.png');
            background-size: cover;
        }

        .selected {
            background-image: url('./src/assets/2.png');
        }

        .logo {
            flex: 0 0 42px;
            width: 42px;
            height: 38px;
            margin-right: 8px;
            background-image: url('./src/assets/3.png');
            background-size: cover;
        }

        .seller {
            flex: 1;
            color: rgb(102, 102, 102);
            font-size: 28px;
        }

        .discount {
            padding-right: 30px;
            color: rgb(102, 102, 102);
            font-size: 24px;
        }
    }

    .activity {
        display: flex;
        border-bottom: 1px solid rgb(217, 217, 217); /* no */
        padding-bottom: 20px;

        p {
            &:nth-of-type(1) {
                flex: 0 0 56px;
                color: #FA3A54;
                font-size: 22px;
                border: 1px solid #FA3A54; /* no */
                border-radius: 3px; /* no */
                padding: 0 4px;
                margin-right: 12px;
            }

            &:nth-of-type(2) {
                flex: 1;
            }
        }
    }

    .goods-content {
        display: flex;
        align-items: center;
        transition: 0.3s;

        .goods-select {
            flex: 0 0 34px;
            width: 34px;
            height: 34px;
            margin: 30px 30px 26px 0;
            background-image: url('./src/assets/1.png');
            background-size: cover;
        }

        .selected {
            background-image: url('./src/assets/2.png');
        }

        .img {
            flex: 0 0 180px;
            padding: 24px 20px 25px 0;

            img {
                width: 160px;
                height: 160px;
            }
        }

        .special {
            border-bottom: 1px solid rgb(217, 217, 217); /* no */
        }

        .detail {
            position: relative;
            flex: 1;
            height: 100%;
            align-self: flex-start;
            padding-bottom: 25px;

            h3 {
                width: calc(100vw - 306px);
                margin-top: 30px;
                font-size: 28px;
                text-overflow: ellipsis;
                overflow: hidden;
                white-space: nowrap;
                color: #000;
            }

            p:nth-of-type(1) {
                margin-top: 20px;
                text-indent: 12px;
                color: rgb(102, 102, 102);
            }

            p:nth-of-type(2) {
                margin-top: 30px;
                text-indent: 12px;
                color: rgb(250, 58, 84);
                font-size: 32px;

                span {
                    font-size: 26px;

                    &:nth-of-type(3) {
                        display: inline-block;
                        color: rgb(142, 140, 140);
                        font-size: 22px;
                    }
                }
            }

            .addreduce {
                position: absolute;
                bottom: 25px;
                right: 0px;
                display: flex;
                align-items: center;

                .img-wrapper {
                    flex: 0 0 50px;
                    text-align: center;
                    width: 50px;
                    height: 52px;
                    border: 1px solid; /* no */

                    img {
                        width: 24px;
                    }

                    &:nth-of-type(1) {
                        border-radius: 3px 0 0 3px; /* no */
                        border-color: rgb(205, 205, 205);
                        border-right: none;
                    }

                    &:nth-of-type(2) {
                        border-radius: 0 3px 3px 0; /* no */
                        border-color: rgb(127, 127, 127);
                        border-left: none;

                        img {
                            margin-top: 13px;
                        }
                    }
                }

                input {
                    flex: 0 0 70px;
                    width: 70px;
                    height: 52px;
                    text-align: center;
                    font-size: 26px;
                    color: rgb(51, 51, 51);
                    border: 1px solid rgb(127, 127, 127); /* no */
                }
            }
        }
    }
}

.balance-wrapper {
    position: fixed;
    bottom: 98px;
    display: flex;
    align-items: center;
    padding-left: 30px;
    width: 100vw;
    height: 96px;
    background-color: #fff;

    .goods-select {
        flex: 0 0 34px;
        width: 34px;
        height: 34px;
        margin: 30px 30px 26px 0;
        background-image: url('./src/assets/1.png');
        background-size: cover;
    }

    .selected {
        background-image: url('./src/assets/2.png');
    }

    .seller {
        flex: 0 0 70px;
        color: rgb(102, 102, 102);
        font-size: 28px;
    }

    .all {
        flex: 1;
        text-align: right;
        margin-right: 20px;
        font-size: 28px;
        color: rgb(0, 0, 51);

        span {
            font-size: 32px;
            color: rgb(250, 58, 84);
        }
    }

    .balance {
        flex: 0 0 224px;
        height: 100%;
        line-height: 96px;
        text-align: center;
        background-color: #FA425B;
        color: #fff;
        font-size: 32px;
    }
}

.footer {
    position: fixed;
    bottom: 0;
    width: 100%;
    height: 98px;
    background-color: #fff;
    border-top: 1px solid #D6D6D6; /* no */
    box-shadow: 0 5px 5px 5px #D6D6D6;

    ul {
        display: flex;
        align-items: center;
        text-align: center;

        li {
            flex: 1;
            height: 100%;
            padding-top: 15px;
            color: #666666;

            img {
                width: 40px;
            }

            &:nth-of-type(3) {
                color: #EA5050;
            }
        }
    }
}

.hidden {
    display: flex;
    margin-left: 32px;
    text-align: center;
    width: 240px;
    height: 207px;
    line-height: 207px;
    font-size: 26px;

    div {
        flex: 1;

        &:nth-of-type(1) {
            width: 120px;
            height: 100%;
            background-color: #F98090;
            color: #fff;
        }

        &:nth-of-type(2) {
            width: 120px;
            height: 100%;
            background-color: #FA3A54;
            color: #fff;
        }
    }
}
</style>
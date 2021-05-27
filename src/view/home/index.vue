<template>
  <div>
    <div class="box1">
      <van-popup
        v-model="videoShow"
        :style="{ background: 'transparent', overflow: 'visible' }"
      >
        <video
          src="https://video-ve.veimg.cn/9first/xianzhixueyuan.mp4"
          class="video"
          controls="controls"
          ref="videoRef"
        ></video>
        <img
          src="../../assets/images/cancel@2x.png"
          alt=""
          class="close"
          @click="onClose"
        />
      </van-popup>
      <img src="../../assets/images/LOGO@2x.png" alt="">
      <div class="look" @click="videoShow = true">观看视频</div>
    </div>
    <div class="box2">
      <div class="item" v-for="(item, index) in box2_data" :key="index">
        <img
          :src="item.url"
          alt=""
        />
        <span>{{item.name}}</span>
        <span>{{item.say}}</span>
      </div>
    </div>
    <div class="box3">
      <div class="title">解决企业培训那些不为人知的“痛”</div>
      <div class="item" v-for="(item, index) in box3_data" :key="index">
        <img :src="item.url" alt="" class="avatar" />
        <div class="content">
          <p>{{ item.name }}</p>
          <p>{{ item.say }}</p>
        </div>
      </div>
    </div>
    <div class="box4">
      <div class="title">提供企业一站式培训需求</div>
      <div class="wrap">
        <div class="item" v-for="(item, index) in box4_data" :key="index">
          <img :src="item.url" alt="" />
          <span>{{ item.name }}</span>
          <p>{{ item.say }}</p>
        </div>
      </div>
    </div>
    <div class="box5">
      <div class="title">培训原来如此简单</div>
      <div class="item" v-for="(item, index) in box5_data" :key="index">
        <img :src="item.url" alt="" />
        <div class="wrap">
          <span>{{ item.name }}</span>
          <p>{{ item.say }}</p>
        </div>
      </div>
    </div>
    <div class="box6">
      <div class="title">旅游服务业企业的信赖之选</div>
      <div class="img_wrap">
        <van-swipe :autoplay="3000" @change="onChange" ref="swipe">
          <van-swipe-item v-for="(image, index) in box6_data" :key="index">
            <img :src="image.url" width="100%" />
          </van-swipe-item>
          <template #indicator>
            <div class="custom-indicator">
              <div
                class="item"
                :class="current === index ? 'current' : ''"
                v-for="(image, index) in box6_data"
                :key="index"
              ></div>
            </div>
          </template>
        </van-swipe>
      </div>
    </div>
    <div class="box7">
      <a href="tel:0571-87765425">客服热线：0571-87765425</a>
      <a href="tel:17706441603">手机联系：17706441603（同微信）</a>
    </div>
    <div class="box8">
      <a
        href="https://p.qiao.baidu.com/im/index?siteid=10457562&ucid=6402298&cp=http%3A%2F%2Fihma.9first.com%2F&cr=http%3A%2F%2Fihma.9first.com%2F&cw=IHMA%E5%AE%98%E7%BD%91"
      >
        <img
          src="../../assets/images/server.png"
          alt=""
        />
        咨询
      </a>
      <a @click="onClickCart">免费试用</a>
    </div>
  </div>
</template>

<script>
import {
  Popup,
  Icon,
  Swipe,
  SwipeItem,
  NavBar,
  Form,
  Field,
  Button,
} from "vant";

export default {
  components: {
    [Popup.name]: Popup,
    [Icon.name]: Icon,
    [Swipe.name]: Swipe,
    [SwipeItem.name]: SwipeItem,
    [NavBar.name]: NavBar,
    [Form.name]: Form,
    [Field.name]: Field,
    [Button.name]: Button,
  },

  data() {
    return {
      videoShow: false,
      current: 0,
      box2_data: [
        {
          url: require("assets/images/mid_3.png"),
          name: "终端用户数",
          say:"160万+",
        },
        {
          url: require("assets/images/mid_4.png"),
          name: "终端用户数",
          say:"20000+",
        },
        {
          url: require("assets/images/mid_2.png"),
          name: "终端用户数",
          say:"20000+",
        },
        {
          url: require("assets/images/mid_1.png"),
          name: "终端用户数",
          say:"92万+",
        },
      ],
      box3_data: [
        {
          url: require("assets/images/user@2x.png"),
          name: "A酒店培训专员 William",
          say:
            "“总经理又在催培训了。想做培训但找不到合适的课程，自己做又不专业，素材收集费时费力”",
        },
        {
          url: require("assets/images/user_2@2x.png"),
          name: "B酒店培训经理 Thomas",
          say:
            "“我们有了课程但是组织培训难，出差的出差，工作的工作，想组织一次好难啊”",
        },
        {
          url: require("assets/images/user_3@2x.png"),
          name: "C 酒店员工 Jack",
          say:
            "“不是我们不愿意学，天天那么多事儿，还要叫我们去培训室去，一去一个小时啥的”",
        },
        {
          url: require("assets/images/user_4@2x.png"),
          name: "D酒店部门经理 Lisa",
          say:
            "“培训培训，哪里来的素材，我怎么设计课件，你培训部有的话直接安排不就得了”",
        },
      ],
      box4_data: [
        {
          url: require("assets/images/mid_8.png"),
          name: "岗位胜任力体系",
          say: "针对岗位开发、八部一室全覆盖、课程的更新迭代",
        },
        {
          url: require("assets/images/mid_7.png"),
          name: "线上培训系统",
          say: "手机学习，急速考核，报表呈现",
        },
        {
          url: require("assets/images/mid_6.png"),
          name: "线下公开课",
          say: "讲师面对面，翻转课堂，打破思维局限",
        },
        {
          url: require("assets/images/mid_5.png"),
          name: "内训与咨询",
          say: "行业专家，企业诊断，一对一服务",
        },
      ],
      box5_data: [
        {
          url: require("assets/images/icon_1@2x.png"),
          name: "学习计划",
          say: "快速为每一个学员安排学习任务，线上安排效率更高",
        },
        {
          url: require("assets/images/icon_2@2x.png"),
          name: "在线考试",
          say: "提供数千道先之题库，自动阅卷，自动排名",
        },
        {
          url: require("assets/images/icon_3@2x.png"),
          name: "成长地图",
          say: "入职即可见成长路径，分配学习任务，职场成长好帮手",
        },
        {
          url: require("assets/images/icon_4@2x.png"),
          name: "面授课程",
          say: "任务发放，报名，签到，课堂互动，总结，践行报告",
        },
        {
          url: require("assets/images/icon_5@2x.png"),
          name: "课程资源",
          say: "提供千门先之课程资源，解决您的找课程烦恼",
        },
        {
          url: require("assets/images/icon_6@2x.png"),
          name: "问卷调查",
          say: "需求调研，满意度调研，统统满足",
        },
        {
          url: require("assets/images/icon_7@2x.png"),
          name: "数据统计",
          say: "培训数据一目了然，一切培训以数据说话",
        },
        {
          url: require("assets/images/icon_8@2x.png"),
          name: "学习证书",
          say: "在线生成专属企业的学习证书",
        },
        {
          url: require("assets/images/icon_9@2x.png"),
          name: "人才测评",
          say: "各类素质测评，科学高效进行人才管理",
        },
        {
          url: require("assets/images/icon_10@2x.png"),
          name: "闯关答题",
          say: "游戏化互动学习，让培训更轻松",
        },
      ],
      box6_data: [
        {url: require("assets/images/logo_1.png")},
        {url: require("assets/images/logo_2.png")},
        {url: require("assets/images/logo_3.png")},
      ]
    };
  },

  methods: {
    onChange(index) {
      this.current = index;
    },
    onClickCart() {
      this.$router.push('apply');
    },
    onClose(){
      this.$refs.videoRef.pause()
      this.videoShow = false
    }
  },
};
</script>

<style lang="less">
.blue {
  color: #186fff;
}
.box1 {
  width: 100%;
  height: 550px;
  overflow: hidden;
  background: url('~assets/images/head.jpg') top center / cover no-repeat;
}
.box1 > img{
  width: 97px;
  position: absolute;
  top: 14px;
  left: 14px;
}
.box1 .look {
  width: 88px;
  height: 32px;
  font-size: 14px;
  text-align: center;
  line-height: 32px;
  color: #186fff;
  margin: 0 auto;
  position: absolute;
  border-radius: 2px;
  top: 213px;
  left: 0;
  right: 0;
  background: #fff;
}
.box1 .video {
  width: 343px;
}
.box1 .close {
  width: 32px;
  height: 32px;
  position: absolute;
  bottom: -38px;
  left: 50%;
  transform: translateX(-50%);
}
.box2 {
  padding: 16px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  background: #f8faff;
}
.box2 .item {
  width: 163px;
  height: 170px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: #fff;
  margin-bottom: 17px;
}
.box2 .item:nth-child(1),
.box2 .item:nth-child(2) {
  margin-top: -62px;
}
.box2 .item > img {
  width: 58px;
}
.box2 .item > span:nth-of-type(1) {
  font-size: 14px;
  margin: 20px 0 10px;
}
.box2 .item > span:nth-of-type(2) {
  font-size: 20px;
}
.box3 {
  padding: 0 20px 21px;
  overflow: hidden;
}
.box3 .title {
  font-size: 20px;
  font-weight: 500;
  color: #262626;
  margin: 32px 0;
  text-align: center;
}
.box3 .item {
  padding: 16px;
  margin-bottom: 10px;
  background: #eef2fa;
  display: flex;
  justify-content: space-between;
}
.box3 .item img.avatar {
  width: 30px;
  height: 30px;
  margin-right: 18px;
  flex-shrink: 0;
}

.box3 .content > p {
  margin: 0;
}
.box3 .item .content > p:nth-child(1) {
  font-size: 14px;
  color: #2b2e34;
}
.box3 .item .content > p:nth-child(2) {
  font-size: 16px;
  font-weight: 300;
  color: #3b4352;
  line-height: 24px;
  margin-top: 5px;
}

.box4 {
  padding: 0 16px 30px;
  background: #292a2c;
  overflow: hidden;
}
.box4 .wrap {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.box4 .title {
  font-size: 20px;
  font-weight: 500;
  color: #fff;
  margin: 32px 0;
  text-align: center;
}
.box4 .item {
  width: 163px;
  height: 178px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: #fff;
  margin-bottom: 16px;
}
.box4 .item:nth-child(2),
.box4 .item:nth-child(3) {
  background: #1977ff;
  border-radius: 2px;
}
.box4 .item:nth-child(2) > *,
.box4 .item:nth-child(3) > * {
  color: #fff;
}
.box4 .item > img {
  width: 83px;
}
.box4 .item > span {
  font-size: 10px;
  font-weight: 600;
  color: #2b2e34;
  margin-top: 9px;
}
.box4 .item > p {
  font-size: 8px;
  width: 140px;
  text-align: center;
  font-weight: 400;
  color: #666666;
  line-height: 18px;
}

.box5 {
  padding: 0 16px 30px;
  overflow: hidden;
}
.box5 p {
  margin: 0;
}
.box5 .title {
  font-size: 22px;
  font-weight: 500;
  color: #2f2f2f;
  margin: 32px 0 20px;
  text-align: center;
}
.box5 .item {
  display: flex;
  align-items: flex-start;
  height: 71px;
  padding: 18px 0 0;
  box-sizing: border-box;
}
.box5 .item .wrap {
  display: flex;
  flex-direction: column;
  flex: 1;
  height: 100%;
  border-bottom: 1px solid #f2f2f2;
}
.box5 .item > img {
  width: 26px;
  height: 26px;
  margin-right: 11px;
}
.box5 .wrap > span {
  font-size: 14px;
  font-weight: 600;
  color: #252d34;
}
.box5 .wrap > p {
  font-size: 12px;
  font-weight: 400;
  color: #6e7173;
  margin-top: 5px;
}

.box6 {
  background: #f8faff;
  overflow: hidden;
}
.box6 .title {
  font-size: 22px;
  font-weight: 500;
  color: #2f2f2f;
  margin: 32px 0;
  text-align: center;
}
.box6 .img_wrap {
  width: 100%;
  height: auto;
  padding: 0 16px 16px;
  box-sizing: border-box;
}
.box6 .custom-indicator {
  width: 100%;
  position: absolute;
  bottom: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.box6 .custom-indicator .item {
  width: 16px;
  height: 2px;
  background: #e0e3ea;
}
.box6 .custom-indicator .item:nth-child(2) {
  margin: 0 8px;
}
.box6 .custom-indicator .item.current {
  background: #1890ff;
}

.box7 {
  background: #363c4a;
  padding: 30px 19px 90px;
}
.box7 > a {
  line-height: 50px;
  text-align: center;
  border: 2px dashed #737373;
  font-size: 14px;
  font-weight: 400;
  color: #ffffff;
  display: block;
  text-decoration: none !important;
}
.box7 > a:first-child {
  margin-bottom: 15px;
}

.box8 {
  display: flex;
  position: fixed;
  bottom: 0;
  width: 100%;
}
.box8 > a > img {
  width: 24px;
  margin-right: 11px;
}
.box8 > * {
  width: 50%;
  height: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #ff6a00;
  font-size: 16px;
  background: #fff;
}
.box8 > a:last-child {
  background: #1890ff;
  color: #fff;
}
</style>

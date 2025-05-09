<template>
  <div id="app">
    <div class="hearTopBox">
      <div class="fixBox">
        <div class="heardContent">
          <div class="heardLeft">
            <div class="title1">星座极光</div>
            <ul class="ulBox">
              <li v-for="(item, index) in navItems" :key="index">
                <a
                  href="javascript:;"
                  :class="{ activeStyle: activeNav === index }"
                  @click="activeNav = index"
                >
                  {{ item }}
                </a>
              </li>
            </ul>
          </div>
          <div class="heardRight">
            <div class="registerBox" @click="navtologin">登录</div>
            <div class="loginBox" @click="navtologin">免费试用</div>
          </div>
        </div>
      </div>
    </div>
    <div>
      <!-- 首页 -->
      <div class="homePage" style="margin-bottom: 20px" v-if="activeNav == 0">
        <div class="bannerBox">
          <div class="banner-text">
            <div class="main-text">酒旅业务增长加速器</div>
            <div class="sub-text">数字化酒旅营销解决方案专家</div>
          </div>
        </div>
        <div class="homePageproductImg">
          <div class="product-container">
            <div class="product-header" style="margin-top: 100px">
              <div class="main-title">全方位产品服务体系</div>
              <div class="sub-title">实现供应链与渠道的高效协同管理</div>
            </div>
            <div class="process-container">
              <div class="process-row">
                <div class="process-item">
                  <div class="process-title">流量获取</div>
                  <div class="process-content">
                    <div>微信H5</div>
                    <div>微信小程序</div>
                    <div>百度小程序</div>
                    <div>API接口</div>
                  </div>
                </div>
                <div class="process-item">
                  <div class="process-title">交易促成</div>
                  <div class="process-content">
                    <div>社交裂变</div>
                    <div>促销策略</div>
                    <div>直播带货</div>
                  </div>
                </div>
                <div class="process-item">
                  <div class="process-title">支付结算</div>
                </div>
                <div class="process-item">
                  <div class="process-title">履约保障</div>
                  <div class="process-content">
                    <div>订单智能分发</div>
                    <div>自动化分账</div>
                    <div>交易数据分析</div>
                  </div>
                </div>
                <div class="process-item">
                  <div class="process-title">供应链优化</div>
                  <div class="process-content">
                    <div>多业务形态管理</div>
                    <div>PMS系统对接</div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="pageTitle">
          <div class="product-header">
            <div class="main-title" style="margin-top: 75px">服务群体</div>
          </div>
        </div>
        <div class="contentBox">
          <ul class="tabBox">
            <li
              v-for="(item, index) in tabs"
              :key="index"
              :class="['tabItem', { specialLi: activeIndex === index }]"
              @click="activeIndex = index"
            >
              {{ item }}
            </li>
          </ul>
          <div class="el-carousel el-carousel--horizontal">
            <div class="container">
              <div class="left-section">
                <div class="el-carousel el-carousel--horizontal">
                  <div class="el-carousel__container">
                    <div class="imgBox">
                      <img
                        :src="slides[activeIndex].image"
                        alt="展示图片"
                        class="rounded-image"
                      />
                    </div>
                  </div>
                </div>
              </div>
              <div class="right-section">
                <div class="content-wrapper">
                  <p class="description">
                    {{ slides[activeIndex].text }}
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="qudaoBox">
          <div class="pageTitle">
            <div class="product-header" style="margin-top: 540px">
              <div class="main-title">全渠道分发系统</div>
              <div class="sub-title">覆盖主流流量平台，实现高效变现</div>
            </div>
            <div class="channel-grid">
              <div class="channel-item">
                <i class="channel-item__icon">
                  <img src="../../assets/image/fenfa/wx.png" />
                </i>
                <h3 class="channel-item__title">微信小程序</h3>
                <p class="channel-item__desc">零代码快速搭建专属小程序商城</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/zfb.png"
                /></i>
                <h3 class="channel-item__title">支付宝小程序</h3>
                <p class="channel-item__desc">多渠道快速分发，触达海量用户</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/db.png"
                /></i>
                <h3 class="channel-item__title">百度小程序</h3>
                <p class="channel-item__desc">精准搜索流量，快速获取用户</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/dy.png"
                /></i>
                <h3 class="channel-item__title">抖音小程序</h3>
                <p class="channel-item__desc">短视频营销，引爆社交传播</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/tt.png"
                /></i>
                <h3 class="channel-item__title">头条小程序</h3>
                <p class="channel-item__desc">信息流推荐，精准触达用户</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/fz.png"
                /></i>
                <h3 class="channel-item__title">飞猪小程序</h3>
                <p class="channel-item__desc">旅游垂直领域，精准用户群体</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/yz.png"
                /></i>
                <h3 class="channel-item__title">有赞小程序</h3>
                <p class="channel-item__desc">电商解决方案，快速搭建店铺</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/dp.png"
                /></i>
                <h3 class="channel-item__title">H5店铺</h3>
                <p class="channel-item__desc">轻量级移动站点，即开即用</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/sdk.png"
                /></i>
                <h3 class="channel-item__title">API/SDK开发</h3>
                <p class="channel-item__desc">开放接口，实现系统深度集成</p>
              </div>
            </div>
          </div>
        </div>
        <div class="priceBox clearfix">
          <div class="price-header">
            <h2 class="price-title">核心服务</h2>
            <p class="price-subtitle">
              独家直连小红书、视频号、抖音等主流平台的酒旅系统服务商
            </p>
          </div>
          <div class="button-container">
            <button class="cooperate-btn">深度合作</button>
            <button class="try-btn">免费使用</button>
          </div>
        </div>
        <div class="contentPriceBox">
          <div class="price-content">
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/gf.png"
              /></i>
              <div class="price-text">
                <h3>多业务管理</h3>
                <p>支持预约套餐、日历房、本地生活、实物商品等多业态管理</p>
              </div>
            </div>
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/fw.png"
              /></i>
              <div class="price-text">
                <h3>微官网建设</h3>
                <p>支持H5、小程序等多终端展示</p>
              </div>
            </div>
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/td.png"
              /></i>
              <div class="price-text">
                <h3>渠道对接</h3>
                <p>直连主流平台，实现多渠道分销</p>
              </div>
            </div>
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/jy.png"
              /></i>
              <div class="price-text">
                <h3>交易管理</h3>
                <p>支持店铺订单、代理订单管理</p>
              </div>
            </div>
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/cw.png"
              /></i>
              <div class="price-text">
                <h3>财务管理</h3>
                <p>自动化分账，在线发票管理</p>
              </div>
            </div>
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/yx.png"
              /></i>
              <div class="price-text">
                <h3>营销工具</h3>
                <p>提供多种营销方案，助力业务增长</p>
              </div>
            </div>
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/jc.png"
              /></i>
              <div class="price-text">
                <h3>数据分析</h3>
                <p>多维度数据报表，助力运营决策</p>
              </div>
            </div>
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/kf.png"
              /></i>
              <div class="price-text">
                <h3>在线支持</h3>
                <p>7*12小时专业客服，快速响应</p>
              </div>
            </div>
          </div>
        </div>
        <div class="cooperateBox">
          <div class="el-dialog__wrapper" style="display: none">
            <div
              role="dialog"
              aria-modal="true"
              aria-label="dialog"
              class="el-dialog"
              style="margin-top: 15vh; width: 650px"
            >
              <div class="el-dialog__header">
                <span class="el-dialog__title"></span
                ><button
                  type="button"
                  aria-label="Close"
                  class="el-dialog__headerbtn"
                >
                  <i class="el-dialog__close el-icon el-icon-close"></i>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="homePage" style="margin-bottom: 20px" v-if="activeNav == 1">
        <div class="bannerBox1">
          <div class="banner-text">
            <div class="main-text">酒旅行业数字化转型专家</div>
            <div class="sub-text">全方位降低酒旅企业运营成本</div>
          </div>
        </div>
        <div class="jYmanagement"></div>
        <div class="contentBox">
          <ul class="tabBox">
            <li
              v-for="(item, index) in tabs1"
              :key="index"
              :class="['tabItem', { specialLi: activeIndex === index }]"
              @click="activeIndex = index"
            >
              {{ item }}
            </li>
          </ul>
          <div class="el-carousel el-carousel--horizontal">
            <div class="container">
              <div class="left-section">
                <div class="el-carousel el-carousel--horizontal">
                  <div class="el-carousel__container">
                    <div class="imgBox">
                      <img
                        :src="slides1[activeIndex].image"
                        alt="展示图片"
                        class="rounded-image"
                      />
                    </div>
                  </div>
                </div>
              </div>
              <div class="right-section">
                <div class="content-wrapper">
                  <div class="business-header">
                    <h3 class="business-title">
                      {{ slides1[activeIndex].title }}
                    </h3>
                  </div>
                  <p class="description">
                    {{ slides1[activeIndex].text }}
                  </p>
                  <div class="features-grid">
                    <div
                      v-for="(feature, index) in slides1[activeIndex].features"
                      :key="index"
                      class="feature-item"
                    >
                      {{ feature }}
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="box"></div>
        <div class="qudaoBox">
          <div class="pageTitle">
            <div class="product-header" style="margin-top: 540px">
              <div class="main-title">多渠道分发体系</div>
              <div class="sub-title">覆盖全平台流量，实现高效转化</div>
            </div>
            <div class="channel-grid">
              <div class="channel-item">
                <i class="channel-item__icon">
                  <img src="../../assets/image/fenfa/wx.png" />
                </i>
                <h3 class="channel-item__title">微信小程序</h3>
                <p class="channel-item__desc">零代码快速搭建专属商城</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/zfb.png"
                /></i>
                <h3 class="channel-item__title">支付宝小程序</h3>
                <p class="channel-item__desc">多渠道快速分发，触达海量用户</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/db.png"
                /></i>
                <h3 class="channel-item__title">百度小程序</h3>
                <p class="channel-item__desc">精准搜索流量，快速获取用户</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/dy.png"
                /></i>
                <h3 class="channel-item__title">抖音小程序</h3>
                <p class="channel-item__desc">短视频营销，引爆社交传播</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/tt.png"
                /></i>
                <h3 class="channel-item__title">头条小程序</h3>
                <p class="channel-item__desc">信息流推荐，精准触达用户</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/fz.png"
                /></i>
                <h3 class="channel-item__title">飞猪小程序</h3>
                <p class="channel-item__desc">旅游垂直领域，精准用户群体</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/yz.png"
                /></i>
                <h3 class="channel-item__title">有赞小程序</h3>
                <p class="channel-item__desc">电商解决方案，快速搭建店铺</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/dp.png"
                /></i>
                <h3 class="channel-item__title">H5店铺</h3>
                <p class="channel-item__desc">轻量级移动站点，即开即用</p>
              </div>
              <div class="channel-item">
                <i class="channel-item__icon"
                  ><img src="../../assets/image/fenfa/sdk.png"
                /></i>
                <h3 class="channel-item__title">API/SDK开发</h3>
                <p class="channel-item__desc">开放接口，实现系统深度集成</p>
              </div>
            </div>
          </div>
        </div>
        <div class="wechatBox">
          <div class="product-header">
            <div class="main-title">以客户价值为核心的全生命周期服务</div>
          </div>
          <div class="service-container">
            <div class="service-row">
              <div class="service-card">
                <div class="service-icon">
                  <i class="el-icon-user-solid"></i>
                </div>
                <h3 class="service-title">专属顾问服务</h3>
                <p class="service-desc">7*12小时一对一专属支持</p>
              </div>
              <div class="service-card">
                <div class="service-icon"><i class="el-icon-trophy"></i></div>
                <h3 class="service-title">业务增长赋能</h3>
                <p class="service-desc">以客户业务增长为核心目标</p>
              </div>
            </div>
            <div class="service-row">
              <div class="service-card">
                <div class="service-icon">
                  <i class="el-icon-data-analysis"></i>
                </div>
                <h3 class="service-title">数字化升级</h3>
                <p class="service-desc">助力企业实现数字化高效运营</p>
              </div>
              <div class="service-card">
                <div class="service-icon"><i class="el-icon-refresh"></i></div>
                <h3 class="service-title">持续服务优化</h3>
                <p class="service-desc">根据需求持续提升服务能力</p>
              </div>
            </div>
          </div>
        </div>
        <div class="useBox" id="useBox">
          <div class="product-header">
            <div class="main-title">星座极光用户案例</div>
            <div class="sub-title">
              服务酒店、民宿、在线旅行社、KOL、垂直流量主及新流量生态企业
            </div>
          </div>
          <div class="brand-container">
            <div class="brand-category">
              <h3 class="category-title">酒店/民宿</h3>
              <div class="brand-grid">
                <div class="brand-item">安麓</div>
                <div class="brand-item">六善</div>
                <div class="brand-item">青普</div>
                <div class="brand-item">大乐之野</div>
                <div class="brand-item">西坡</div>
              </div>
            </div>
            <div class="brand-category">
              <h3 class="category-title">在线旅行社</h3>
              <div class="brand-grid">
                <div class="brand-item">几何</div>
                <div class="brand-item">借宿</div>
                <div class="brand-item">懒猫旅行</div>
                <div class="brand-item">乐周末度假</div>
                <div class="brand-item">游虾旅游</div>
              </div>
            </div>
            <div class="brand-category">
              <h3 class="category-title">KOL</h3>
              <div class="brand-grid">
                <div class="brand-item">嘻妈爱旅行</div>
                <div class="brand-item">嬉游</div>
                <div class="brand-item">可乐乐Superchloe</div>
                <div class="brand-item">民宿大叔</div>
                <div class="brand-item">紫情小仙女</div>
              </div>
            </div>
            <div class="brand-category">
              <h3 class="category-title">垂直流量主</h3>
              <div class="brand-grid">
                <div class="brand-item">臻美妈咪</div>
                <div class="brand-item">住店打尖</div>
                <div class="brand-item">拔草</div>
                <div class="brand-item">隐心严选</div>
                <div class="brand-item">小居民宿</div>
              </div>
            </div>
            <div class="brand-category">
              <h3 class="category-title">新流量生态</h3>
              <div class="brand-grid">
                <div class="brand-item">一田一墅</div>
                <div class="brand-item">璞缇客</div>
                <div class="brand-item">游侠客</div>
                <div class="brand-item">洋家乐</div>
                <div class="brand-item">浪花朵朵</div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="homePage" style="margin-bottom: 20px" v-if="activeNav == 2">
        <div class="priceBox clearfix">
          <div class="price-header">
            <h2 class="price-title">核心功能</h2>
            <p class="price-subtitle">
              独家整合小红书、视频号、抖音等主流平台的酒旅行业解决方案
            </p>
          </div>
          <div class="button-container">
            <button class="cooperate-btn">深度合作</button>
            <button class="try-btn">免费使用</button>
          </div>
        </div>
        <div class="contentPriceBox">
          <div class="price-content">
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/gf.png"
              /></i>
              <div class="price-text">
                <h3>多元化业务管理</h3>
                <p>支持预约套餐、日历房、本地生活、实物商品等多类型业务管理</p>
              </div>
            </div>
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/fw.png"
              /></i>
              <div class="price-text">
                <h3>多终端官网</h3>
                <p>支持H5、小程序等多平台展示</p>
              </div>
            </div>
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/td.png"
              /></i>
              <div class="price-text">
                <h3>多渠道对接</h3>
                <p>直连主流平台，实现多渠道分销</p>
              </div>
            </div>
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/jy.png"
              /></i>
              <div class="price-text">
                <h3>订单管理</h3>
                <p>支持店铺订单、代理订单管理</p>
              </div>
            </div>
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/cw.png"
              /></i>
              <div class="price-text">
                <h3>财务结算</h3>
                <p>自动化分账，在线发票管理</p>
              </div>
            </div>
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/yx.png"
              /></i>
              <div class="price-text">
                <h3>营销推广</h3>
                <p>提供多种营销方案，助力业务增长</p>
              </div>
            </div>
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/jc.png"
              /></i>
              <div class="price-text">
                <h3>数据报表</h3>
                <p>多维度数据报表，助力运营决策</p>
              </div>
            </div>
            <div class="price-item">
              <i class="price-icon"
                ><img src="../../assets/image/fuwu/kf.png"
              /></i>
              <div class="price-text">
                <h3>在线支持</h3>
                <p>7*12小时专业客服，快速响应</p>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="contentBox1" v-if="activeNav == 3">
        <div class="product-header">
          <div class="main-title">关于我们</div>
        </div>
        <div class="about-container">
          <div class="about-content">
            <div class="about-section">
              <h3>中国旅游市场的数字化分销平台</h3>
              <p>
                为酒店供应链企业（包括酒店集团、精品酒店、旅游代理机构及旅行社）提供全面的分销管理解决方案，涵盖在线预订、日历房管理及本地生活服务等多元化业务。
              </p>
              <p>
                同时为流量主提供完整的交易解决方案，包括个性化微官网搭建、营销工具集成及会员体系管理等一站式服务。
              </p>
            </div>
            <div class="about-section">
              <h3>新兴流量平台的深度合作伙伴</h3>
              <p>
                作为微信、小红书、抖音、有赞、飞猪等新兴流量平台的官方服务商，我们实现了酒旅产品的全平台同步，支持系统自动接单与智能分账，大幅提升运营效率。
              </p>
              <p>
                通过与主流PMS和CRS系统的深度对接，有效降低了酒店在多渠道管理中的运营成本，全面提升了酒旅行业的交易效率。
              </p>
            </div>
          </div>
          <div class="about-image">
            <img src="../../assets/image/home/55.jpg" alt="关于我们" />
          </div>
        </div>
      </div>
    </div>
    <div class="footerBox">
      <div class="content">
        <div class="bottomImgInfo">
          <!-- <div class="contion">111<11/div> -->
          <div class="btn"></div>
        </div>
        <div class="companyTitle">
          <div class="leftText">
            成都星座极光科技有限公司 2019 @ All Rights Reserved
          </div>
          <div class="rightText">蜀ICP备14041939号-3</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import u from "../../assets/js/util.js";
export default {
  data() {
    return {
      // ... 其他数据保持不变 ...
      activeNav: 0,
      activeIndex1: 0,
      navItems: ["首页", "产品与服务", "核心功能", "关于我们"],

      activeIndex: 0,
      tabs: ["酒店民宿", "在线旅行社", "KOL达人", "垂直领域", "新兴生态"],
      tabs1: ["业务管理", "多端操作", "营销策略", "财务系统", "定制服务"],
      // ... existing code ...
      slides: [
        {
          image: require("@/assets/image/home/1.jpg"),
          text: "针对酒店集团及精品酒店，我们提供全方位的运营优化方案，涵盖分销系统、PMS对接及数字化营销，助力提升订单量与营收",
        },
        {
          image: require("@/assets/image/home/2.jpg"),
          text: "为在线旅行社提供网站优化方案，提升用户体验与转化率，增加预订量与佣金收益",
        },
        {
          image: require("@/assets/image/home/4.jpg"),
          text: "为旅游领域KOL提供完整的供应链解决方案与品牌推广支持，实现高效流量变现",
        },
        {
          image: require("@/assets/image/home/5.jpg"),
          text: "为垂直领域流量主提供稳定的酒店民宿供应链，支持在线预订、订单处理与智能分账",
        },
        {
          image: require("@/assets/image/home/6.jpg"),
          text: "为新兴生态企业提供供应链整合方案，实现多平台直连，提升运营效率与变现能力",
        },
      ],
      slides1: [
        {
          image: require("@/assets/image/home/7.jpg"),
          text: "支持多种业务形态管理，包括日历房、预约套餐、本地生活等，实现供应链高效管理",
          title: "业务管理",
          features: [
            "日历房管理",
            "预约套餐",
            "本地生活",
            "实物商品",
            "虚拟商品",
            "旅游线路",
          ],
        },
        {
          image: require("@/assets/image/home/8.jpg"),
          text: "支持多终端操作，移动端实时接单，PC端提供更丰富的功能支持",
          title: "多端操作",
          features: ["PC端", "移动端"],
        },
        {
          image: require("@/assets/image/home/9.jpg"),
          text: "提供多渠道营销工具与策略，帮助提升订单量与用户流量",
          title: "营销策略",
          features: ["渠道对接", "电子卡券", "营销工具"],
        },
        {
          image: require("@/assets/image/home/10.jpg"),
          text: "提供安全可靠的财务管理系统，支持自动分账与在线发票管理",
          title: "财务系统",
          features: ["资金安全", "自动分账", "发票管理"],
        },
        {
          image: require("@/assets/image/home/11.jpg"),
          text: "提供个性化定制服务，支持店铺装修与活动页面设计",
          title: "定制服务",
          features: ["店铺装修"],
        },
      ],
      // ... existing code ...
    };
  },
  async mounted() {
    this.getOem();
  },
  methods: {
    navtologin() {
      this.$router.push("/login");
    },
    async getOem() {
      var oem = await u.get_oem(window.location.host);
      console.log(oem, "oe22222222222m");
    },
  },
};
</script>
<style scoped>
@import url("../../assets/styles/home.css");
/* 添加点击效果样式 */
.tabItem {
  cursor: pointer;
  transition: all 0.3s ease;
}
/* 确保 activeStyle 优先级 */
.ulBox li a.activeStyle {
  color: #409eff !important;
  font-weight: bold;
}
.title1 {
  font-size: 28px;
  font-weight: 600;
  color: #333;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
  letter-spacing: 1px;
  padding: 10px 0;
  position: relative;
  display: inline-block;
}

.title1::after {
  content: "";
  position: absolute;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 3px;
  background: linear-gradient(90deg, #409eff, #67c23a);
  transform: scaleX(0);
  transition: transform 0.3s ease;
}

.title1:hover::after {
  transform: scaleX(1);
}

.bannerBox {
  position: relative;
  /* 保持原有背景图片样式 */
}
.bannerBox1 {
  position: relative;
  /* 保持原有背景图片样式 */
}
.banner-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  color: white;
}

.main-text {
  font-size: 58px;
  font-weight: bold;
  margin-bottom: 10px;
}

.sub-text {
  font-size: 24px;
}

.product-header {
  text-align: center;
  margin-bottom: 40px;
}

.main-title {
  font-size: 26px;
  font-weight: bold;
  color: #333;
  margin-bottom: 10px;
}

.sub-title {
  font-size: 14px;
  color: #666;
}

.product-container {
  max-width: 1200px;
  margin: 0 auto;
}

.process-row {
  display: flex;
  justify-content: space-between;
  gap: 15px;
}

.process-item {
  flex: 1;
  min-width: 200px;
  text-align: center;
}

.process-title {
  background: #007bff;
  color: white;
  padding: 10px 20px;
  border-radius: 25px;
  margin-bottom: 20px;
  display: -webkit-inline-box;
  display: -ms-inline-flexbox;
  display: inline-flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  justify-content: center;
  /* min-width: 120px; */
  height: 130px;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  border-radius: 50%;
  width: 130px;
  text-align: center;
}

.process-content {
  background: #f0f0f05e;
  border-radius: 8px;
  height: 255px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.process-content div {
  padding: 10px 0;
  color: #666;
}

.process-content div:last-child {
  border-bottom: none;
}
</style>






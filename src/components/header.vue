<template>
  <div style="width: 100%">
    <a-layout v-if="screenWidth>=600">
      <div class="logo">
        <a
          href="https://opendrivelab.com/"
          target="_blank"
          rel="noopener noreferrer"
          style="display: flex; justify-content: center; align-items: center"
        >
          <img src="../assets/OpenDriveLab.png" alt="Logo"
        /></a>
      </div>
      <a-layout-header class="layout-header">
        <a-menu mode="horizontal">
          <a-menu-item>
            <router-link to="/">
              <a-icon type="database" />AD-Datasets</router-link
            >
          </a-menu-item>
          <a-menu-item key="Sponsor">
            <a
              href="https://github.com/sponsors/OpenDriveLab"
              target="_blank"
              rel="noopener noreferrer"
            >
              <a-icon
                type="heart"
                theme="filled"
                style="color: rgba(220, 20, 60, 1)"
              />Sponsor</a
            >
          </a-menu-item>
        </a-menu>
      </a-layout-header>
    </a-layout>
    <div class="mobile-class" v-else>
      <div class="logo">
        <a
          href="https://opendrivelab.com/"
          target="_blank"
          rel="noopener noreferrer"
          style="display: flex; justify-content: center; align-items: center"
        >
          <img src="../assets/OpenDriveLab.png" alt="Logo"
        /></a>
      </div>
      <div style="width: 180px" class="mobile-class-menu">
        <a-button
          type="primary"
          style="margin-bottom: 16px; margin-left: 120px; width: 45px"
          @click="toggleCollapsed"
        >
          <a-icon :type="collapsed ? 'menu-unfold' : 'menu-fold'" />
        </a-button>
        <a-menu
          :default-selected-keys="['database']"
          :default-open-keys="['sub1']"
          mode="inline"
          theme="light"
          :inline-collapsed="collapsed"
          v-show="menuShow"
        >
          <a-menu-item key="database">
            <router-link to="/">
              <a-icon type="database" />AD-Datasets</router-link
            >
          </a-menu-item>
          <a-menu-item key="Sponsor">
            <a
              href="https://github.com/sponsors/OpenDriveLab"
              target="_blank"
              rel="noopener noreferrer"
            >
              <a-icon
                type="heart"
                theme="filled"
                style="color: rgba(220, 20, 60, 1)"
              />Sponsor</a
            >
          </a-menu-item>
          <!-- <a-menu-item key="1" >
            <a-icon type="pie-chart" />
            <span>Option 1</span>
          </a-menu-item>
          <a-menu-item key="2" >
            <a-icon type="desktop" />
            <span>Option 2</span>
          </a-menu-item> -->
        </a-menu>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      screenWidth: document.body.clientWidth,
      collapsed: true,
      menuShow: false,
    };
  },
  created() {
    // console.log("this.screenWidth===================", this.screenWidth);
  },
  mounted() {
    window.onresize = () => {
      this.screenWidth = document.body.clientWidth;
      // console.log("this.screenWidth===================", this.screenWidth);
    };
  },
  watch: {
    screenWidth(newValue) {
      // 为了避免频繁触发resize函数导致页面卡顿，使用定时器
      if (!this.timer) {
        // 一旦监听到的screenWidth值改变，就将其重新赋给data里的screenWidth
        this.screenWidth = newValue;
        this.timer = true;
        setTimeout(() => {
          //console.log(this.screenWidth);
          this.timer = false;
        }, 400);
      }
    },
  },
  methods: {
    toggleCollapsed() {
      this.collapsed = !this.collapsed;
      this.menuShow = !this.menuShow;
    },
  },
};
</script>

<style lang="scss" scoped>
.mobile-class {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  padding: 20px;
}
.mobile-class-menu {
  display: flex;
  flex-direction: column;
  margin-top: 10px;
}
.ant-menu-horizontal {
  line-height: 65px;
  white-space: nowrap;
  border: 0;
  /* border-bottom: 1px solid #e8e8e8; */
  box-shadow: none;
}
/* .ant-layout {
  display: flex;
  flex: auto;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  min-height: 0;
  background: #fff;
}
.ant-layout-header {
  height: 64px;
  padding: 0 50px;
  line-height: 64px;
  background: #fff;
}
.logo {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50px;
  padding: 0 24px;
  img {
    height: 25px;
    width: 160px;
  }
} */
.ant-layout {
  display: flex;
  flex-direction: row;
  justify-content: space-between; /* 让子元素分别靠左边和右边 */
  align-items: center;
  min-height: 0;
  background: #fff;
  padding: 0 5%; /* 左右边距为5% */
}

.logo {
  display: flex;
  justify-content: flex-start; /* 让logo靠左边 */
  align-items: center;
  height: 50px;
  img {
    height: 25px;
    width: 160px;
  }
}

.ant-layout-header {
  line-height: 64px;
  background: #fff;
  padding: 0;
}
/* .layout-header {
  display: flex;
  justify-content: flex-end; 
  align-items: center;
  height: 64px;
  padding: 0 5%; 
} */
</style>

<template>
  <div
    v-if="showInMobile"
    class="reward"
  >
    <div
      ref="reward-btn"
      class="reward-btn animated"
      @click="show"
    >
      <span>{{ btnText }}</span>
    </div>

    <div
      ref="reward-container"
      class="reward-container animated"
    >
      <div class="reward-container-header">
        <span class="reward-container-header--title">{{ title }}</span>
        <i @click="closed">
          <svg
            t="1572509238160"
            class="icon"
            viewBox="0 0 1024 1024"
            version="1.1"
            xmlns="http://www.w3.org/2000/svg"
            p-id="4215"
            width="16"
            height="16"
          >
            <path
              d="M887.2 774.2 624.8 510.8l263-260c10.8-10.8 10.8-28.4 0-39.2l-74.8-75.2c-5.2-5.2-12.2-8-19.6-8-7.4 0-14.4 3-19.6 8L512 395.6 249.8 136.6c-5.2-5.2-12.2-8-19.6-8-7.4 0-14.4 3-19.6 8L136 211.8c-10.8 10.8-10.8 28.4 0 39.2l263 260L136.8 774.2c-5.2 5.2-8.2 12.2-8.2 19.6 0 7.4 2.8 14.4 8.2 19.6l74.8 75.2c5.4 5.4 12.4 8.2 19.6 8.2 7 0 14.2-2.6 19.6-8.2L512 626.2l261.4 262.2c5.4 5.4 12.4 8.2 19.6 8.2 7 0 14.2-2.6 19.6-8.2l74.8-75.2c5.2-5.2 8.2-12.2 8.2-19.6C895.4 786.4 892.4 779.4 887.2 774.2z"
              p-id="4216"
            />
          </svg>
        </i>
      </div>
      <div class="reward-container-body">
        <span class="reward-container-header--subTitle">{{ subTitle }}</span>
        <div class="reward-container-body-img-container">
          <div
            v-for="(item, index) in rewardOption"
            :key="index"
            class="reward-container-body-img"
          >
            <img
              :src="item.url"
              :alt="item.text"
            >
            <span>{{ item.text }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "Reward",

    data() {
      return {
        btnText: BTN_TEXT,
        title: TITLE,
        subTitle: SUB_TITLE,
        rewardOption: REWARD_OPTION,
        showInMobile: false
      };
    },

    mounted() {
      const rewardContainer = this.$refs["reward-container"];
      if (rewardContainer) {
        const offsetHeight = rewardContainer.offsetHeight;
        rewardContainer.style.top = `calc(50% - ${offsetHeight / 2}px + 20px)`;
      }
      this.showInMobile = this.isShowReward();
    },

    methods: {
      isShowReward() {
        const isMobile = !!/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(
          navigator.userAgent
        );
        if (isMobile && !SHOW_IN_MOBILE) {
          return false;
        }
        return true;
      },
      show() {
        const rewardBtn = this.$refs["reward-btn"];
        rewardBtn.classList.remove("slideInRight");
        rewardBtn.classList.add("slideOutRight");
        const rewardContainer = this.$refs["reward-container"];
        rewardContainer.classList.remove("slideOutRight");
        rewardContainer.classList.add("slideInRight");
      },
      closed() {
        const rewardContainer = this.$refs["reward-container"];
        rewardContainer.classList.remove("slideInRight");
        rewardContainer.classList.add("slideOutRight");

        setTimeout(() => {
          const rewardBtn = this.$refs["reward-btn"];
          rewardBtn.classList.remove("slideOutRight");
          rewardBtn.classList.add("slideInRight");
        }, 800);
      }
    }
  };
</script>

<style lang="stylus" scoped>
  .reward {
    font-family: 'Helvetica Neue', Helvetica, 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', '微软雅黑', Arial, sans-serif;

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    img {
      width: 85%;
      object-fit: contain;
      display: inline-block;
      vertical-align: middle;
    }

    &-btn {
      color: $accentColor;
      background-color: lighten($accentColor, 50%);
      position: fixed;
      top: 50%;
      right: 0;
      padding: 10px;
      font-size: 16px;
      font-weight: 600;
      padding-left: 0;
      cursor: pointer;
      height: 40px;

      &::after {
        content: '¥';
        position: absolute;
        display: inline-flex;
        justify-content: center;
        vertical-align: middle;
        align-items: center;
        height: 100%;
        width: 30px;
        background-color: lighten($accentColor, 50%);
        top: 0;
        left: -29px;
        border-top-left-radius: 50%;
        border-bottom-left-radius: 50%;
        z-index: -1;
      }
    }

    &-container {
      transform: translate3d(200%, 0, 0);
      color: $accentColor;
      width: 280px;
      height: max-content;
      background-color: #fff;
      border: 1px solid lighten($textColor, 30%);
      position: fixed;
      min-height: 260px;
      top: calc(50% - 130px + 20px);
      right: 0;
      border-radius: 5px;
      overflow: hidden;

      &-header {
        padding: 10px 20px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        border-bottom: 2px dotted #dedede;

        i {
          font-size: 16px;
          fill: $accentColor;
          display: flex;
          align-items: center;
          justify-content: center;
          cursor: pointer;
        }

        &--title {
          font-size: 18px;
        }

        &--title, &--subTitle {
          display: block;
        }

        &--subTitle {
          font-size: 14px;
          color: $textColor;
          text-align: center;
        }
      }

      &-body {
        color: $textColor;
        padding: 20px;

        &-img-container {
          display: flex;
          justify-content: space-between;
          margin-top: 20px;
        }

        &-img {
          text-align: center;

          img {
            width: 100px;
            height: 100px;
          }

          span {
            display: block;
            margin-top: 10px;
          }
        }
      }
    }
  }

  @keyframes slideOutRight {
    from {
      -webkit-transform: translate3d(0, 0, 0);
      transform: translate3d(0, 0, 0);
    }

    to {
      visibility: hidden;
      -webkit-transform: translate3d(100%, 0, 0);
      transform: translate3d(100%, 0, 0);
    }
  }

  .slideOutRight {
    -webkit-animation-name: slideOutRight;
    animation-name: slideOutRight;
  }

  @keyframes slideInRight {
    from {
      -webkit-transform: translate3d(100%, 0, 0);
      transform: translate3d(100%, 0, 0);
      visibility: visible;
    }

    to {
      -webkit-transform: translate3d(0, 0, 0);
      transform: translate3d(0, 0, 0);
    }
  }

  .slideInRight {
    -webkit-animation-name: slideInRight;
    animation-name: slideInRight;
  }

  .animated {
    -webkit-animation-duration: 1s;
    animation-duration: 1s;
    -webkit-animation-fill-mode: both;
    animation-fill-mode: both;
  }
</style>

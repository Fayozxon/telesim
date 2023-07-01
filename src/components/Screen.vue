<script>

export default {
  data() {
    return {
      profilePicSrc: '',
      username: 'Fayozxon Sh.',
      userStatus: 'online',
      time: ''
    }
  },
  computed: {
    isStatusOnline() {
      if (this.userStatus.toLowerCase() == 'online') return true;
      return false;
    },
    getUsernameLetters() {
      let name = this.username.split(' ');
      if (name.length > 1 && name[1][0]) {
        return name[0][0]+name[1][0];
      }
      return name[0][0];
    }
  },
  methods: {
    onFilePicked(event) {
      const files = event.target.files;
      const fileReader = new FileReader();
      fileReader.addEventListener('load', () => {
        this.profilePicSrc = fileReader.result;
      });
      fileReader.readAsDataURL(files[0]);
      this.profilePicSrc = files[0];
    },
    getTime() {
      setInterval(() => {
        let now = new Date(),
            hour = now.getHours(),
            min = now.getMinutes();
            
        this.time = `${hour}:${min}`
      }, -1000);
    }
  },
  mounted() {
    this.getTime();
  }
}
</script>

<template>
  
  <div class="box">
    <div class="screen">
      <!-- header -->
      <div class="screen__header">
        <div class="screen__header--status">
          <span class="time">{{ time }}</span>
          <div class="icons">
            <img src="../assets/icons/icon-signal.svg">
            <img src="../assets/icons/icon-wifi.svg">
            <img src="../assets/icons/icon-battery.svg">
          </div>
        </div>
        <!-- profile -->
        <div class="screen__header--profile">
          <span class="button">
            <img src="../assets/icons/icon-back.svg">
            Chats
          </span>
          <div class="name">
            <input
              class="input-name"
              type="text"
              v-model="username"
              placeholder="Name"
              spellcheck="false">
            <input
              class="input-status"
              :class="{accent: isStatusOnline}"
              type="text"
              v-model="userStatus"
              placeholder="status"
              spellcheck="false">
          </div>
          <div class="img" :class="{bg: !profilePicSrc}">
            <h3 v-if="!profilePicSrc">{{ getUsernameLetters }}</h3>
            <img class="pic" v-if="profilePicSrc" :src="profilePicSrc">
            <div class="icon-box">
              <img class="icon" src="../assets/icons/icon-camera.svg">
            </div>
            <input class="file-input" accept="image/png, image/jpeg, image/jpg" type="file" @change="onFilePicked">
          </div>
        </div>
      </div>
      <!-- screen -->
      <div class="screen__messages">
        <div class="right">

        </div>
      </div>
      <!-- input -->
      <div class="screen__input">
        <div class="screen__input--icons">
          <img src="../assets/icons/icon-attach.svg">
          <div class="input">
            <span>Message</span>
            <img src="../assets/icons/icon-stickers.svg">
          </div>
          <img src="../assets/icons/icon-mic.svg">
        </div>
        <!-- home btn -->
        <div class="screen__input--home-btn">
          <span></span>
        </div>
      </div>
    </div>
  </div>

</template>

<style lang="scss" scoped>

.box {
  display: flex;
  justify-content: center;
}

.screen {
  position: relative;
  width: 375px;
  min-width: 375px;
  height: 812px;
  background: url('../assets/screen-bg.png') no-repeat;
  background-size: cover;
  color: #000;
  box-shadow: 0 20px 70px rgba(0,0,0,0.15);

  // @media only screen and (max-width: 374px) {
  //   transform: scale(0.8);
  // }

  &__header {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 88px;
    background: #F6F6F6;

    &--status {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 14px 15px;
      padding-left: 30px;
      padding-bottom: 9px;

      .time {
        font-size: 15px;
        font-weight: 700;
      }

      .icons {
        display: flex;
        align-items: center;
        gap: 5px;
      }
    }

    &--profile {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding-left: 8px;
      padding-right: 6px;

      .button {
        display: flex;
        align-items: center;
        gap: 7px;
        font-size: 17px;
        color: #037EE5;
      }

      .name {
        text-align: center;
        padding-right: 18px;
        display: flex;
        flex-direction: column;
        
        .input-name {
          font-size: 17px;
          font-weight: 700;
          letter-spacing: -0.5px;
          background: transparent;
          border: none;
          text-align: center;
        }

        .input-status {
          font-size: 13px;
          letter-spacing: 0.3px;
          color: #787878;
          background: transparent;
          width: auto;
          border: none;
          text-align: center;

          &.accent {
            color: #037EE5;
          }
        }

      }

      .img {
        position: relative;
        width: 37px;
        height: 37px;
        border-radius: 50%;
        overflow: hidden;
        cursor: pointer;

        &.bg {
          background: linear-gradient(to bottom right, rgb(12, 255, 255), rgb(41, 191, 255));
        }

        .file-input {
          position: absolute;
          top: -40px;
          left: 0;
          right: 0;
          bottom: 0;
          cursor: pointer;
          opacity: 0;
        }

        &:hover .icon-box {
          opacity: 1;
        }

        h3 {
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%,-50%);
          font-size: 14px;
          color: #fff;
          text-transform: uppercase;
          font-weight: 700;
          z-index: 1;
          pointer-events: none;
        }

        .pic {
          position: absolute;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
          object-fit: cover;
        }
        
        .icon-box {
          position: absolute;
          top: 0;
          left: 0;
          right: 0;
          bottom: 0;
          background: rgba(0,0,0,0.8);
          transition: 200ms;
          opacity: 0;
          z-index: 5;
          pointer-events: none;

          .icon {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%,-50%);
            width: 18px;
            height: 18px;
            filter: invert(1);
          }
        }
      }
    }
  }

  &__input {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    height: 79px;
    display: flex;
    justify-content: end;
    flex-direction: column;
    background: #F6F6F6;
    
    &--icons {
      display: flex;
    }

    &--icons {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding-bottom: 22px;
      padding-left: 7px;
      padding-right: 11px;

      .input {
        display: flex;
        align-items: center;
        background: #fff;
        border-radius: 50px;
        padding-top: 5px;
        padding-bottom: 6px;
        padding-left: 13px;
        padding-right: 8px;
        border: 1px solid #D1D1D6;

        span {
          font-size: 17px;
          color: #AEAEB2;
        }

        img {
          margin-left: 180px;
        }
      }
    }

    &--home-btn {
      display: flex;
      justify-content: center;
      padding-bottom: 9px;
      
      span {
        width: 134px;
        height: 5px;
        background: rgba(128, 128, 128, 0.3);
        border-radius: 10px;
      }
    }
  }
}
</style>
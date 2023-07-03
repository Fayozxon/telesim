<script>

export default {
  props: ['messages', 'isLightTheme', 'screenBgSrc', 'isBgBlurred'],
  data() {
    return {
      profilePicSrc: '',
      username: 'Pavel Durov',
      userStatus: 'online',
      time: '',
      date: ''
    }
  },
  computed: {
    isStatusOnline() {
      let statuses = ['online', 'typing', 'yozmoqda', 'onlayn']
      for (let i = 0; i < statuses.length; i++) {
        if (this.userStatus.includes(statuses[i])) return true;
      }
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
        
        if (min.toString().length < 2) {
          min = '0'+min;
        }
            
        this.time = `${hour}:${min}`
      }, -1000);
    },
    getDate() {
      let months = ['January','February','March','April','May','June','July','August','September','October','November','December'];
      let today = new Date();
      this.date = `${months[today.getMonth()]} ${today.getDate()}`;
    }
  },
  mounted() {
    this.getTime();
    this.getDate();
  }
}
</script>

<template>
  
  <div class="box">
    <div class="screen" :class="{dark: !isLightTheme}">
      <img
        v-if="screenBgSrc"
        :src="screenBgSrc"
        class="screen__bg"
        :class="{blurred: isBgBlurred}"
        alt="Background image">
      <!-- greeting -->
      <div v-if="!messages.length" class="screen__greeting-box">
        <h3>No messages here yet...</h3>
        <p>Start the conversation or tap the greeting below.</p>
        <img src="../assets/stickers/sticker-5.gif" alt="Sticker">
      </div>
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
            Back
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
        <p v-for="msg in messages" class="msg" :class="`msg-${msg.side}`, {img: msg.img.length}">
          {{ msg.text }}
          <img v-if="msg.img.length" :src="msg.img" alt="Image in message" class="msg-img">
          <span class="time">{{ msg.time }}</span>
          <img class="icon" v-if="msg.side == 'right' && msg.isRead && isLightTheme" src="../assets/icons/icon-read.svg">
          <img class="icon" v-if="msg.side == 'right' && !msg.isRead && isLightTheme" src="../assets/icons/icon-not-read.svg">
          <img class="icon" v-if="msg.side == 'right' && msg.isRead  && !isLightTheme" src="../assets/icons/icon-dk-read.svg">
          <img class="icon" v-if="msg.side == 'right' && !msg.isRead  && !isLightTheme" src="../assets/icons/icon-dk-not-read.png">
        </p>
        <h3 v-if="messages.length" class="screen__messages--date">{{ date }}</h3>
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
  overflow: hidden;

  // @media only screen and (max-width: 374px) {
  //   transform: scale(0.8);
  // }

  &__bg {
    display: block;
    position: absolute;
    top: -5px;
    left: -5px;
    width: 105%;
    height: 105%;
    object-fit: cover;

    &.blurred {
      filter: blur(10px);
    }
  }

  &__greeting-box {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 220px;
    transform: translate(-50%,-50%);
    background: rgba(0, 0, 0, 0.1);
    backdrop-filter: blur(20px);
    box-shadow: 0 1px 10px rgba(0,0,0,0.03);
    color: #fff;
    font-size: 13px;
    text-align: center;
    border-radius: 10px;
    padding: 15px;

    h3 {
      padding-bottom: 5px;
    }

    img {
      width: 100px;
      margin-top: 10px;
    }
  }

  &__header {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 88px;
    background: rgba(246, 246, 246, 0.85);
    backdrop-filter: blur(15px);
    z-index: 2;

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
        color: #037EE5 !important;
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

  &__messages {
    position: absolute;
    top: 0;
    bottom: 79px;
    display: flex;
    flex-direction: column-reverse;
    justify-content: end;
    align-items: start;
    padding: 5px 20px;
    font-size: 15px;
    width: 100%;
    overflow: hidden;

    &--date {
      align-self: center;
      background: rgba(0, 0, 0, 0.2);
      color: #fff;
      padding: 2px 10px;
      border-radius: 20px;
      font-size: 14px;
      margin-bottom: 20px;
    }

    .msg-right + .msg-right::before {
      display: none;
    }
    .msg-left + .msg-left::before {
      display: none;
    }
    .msg-left + .msg-right {
      margin-bottom: 5px;
    }

    .msg-right + .msg-left {
      margin-bottom: 5px;
    }

    .msg {
      position: relative;
      max-width: 298px;
      padding: 8px 12px;
      margin: 2px 0;
      display: flex;
      flex-wrap: wrap;
      align-items: flex-end;
      justify-content: end;
      column-gap: 3px;

      &.img {
        padding: 2px;
        justify-content: center;
        align-items: center;
        
        .msg-img {
          position: relative;
          width: 100%;
          border-radius: inherit;
        }

        .time {
          position: absolute;
          bottom: 10px;
          right: 20px;
          background: rgba(0,0,0,0.2);
          color: #fff;
          padding: 1px 7px;
          border-radius: 10px;
        }
      }

      &-right.img {
        .time {
          padding-right: 25px;
        }
        
        .icon {
          position: absolute;
          right: 27px;
          filter: brightness(100);
          bottom: 14px;
        }
      }

      .time {
        position: relative;
        right: -3px;
        bottom: -4px;
        font-size: 12px;
        color: #9C9CA3;
      }

      &-left {
        background: #fff;
        border-radius: 18px;
        border-top-left-radius: 12px;
        border-bottom-left-radius: 12px;

        &::before {
          content: url('../assets/icons/msg-lt-left.svg');
          position: absolute;
          bottom: -5px;
          left: -6px;
        }
      }

      &-right {
        background: #E7FECC;
        border-radius: 18px;
        border-top-right-radius: 12px;
        border-bottom-right-radius: 12px;
        align-self: end;

        .time {
          position: relative;
          right: -4px;
          bottom: -5px;
        }

        .icon {
          position: relative;
          right: -5px;
          bottom: -2;
        }

        &::before {
          content: url('../assets/icons/msg-lt-right.svg');
          position: absolute;
          bottom: -5px;
          right: -6px;
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
    background: rgba(246, 246, 246, 0.8);
    backdrop-filter: blur(15px);
    
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

  // Dark mode
  &.dark {
    background-image: url('../assets/screen-bg-dark.png');
    background-color: #000;

    * {
      color: #fff;
    }

    .screen__messages--date {
      background: rgba(255, 255, 255, 0.15);
    }

    .screen__header {
      background: rgba(23, 23, 23, 0.9);

      &--status img {
        filter: invert(1);
      }
    }

    .screen__input {
      background: rgba(38, 38, 40, 0.9);

      .input {
        background: #000;
        border-color: #4B4B4D;
      }
    }

    .msg {
      &-left {
        background: #252033;

        &::before {
          content: url('../assets/icons/msg-dk-left.svg');
        }
      }

      &-right {
        background: #7253F6;

        .time {
          color: #E9E9EB;
        }

        img {
          bottom: -4px;
        }

        &::before {
          content: url('../assets/icons/msg-dk-right.svg');
        }
      }
    }
  }
}
</style>
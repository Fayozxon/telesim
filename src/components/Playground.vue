<script>

export default {
    props: ['isLightTheme'],
    data() {
    return {
        msg: '',
        img: '',
        markAsRead: true,
        isBlurred: false
    }
  },
  methods: {
    getTime() {
        let now = new Date(),
            hour = now.getHours(),
            min = now.getMinutes();
        
        if (min.toString().length < 2) {
          min = '0'+min;
        }

        return `${hour}:${min}`;
    },
    newMessage(side) {
        if (this.msg.length || this.img.length) {
            let msg = {
                text: this.msg,
                isRead: this.markAsRead,
                time: this.getTime(),
                img: this.img,
                side
            }
    
            this.$emit('addMessage', msg);
            this.msg = '';
            this.img = '';
        }
    },
    sendMessage() {
        this.newMessage('right');
    },
    receiveMessage() {
        this.newMessage('left');
    },
    onBgPicked(event) {
      const files = event.target.files;
      let img = URL.createObjectURL(files[0]);
      this.$emit('newScreenBg', img);
    },
    pressInput() {
        bgInput.click();
    },
    pressSendImgInput() {
        sendImgInput.click();
    },
    pressReceiveImgInput() {
        receiveImgInput.click();
    },
    sendImg(event) {
        this.msg = '';
        const files = event.target.files;
        this.img = URL.createObjectURL(files[0]);
        this.newMessage('right');
    },
    receiveImg(event) {
        this.msg = '';
        const files = event.target.files;
        this.img = URL.createObjectURL(files[0]);
        this.newMessage('left');
    }
  }
}
</script>

<template>
    
    <div class="playground">
        <h2 class="playground__title">
            {{ $t("pg-dark") }} 
            <div class="toggle">
                <input type="checkbox" :checked="isLightTheme" @click="$emit('switchScreenTheme')">
                <div class="custom"></div>
            </div>
            {{ $t("pg-light") }}
        </h2>
        <!-- input -->
        <textarea v-model="msg" class="playground__input" :placeholder="$t('pg-placeholder')"></textarea>
        <div class="playground__checkbox">
            <div class="checkbox">
                <input type="checkbox" v-model="markAsRead" id="markAsRead">
                <div class="custom"></div>
            </div>
            <label for="markAsRead">{{ $t("pg-subtext-1") }}</label>
        </div>
        <!-- buttons -->
        <div class="playground__btns">
            <div>
                <button @click="sendMessage" class="btn btn-send">
                    <img src="../assets/icons/icon-up.svg">
                    <span class="hide-mobile">{{ $t("pg-btn-1") }}</span>
                </button>
                <button @click="receiveMessage" class="btn">
                    <img src="../assets/icons/icon-down.svg">
                    <span class="hide-mobile">{{ $t("pg-btn-2") }}</span>
                </button>
                <button @click="$emit('deleteLastMessage')" class="btn btn-reset">
                    <img src="../assets/icons/icon-reset.svg">
                </button>
            </div>
            <div>
                <button class="btn btn-secondary"  @click="pressSendImgInput">
                    <img src="../assets/icons/icon-photo.svg">
                    {{ $t("pg-btn-1") }}
                </button>
                <input
                  type="file"
                  accept="image/png, image/jpeg"
                  id="sendImgInput"
                  style="display: none;"
                  @change="sendImg">
                <button class="btn btn-secondary" @click="pressReceiveImgInput">
                    <img src="../assets/icons/icon-photo.svg">
                    {{ $t("pg-btn-2") }}
                </button>
                <input
                  type="file"
                  accept="image/png, image/jpeg"
                  id="receiveImgInput"
                  style="display: none;"
                  @change="receiveImg">
            </div>
        </div>
        <!-- bg control -->
        <div class="file-input">
            <button class="btn" @click="pressInput">{{ $t("pg-btn-3") }}</button>
            <input type="file" @change="onBgPicked" accept="image/png, image/jpeg" id="bgInput">
        </div>
        <div class="playground__checkbox">
            <div class="checkbox">
                <input type="checkbox" @click="$emit('makeBgBlurred')" id="isBlurred">
                <div class="custom"></div>
            </div>
            <label for="isBlurred">{{ $t("pg-subtext-2") }}</label>
        </div>
        <!-- download ss -->
        <button class="btn" @click="$emit('takeScreenshot')">
            <img src="../assets/icons/icon-download.svg">
            {{ $t("pg-btn-4") }}
        </button>
    </div>

</template>

<style lang="scss" scoped>
@import '../main.scss';

.playground {
    &__title {
        font-size: $fs-300;
        padding-bottom: 30px;

        .toggle {
            margin: 0 15px;
        }
    }

    &__input {
        padding: 10px;
        width: 100%;
        border: 1px solid $clr-primary-300;
        border-radius: 5px;
        outline: none;
        height: 110px;
        resize: vertical;
        background: $clr-primary-200;
        transition: $ts-200;

        &:focus {
            border-color: $clr-accent-500;
        }

        &::placeholder {
            color: $clr-primary-400;
        }
    }

    &__checkbox {
        display: flex;
        align-items: center;
        padding-top: 10px;
        padding-bottom: 30px;
        user-select: none;

        .checkbox {
            margin-right: 10px;
        }
    }

    &__btns {
        padding-bottom: 20px;

        .btn {
            padding: 12px;
            
            @media only screen and (max-width: 456px) {
                svg, img, i {
                    margin-right: 0;
                }
            }
        }

        & > div {
            display: flex;
            justify-content: stretch;
            gap: 10px;
            padding-bottom: 10px;
        }

        .btn-reset {
            svg, img, i {
                margin-right: 0;
            }
        }

        .btn-send {
            svg, img, i {
                margin: 0 3px;
            }
        }
    }

    .file-input {
        input {
            display: none;
        }
    }
}
</style>

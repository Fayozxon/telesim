<script>

export default {
  data() {
    return {
        isLightTheme: true,
        msg: '',
        markAsRead: true,
        isBlurred: false
    }
  }
}
</script>

<template>
    
    <div class="playground">
        <h2 class="playground__title">
            Yorqin
            <div class="toggle">
                <input type="checkbox" v-model="isLightTheme">
                <div class="custom"></div>
            </div>
            Qorong'u
        </h2>
        <!-- input -->
        <textarea v-model="msg" class="playground__input" placeholder="xabarni yozing..."></textarea>
        <div class="playground__checkbox">
            <div class="checkbox">
                <input type="checkbox" v-model="markAsRead" id="markAsRead">
                <div class="custom"></div>
            </div>
            <label for="markAsRead">o'qilgan deb belgilash</label>
        </div>
        <!-- buttons -->
        <div class="playground__btns">
            <div>
                <button class="btn">
                    <img src="../assets/icons/icon-up.svg">
                    <span class="hide-mobile">Yuborish</span>
                </button>
                <button class="btn">
                    <img src="../assets/icons/icon-down.svg">
                    <span class="hide-mobile">Qabul qilish</span>
                </button>
                <button class="btn btn-reset">
                    <img src="../assets/icons/icon-reset.svg">
                </button>
            </div>
            <div>
                <button class="btn btn-secondary">
                    <img src="../assets/icons/icon-photo.svg">
                    Yuborish
                </button>
                <button class="btn btn-secondary">
                    <img src="../assets/icons/icon-photo.svg">
                    Qabul qilish
                </button>
            </div>
        </div>
        <!-- bg control -->
        <button class="btn">Fon rasmini qo'shish</button>
        <div class="playground__checkbox">
            <div class="checkbox">
                <input type="checkbox" v-model="isBlurred" id="isBlurred">
                <div class="custom"></div>
            </div>
            <label for="isBlurred">fon xiralashish effekti</label>
        </div>
        <!-- download ss -->
        <button class="btn">
            <img src="../assets/icons/icon-download.svg">
            Skrinshot
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
            flex-wrap: wrap;
            gap: 10px;
            padding-bottom: 10px;
        }

        .btn-reset {
            svg, img, i {
                margin-right: 0;
            }
        }
    }
}
</style>
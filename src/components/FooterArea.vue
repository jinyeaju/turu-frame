<template>
    <div class="footerContent" ref="footerArea">
        <a href="#" class="footerLogo">
            <img src="../assets/image/lisn_logo_black.png" alt="리즌 디자인의 로고">
        </a>
        <div class="copyrightArea">
            <p>@copyright 2023. Jin YeaJu</p>
        </div>
    </div>
</template>
<script>
// import { ref, computed } from 'vue';
export default {
    name: 'PageFour',
    components: {
    },
    props: {
        hPercent : Number
    },
    data() {
		return {
            heightPercentage: this.hPercent,
        }
	},
};
</script>

<style lang="scss" scoped>
// @import "../assets/scss/footer-area.scss";

.footerContent {
    // position: fixed;
    // top: calc(100% - 64px);
    // transition: top 0.3s;
    // top: 100%;
    // left: 0;
    width: 100%;
    height: 64px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 100px;
    background-color: skyblue;
    z-index: 100;
    a {
        img {
            display: block;
            height: 30px;
            filter: brightness(0);
        }
    }
    .copyrightArea {
        p {
            display: block;
            height: 100%;
            color: #333;
            font-size: 16px;
            padding: 0 20px;
            line-height: 40px;
        }
    }
}
</style>
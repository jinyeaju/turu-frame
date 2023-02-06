<template>
    <div class="secondContentPage">
        <!-- 콘텐츠 영역 시작 -->
        <div class="pageOneInnerContent">
            <!-- <div class="firstWording" ref="firstStyle" :style="`transform: ${titleFontResize}`"> -->
            <div class="firstWording" ref="firstStyle">
                2016
            </div>
        </div>
        <!-- 콘텐츠 영역 끝 -->
    </div>
</template>
<script>
// import { ref, computed } from 'vue';
export default {
    name: 'PageTwo',
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
    methods: {
    },
    mounted() {
    },
    // setup(props) {
    //     const titleFontResizeMove = computed(() => {
    //         // console.log('translate3d(-50%, -50%, '+ (470 - Math.min(100, props.hPercent) * (12 / 10)) + 'sdsdsdsds)');
    //         if(props.hPercent <= 100){
    //             return `translate3d(-50%, -50%, ${470 - Math.min(100, props.hPercent) * (12 / 10)}px)` 
    //         }else if(props.hPercent <= 140){
    //             return `translate3d(${-50 - Math.min(40, props.hPercent - 100) * (5 / 4)}%, -50%, 350px)`
    //         }else if(props.hPercent <= 200){
    //             return `translate3d(-100%, ${-50 - Math.min(60, props.hPercent - 140) * (5 / 2)}%, 350px)`
    //         }else{
    //             return `translate3d(-100%, -200%, 350px)`
    //         }
    //         // return props.hPercent <= 100 
    //         // ? `translate3d(-50%, -50%, ${470 - Math.min(100, props.hPercent) * (12 / 10)}px)` 
    //         // : props.hPercent <= 140 
    //         // ? `translate3d(${-50 - Math.min(40, props.hPercent - 100) * (5 / 4)}%, -50%, 350px)` 
    //         // : props.hPercent <= 180 
    //         // ? `translate3d(-100%, ${-50 - Math.min(40, props.hPercent - 140) * (9 / 4)}%, 350px)` 
    //         // : `translate3d(-100%, -140%, 350px)`;
    //     });
    //     // const titleFontOpacityUp = computed(() => {
    //     //     return `${0 + Math.min(50, props.hPercent - 180) * 0.02}` 
    //     // });

    //     const firstStyle = ref(null)
        
    //     return {
    //         firstStyle,
    //         titleFontResizeMove,
    //     }
        
    // },
};
</script>

<style lang="scss" scoped>
// @import "../assets/scss/PageOne.scss";

.secondContentPage {
    // width: 100%;
    // height: 3000vh;
    // position: absolute;
    // top: 100vh;
    // left: 0;
    // overflow: hidden;
    // background-color: red;
    .pageOneInnerContent {
        position: absolute;
        top: 0;
        left: 50%;
        transform: translateX(-50%);
        perspective: 500px;
        width: 100%;
        height: 100vh;
        padding-top: 64px;
        .firstWording {
            color: white;
            font-size: 40px;
            font-weight: bold;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            // transform: translate3d(-50%, -50%, 470px);
            // transform: v-bind('titleFontResizeMove');
        }

        .bottomArrow {
            position: absolute;
            bottom: 5%;
            left: 50%;
            transform: translateX(-50%);
            width: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            img {
                height: 30px;
                filter: invert(100%);
            }
        }

        

    }
}

</style>
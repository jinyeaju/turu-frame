<template>
    <div class="firstContentPage">
        <div class="backgroundVideo">
            <video autoplay loop muted playsinline>
                <source src="../assets/video/page01_background.mp4" type="video/mp4" media="(min-width: 640px)">
                <source src="../assets/video/sero-video-one.mp4" type="video/mp4">
            </video>
        </div>
    </div>
</template>
<script>
// import { ref, computed } from 'vue';
export default {
    name: 'PageOne',
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
    setup() {
        // const titleFontResizeMove = computed(() => {
        //     // console.log('translate3d(-50%, -50%, '+ (470 - Math.min(100, props.hPercent) * (12 / 10)) + 'sdsdsdsds)');
        //     if(props.hPercent <= 100){
        //         return `translate3d(-50%, -50%, ${470 - Math.min(100, props.hPercent) * (12 / 10)}px)` 
        //     }else if(props.hPercent <= 140){
        //         return `translate3d(${-50 - Math.min(40, props.hPercent - 100) * (5 / 4)}%, -50%, 350px)`
        //     }else if(props.hPercent <= 200){
        //         return `translate3d(-100%, ${-50 - Math.min(60, props.hPercent - 140) * (5 / 2)}%, 350px)`
        //     }else{
        //         return `translate3d(-100%, -200%, 350px)`
        //     }
        //     // return props.hPercent <= 100 
        //     // ? `translate3d(-50%, -50%, ${470 - Math.min(100, props.hPercent) * (12 / 10)}px)` 
        //     // : props.hPercent <= 140 
        //     // ? `translate3d(${-50 - Math.min(40, props.hPercent - 100) * (5 / 4)}%, -50%, 350px)` 
        //     // : props.hPercent <= 180 
        //     // ? `translate3d(-100%, ${-50 - Math.min(40, props.hPercent - 140) * (9 / 4)}%, 350px)` 
        //     // : `translate3d(-100%, -140%, 350px)`;
        // });


        // const firstStyle = ref(null)
        
        return {
            // firstStyle,
            // titleFontResizeMove,
        }
        
    },
};
</script>

<style lang="scss" scoped>
// @import "../assets/scss/PageOne.scss";

.firstContentPage {
    // width: 100%;
    // height: 100vh;
    // position: absolute;
    // top: 0px;
    // left: 0;
    // overflow: hidden;
    // padding-top: 64px;
    .backgroundVideo {
        width: 100%;
        height: 100vh;
        overflow: hidden;
        // position: fixed;
        // top: 0;
        video {
            // padding-top: 64px;
            // position: absolute;
            // top: 0;
            // left: 0;
            // bottom: 0;
            // right: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
        } 
    }
}

</style>
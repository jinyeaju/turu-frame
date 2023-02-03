<template>
    <div class="headerContent" ref="headerArea">
        <a href="#" class="headerLogo">
            <img src="../assets/image/lisn_logo_black.png" alt="리즌 디자인의 로고">
        </a>
        <div class="headerGnb">
            <a href="#">스토리</a>
        </div>
    </div>
</template>
<script>
// import { onMounted, ref } from 'vue';
export default {
    name: 'HeaderArea',
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
    // setup(props) {
    //     const headerArea = ref(null)
    //     // const pageOneHeightPercent = ref(null)
    //     onMounted(() => {
    //         // console.log(props.hPercent, 'dsdqduqgdqgig');
    //     })
        
    //     window.addEventListener("scroll", () => {
            
    //         console.log(headerArea.value)
    //         console.log(props.hPercent, 'lam;ksakcnksv');
            
    //         // if(props.hPercent >= 20370){ 
    //         //     headerArea.value.style.zIndex = 4;
    //         //     if(props.hPercent <= 23000){ 
    //         //         headerArea.value.style.background = `rgba(255, 255, 255, ${ 0.3 - (props.hPercent-22000) / 3000} )`;
    //         //     }else if(props.hPercent <= 36666){
    //         //         headerArea.value.style.background = `rgba(255, 255, 255, 0 )`;
    //         //     }else if(props.hPercent > 36666){
    //         //         headerArea.value.style.background = `rgba(0, 0, 0, 1 )`;
    //         //     }
    //         // }else if(0 < props.hPercent < 20370){ 
    //         //     headerArea.value.style.zIndex = 0;
    //         //     headerArea.value.style.background = `rgba(255, 255, 255, 0.3 )`;
    //         // }
    //     });
    //     return {
    //         headerArea,
    //     }
    // },
};
</script>

<style lang="scss">
@import "../assets/scss/header-area.scss";
</style>
<template>
  <HeaderArea :hPercent="heightPercentage"/>
  <div class="page" ref="mainPage">
    <PageOne class="index-page-01 pageOne" :hPercent="heightPercentage"/>
    <PageTwo class="index-page-02 pageTwo" :hPercent="heightPercentage - 100"/>
    <PageThree class="index-page-03 pageThree" :hPercent="heightPercentage - 200"/>
    <PageFour class="index-page-04 pageFour" :hPercent="heightPercentage - 300"/>
    <div class="footerArea">
      <FooterArea class="index-page-05" :hPercent="heightPercentage" ref="footerArea"/>
    </div>
  </div>
  
</template>

<script>
import HeaderArea from './components/HeaderArea.vue'
import PageOne from './components/PageOne.vue'
import PageTwo from './components/PageTwo.vue'
import PageThree from './components/PageThree.vue'
import PageFour from './components/PageFour.vue'
import FooterArea from './components/FooterArea.vue'
import { ref, onMounted, onBeforeUnmount, computed } from 'vue'

export default {
  name: 'App',
  components: {
    HeaderArea,
    PageOne,
    PageTwo,
    PageThree,
    PageFour,
    FooterArea,
  },
  data() {
    return {
      
    }
  },

  
  methods: {
  },
  setup() {
    const footerArea = ref(null)
    const mainPage = ref(null)
    const heightPercentage = ref(null)
    const LastScrollY = ref(null)
    const timer = ref(null)
    const setList = ref(
      {
        activePageIndex : 0,
        eventRoading: false,
        emptyArr: [],
      }
    )

    onMounted(() => {
      window.scrollTo(0, 0);
      //{passive : false}는 이 함수가 작동하는지에 대해 능동적 감시를 false 시킨다.
      window.addEventListener("scroll", function(e){
        e.preventDefault(); // 기본 이벤트 차단 
      },{passive : false});

      document.addEventListener('scroll', onScroll);
      
      // 각 페이지의 .top 높이 구하기
      const boxArray = mainPage.value.children;
      for(let i = 0; i < boxArray.length; i++){
        // console.log(boxArray[i].getBoundingClientRect().top);
        setList.value.emptyArr[i] = `${boxArray[i].getBoundingClientRect().top}`;
      }
      console.log(setList.value.emptyArr);
    })
    onBeforeUnmount(() => {
      document.removeEventListener('scroll', onScroll);
    })
    
    const onScroll = (() => {
      if(setList.value.eventRoading === true){
        // document.removeEventListener('wheel', onMouseWheel);
        // event.stopImmediatePropagation();
        return;
      }
      // event.stopImmediatePropagation();

      // event chceck
      // console.log(event)

      // console.log(setList.value.activePageIndex + 1)

      setList.value.eventRoading = true;
      setTimeout(() => {
        setList.value.eventRoading = false;
        // console.log("setList.value.eventRoading : "+setList.value.eventRoading)
      }, 400);
      // console.log("setList.value.eventRoading : "+setList.value.eventRoading)

      // if(timer.value !== null) {
      //   clearTimeout(timer.value);        
      // }
      // timer.value = setTimeout(function() {
        
        // vh 단위 퍼센테이지 구하기
        heightPercentage.value = window.scrollY / window.outerHeight * 100
        console.log("window.scrollTop : "  + heightPercentage.value);
        console.log("window.scrollY : "  + window.scrollY);
        console.log("Last scrollY : "+LastScrollY.value);
        // scroll direction(방향) 확인
        const scrollDirection = window.scrollY > LastScrollY.value 
        ? "Down" 
        : window.scrollY < LastScrollY.value 
        ? "Up" 
        : "Scroll Error";
        console.log("scrollDirection : "+scrollDirection);
        // 현재의 스크롤 값을 저장
        LastScrollY.value = window.scrollY;


        // if(scrollDirection === "Down"){
        //   if(setList.value.activePageIndex >= setList.value.emptyArr.length - 1){
        //     // console.log(setList.value.emptyArr.length);
        //     // console.log(setList.value.activePageIndex);
        //     // if(setList.value.activePageIndex == setList.value.emptyArr.length - 1){
        //       setList.value.activePageIndex = setList.value.emptyArr.length - 1
        //       // setList.value.activePageIndex = setList.value.emptyArr.length - 1
        //       // console.log(setList.value.emptyArr.length);
        //       // console.log(setList.value.activePageIndex);
        //     // }
        //   }else{
        //     setList.value.activePageIndex++;
        //     console.log(setList.value.activePageIndex);
        //   }
        // }else if(scrollDirection === "Up"){
        //   if(setList.value.activePageIndex <= 0){
        //     setList.value.activePageIndex = 0
        //     console.log(setList.value.activePageIndex);
        //   }else{
        //     setList.value.activePageIndex--;
        //     console.log(setList.value.activePageIndex);
        //   }
        // }else{
        //   console.log("scroll error")
        // }

      // }, 150);
    });

    const pageTopMove = computed(() => {
      if(setList.value.activePageIndex < 0){
        return "0";
      }else{
        // console.log((-100 * setList.value.activePageIndex) + "vh")
        return setList.value.activePageIndex == setList.value.emptyArr.length - 1 ? "calc(-300vh - 64px)" : (-100 * setList.value.activePageIndex) + "vh";
      }
    });

    // const secondPageTopMove = computed(() => {
    //   if(setList.value.activePageIndex >= 0){
    //     // console.log(100 + (-100 * setList.value.activePageIndex) + "vh")
    //     return 100 + (-100 * setList.value.activePageIndex) + "vh";
    //   }else{
    //     return "100vh";
    //   }
    // });

    // const thirdPageTopMove = computed(() => {
    //   if(setList.value.activePageIndex >= 0){
    //     // console.log(200 + (-100 * setList.value.activePageIndex) + "vh")
    //     return 200 + (-100 * setList.value.activePageIndex) + "vh";
    //   }else{
    //     return "200vh";
    //   }
    // });

    // const fourthPageTopMove = computed(() => {
    //   if(setList.value.activePageIndex >= 0){
    //     console.log(300 + (-100 * setList.value.activePageIndex) + "vh")
    //     if(setList.value.activePageIndex == setList.value.emptyArr.length - 1){
    //       return "calc(0vh - 64px)"
    //     }else{
    //       return 300 + (-100 * setList.value.activePageIndex) + "vh";
    //     }
    //   }else{
    //     return "300vh";
    //   }
    // });

    // const footerTopMove = computed(() => {
    //   if(setList.value.activePageIndex == setList.value.emptyArr.length - 1){
    //     return "calc(100vh - 64px)"
    //   }else{
    //     return "100vh";
    //   }
    // });

    return {
      footerArea,
      mainPage,
      timer,
      heightPercentage,
      LastScrollY,
      setList,
      pageTopMove,
      // secondPageTopMove,
      // thirdPageTopMove,
      // fourthPageTopMove,
      // footerTopMove,
    }
  },
} 
</script>

<style lang="scss">
  @import "./assets/scss/main.scss";
  body {
    height: 5000vh;
  }
  .page {
    position: fixed;
    top: 0;
    left: 50%;
    transform: translate(-50%, v-bind('pageTopMove')); //translate(-50%, (0, -100vh, -200vh, ...))
    transition: transform 0.3s ease-in;
    width: 100%;
    .index-page-01 {
      z-index: 10;
      width: 100%;
      height: 100vh;
      position: relative;
      // top: v-bind('firstPageTopMove');
      // left: 0;
      overflow: hidden;
      // transition: top 0.3s;
    }
    
    .index-page-02 { 
      z-index: 9;
      width: 100%;
      height: 100vh;
      position: relative;
      // top: v-bind('secondPageTopMove');
      // left: 0;
      overflow: hidden;
      // transition: top 0.3s;
      background-color: red;
    }
    
    .index-page-03 { 
      z-index: 8;
      width: 100%;
      height: 100vh;
      position: relative;
      // top: v-bind('thirdPageTopMove');
      // left: 0;
      overflow: hidden;
      // transition: top 0.3s;
      background-color: orange;
    }
    
    .index-page-04 { 
      z-index: 7;
      width: 100%;
      height: 100vh;
      position: relative;
      // top: v-bind('fourthPageTopMove');
      // left: 0;
      overflow: hidden;
      // transition: top 0.3s;
      background-color: yellow;
    }
  }
  
  .footerArea {
    position: relative;
    // top: calc(100% - 64px);
    transition: top 0.3s;
    // top: v-bind('footerTopMove');
    // left: 0;
    width: 100%;
    height: 64px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 100px;
    background-color: skyblue;
    z-index: 100;
  }

</style>

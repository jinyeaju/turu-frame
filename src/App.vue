<template>
  <HeaderArea />
  <div class="page" ref="mainPage">
    <PageOne class="index-page-01 pageOne"/>
    <PageTwo class="index-page-02 pageTwo"/>
    <PageThree class="index-page-03 pageThree"/>
    <PageFour class="index-page-04 pageFour"/>
    <div class="footerArea">
      <FooterArea class="index-page-05" ref="footerArea"/>
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
// import { ref, onMounted, onBeforeUnmount } from 'vue'

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
    const prevScroll = ref(null);
    const scrollDirection = ref(null);
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
      const currScroll = window.scrollY;
      console.log("currScroll : " + currScroll)
      console.log("prevScroll.value : " + prevScroll.value)
      if (prevScroll.value > currScroll) {
        scrollDirection.value = 'Up'; 
      }
      else {
        scrollDirection.value = 'Down';
      }
      prevScroll.value = currScroll;
      console.log(scrollDirection.value)

      if(setList.value.eventRoading === true){
        return;
      }

      // event chceck
      // console.log(event)
      
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

      if(scrollDirection.value === "Down"){
        if(setList.value.activePageIndex >= setList.value.emptyArr.length - 1){
          // console.log(setList.value.emptyArr.length);
          // console.log(setList.value.activePageIndex);
          // if(setList.value.activePageIndex == setList.value.emptyArr.length - 1){
            setList.value.activePageIndex = setList.value.emptyArr.length - 1
            // setList.value.activePageIndex = setList.value.emptyArr.length - 1
            // console.log(setList.value.emptyArr.length);
            // console.log(setList.value.activePageIndex);
          // }
        }else{
          setList.value.activePageIndex++;
          console.log(setList.value.activePageIndex);
        }
      }else if(scrollDirection.value === "Up"){
        if(setList.value.activePageIndex <= 0){
          setList.value.activePageIndex = 0
          console.log(setList.value.activePageIndex);
        }else{
          setList.value.activePageIndex--;
          console.log(setList.value.activePageIndex);
        }
      }else{
        console.log("scroll error")
      }
      // const sTop = setList.value.emptyArr[setList.value.activePageIndex - 1]
      // console.log("sTop : " + sTop)
      // window.scrollTo({top: sTop, behavior:"smooth" })

        // if(scrollDirection === "Down"){
        //   onScrollDown
        // }else if(scrollDirection === "Up"){
        //   onScrollUp
        // }else{
        //   console.log("scroll error")
        // }


      // }, 150);
    });

    // const onScrollDown = (() => {
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
    // });
    // const onScrollUp = (() => {
    //   if(setList.value.activePageIndex <= 0){
    //     setList.value.activePageIndex = 0
    //     console.log(setList.value.activePageIndex);
    //   }else{
    //     setList.value.activePageIndex--;
    //     console.log(setList.value.activePageIndex);
    //   }
    // });
    // window.scrollTo({top: setList.value.emptyArr[setList.value.activePageIndex - 1], behavior:"smooth" })

    const pageTopMove = computed(() => {
      if(setList.value.activePageIndex < 0){
        return "0";
      }else{
        return setList.value.activePageIndex == setList.value.emptyArr.length - 1 ? "calc(-300vh - 64px)" : (-100 * setList.value.activePageIndex) + "vh";
      }
    });


    return {
      prevScroll,
      scrollDirection,
      footerArea,
      mainPage,
      timer,
      heightPercentage,
      LastScrollY,
      setList,
      pageTopMove,
    }
  },
} 
</script>

<style lang="scss">
  @import "./assets/scss/main.scss";
  body {
    height: calc(500vh + 64px);
    height: 1000vh;
  }
  .page {
    position: fixed;
    top: 0;
    left: 50%;
    transform: translate(-50%, v-bind('pageTopMove')); //translate(-50%, (0, -100vh, -200vh, ...))
    // transform: translateX(-50%);
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

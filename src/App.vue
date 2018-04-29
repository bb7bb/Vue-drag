<template>
  <div id="app">
    <div class="container">
      <transition >
        <div class="block animated"  :style="{top:this.positionY,left:this.positionX,gridArea:'main2'}" @mousedown="move" ref="block">
          {{sum}}
        </div>
      </transition>
      <div class="score-block">{{head1score}}</div>
      <div class="score-block">{{head2score}}</div>
      <div class="score-block">{{head3score}}</div>
      <div class="score-block">{{main1score}}</div>
      <div class="score-block">{{main2score}}</div>
      <div class="score-block">{{main3score}}</div>
      <div class="score-block">{{footer1score}}</div>
      <div class="score-block">{{footer2score}}</div>
      <div class="score-block">{{footer3score}}</div>
    </div>
    <button @click="replay">RePlay</button>
  </div>
</template>

<script>
import animate from 'animate.css';

export default {
  name: 'app',
  data () {
    return {
      positionX:0,
      positionY:0,
      head1score:1,
      head2score:1,
      head3score:1,
      main1score:1,
      main2score:1,
      main3score:1,
      footer1score:1,
      footer2score:1,
      footer3score:1,
      sum:1,
      num:20,
    }
  },
  methods:{
    move(e){
      let oDiv = e.target;
      let gDiv = e.path[1];
      let disX = e.clientX - 0;
      let disY = e.clientY - 0;
      document.onmousemove = (e)=>{
        let left = e.clientX - disX;
        let top = e.clientY - disY;
        switch (oDiv.style.gridArea){
          case "head1 / head1 / head1 / head1":this.rangeOfHead1(left,top,oDiv);break;
          case "head2 / head2 / head2 / head2":this.rangeOfHead2(left,top,oDiv);break;
          case "head3 / head3 / head3 / head3":this.rangeOfHead3(left,top,oDiv);break;
          case "main1 / main1 / main1 / main1":this.rangeOfMain1(left,top,oDiv);break;
          case "main2 / main2 / main2 / main2":this.rangeOfMain2(left,top,oDiv);break;
          case "main3 / main3 / main3 / main3":this.rangeOfMain3(left,top,oDiv);break;
          case "footer1 / footer1 / footer1 / footer1":this.rangeOfFooter1(left,top,oDiv);break;
          case "footer2 / footer2 / footer2 / footer2":this.rangeOfFooter2(left,top,oDiv);break;
          case "footer3 / footer3 / footer3 / footer3":this.rangeOfFooter3(left,top,oDiv);break;
        }
        //this.rangeOfHead1(left,top,oDiv);

      };
      document.onmouseup = (e)=>{

        let hard = Math.round(Math.random()*this.num)+1;
        if(e.clientY-gDiv.offsetTop<100&&e.clientX-gDiv.offsetLeft<100){
          this.changeBlock("head1",oDiv,hard);
        }else if(e.clientY-gDiv.offsetTop>100&&e.clientX-gDiv.offsetLeft<100&&e.clientY-gDiv.offsetTop<200){
          this.changeBlock("main1",oDiv,hard);
        }else if(e.clientY-gDiv.offsetTop>200&&e.clientX-gDiv.offsetLeft<100){
          this.changeBlock("footer1",oDiv,hard);
        }else if(e.clientY-gDiv.offsetTop<100&&e.clientX-gDiv.offsetLeft>100&&e.clientX-gDiv.offsetLeft<200){
          this.changeBlock("head2",oDiv,hard);
        }else if(e.clientY-gDiv.offsetTop<100&&e.clientX-gDiv.offsetLeft>200){
          this.changeBlock("head3",oDiv,hard);
        }else if(e.clientY-gDiv.offsetTop>100&&e.clientX-gDiv.offsetLeft>200&&e.clientY-gDiv.offsetTop<200){
          this.changeBlock("main3",oDiv,hard);
        }else if(e.clientY-gDiv.offsetTop>200&&e.clientX-gDiv.offsetLeft>200){
          this.changeBlock("footer3",oDiv,hard);
        }else if(e.clientY-gDiv.offsetTop>200&&e.clientX-gDiv.offsetLeft>100&&e.clientX-gDiv.offsetLeft<200){
          this.changeBlock("footer2",oDiv,hard);
        }else {
          this.changeBlock("main2",oDiv,hard);
        }
        document.onmousemove=null;
        document.onmousedown = null;

        oDiv.className = "block animated wobble";
        let removeClass = setTimeout(()=>{
          oDiv.className = "block animated";
        },500);

      };
    },
    rangeOfHead1(x,y,oDiv){
      if(x>=200){
        x=200;
      }else if(x<=0){
        x=0;
      }
      if(y>=200){
        y=200;
      }else if(y<=0){
        y=0;
      }
      oDiv.style.left = x + 'px';
      oDiv.style.top = y + 'px';
      this.positionX = x;
      this.positionY = y;

    },
    rangeOfHead2(x,y,oDiv){
      if(x>=100){
        x=100;
      }else if(x<=-100){
        x=-100;
      }
      if(y>=200){
        y=200;
      }else if(y<=0){
        y=0;
      }
      oDiv.style.left = x + 'px';
      oDiv.style.top = y + 'px';

      this.positionX = x;
      this.positionY = y;

    },
    rangeOfHead3(x,y,oDiv){
      if(x>=0){
        x=0;
      }else if(x<=-200){
        x=-200;
      }
      if(y>=200){
        y=200;
      }else if(y<=0){
        y=0;
      }
      oDiv.style.left = x + 'px';
      oDiv.style.top = y + 'px';

      this.positionX = x;
      this.positionY = y;

    },
    rangeOfMain3(x,y,oDiv){
      if(x>=0){
        x=0;
      }else if(x<=-200){
        x=-200;
      }
      if(y>=100){
        y=100;
      }else if(y<=-100){
        y=-100;
      }
      oDiv.style.left = x + 'px';
      oDiv.style.top = y + 'px';

      this.positionX = x;
      this.positionY = y;

    },
    rangeOfFooter3(x,y,oDiv){
      if(x>=0){
        x=0;
      }else if(x<=-200){
        x=-200;
      }
      if(y>=0){
        y=0;
      }else if(y<=-200){
        y=-200;
      }
      oDiv.style.left = x + 'px';
      oDiv.style.top = y + 'px';

      this.positionX = x;
      this.positionY = y;

    },
    rangeOfFooter2(x,y,oDiv){
      if(x>=100){
        x=100;
      }else if(x<=-100){
        x=-100;
      }
      if(y>=0){
        y=0;
      }else if(y<=-200){
        y=-200;
      }
      oDiv.style.left = x + 'px';
      oDiv.style.top = y + 'px';

      this.positionX = x;
      this.positionY = y;

    },
    rangeOfFooter1(x,y,oDiv){
      if(x>=200){
        x=200;
      }else if(x<=0){
        x=0;
      }
      if(y>=0){
        y=0;
      }else if(y<=-200){
        y=-200;
      }
      oDiv.style.left = x + 'px';
      oDiv.style.top = y + 'px';

      this.positionX = x;
      this.positionY = y;

    },
    rangeOfMain1(x,y,oDiv){
      if(x>=200){
        x=200;
      }else if(x<=0){
        x=0;
      }
      if(y>=100){
        y=100;
      }else if(y<=-100){
        y=-100;
      }
      oDiv.style.left = x + 'px';
      oDiv.style.top = y + 'px';

      this.positionX = x;
      this.positionY = y;

    },
    rangeOfMain2(x,y,oDiv){
      if(x>=100){
        x=100;
      }else if(x<=-100){
        x=-100;
      }
      if(y>=100){
        y=100;
      }else if(y<=-100){
        y=-100;
      }
      oDiv.style.left = x + 'px';
      oDiv.style.top = y + 'px';

      this.positionX = x;
      this.positionY = y;

    },
    changeBlock(blockName,oDiv,hard){
      let blockRow = oDiv.style.gridRowStart.slice(0,-1);   //取得将要方块正处于的行名
      let rowNum = parseInt(oDiv.style.gridRowStart.substr(-1));   //取得将要方块正处于的行数
      let pre = "nothing";
      let next = "nothing";
      if(blockRow==="main"){
        pre='head';
        next='footer'
      }else if(blockRow==="head"){
        pre="nothing";
        next="main";
      }else{
        pre="main";
        next="nothing";
      }
      let pattern = new RegExp(blockName);
      let rowPat = new RegExp(blockRow);   //转成正则对象
      let prePat = new RegExp(pre);   //转成正则对象
      let nextPat = new RegExp(next);   //转成正则对象
      let betweenP = new RegExp(blockRow+(rowNum+1));
      let betweenN = new RegExp(blockRow+(rowNum-1));
      //if(oDiv.style.gridRowStart)
      let isAround = !(prePat.test(blockName)||nextPat.test(blockName)||betweenP.test(blockName)||betweenN.test(blockName));
      if(pattern.test(oDiv.style.gridArea)||isAround){
        this.positionX = 0;
        this.positionY = 0;
        return;
      }
      this.positionX = 0;
      this.positionY = 0;
      let scoreName = blockName+"score";

      if(this.sum>=this[scoreName]){
        oDiv.style.gridArea=blockName;
        this.sum += parseInt(this[scoreName]);
        this[scoreName]*=hard;
        this[scoreName]+= this.sum;
      }
    },
    replay(){
      window.location='/';
    }
  },
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
  .container{
    position: relative;   /*实现定位，使得滑块定位相对于此*/
    display: grid;        /*定义网格布局*/
    width: 300px;
    height: 300px;
    grid-template-columns: 100px 100px 100px;     /*实现九宫格，行列各三*/
    grid-template-rows: 100px 100px 100px;
    grid-template-areas: "head1 head2 head3"      /*定义个格子的名称，方便计算*/
                          "main1 main2 main3"
                          "footer1 footer2 footer3";
    border: 1px solid #000;
    margin: 0 auto;
  }
  .block{
    position: absolute;     /*相对于container定位*/
    width: 100px;
    height: 100px;
    display: flex;        /*flex布局，使得文字在中央*/
    justify-content: center;
    justify-items: center;
    align-items: center;
    align-content: center;
    user-select: none;      /*用户不可选定文字*/
    background: olivedrab;
    border: 1px solid #000
  }
  .score-block{
    width: 100px;
    height: 100px;
    border: 1px solid #000;
    display: flex;
    justify-content: center;
    justify-items: center;
    align-items: center;
    align-content: center;
    user-select: none;
  }
</style>

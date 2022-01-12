<template>
  <div style="position:relative;" ref="parent">

    <div style="position:absolute;top:0px;left;0px;z-index:0;"
        @mousedown="touchstart($event)"
        @mousemove="imgdrag($event)"
        @mouseleave="touchend($event)"
        @mouseup="touchend($event)"        
    >
        <img :src="imageA" ref="imgref">
        <div style="position:absolute;top:0px;left;0px;" :style="posset">
            <img class="imgtrim" :src="imageB">
        </div>
        <span :style="barheight"></span>

    </div>
   
  </div>

</template>

<script>

export default {
    name: 'App',
    props:['srcA','srcB'],
    data:function(){
        return{
            clicked:false,
            xpos:0,
            size:{width:0,height:0},
        }
    },
    mounted:function(){
        this.size.height = this.$refs.imgref.naturalHeight;
        this.size.width = this.$refs.imgref.naturalWidth;     
    },
    computed:{
        imageA:function(){
            return require("@/"+this.srcA);
        },
        imageB:function(){
            return require("@/"+this.srcB);
        },
        posset:function(){ 
            return {width:this.xpos+'px',height:this.size.height+'px'};
        },
        barheight:function(){
            return {width:'4px',height:this.size.height+'px',
            position:'absolute',
            top:'0px',
            left:this.xpos+'px',
            background: '#000000',
            'z-index':'2',
            };
        }
    },
    methods:{
        touchstart:function(e){
            this.clicked = true;
            this.xpos = e.clientX - this.$refs.parent.getBoundingClientRect().left -1;

        },
        imgdrag:function(e){
            if(this.clicked){
                this.xpos = Math.max(0,Math.min(this.size.width,e.clientX - this.$refs.parent.getBoundingClientRect().left -1));
            }
        },
        touchend:function(){
            this.clicked = false;
        },
    }
}
</script>

<style>
    img{
        pointer-events: none;
        user-select: none;
        -webkit-user-drag: none;
        -moz-user-select: none;
    }
    .imgtrim{
        width:100%;
        height:100%;
        object-fit: cover;
        object-position:0 0%;
    }
</style>

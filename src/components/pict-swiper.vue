<template>
  <div style="position:relative;" ref="parent">
    <div style="top:0px;left:0px;z-index:0;" :style="awidth"
        @mousedown="touchstart($event)"
        @mousemove="imgdrag($event)"
        @mouseleave="touchend($event)"
        @mouseup="touchend($event)"        
    >
        <img class="dragignore" :src="imageA" ref="imgref">
        <div style="position:absolute;top:0px;left;0px;" :style="posset">
            <img class="imgtrim dragignore" :src="imageB">
        </div>
        <span :style="barheight" style="text-align:left"></span>

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
        },
        awidth:function(){
            return {width:this.size.width+'px'}
        }
    },
    methods:{
        touchstart:function(e){
            this.clicked = true;
            this.xpos = Math.max(0,Math.min(this.size.width,e.clientX - this.$refs.parent.getBoundingClientRect().left -1));

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

    .dragignore{
        pointer-events: none;
        user-select: none;
        -webkit-user-drag:none;
        -khtml-user-drag:none;
        -moz-user-select: none;
    }
    .imgtrim{
        width:100%;
        height:100%;
        object-fit: cover;
        object-position:0 0%;
    }
</style>

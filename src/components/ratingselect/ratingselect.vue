<template>
  <div class="ratingselect">
    <div class="rating-type">

      <span @click="select(2,$event)" class="block positive" :class="{'active':selectType===2}">{{desc.all}}<span class="count">
        {{ratings.length}}
      </span></span>

      <span @click="select(0,$event)" class="block positive" :class="{'active':selectType===0}">{{desc.positive}}<span class="count">
        {{positives.length}}
      </span></span>

      <span @click="select(1,$event)"  class="block negative" :class="{'active':selectType===1}">{{desc.negative}}<span class="count">
        {{negatives.length}}
      </span></span>

    </div>
    <div @click="toggleContent($event)" class="switch" :class="{'on':onlyContent}">
      <span class="checkIcon ">√</span>
      <span class="text">只看有内容的评价</span>
    </div>

  </div>
</template>

<script>
  const POSITIVE = 0;
  const NEGATIVE = 1;
  const ALL = 2;

  export default {
    name: "ratingselect",
    props: {
      ratings: {
        type: Array,
        default() {
          return [];
        }
      },
      selectType:{
        type:Number,
        default:ALL,
      },
      onlyContent:{
        type:Boolean,
        default:false
      },
      desc:{
        type:Object,
        default(){
          return{
            all:'全部',
            positive:'满意',
            negative:'不满意',
          }
        }
      }
    },
    computed:{
      positives:function(){
       return this.ratings.filter((rating) => {
          return rating.rateType === POSITIVE;
        })
      },
      negatives:function(){
        return this.ratings.filter((rating) => {
          return rating.rateType === NEGATIVE;
        })
      },
    },
    methods:{
      toggleContent:function(event){
        if(!event._constructed){
          return;
        }
        this.onlyContent = !this.onlyContent;
        console.log('跳过了这个error_onlycontent')
        // this.$emit('content.toggle',this.onlyContent);
    },
      select:function(type,event){
        if(!event._constructed){
          return;
        }
        // 改变不了父组件的
        this.selectType = type;
        console.log('跳过了这个error_type');
        // this.$emit('ratingtype.select',type)
      },
    },
  }
</script>

<style lang="less" scoped>
  @import './style.less';
</style>

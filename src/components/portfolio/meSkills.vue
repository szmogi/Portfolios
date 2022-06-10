


<template>

   <div v-if="skills" class="skills-flex">    
        
         <figure :id="'icon-'+this.ide">
               <img :class="this.name" style="cursor:pointer" @mouseover="mouse(event)"  @mouseleave="mouse(event)"  :src="'src/assets/icon/'+iconName"   alt="">     
         </figure>      
      <div  ref='endAnime' class="skills-meter">
          <div :data-interval="progressInterval" :data-endwidth="progressWidth" :style="'background:'+this.progressColor+';'+this.width" :id="'progress-bar'+ide"></div>
          <strong id="count-match"  :data-counttarget="numberPercente" :data-duration="progressDuration" ></strong>                   
      </div>

   </div>
   
</template>

<script>
import {progressBarCount,resetProgressBar} from "../helpers/helpers.js"
export default {
   props: {
      iconName:{
         type:String         
      },
      numberPercente:{
         type:Number,
         default:80,
      },
      progressColor:{
         type:String,
         default:"ffff"
      },
      ide:{
         type:Number,
         default:null,
      },
      progressWidth:{
         type:String,
         default:'80%',
      },
      progressDuration:{
         type:Number,
         default:1500,
      },
      progressInterval:{
         type:Number,
         default:500,
      },
      skillsAnime:{
         type:Boolean,
         default:false,
      },
      hoverTxt:{
         type:Boolean,
         default:false,
      },
      name:{
         type:String,
         default:'nop'
      }
     
   },
   data () {  
      return {    
         endNumber:0,    
         count:0,
         width:"",
         number:0,
         endAnimated:false,
         skills:true,         

      }      
   

   },watch:{
      skillsAnime:function(val){         
         if(val === true){
            this.progressBar()           
            var interVal =  setInterval(()=>{
                if(document.getElementById('end-animated')){
                     this.endAnimated = true
                     clearInterval(interVal);                     
                }else{return}
            },500)
         }else{
           this.resetProgressBar()
            if(document.getElementById('end-animated')){
                     this.endAnimated = false
                   
              }else{return}
         }
      },
      endAnimated:function(val){
            if(val === true){
               this.$emit('next-Pages',true)
            }else{return}
      },
    
    },  
   mounted (){      
         
    }, 
     
    created(){         

    },methods:{
        resetProgressBar,
        progressBarCount,
        progressBar(){
              this.progressBarCount()
          
        }, 
         mouse(){           
          var X = event.clientX
          var Y = event.clientY
          var Xpercent = Math.round((X * 100 / window.innerWidth)  ) + '%'
          var Ypercent = Math.round((Y * 100 / window.innerHeight) ) + '%'
          var name = this.$el.children[0].firstElementChild.className;


          if(event.type === 'mouseleave'){              
                document.getElementById('appendText').remove()             
            
          }else{

          if(document.getElementById('appendText')){
             document.getElementById('appendText').remove()
          }           

          var element = document.createElement('h1')
          element.id = 'appendText'
          element.className = name
          element.style.cssText = 'opacity:0; pointer-events: none; position: fixed; cursor:pointer; z-index: 10; color: rgb(53, 52, 52); padding: 0rem 0.3rem; background: #fff; border: 1px solid lightgrey; border-radius: 5px ;  font-size: 0.8rem; font-weight: 100;'
          element.innerText = name      
          element.style.left = Xpercent;
          element.style.top = Ypercent;
           
          document.querySelector('#app').append(element) 
          element.animate([{opacity:0},{opacity:1}],{duration:300})
          setTimeout(()=>{element.style.opacity = 1},10 )

          }

      },
       
        
        
     }
    
   }
</script>

<style lang="scss" scoped>


figure{
   width: 100px;
   opacity: 0;
}


img{
  width: 60%;
}

h1{
   width:400px;
}


.skills-flex {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: horizontal;
    -webkit-box-direction: normal;
        -ms-flex-direction: row;
            flex-direction: row;
    -webkit-box-align: center;
        -ms-flex-align: center;
            align-items: center;
   
   
}

  .skills-meter{
   
    display: -webkit-box;
   
    display: -ms-flexbox;
   
    display: flex;
    width: 22rem;
    -webkit-box-orient: horizontal;
    -webkit-box-direction: normal;
        -ms-flex-direction: row;
            flex-direction: row;
    -webkit-box-pack: start;
        -ms-flex-pack: start;
            justify-content: flex-start;
    -webkit-box-align: center;
        -ms-flex-align: center;
            align-items: center;    
    padding: 0.5rem 0rem;



      
   strong{
      width:20%;    
   }

   div{
      width:0%;      
      height: .6rem;
      border-bottom-right-radius: 1pc;
      border-top-right-radius: 1pc;

   }
}




         .bounce-enter-active {
         -webkit-animation: bounce-in 0.5s;
                 animation: bounce-in 0.5s;
         }
         
 
         @-webkit-keyframes bounce-in {
         0% {
             -webkit-transform: scale(.75);
                     transform: scale(.75);
         }
         50% {
             -webkit-transform: scale(1.5);
                     transform: scale(1.5);
         }
         100% {
             -webkit-transform: scale(1);
                     transform: scale(1);
         }
      }
         
 
         @keyframes bounce-in {
         0% {
             -webkit-transform: scale(.75);
                     transform: scale(.75);
         }
         50% {
             -webkit-transform: scale(1.5);
                     transform: scale(1.5);
         }
         100% {
             -webkit-transform: scale(1);
                     transform: scale(1);
         }
      }  


   
    

</style>
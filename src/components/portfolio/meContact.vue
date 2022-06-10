<template>    
      <div v-show="contactVis" class="contact">
            <nav>        
                  <ul >
                      <transition name="contactOne">             
                          <a href="mailto:juraj.smatana@szmogi.site" @mouseenter="mouse(event)" @mouseleave="mouse(event)" v-show="contactVis"><img src="/src/assets/icon/icons8-mail-96.png" alt=""></a>   
                    </transition> 
                      <transition name="contactTwo">  
                            <a href="https://www.facebook.com/juraj.smatana.9" target="_blank" @mouseenter="mouse(event)" @mouseleave="mouse(event)" v-show="contactVis"><img src="/src/assets/icon/icons8-facebook-96.png" alt=""></a>     
                      </transition>         
                  </ul>            
            </nav>
      </div>
 
</template>

<script>
export default {
     props:{
       visContact:{
         type:Boolean,
         default:false,
       }
     },  
    data () {         
        return {
          facebook: '',
          email:'',
          contactVis:this.visContact,

        }
    },watch:{
       visContact:function (val){
         if(val === true){
           this.Open()
           this.contactVis = true
         }else{
           this.contactVis = false
         }
       }
    },
    mounted() {
      
    },
    methods: {
      mouse(){
        if(event.type === 'mouseenter'){
          event.target.animate([{right:'2.8rem'},{right:'2.2rem'}],{duration:300})
          event.target.style.right = '2.2rem'

        }else if(event.type === 'mouseleave'){
          event.target.animate([{right:'2.2rem'},{right:'2.8rem'}],{duration:300})
          event.target.style.right = '2.8rem'
        }

      },Open(){
        document.querySelector('.contact').animate([{width:'0rem'},{width:'6rem'}],{duration:1000})
      }
    }
}
</script>

<style lang="scss" scoped>

 
 .contact{    
    z-index: 3;
    position: absolute;
  }


  
  a{
    background: rgb(120,245,146);
    background: -o-linear-gradient(154deg, rgb(87 219 114) 0%, rgb(82, 171, 255) 100%);
    background: linear-gradient(296deg, rgb(87 219 114) 0%, rgb(82, 171, 255) 100%);
    padding:0rem;       
    border-top-right-radius: 1pc;
    border-bottom-right-radius: 1pc;   
    -webkit-box-orient: vertical;   
    -webkit-box-direction: normal;   
        -ms-flex-direction: column;   
            flex-direction: column;
    -webkit-box-align: center;
        -ms-flex-align: center;
            align-items: center;
    position: relative;
    cursor: pointer;
    justify-items: end;        
    display: -ms-inline-grid;        
    display: inline-grid;
    right: 2.8rem;

  }

  ul{
    padding: 4rem 0rem;
     display: -webkit-box;
     display: -ms-flexbox;
     display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
    -webkit-box-pack: justify;
        -ms-flex-pack: justify;
            justify-content: space-between;
    height: 15rem;
    width:6rem
  }


  img{
        width: 50%;
  }



        
        .contactOne-enter-active {       
          -webkit-animation: contactOne-on 1.5s ease-in;       
                  animation: contactOne-on 1.5s ease-in;
         
         }
         .contactOne-leave-active {
         animation: contactOne-off .8s reverse;
        
        
         }
 
         @-webkit-keyframes contactOne-on {
             0% {
                 -webkit-transform: translateX(-6rem);
                         transform: translateX(-6rem);                             
             }         
             20%{
               opacity:0%;      
             }
             100% {
                 -webkit-transform: translateX(0rem);
                         transform: translateX(0rem);   
                 opacity:100%;        
                
             }
          }
 
         @keyframes contactOne-on {
             0% {
                 -webkit-transform: translateX(-6rem);
                         transform: translateX(-6rem);                             
             }         
             20%{
               opacity:0%;      
             }
             100% {
                 -webkit-transform: translateX(0rem);
                         transform: translateX(0rem);   
                 opacity:100%;        
                
             }
          }
         
 
         @-webkit-keyframes contactOne-off {
             from {
                 -webkit-transform: translateX(-6rem);
                         transform: translateX(-6rem)   
             }
             to {
                  -webkit-transform: translateX(0rem);
                          transform: translateX(0rem)    
             }

         }
         
 
         @keyframes contactOne-off {
             from {
                 -webkit-transform: translateX(-6rem);
                         transform: translateX(-6rem)   
             }
             to {
                  -webkit-transform: translateX(0rem);
                          transform: translateX(0rem)    
             }

         }


          
        .contactTwo-enter-active {       
          -webkit-animation: contactTwo-on 2s ease-in;       
                  animation: contactTwo-on 2s ease-in;
         
         }
         .contactTwo-leave-active {
         animation: contactTwo-off .8s reverse;
        
        
         }
 
         @-webkit-keyframes contactTwo-on {
             0% {
                 -webkit-transform: translateX(-6rem);
                         transform: translateX(-6rem);       
                     
             }                 
             20%{
               opacity:0%;      
             } 
             100% {
                 -webkit-transform: translateX(0rem);
                         transform: translateX(0rem);     
                  opacity:100%;    
                
             }
          }
 
         @keyframes contactTwo-on {
             0% {
                 -webkit-transform: translateX(-6rem);
                         transform: translateX(-6rem);       
                     
             }                 
             20%{
               opacity:0%;      
             } 
             100% {
                 -webkit-transform: translateX(0rem);
                         transform: translateX(0rem);     
                  opacity:100%;    
                
             }
          }
         
 
         @-webkit-keyframes contactTwo-off {
             from {
                 -webkit-transform: translateX(-6rem);
                         transform: translateX(-6rem)   
             }
             to {
                  -webkit-transform: translateX(0rem);
                          transform: translateX(0rem)    
             }

         }
         
 
         @keyframes contactTwo-off {
             from {
                 -webkit-transform: translateX(-6rem);
                         transform: translateX(-6rem)   
             }
             to {
                  -webkit-transform: translateX(0rem);
                          transform: translateX(0rem)    
             }

         }


    
       #medium-size{
           .contact{
             position: fixed;
             top:-2rem;
           }
       }    
     
 
     
   
    
     
   
   

</style>
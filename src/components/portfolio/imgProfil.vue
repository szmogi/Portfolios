<template>
     <div class="profil-img-title">         
        <transition name="images">
            <figure v-show="imageVis" class="image-profil">
               <div>
                    <img src="/src/assets/img/JurajProfil.png" alt="">
               </div>                
            </figure>      
         </transition>
               <nav>                                   
                    <ul>                   
                        <transition name="title">  
                             <li class="title-profil" v-show="titleVis"><h3>{{title}}</h3></li>
                         </transition>   
                         <transition name="name">  
                             <li  class="name-profil"  v-show="titleVis"><h4>{{name}}</h4></li>
                         </transition>   
                             
                                            
                    </ul>                    
             </nav>     
        
    </div>
</template>

<script>



export default {
       props:{
          animated:{
              type:Boolean,
              default:false,
          },
          visible:{
              type:Boolean,
              default:false,
          }
         
       },
      
    data (){
    
        return {
          imageVis:false,  
          titleVis:false,          
          titleAnime:'',
          title:'',
          name:'',
          isAnimated:this.animated,
        }
    },
    watch:{
        animated: function(val){
               if(val === true){                  
                    this.titleOn()          
                          
               }else{
                   this.titleOff()
                         
              }
         }
      },
    mounted(){     
        
        if(this.visible === true){
            this.titleOn()
        }
        
    },
    methods:{
        titleOn(){       
            this.imageVis = true
            this.titleVis = true
              setTimeout(()=>{
                   this.title ='Portfólio',
                   this.name = 'Juraj Smatana'
                   document.querySelector('.title-profil > h3').animate([{opacity:'0%'},{opacity:'100%'}],{duration:500})
                   document.querySelector('.name-profil > h4').animate([{opacity:'0%'},{opacity:'100%'}],{duration:500})
                   document.querySelector('.title-profil > h3').style.opacity = '100%'
                   document.querySelector('.name-profil > h4').style.opacity = '100%'
              },800)
            
          
        },
        titleOff(){
               this.imageVis = false
               this.titleVis = false
               this.title ='',
               this.name = ''
               document.querySelector('.title-profil > h3').style.opacity = '0%'
               document.querySelector('.name-profil > h4').style.opacity = '0%'

        }
    }
}

</script>

<style lang="scss" scoped>

 figure{
       width:100%;
       height:260px; 
       overflow: hidden;     
       
     
       

   }

   img{
       width:80%;
      
      
      
      
   }


    nav{
        height:120px;       
        

    }

   ul{
       margin-top: 0.2rem;
       padding: 0;


       li{
          
           list-style: none;          

         
       }

   }

   .title-profil{
       font-size:2rem;
       font-family: oswald;
       font-weight:600;
       letter-spacing: .5px;
       width: 90%;
       margin-bottom: 0.3rem;
       
      
      
       border-bottom-right-radius: 3pc;
       border-top-right-radius: 3pc;
       background: rgb(120,245,146);
       background: -o-linear-gradient(315deg, rgba(120,245,146) 0%, rgba(82,171,255) 100%);
       background: linear-gradient(135deg, rgba(120,245,146) 0%, rgba(82,171,255) 100%);



         h3{
             height:4rem
         }
       
   }


   
   .name-profil{
       font-size:1.5rem;
       font-family: oswald;
       font-weight:600;
       letter-spacing: .5px;
       width:80%;
       
      
       border-bottom-right-radius: 3pc;
       border-top-right-radius: 3pc;
       background: rgb(120,245,146);
       background: -o-linear-gradient(315deg, rgba(120,245,146) 0%, rgba(82,171,255) 100%);
       background: linear-gradient(135deg, rgba(120,245,146) 0%, rgba(82,171,255) 100%);


          h4{
             height:2.8rem
           }       
   }

   .image-profil{
       position: relative;
      
   }


        .title-enter-active {
         -webkit-animation: title-on 2s;
                 animation: title-on 2s;
        
         }
         .title-leave-active {
         animation: title-off 1s reverse;
        
         }
 
         @-webkit-keyframes title-on {
             0% {
                 width:0%;              
             }         
             100% {
                 width:90%;              
             }         
                
             
      }
 
         @keyframes title-on {
             0% {
                 width:0%;              
             }         
             100% {
                 width:90%;              
             }         
                
             
      }
         
 
         @-webkit-keyframes title-off {
             from {
                 width:90%;
             }
             to {
                 width:0%;
             }

         }
         
 
         @keyframes title-off {
             from {
                 width:90%;
             }
             to {
                 width:0%;
             }

         }


         
        .name-enter-active {
         -webkit-animation: name-on 2.5s;
                 animation: name-on 2.5s;
        
         }
         .name-leave-active {
         animation: name-off .8s reverse;
        
         }
 
         @-webkit-keyframes name-on {
             0% {
                 width:0%;                
             }         
             100% {
                 width:80%;
                
             }
      }
 
         @keyframes name-on {
             0% {
                 width:0%;                
             }         
             100% {
                 width:80%;
                
             }
      }
         
 
         @-webkit-keyframes name-off {
             from {
                 width:80%;
             }
             to {
                 width:0%;
             }

         }
         
 
         @keyframes name-off {
             from {
                 width:80%;
             }
             to {
                 width:0%;
             }

         }


        .images-enter-active {
            -webkit-animation: images-on 2s ease-in-out;
                    animation: images-on 2s ease-in-out;
            position: relative;
         
          
        
         }
         .images-leave-active {
            -webkit-animation: images-off 1s ease-in-out;
                    animation: images-off 1s ease-in-out;
            position: relative;
        
         }
 
         @-webkit-keyframes images-on {
             0% {
                -webkit-transform: translateX(-50rem);
                        transform: translateX(-50rem);                                 
             }    
             40%{                
                -webkit-transform: translateX(1rem);                
                        transform: translateX(1rem);               
             }              
             50%{                
                -webkit-transform: translateX(-.8rem);                
                        transform: translateX(-.8rem);               
             }     
             60%{
                -webkit-transform: translateX(.6rem);
                        transform: translateX(.6rem); 
             }        
             70%{
                -webkit-transform: translateX(-.4rem);
                        transform: translateX(-.4rem); 
             }                  
                   
             90%{
                -webkit-transform: translateX(.2rem);
                        transform: translateX(.2rem); 
             }             
                   
             100% {
                  -webkit-transform: translateX(0rem);
                          transform: translateX(0rem);                      
             }         
                
             
      }
 
         @keyframes images-on {
             0% {
                -webkit-transform: translateX(-50rem);
                        transform: translateX(-50rem);                                 
             }    
             40%{                
                -webkit-transform: translateX(1rem);                
                        transform: translateX(1rem);               
             }              
             50%{                
                -webkit-transform: translateX(-.8rem);                
                        transform: translateX(-.8rem);               
             }     
             60%{
                -webkit-transform: translateX(.6rem);
                        transform: translateX(.6rem); 
             }        
             70%{
                -webkit-transform: translateX(-.4rem);
                        transform: translateX(-.4rem); 
             }                  
                   
             90%{
                -webkit-transform: translateX(.2rem);
                        transform: translateX(.2rem); 
             }             
                   
             100% {
                  -webkit-transform: translateX(0rem);
                          transform: translateX(0rem);                      
             }         
                
             
      }
         
 
         @-webkit-keyframes images-off {
             from {
                 -webkit-transform: translateX(0rem);
                         transform: translateX(0rem);                  
             }
             to {
                -webkit-transform: translateX(50rem);
                        transform: translateX(50rem); 
                
             }

         }
         
 
         @keyframes images-off {
             from {
                 -webkit-transform: translateX(0rem);
                         transform: translateX(0rem);                  
             }
             to {
                -webkit-transform: translateX(50rem);
                        transform: translateX(50rem); 
                
             }

         }
                
           .main-fade-enter-active {
               -webkit-transition: all 1s ease-out;
               -o-transition: all 1s ease-out;
               transition: all 1s ease-out;
               
            }

            .main-fade-leave-active {
               -webkit-transition: all 0.5s cubic-bezier(1, 0.5, 0.8, 1);
               -o-transition: all 0.5s cubic-bezier(1, 0.5, 0.8, 1);
               transition: all 0.5s cubic-bezier(1, 0.5, 0.8, 1);
            }

            .main-fade-enter-from,
            .main-fade-leave-to {

            -webkit-transform: translateX(100rem);

                -ms-transform: translateX(100rem);

                    transform: translateX(100rem);
            opacity: 0%;
            z-index:-1;


           }   





    #medium-size{
       .image-profil{
           height: auto;

       }

    }



     


</style>
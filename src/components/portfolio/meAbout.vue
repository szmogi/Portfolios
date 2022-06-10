<template>
            
        <div class="about-title-group">
            <transition name="title">   
                    <section class="title-about" v-if="this.titleVis">
                        <h3>{{this.title}}</h3>               
                    </section>
            </transition>                   
                        <section v-if="pdfLink" class="pdf-link">
                                <ul>
                                    <button @click="this.review = !this.review">Pracovné posudky</button>        
                                    <li class="review" v-show="review">
                                        <a @click.prevent="pdfOpen()"  href="#">posudok 1</a>
                                        <a @click.prevent="pdfOpen()"  href="#">posudok 2</a></li> 
                                                    
                            </ul>    
                            <button @click="biografi()">Životopis</button>
                        </section>             
          </div>    
      
        <div class="text-about" v-if="this.textVis">
      
      
        <transition name="text">
           <section v-if="visText == 'one'">
                <p>Môj záujem o IT svet začal už v 12 rokoch. 
                    Prvý projekt, ktorý som robil bola tvorba CD na autoplay, ktoré malo menu v html. Bol tam zoznam programov a hier na stiahnutie, v podstate ako CD v PC časopisoch.
                    Môj život sa vybral však iným smerom. Išiel som študovať elektromechaniku. No nakoniec som v pracovnom živote robil opatrovateľa. Avšak po siedmych rokoch opatrovania som mal vnútornú potrebu zmeniť povolanie.
                    Záujem z detstva o IT svet dostal opäť zelenú. V tejto túžbe profesijnej zmeny mám podporu mojej manželky, s ktorou máme teraz 16 mesačného synčeka. 
                    A od 11/2021 má IT svet programovania u mňa opäť svoje miesto. 
                </p>               
           </section> 
           <section v-else-if="visText == 'two'">
                    <p>
                        Najprv bola moja otázka <q>Ako začať v tomto učení?</q>
                        Rozhodol som pre vzdelávanie z Learn2Code.
                    </p>
                    <ul>
                        <h4>Najprv som začal kurzami: </h4>
                        <li>Webrebel 1 html/css/scss/jq</li>
                        <li>Webrebel 2 php/OOP</li>
                        <br>
                        <h4>A ďalej som sa rozhodol pre programovacie jazyky:</h4>
                        <li>Laravel/Vue/JS. </li>
                    </ul>
                    <p>Takže posledných 7 mesiacov 7 dní v týždni po 8-10 hodín denne sa učím,
                      pretože túžim po zmene profesie a zabezpečení rodiny.
                    </p>
           </section>
           <section v-else-if="visText == 'thee'" >                 
                 <p>
                     V rámci môjho projektu som sa veľa naučil a rád sa ďalej budem v IT sfére učiť nové. Je to profesia, ktorá zahŕňa celoživotné vzdelávanie a to je výborné. 
                     Na projekte čo som tvoril som veľmi rád hľadal riešenia. Skúšal a hľadal som dovtedy, kým to nebolo funkčné.
                     Myslím, že to je základný pilier pre dobré programovanie.
                     Verím, že mi dáte profesijnú možnosť byť u vás programátorom. 
                     Verím v zmenu z opatrovateľa programátor.

                 </p>
           </section>
         </transition>


        </div>
     
      
           <figure  class="next-text">
              <img v-if="nextIcon" v-bind:class="{nextIcon:isNextAnimated , nextvis:isNextStart }" @click="nextText()" @mouseenter="mouseOn()" @mouseleave="mouseOn()" src="/src/assets/icon/icons8-right-32.png" alt="right">
          </figure>      
      
       

   
</template>

<script>
export default {
        props:{
            aboutVis:{
               type:Boolean,
               default:false,
            }
        },
    data () {      

        return {
            title:'O mne',
            titleVis:false,
            textVis:false,
            nextIcon:false,
            visText:'',
            isNextAnimated:false,
            isNextStart:false,
            stopInterval:false,
            visAbout:true,
            review:false,
            pdfLink:false,

           
        }

    },watch:{
        aboutVis:function(val){            
             if(val === true){
                 this.aboutMeVis()
              
             }
        }
    },
    mounted () {
   
             
     
  
       

    },methods: {
          aboutMeVis(){
               this.titleVis = true               
               this.autoText()     
               this.textVis = true
               this.pdfLink = true    
             
               
                setTimeout(()=>{
                    this.title = 'O mne' 
                    this.visText = 'one'         
                    this.nextIcon = true      
                    this.isNextStart = true    
                   document.querySelector('.pdf-link').animate([
                     {opacity:0},{opacity:1}
                   ],{duration:1000})   
                   
                   document.querySelector('.pdf-link').style.opacity = 1   
                   document.querySelector('.title-about > h3').animate([
                       {opacity:0},{opacity:1}
                   ],{duration:500})
                   document.querySelector('.title-about > h3').style.opacity = 1;
               },1000)
          },
          autoText(data){       
              var interval = setInterval(()=>{              
                  if(this.stopInterval === false){
                        if(this.visText === 'one'){
                            this.visText = 'two'
                        }else if(this.visText === 'two'){
                            this.visText = 'thee'
                        }else if(this.visText === 'thee'){
                            this.visText = ''
                            setTimeout(()=>{this.visText = 'one'},200) 
                        }
                      }else{ 
                          clearInterval(interval)
                         return
                     }      },5000)
          },
          nextText(){
               this.stopInterval = true
               if(this.visText === 'one'){
                     this.visText = 'two'
                }else if(this.visText === 'two'){
                    this.visText = 'thee'
                }else if(this.visText === 'thee'){
                    this.visText = 'one'
                }

          },mouseOn(){
              if(event.type == 'mouseenter'){
                  this.isNextAnimated = true
                  this.isNextStart = false
              }else if (event.type == 'mouseleave'){
                  this.isNextAnimated = false
              }
              
          },
          biografi(){
              var pdf = '/src/assets/pdf/Juraj_Smatana_sk_CV.pdf' 
               window.open(pdf)

          },
          pdfOpen(){
              var pdf = '/src/assets/pdf/img20220505_16013368.pdf'
              if(event.target.innerText === 'posudok 2'){
                  pdf =  '/src/assets/pdf/img20220505_16022917.pdf'
              }

              window.open(pdf)
          }

    }

}
</script>

<style lang="scss" scoped>



   .title-about{
       font-size:2rem;
       font-family: oswald;
       font-weight:600;
       letter-spacing: .5px;
       width: 50%;
       margin-bottom: 0.3rem;       
      
      
       border-bottom-right-radius: 3pc;
       border-top-right-radius: 3pc;
       background: rgb(120,245,146);
       background: -o-linear-gradient(315deg, rgba(120,245,146) 0%, rgba(82,171,255) 100%);
       background: linear-gradient(135deg, rgba(120,245,146) 0%, rgba(82,171,255) 100%);

         h3{
             height:4rem;
             opacity:0;
         }
       
   }



   .text-about{
       
        font-size: 1rem;
       
        height: 15rem;
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        -webkit-box-orient: vertical;
        -webkit-box-direction: normal;
            -ms-flex-direction: column;
                flex-direction: column;
        -ms-flex-pack: distribute;
            justify-content: space-around;
        -ms-flex-wrap: wrap;
            flex-wrap: wrap;

     
       p{
           padding:.5rem 2rem 0rem;           
       
       }

       ul{
           padding: 0;

       }

       li{
           list-style: none;
       }

       h4{
           font-weight:600;
       }

   }

   .about-title-group{
       width:600px;       
       display: -webkit-box;       
       display: -ms-flexbox;       
       display: flex;
       -ms-flex-pack: distribute;
           justify-content: space-around;
       margin-bottom: 0.5rem;


   }


   
   .review{
         display: -ms-grid;
         display: grid;
         position: absolute;
         left: 2rem;
        
   }


   .pdf-link{
       display: -webkit-box;
       display: -ms-flexbox;
       display: flex;
       width: 200px;
       -ms-flex-pack: distribute;
           justify-content: space-around;
       opacity:0;
    
       
       ul{
           padding: 0;
           line-height: 1.3;
          
       }

     

       li{
           list-style: none;
           cursor: pointer;
       }

       a{
           text-decoration: none;
           color: #0066a7;
           padding: 0.1rem;

           &:hover,
           &:active{
               color: #03598f;
               border-bottom: 1px solid #03598f;
           }
       }

       button{
         cursor: pointer;  
         background: rgb(120,245,146);
         background: -o-linear-gradient(315deg, rgb(120 245 146 / 39%) 0%, rgb(82 171 255 / 36%) 100%);
         background: linear-gradient(135deg, rgb(120 245 146 / 39%) 0%, rgb(82 171 255 / 36%) 100%);
         height: 1.5rem;
         border:none;
         border-radius:.5pc;

         &:hover,
         &:active{
           background: rgb(120,245,146);
           background: -o-linear-gradient(315deg, rgba(120, 245, 145, 0.616) 0%, rgba(82, 171, 255, 0.61) 100%);
           background: linear-gradient(135deg, rgba(120, 245, 145, 0.616) 0%, rgba(82, 171, 255, 0.61) 100%);    
         }

       }
   }


   .next-text{
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        -webkit-box-pack: end;
            -ms-flex-pack: end;
                justify-content: flex-end;    
        width: 100%;
      
       img{
           margin-right: 2rem;
           cursor: pointer;
       }
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
                 width:50%;              
             }         
                
             
         }
 
         @keyframes title-on {
             0% {
                 width:0%;              
             }         
             100% {
                 width:50%;              
             }         
                
             
         }
         
 
         @-webkit-keyframes title-off {
             from {
                 width:50%;
             }
             to {
                 width:0%;
             }

         }
         
 
         @keyframes title-off {
             from {
                 width:50%;
             }
             to {
                 width:0%;
             }

         }



            
        .text-enter-active {
          -webkit-animation: text-on 1s;
                  animation: text-on 1s;
            
         }
         .text-leave-active {
         -webkit-animation: text-off .5s ;
                 animation: text-off .5s ;
        
         }
 
         @-webkit-keyframes text-on {
             0% {
                -webkit-transform:translateX(100rem);
                        transform:translateX(100rem);                 
                opacity:0; 
             }         
             100% {
                 -webkit-transform:translateX(0rem);
                         transform:translateX(0rem);         
                 opacity:1;            
             }         
                
             
      }
 
         @keyframes text-on {
             0% {
                -webkit-transform:translateX(100rem);
                        transform:translateX(100rem);                 
                opacity:0; 
             }         
             100% {
                 -webkit-transform:translateX(0rem);
                         transform:translateX(0rem);         
                 opacity:1;            
             }         
                
             
      }
         
 
      @-webkit-keyframes text-off {
             from {
                 -webkit-transform:translateX(0rem);
                         transform:translateX(0rem) 
             }
             to {
                -webkit-transform:translateX(100rem);
                        transform:translateX(100rem)   
             }

         }
         
 
      @keyframes text-off {
             from {
                 -webkit-transform:translateX(0rem);
                         transform:translateX(0rem) 
             }
             to {
                -webkit-transform:translateX(100rem);
                        transform:translateX(100rem)   
             }

         }

                  
        .nextIcon {
            -webkit-animation: nextIcon-on .5s infinite;
                    animation: nextIcon-on .5s infinite;
            
            }
     
 
         @-webkit-keyframes nextIcon-on {
             0% {
                -webkit-transform:translateX(0rem);
                        transform:translateX(0rem);                 
                 
             }   
             25% {
                 -webkit-transform:translateX(.5rem);
                         transform:translateX(.5rem);         
                           
             }            
             50% {
                 -webkit-transform:translateX(0rem);
                         transform:translateX(0rem);         
                           
             }          
             75% {
                 -webkit-transform:translateX(.5rem);
                         transform:translateX(.5rem);         
                           
             } 
             75% {
                 -webkit-transform:translateX(0rem);
                         transform:translateX(0rem);         
                           
             }             
                
             
      }
     
 
         @keyframes nextIcon-on {
             0% {
                -webkit-transform:translateX(0rem);
                        transform:translateX(0rem);                 
                 
             }   
             25% {
                 -webkit-transform:translateX(.5rem);
                         transform:translateX(.5rem);         
                           
             }            
             50% {
                 -webkit-transform:translateX(0rem);
                         transform:translateX(0rem);         
                           
             }          
             75% {
                 -webkit-transform:translateX(.5rem);
                         transform:translateX(.5rem);         
                           
             } 
             75% {
                 -webkit-transform:translateX(0rem);
                         transform:translateX(0rem);         
                           
             }             
                
             
      }


         .nextvis {
            -webkit-animation: nextvis-on 2s ;
                    animation: nextvis-on 2s ;
            
            }
     
 
         @-webkit-keyframes nextvis-on {
             0% {
                -webkit-transform:scale(0);
                        transform:scale(0);                 
                 
             }   
             25% {
                 -webkit-transform:scale(1.50);
                         transform:scale(1.50);                                    
             }                           
             50% {
                   -webkit-transform:scale(1);
                           transform:scale(1);         
                           
             }          
             75% {
                 -webkit-transform:scale(1.50);
                         transform:scale(1.50);         
                           
             } 
            100% {
                 -webkit-transform:scale(1);
                         transform:scale(1);                                  
                           
             }             
                
             
      }
     
 
         @keyframes nextvis-on {
             0% {
                -webkit-transform:scale(0);
                        transform:scale(0);                 
                 
             }   
             25% {
                 -webkit-transform:scale(1.50);
                         transform:scale(1.50);                                    
             }                           
             50% {
                   -webkit-transform:scale(1);
                           transform:scale(1);         
                           
             }          
             75% {
                 -webkit-transform:scale(1.50);
                         transform:scale(1.50);         
                           
             } 
            100% {
                 -webkit-transform:scale(1);
                         transform:scale(1);                                  
                           
             }             
                
             
      }



     #medium-size{
         .about-title-group{
                 width: auto;
                 display: -webkit-box;
                 display: -ms-flexbox;
                 display: flex;
                 -webkit-box-pack: justify;
                     -ms-flex-pack: justify;
                         justify-content: space-between;
                 -webkit-box-orient: horizontal;
                 -webkit-box-direction: normal;
                     -ms-flex-direction: row;
                         flex-direction: row;
         }

         .pdf-link{
             width: 250px;
             -webkit-box-pack: space-evenly;
                 -ms-flex-pack: space-evenly;
                     justify-content: space-evenly;
         }


         .text-about{
             height: 20rem;
         }



        
   }



    @media (max-width:500px){
        #medium-size{

            .text-about{
                height: 30rem;

                P{
                  padding: 0.5rem 1rem 0rem;
                }
            }

            .pdf-link{
             width: 210px;
             -webkit-box-pack: space-evenly;
                 -ms-flex-pack: space-evenly;
                     justify-content: space-evenly;
            }


            .title-about{
                font-size: 1.5rem;

              h3{
                  height: 3rem;
              }

            }
        }
    }

      
 
    


          

</style>
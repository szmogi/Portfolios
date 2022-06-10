<template>
    <div class="project-group">
        <figure v-show="this.backIconVis" :style="'text-align: initial; cursor:pointer;'">
            <img :style="'height: 2rem; margin-left:1rem;'" v-show="backIcon" v-bind:class="{backicon:isNextStart }" @click="backPages()" src="/src/assets/icon/icons8-back-32.png" alt="back">
        </figure>
        <div class="title-project">
                    
                    <section class="title">   
                        <transition name="title">         
                              <h1 v-show="titleGroup.titleVis"><strong>{{titleGroup.title}}</strong></h1>
                        </transition>   
                        <transition name="link"> 
                              <h2 v-show="titleGroup.linkVis"><a target="_blank" :href="'http://'+titleGroup.pagesName.replace('_','')"  >{{titleGroup.pagesName}}</a></h2>         
                        </transition>                            
                    </section>
           
            <section class="story">
              <transition name="story-fade">     
                        <h3 v-show="storyVis">
                          Môj prvý projekt je určený pre používateľa, ktorý si plne spravuje stránku sám, cez Admin podstránku. 
                          Možnosti Admin podstránky sú: pridávanie, editovanie a zmazávanie postov, článkov a príbehov.
                          V projekte som spojil všetky moje doterajšie back-end a front- end vedomosti. Pri realizácii projektu sa vyskytli rôzne reálne prekážky, pre ktoré som nevyhnutne musel hľadať riešenia. Niektoré som riešil dlhšie, niektoré kratšie. Pri riešeniach mi boli nápomocné vedomosti, ktoré som si vyhľadával na internete. Veľa som sa cez tvorbu tohoto projektu naučil. 
                          Získané vedomosti rád využijem vo Vašich projektoch.

                        </h3>  
             </transition>  
            </section>               
        </div>    
        
        <transition name="slide-portfolio">
                <div v-show="descripProject" class="project-container">
                <transition-group name="slide-content">  
                        <div v-for="item in projektContainer" :key="item.id" v-show="this.projectSlide === item.visName"    class="content-group">    
                                                      
                                 <figure class="img-project">
                                      <img @click="imageSize(event)" v-for="img in item.img" :key="img.id" :alt="img" :src="'/src/assets/img/'+img">                                      
                                        
                                </figure>
                          
                                

                            <section class="content">
                                <figure  class="icon-project">
                                        <img v-for="icon in item.icon" :key="icon.id" :alt="icon.replace('.png','')" :src="'/src/assets/icon/'+icon">
                                                
                                </figure>
                                    <h1>{{item.title}}</h1>
                                    <p>
                                        {{item.text}}
                                    </p>
                            </section>                            

                        </div>

                    </transition-group>    
                </div>  
        </transition>  

         <figure  class="next-slide">
              <img v-show="nextIcon" v-bind:class="{nextIcon:isNextAnimated , nextvis:isNextStart }" @click="nextText()" @mouseenter="mouseOn()" @mouseleave="mouseOn()" src="/src/assets/icon/icons8-right-32.png" alt="right">              
           
      </figure>             
    </div>
    
</template>

<script>

var id = 0;
export default {
    props:{
        projectAnimated:{
            type: Boolean,
            default:false,
        },
        backIconVis:{
            type:Boolean,
            default:true,
        }
    },

    data () {
        

        return {            
            titleGroup:{
                title:'',
                pagesName:'',
                titleVis:false,
                linkVis:false ,},
            
            storyVis:false,   
            descripProject:false,   
            containerVis:'',
            nextIcon:false, 
            animated:this.projectAnimated,
            isNextAnimated:false,
            isNextStart:false, 

            backIcon:false,                    

            projectSlide:'back',

            
            projektContainer:[
               {id:id++ , visName:'back' , 
               img:['front-end/front-end-1.png'], 
               icon:['icons8-mysql-logo-96.png','icons8-laravel-100.png','icons8-php-logo-96.png','icons8-git-96.png'],
               title:"Back-end",
               text:'Back-end som spravoval s Laravel (framework), ktorý je postavený na programovacom jazyku PHP. Databázu som použil MariaDB a zálohy som robil s Git-om.Databázové tabuľky som vytváral migráciou. Data som sťahoval v Controller-i cez Model. Používal som Storage na ukladanie dát a Mail na posielanie mailov.'},
               {id:id++ , visName:'front' , 
               img:['front-end/front-end-2.png'], 
               icon:['icons8-vuejs-96.png','icons8-css3-120.png','icons8-sass-avatar-96.png','icons8-javascript-logo-96.png'],
               title:"Front-end",
               text:"Projekt som vyvíjal na začiatku 50% JScript a 50% Vue.js. Po krátkom čase som videl, že pre funkčnosť projektu je efektívnejšie riešenie využiť na 90% Vue.js a 10% JScript.Pre komunikáciu medzi rodičom a dieťaťom to bolo najlepšie rozhodnutie. Takto som mohol využiť Props, &emit, Watch tak, aby každý element vedel medzi sebou komunikovať a posielať údaje."},
               {id:id++ , visName:'admin' , 
               img:['admin/admin-img-1.png'], 
               icon:['icons8-admin-96.png'],
               title:"Admin",
               text:"Slúži na pridávanie, editáciu a zmazanie postov, článkov a príbehov. Takto si môže administrátor spravovať 80% dát na stránke.Pre lepšiu funkčnosť stránky som použil axios, cez ktorý sa údaje posielajú a sťahujú."},
            ]
            
            
        }   
        
    },watch:{
       projectAnimated : function (val) {
                if(val == true){
                   setTimeout(()=>{
                      this.projectVisAnimate()
                   },1000) 
                    
                }
        }      
    },
    mounted() {
        if(this.animated === true){
         this.projectVisAnimate() 
        }


    },
    methods:{
        projectVisAnimate(){
             this.titleGroup.titleVis = true  
             this.titleGroup.linkVis = true     
             this.storyVis = true    
             this.descripProject = true             
             this.containerVis = 'back' 
             this.titleGroup.title = '',
             this.titleGroup.pagesName = ''  
             setTimeout(()=>{
                this.titleGroup.title = 'Projekt',
                this.titleGroup.pagesName = 'Logopedka_jednoducho.sk'  
                document.querySelector('.title > h1 > strong').animate([{opacity:0},{opacity:1}],{duration:500})     
                document.querySelector('.title > h1 > strong').style.opacity = '100%'
                document.querySelector('.title > h2 > a').animate([{opacity:0},{opacity:1}],{duration:500})     
                document.querySelector('.title > h2 > a').style.opacity = '100%'          
                
                    setTimeout(()=>{
                        this.nextIcon = true,
                        this.isNextStart = true
                        this.backIcon = true
                    },1500)

             },1000)
         },
          nextText(){        
                 if(this.projectSlide === 'back'){
                   this.projectSlide = ''
                   setTimeout(()=>{this.projectSlide = 'front'},200)    
                 }else if (this.projectSlide ==='front'){                   
                      this.projectSlide = ''         
                  setTimeout(()=>{this.projectSlide = 'admin'},200)               
                             
                 }else if(this.projectSlide === 'admin'){        
                     this.projectSlide = ''         
                    setTimeout(()=>{this.projectSlide = 'back'},200)               
                 }            

          },mouseOn(){
              if(event.type == 'mouseenter'){
                  this.isNextAnimated = true
                  this.isNextStart = false
              }else if (event.type == 'mouseleave'){
                  this.isNextAnimated = false
              }
              
          },
          backPages(){
              this.$emit('back-page', true)
         },
         imageSize(){
             if(document.getElementById('full-size-img') === null ){
                 var idName = event.target.alt
                 var elemetDiv = document.createElement('div')
                 var elementButton = document.createElement('button')
                 var elementImg = document.createElement('img')
                    elementButton.setAttribute('class', 'size-button' )
                    elementButton.innerHTML = 'X'           
                    elementImg.src = '/src/assets/img/'+idName
                    elementImg.alt = idName.substr(idName.indexOf('/')+1)
                    elemetDiv.setAttribute('id','full-size-img')          
                    
                    document.querySelector('body').prepend(elemetDiv)            
                    elemetDiv.append(elementImg)
                    elemetDiv.prepend(elementButton)

                    elemetDiv.animate([{left:'-100rem'},{left:'0rem'}],{duration:500})

                elementButton.addEventListener('click', function(){
                  elemetDiv.animate([{left:'0rem'},{left:'-200rem'}],{duration:500})  
                  setTimeout(()=>{elemetDiv.remove()},400)
                });
                
            }else{
                return        }
                
         }
         

    },
    


}

</script>

<style lang="scss" scoped>


 
    .project-group{
        width:1000px;
        height:800px;         
        display: -webkit-box;         
        display: -ms-flexbox;         
        display: flex;
        -webkit-box-orient: vertical;
        -webkit-box-direction: normal;
            -ms-flex-direction: column;
                flex-direction: column;
        -webkit-box-pack: center;
            -ms-flex-pack: center;
                justify-content: center;

    }


   .title{
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        -webkit-box-orient: horizontal;
        -webkit-box-direction: normal;
            -ms-flex-direction: row;
                flex-direction: row;
        -webkit-box-pack: justify;
            -ms-flex-pack: justify;
                justify-content: space-between;
        -webkit-box-align: center;
            -ms-flex-align: center;
                align-items: center;
        height: 4rem;
        
       
       h1 , h2{
          background: rgb(120,245,146);
          background: -o-linear-gradient(16deg, rgba(120,245,146) 0%, rgba(82,171,255) 100%);
          background: linear-gradient(74deg, rgba(120,245,146) 0%, rgba(82,171,255) 100%);
          padding: 0.3rem;
          width:40%;

       }
         

        h1{            
            border-top-right-radius: 3pc;
            border-bottom-right-radius: 3pc;         
            font-size: 2rem;           
            height: 4rem;
 

            strong{
                opacity:1;
            }
        } 


        h2{           
            border-top-left-radius: 3pc;
            border-bottom-left-radius: 3pc;                   
            height: 3rem;
            background: -o-linear-gradient(230deg, rgba(120,245,146) 0%, rgba(82,171,255) 100%);
            background: linear-gradient(220deg, rgba(120,245,146) 0%, rgba(82,171,255) 100%);
           
            &:hover,
            &:active{
              background: -o-linear-gradient(340deg, rgba(120,245,146) 0%, rgba(82,171,255) 100%);
              background: linear-gradient(110deg, rgba(120,245,146) 0%, rgba(82,171,255) 100%);
            }
          

            a{
               opacity:1;
               text-decoration: none;
               color:#2c3e50;
               margin-left: 0.2em;

             
            }
        }



   }

   .title-project{
           display: -ms-grid;
           display: grid;
            height: 22rem;
            -webkit-box-orient: vertical;
            -webkit-box-direction: normal;
                -ms-flex-direction: column;
                    flex-direction: column;
            -webkit-box-pack: start;
                -ms-flex-pack: start;
                    justify-content: flex-start;
            -ms-flex-line-pack: stretch;
                align-content: stretch;
            justify-items: stretch;
            -webkit-box-align: center;
                -ms-flex-align: center;
                    align-items: center;
   }


   .story{
       padding: 3rem;

       h3{
           font-weight: 600;
       }
   }


   .icon-project{
       display: -webkit-box;
       display: -ms-flexbox;
       display: flex;
       -webkit-box-orient: horizontal;
       -webkit-box-direction: normal;
           -ms-flex-direction: row;
               flex-direction: row;
       -webkit-box-pack: space-evenly;
           -ms-flex-pack: space-evenly;
               justify-content: space-evenly;

       width: 100%;
       
       img{
         width: 12%;
         cursor: pointer;
        
       }
       
   }


   .img-project{
       width: 100%;
       display: -webkit-box;
       display: -ms-flexbox;
       display: flex;
       -webkit-box-orient: horizontal;
       -webkit-box-direction: normal;
           -ms-flex-direction: row;
               flex-direction: row;    
       -webkit-box-pack: space-evenly;    
           -ms-flex-pack: space-evenly;    
               justify-content: space-evenly;

        img{
            width: 90%;
            padding: .3rem;
            -webkit-box-shadow: 0 0 11px 7px #016b99;
                    box-shadow: 0 0 11px 7px #016b99;
            cursor: pointer;
        }  
   }


   .content-group{
            display: -webkit-box;
            display: -ms-flexbox;
            display: flex;
            -webkit-box-orient: horizontal;
            -webkit-box-direction: normal;
                -ms-flex-direction: row;
                    flex-direction: row;
            padding: 1rem;
            -webkit-box-align: center;
                -ms-flex-align: center;
                    align-items: center;       
            height: 18rem; 


            p{
                padding: .2rem;
            }

            h1{
                padding: .3rem;
            }
                    
                
   }


   .next-slide{
       text-align: end;

       img{
           cursor: pointer;           
           margin-right:2rem ;
           height:3rem;
       }
      

   }

    .project-container{
           height: 18rem;
           display: -webkit-inline-box;
       
            
    }




            .title-enter-active { -webkit-animation: title-on 2s; animation: title-on 2s; }
            .title-leave-active {animation: title-off .8s reverse; }
    
            @-webkit-keyframes title-on {
                0% {width:0%; opacity:0; }         
                100% {width:40%; opacity:1; }
            }
    
            @keyframes title-on {
                0% {width:0%; opacity:0; }         
                100% {width:40%; opacity:1; }
            }
            
    
            @-webkit-keyframes title-off {
                from { width:40%;}
                to {width:0%;}
            }
            
    
            @keyframes title-off {
                from { width:40%;}
                to {width:0%;}
            }


            .link-enter-active {-webkit-animation: link-on 2.5s;animation: link-on 2.5s;}
            .link-leave-active {animation: link-off .8s reverse;}

            @-webkit-keyframes link-on {
                0% {width:0%; opacity:0; }         
                100% {width:40%; opacity:1; }
            }

            @keyframes link-on {
                0% {width:0%; opacity:0; }         
                100% {width:40%; opacity:1; }
            }
            
    
            @-webkit-keyframes link-off {
                from { width:40%;}
                to {width:0%;}
            }
            
    
            @keyframes link-off {
                from { width:40%;}
                to {width:0%;}
            }



            .story-fade-enter-active {
             -webkit-animation-delay: .5s;
                     animation-delay: .5s;   
             -webkit-animation: story-fade-on 2s;   
                     animation: story-fade-on 2s; }

            .story-fade-leave-active {
            animation: story-fade-off .8s reverse; }
    
            @-webkit-keyframes story-fade-on {
                0% {-webkit-transform:scale(0);transform:scale(0)}         
                100% {-webkit-transform:scale(1);transform:scale(1)}
            }
    
            @keyframes story-fade-on {
                0% {-webkit-transform:scale(0);transform:scale(0)}         
                100% {-webkit-transform:scale(1);transform:scale(1)}
            }
            
    
            @-webkit-keyframes story-fade-off {
                from {-webkit-transform:scale(1);transform:scale(1)}
                to {-webkit-transform: scale(0);transform: scale(0)}  
            }
            
    
            @keyframes story-fade-off {
                from {-webkit-transform:scale(1);transform:scale(1)}
                to {-webkit-transform: scale(0);transform: scale(0)}  
            }


            .slide-portfolio-enter-active {                      
            -webkit-animation: slide-on 2.8s;                      
                    animation: slide-on 2.8s; }
            .slide-portfolio-leave-active {
            -webkit-animation: slide-off .2s;
                    animation: slide-off .2s;}

            .slide-content-enter-active {                      
            -webkit-animation: slide-on 1s;                      
                    animation: slide-on 1s; }
            .slide-content-leave-active {
            -webkit-animation: slide-off .2s;
                    animation: slide-off .2s;}
    
            @-webkit-keyframes slide-on {
                0% {-webkit-transform:translateX(200rem);transform:translateX(200rem)}         
                100% {-webkit-transform:translateX(0rem);transform:translateX(0rem)}
            }
    
            @keyframes slide-on {
                0% {-webkit-transform:translateX(200rem);transform:translateX(200rem)}         
                100% {-webkit-transform:translateX(0rem);transform:translateX(0rem)}
            }
            
    
            @-webkit-keyframes slide-off {
                from {opacity:1;}
                to {opacity:0;}
            }
            
    
            @keyframes slide-off {
                from {opacity:1;}
                to {opacity:0;}
            }

            
           
    
        

  
      .nextIcon {-webkit-animation: nextIcon-on 2s infinite;animation: nextIcon-on 2s infinite;}     
 
         @-webkit-keyframes nextIcon-on {
             0% {-webkit-transform:translateX(0rem);transform:translateX(0rem);}   
             25% {-webkit-transform:translateX(1rem);transform:translateX(1rem); }            
             50% {-webkit-transform:translateX(0rem);transform:translateX(0rem); }          
             75% {-webkit-transform:translateX(1rem);transform:translateX(1rem);}        
            100%{-webkit-transform:translateX(0rem);transform:translateX(0rem); }           
             
      }     
 
         @keyframes nextIcon-on {
             0% {-webkit-transform:translateX(0rem);transform:translateX(0rem);}   
             25% {-webkit-transform:translateX(1rem);transform:translateX(1rem); }            
             50% {-webkit-transform:translateX(0rem);transform:translateX(0rem); }          
             75% {-webkit-transform:translateX(1rem);transform:translateX(1rem);}        
            100%{-webkit-transform:translateX(0rem);transform:translateX(0rem); }           
             
      }


        .backicon {-webkit-animation: back-icon-on 1s;animation: back-icon-on 1s;}     
        
              @-webkit-keyframes back-icon-on {
                0% {-webkit-transform:translateX(-20rem);transform:translateX(-20rem); }   
               100% {-webkit-transform:translateX(0rem);transform:translateX(0rem); }          
        }     
        
              @keyframes back-icon-on {
                0% {-webkit-transform:translateX(-20rem);transform:translateX(-20rem); }   
               100% {-webkit-transform:translateX(0rem);transform:translateX(0rem); }          
        }


         .nextvis {-webkit-animation: nextvis-on 2s ;animation: nextvis-on 2s ; }
     
            @-webkit-keyframes nextvis-on {
                 0% { -webkit-transform:scale(0); transform:scale(0);    }   
                25% { -webkit-transform:scale(1.50); transform:scale(1.50); }                           
                50% { -webkit-transform:scale(1); transform:scale(1); }         
                75% { -webkit-transform:scale(1.50); transform:scale(1.50);} 
                100% {-webkit-transform:scale(1);transform:scale(1); }                     
                
        }
     
            @keyframes nextvis-on {
                 0% { -webkit-transform:scale(0); transform:scale(0);    }   
                25% { -webkit-transform:scale(1.50); transform:scale(1.50); }                           
                50% { -webkit-transform:scale(1); transform:scale(1); }         
                75% { -webkit-transform:scale(1.50); transform:scale(1.50);} 
                100% {-webkit-transform:scale(1);transform:scale(1); }                     
                
        }

    #medium-size{
        .project-group{
            width: auto;
            height: auto;
            padding: 6rem 0rem 1rem;
            overflow: hidden;

        }

        .project-container{           
            display: -webkit-box;           
            display: -ms-flexbox;           
            display: flex;
            -webkit-box-align: center;
                -ms-flex-align: center;
                    align-items: center;
            -ms-flex-wrap: wrap;
                flex-wrap: wrap;
            -webkit-box-orient: horizontal;
            -webkit-box-direction: normal;
                -ms-flex-direction: row;
                    flex-direction: row;            
            height: unset;
            

        }


        .title-project{
            height: auto;
        }


        .content{
            margin-top: 2rem;

              img{
                  width:13%;
                }

               p{
                   padding: 2rem
               }         
        }

      

        .content-group{
              display: -webkit-box;
              display: -ms-flexbox;
              display: flex;
              -webkit-box-orient: vertical;
              -webkit-box-direction: normal;
                  -ms-flex-direction: column;
                      flex-direction: column;
                padding: 1rem;
                -webkit-box-align: center;
                    -ms-flex-align: center;
                        align-items: center;
                 height: auto;

                .img-project{
                        -webkit-box-pack: space-evenly;
                            -ms-flex-pack: space-evenly;
                                justify-content: space-evenly;

                      
                }
          }
      

    }


    @media (max-width:500px){


        #medium-size{

              .title{
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
              -webkit-box-align: start;
                  -ms-flex-align: start;
                      align-items: flex-start;
              height: auto;

              h2{
                  margin-top:1rem;
                  border-top-right-radius: 3pc;
                  border-bottom-right-radius: 3pc;
                  border-top-left-radius: 0;
                  border-bottom-left-radius: 0;
                  display: table;
              }

              
          }

          .story{
                  padding: 1rem
              }        



          .next-slide{
              img{
                  height: 2rem;
              }
          }

          .content{
              p{
                padding: 1rem;  
              }
              
          }

        }  
            
          

    }







</style>
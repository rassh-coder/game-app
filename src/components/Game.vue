<template>
    <div class="container">
        <div class="stats">
            <div class="steps">
                {{steps}}
            </div>
            <div class="time">               
                <svg version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
                    width="87px" height="87px" viewBox="0 0 510 510" style="enable-background:new 0 0 87 87;" xml:space="preserve">
                    <g>
                        <g id="access-time">
                            <path style="fill-opacity:0.9;" d="M255,0C114.75,0,0,114.75,0,255s114.75,255,255,255s255-114.75,255-255S395.25,0,255,0z
                                M255,459c-112.2,0-204-91.8-204-204S142.8,51,255,51s204,91.8,204,204S367.2,459,255,459z"/>
                            <polygon style="fill-opacity:0.9;" points="267.75,127.5 229.5,127.5 229.5,280.5 362.1,362.1 382.5,328.95 267.75,260.1"/>
                        </g>
                    </g>
                </svg>

                <div class="timer">
                    {{min}}:{{sec}}
                </div>
            </div>
        </div>
        <div class="gamefield"
         @keydown.left.up.right.down="gamefunc"
         @focus="timer"
         :tabindex="Math.floor(Math.random(1,1000))"
         >
            <div class="win"
            v-if="winv"
            >
                Вы победили! <br>
                Ваши ходы {{steps}}. 
                <br>Ваше время {{min}}:{{sec}}
                <button id="newGame"
                 @click="newGame"
                >
                    Новая игра
                </button>
            </div>
            <div 
                v-for="(k) in kol" 
                :key="k" 
                class="gf"
                :class="{empty: k.trim() == '',moveright:k + 'right' == kVal,moveleft: k + 'left'==  kVal,moveup: k + 'up' == kVal,movedown:k + 'down' == kVal}"
                :id="`k${k}`"
            >
            
                <p>{{k}}</p>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
$bggfcolor: #5785ff; 
$gf:#b3c8ff;
$cc:hsla(222, 100%, 95%, 0.788);
$bfwidth: 500px;
$bfheight:500px;
$gfwh:118px;
$animtime: .5s;
$animiter:1;
$btncolor:#ffff00;
.gamefield {
    outline: none;
    background: $bggfcolor;
    width: $bfwidth;
    height:$bfheight;
    border: 4px solid $bggfcolor;
    border-radius: 2%;
    position:relative;
       
}
.empty
    {
        background:transparent!important;
    }
.gf{
    background: $gf;
    border-radius: 15%;
    margin-left: 4px;
    margin-top: 4px;
    width: $gfwh;
    height: $gfwh;
    font-size: 40px;
    color:#5a5a5a;
    float: left;
    

}
.win{
    position: absolute;
    width: 430px;
    height: 300px;
    top: 14%;
    left: 2%;
    font-size: 45px;
    background: $gf;
    border: 10px solid #ffff009c;
    border-radius:15px;

}
#newGame{
    background: $bggfcolor;
    border: 3px solid $btncolor;
    display: block;
    margin-left: 26%;
    width: 200px;
    font-size: 17px;
    color: $btncolor;
    margin-top: 11%;
    height: 50px;
}
.moveleft{
    animation: moveleft $animtime $animiter;
}
.moveright{
    animation: moverights $animtime $animiter;
}
.moveup{
    animation: moveup $animtime $animiter;
}
.movedown{
    animation: movedown $animtime $animiter;
}
@keyframes moveleft {
    0%{
        transform: translateX(0%)scale(1);
    }
    50%{
        transform: translateX(-50%)scale(1.5);
    }
    100%{
        transform: translateX(-103%)scale(1);
    }
}

@keyframes moverights {
    0%{
        transform: translateX(0%)scale(1);
    }
    50%{
        transform: translateX(50%)scale(1.5);
    }
    100%{
        transform: translateX(103%)scale(1);
    }
}
@keyframes moveup {
    0%{
        transform: translateY(0%)scale(1);
    }
    50%{
        transform: translateY(-50%)scale(1.5);
    }
    100%{
        transform: translateY(-103%)scale(1);
    }
}
@keyframes movedown {
    0%{
        transform: translateY(0%)scale(1);
    }
    50%{
        transform: translateY(50%)scale(1.5);
    }
    100%{
        transform: translateY(103%)scale(1);
    }
}
.container{
    background:$cc;
    width: $bfwidth +30px;
    height: $bfheight + 165px;
    border-radius: 3%;
    padding-top: 0.5%;
    display: inline-block;
    margin-right: 5%;
    margin-top: 2%;
}
.stats{
    width: $bfwidth ;
    height: 134px;
    border: 2px solid grey;
    border-radius: 15px;
    margin-left: 2%;
    margin-bottom: 1%;
    display: flex;
}
.steps{
   border: 5px solid grey;
    width: 180px;
    height: 80px;
    border-radius: 11%;
    font-size: 69px;
    color: grey;
    margin-left: 5%;
    margin-top: 4%;
}
.time{
    width: 300px;
    margin-left:3%;
    margin-top: 4%;
    display: flex;
}
.timer{
    font-size: 69px;
    margin-left: 2%;
    margin-top: 2%;
}
</style>

<script>
export default {
    name: 'Game',
    data:()=>({
        kol:[
            '1','2','3','4',
            '5','6','7','8',
            '9','10','11','12',
            '13','14','15',''
        ],
        winArray:[
            '1','2','3','4',
            '5','6','7','8',
            '9','10','11','12',
            '13','14','15',''
        ],
        testArr:[],
        steps: 0,
        move:false,
        kVal:0,
        min:0,
        sec:0,
        winv:false,
        focuscount: 0,
    }),
    
    methods:{
        timer(){
            if(this.focuscount == 0){
                this.move = true;
                this.interval = setInterval(()=>{
                    if(this.sec == 60 ){
                        this.sec = 0;
                        this.min++;
                        } 
                    else{
                        this.sec++;
                        }
                        }, 1000);
                    }
            this.focuscount++

        },    
        stop(){
            this.winv = true;
            this.move = false;
            clearInterval(this.interval);

        },
        newGame(){
            this.winv = false;
            this.startGame();
            this.sec = 0;
            this.min = 0;
            this.focuscount = 0;
            this.steps = 0;
        },
        gamefunc(e){
            e.preventDefault();
            var empty = this.kol.indexOf('');
            var usednum;
            var count;
            var bbb;
            if(e.keyCode == 37){
                if(this.kol[empty+1] && (empty+1) % 4 !== 0 && this.move){
                    count = 0;
                    usednum = this.kol[empty+1];
                    this.kVal = usednum + 'left'; 
                    this.move = false;
                    bbb = (e.target).querySelector(`#k${usednum}`);
                    bbb.addEventListener('animationend',()=>{
                        bbb.classList.remove('moveleft');                     
                        if(count == 0){
                        this.kol.splice(empty,1,usednum);
                        this.kol.splice(empty+1,1,'');
                        empty = this.kol.indexOf('');
                        this.steps++;
                        this.checkWin(this.kol);
                        this.move = true;
                        }
                        count++;
                    })
                       
                }
            }else if(e.keyCode == 38){
                if(this.kol[empty+4] && this.move){
                    count = 0;
                    usednum = this.kol[empty+4];
                    this.kVal =  usednum+'up';
                    this.move = false;
                    bbb = (e.target).querySelector(`#k${usednum}`);
                    bbb.addEventListener('animationend',()=>{
                        bbb.classList.remove('moveup');
                        if(count == 0){
                            this.kol.splice(empty,1,usednum)
                            this.kol.splice(empty+4,1,'');
                            empty = this.kol.indexOf('');
                            this.steps++;
                            this.checkWin(this.kol);
                            this.move = true;
                        }
                        count++;
                    }) 
                    
                }
            }else if(e.keyCode == 39){
                if(this.kol[empty-1] && empty % 4 !== 0 && this.move){
                    count = 0;
                    usednum = this.kol[empty-1];
                    this.kVal =  usednum + 'right'; 
                    this.move = false;
                    bbb = (e.target).querySelector(`#k${usednum}`);
                    bbb.addEventListener('animationend',()=>{
                        bbb.classList.remove('moveright');                     
                        if(count == 0){
                            this.kol.splice(empty,1,usednum)
                            this.kol.splice(empty-1,1,'');
                            empty = this.kol.indexOf('');
                            this.steps++;
                            this.checkWin(this.kol);
                            this.move = true;
                        }
                        count++;
                    })
                }
            } else if(e.keyCode == 40){
                if(this.kol[empty-4] && this.move){
                    count = 0
                    usednum = this.kol[empty-4];
                    this.kVal =  usednum+'down'; 
                    this.move = false;
                     bbb = (e.target).querySelector(`#k${usednum}`);
                        bbb.addEventListener('animationend',()=>{
                        bbb.classList.remove('movedown');
                        if(count == 0){
                        this.kol.splice(empty,1,usednum);
                        this.kol.splice(empty-4,1,'');
                        empty = this.kol.indexOf('');
                        this.steps++;
                        
                        this.checkWin(this.kol);
                        this.move = true;
                        }
                        count++;
                    })
                    
                }
            }

           
        },
        testOnSolved(arr){
            for(var k = 0,i = 1, len = arr.length-1; i<len;i++){
                for(var j = i-1; j >=0;j--){
                    if(arr[j]>arr[i]){
                        k++
                    }
                }
            }
            return !(k % 2);
        },
        checkWin(arr){
            this.testArr.splice(0,16,'');
            for(var i=0;i<16;i++){
                if(this.winArray[i] == arr[i]){
                 this.testArr.push(arr[i]);
                }
            }
            if(this.testArr.length == 17){
                this.stop();
            }
        },
        startGame(){
            var swi1;
            var swi2;
            this.kol.sort(()=>{
            return Math.random()-.5;
            });
            if(this.testOnSolved(this.kol)){
                swi1 = this.kol[0];
                swi2 = this.kol[1];
                this.kol.splice(0,1,swi2);
                this.kol.splice(1,1,swi1);
            };
            
        }
       
    },
    mounted(){
        this.startGame();
        var interval;

    }
}
</script>
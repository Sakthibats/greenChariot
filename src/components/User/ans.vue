<template>
    <div>
        <div class = "bg">
            <Head v-bind:id="id" class="head"></Head>
            <div class = "content">
                <p id = "question"> {{this.selectedQuestions[0].question}}</p><br>
                <br>
                <ul>
                    <li>
                        <div id='help'>
                            <button class='mcq' type='button' id=0 v-on:click='color(0)'>
                                1. {{this.selectedQuestions[0].options[0]}}
                            </button>
                        </div>
                    </li>
                    <li>
                        <div id='help'>
                            <button class='mcq' type='button' id=1 v-on:click='color(1)'>
                                2. {{this.selectedQuestions[0].options[1]}}
                            </button>
                        </div>
                    </li>
                    <li v-if='this.selectedQuestions[0].options.length>=3'>
                        <div id='help'>
                            <button class='mcq' type='button' id=2 v-on:click='color(2)'>
                                3. {{this.selectedQuestions[0].options[2]}}
                            </button>
                        </div>
                    </li>
                    <li v-if='this.selectedQuestions[0].options.length>=4' v-on:click='color(3)'>
                        <div id='help'>
                            <button class='mcq' type='button' id=3>
                                4. {{this.selectedQuestions[0].options[3]}}
                            </button>
                        </div>
                    </li>
                </ul>
                <button class = "btn" type='button' v-on:click="next()">Next</button>
            </div>
        </div>
        <Footer></Footer>
    </div>
</template>

<script>
import Head from './Header.vue'
import Footer from '../Footer.vue'
export default {
    name: 'ans',
    components :{
        Head,
        Footer
    },
    data() {
        return {
            id: this.$route.query.id,
            chose:this.$route.query.chose, //index of answer selected
            answer:this.$route.query.answer, //index of answer
            selectedQuestions:this.$route.query.selectedQuestions,
            score:this.$route.query.score,
            correct:this.$route.query.correct,
            ans: false
        }
    },
    methods: {
        toScore: function() {
            this.$router.push({name:'score',query:{id:this.id,score:this.score}})
        },
        next: function() {
            this.selectedQuestions.shift();
            if (this.selectedQuestions.length==0) {
                this.toScore()
            } else {
                this.$router.push({name:'question',query:{id:this.id,score:this.score,selectedQuestions:this.selectedQuestions}})
            }
        },
        color: function(ans) {
            if (this.answer != this.chose && !this.ans) {
                document.getElementById(ans).style.background = "red";
                document.getElementById(this.answer).style.background = "green";
                this.ans = true
            } else if (!this.ans) {
                document.getElementById(this.answer).style.background = "green";
            }
        },
        turnGreen: function() {
            document.getElementById(this.answer).style.color = "green";
        }
    },
    created() {
        this.color()
    }
}
</script>

<style scoped>
    @import url('https://fonts.googleapis.com/css?family=Montserrat');
    .bg {
        background-color: #9AD5FF;
        padding: 0px;
        margin: 0px;
        width: 100%;
        min-height: 120vh;
    }
    @keyframes zoomIn {
        from {
            transform: translate3d(0,30px,0);
            opacity: 0
        }

        to {
            transform: translate3d(0,0,0);
            opacity: 1
        }
    }
    .mcq{
        font-family: Montserrat;
        font-style: normal;
        background-color: #FFFFFF;
        padding:15px;
        border-radius:15px;
        border-width:1px;
        display:flex;
        font-size:25px;
        width:100%;
        cursor: pointer;
    }
    .head {
        position: sticky;
        top: 0;
        position: -webkit-sticky;
    }  
    li{
        list-style-type:none;
        padding:5px;
        margin-left: 40px;
        margin-right:40px;
    }
    .content {
        background-color: #FFFFFF;
        margin-top: 1%;
        margin-left: 10%;
        margin-right: 10%;
        margin-top:5%;
        height: 60%;
        width: 80%;
        justify-content: center;
        align-items: center;
        text-align: center;
        border-radius: 8px;
        padding: 10px
    }
    #question {
        font-family: Montserrat;
        font-style: normal;
        font-weight: bold;
        font-size: 30px;
        margin: 10px;
        padding:10px;
        float:left
    }
    #q {
        font-family: Montserrat;
        padding: 8px;
        width: 80%;
        margin: 2%;
        margin-left:8%;
        margin-right:8%;
        font-size: 20px;
        border-radius: 8px;
        border: 10px solid black;
        display: flex;
        align-items: center;
    }
    .btn {
        background: #2D8F8A;
        border-radius: 8px;
        font-family: Montserrat;
        font-style: normal;
        font-weight: bold;
        font-size: 20px;
        line-height: 24px;
        text-align: center;
        color: #FFFFFF;
        width: 30%;
        height: 50px;
        margin: 20px;
        cursor: pointer;
    }
    .title2 {
        font-family: Inter;
        font-style: normal;
        font-weight: bold;
        font-size: 15px;
        line-height: 58px;
        text-align: center;
        color: #1C746F;
        height:150px
    }
</style>
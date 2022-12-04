<template>
     <h2 class="heading">My BirthDay Countdown</h2>
    <div class="countdown">
        <div v-if="days" class="countdown__block">
            <div class="countdown__digit">{{ days | twoDigits }}</div>
            <div class="countdown__text">Days</div>
        </div>
        <div class="countdown__block">
            <div class="countdown__digit">{{ hours | twoDigits }}</div>
            <div class="countdown__text">Hours</div>
        </div>
        <div class="countdown__block">
            <div class="countdown__digit">{{ minutes | twoDigits }}</div>
            <div class="countdown__text">Minutes</div>
        </div>
        <div class="countdown__block">
            <div class="countdown__digit">{{ seconds | twoDigits }}</div>
            <div class="countdown__text">Seconds</div>
        </div>
    </div>
</template>

<script>
export default{
    props:{
        date:null
    },
    data(){
        return {
            now: Math.trunc((new Date()).getTime() / 1000),
            event:this.date,
            finish: false,
        }
    },
    mounted(){
        const _self = this
        window.setInterval(() => {
            this.now = Math.trunc((new Date()).getTime() / 1000)
            if(!this.finish && this.calculateDate - this.now <= 0){
                _self.finish = true
                _self.$emit('onFinish')
            }
        }, 1000)
    },

    computed:{
        secondCount (){
            return this.calculateDate - this.now
        },
        calculateDate(){
            return Math.trunc(Date.parse(this.event) / 1000)
        },
        seconds(){
            if(this.secondCount < 0) return 0
            return this.secondCount % 60
        },
        minutes(){
            if(this.secondCount < 0) return 0
            return Math.trunc(this.secondCount / 60) % 60
        },
        hours(){
            if(this.secondCount < 0) return 0
            return Math.trunc(this.secondCount / 60 / 60) % 24
        },
        days(){
            if(this.secondCount < 0) return 0
            return Math.trunc(this.secondCount / 60 /60 / 24)
        }
    },
    filters: {
        twoDigits (value){
            if(value.toString().length <= 1){
                return '0'+value.toString()
            }
            return value.toString()
        }
    }
}
</script>

<style lang="css">
.countdown{
    display: flex;
  justify-content: center;
  align-items: center;
  height: 200px;
}
.countdown .heading{
    display: inline-block !important;
}
.countdown__block{
    text-align: center;
    padding: 0px 15px;
    position:relative;
}
   
.countdown__block:first-child{
    padding-left: 0;
}
.countdown__digit:before{
     display: none;
    
}
.countdown__block:last-child{
    padding-right: 0;
}

.countdown__text{
    text-transform: uppercase;
    margin-bottom: 5px;
}
.countdown__digit{
    font-size: 30px;
    font-weight: bold;
    line-height: 1;
    margin-bottom: 5px;
}
.countdown__digit:before{
    content: ";";
    position: absolute;
    left: -5px;
}
</style>
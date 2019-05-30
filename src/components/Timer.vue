<template>
    <div id="clock">
        <p class="date">{{ date }}</p>
        <p class="time">{{ time }}</p>
        <p class="text">DIGITAL CLOCK with Vue.js</p>
    </div>
</template>

<script>

export default {
    
    data: {
        time: '',
        date: '',
        week : ['SUN', 'MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT'],
        timerID : setInterval(updateTime, 1000)
    },
    components: {
        Name
    },
    methods: {
        updateTime() {
            var cd = new Date();
            clock.time = zeroPadding(cd.getHours(), 2) + ':' + zeroPadding(cd.getMinutes(), 2) + ':' + zeroPadding(cd.getSeconds(), 2);
            clock.date = zeroPadding(cd.getFullYear(), 4) + '-' + zeroPadding(cd.getMonth()+1, 2) + '-' + zeroPadding(cd.getDate(), 2) + ' ' + week[cd.getDay()];
        },
        zeroPadding(num, digit) {
            var zero = '';
            for(var i = 0; i < digit; i++) {
                zero += '0';
            }
            return (zero + num).slice(-digit);
        }    
    },
    mounted(){
        this.updateTime()
    },
    
}

</script>

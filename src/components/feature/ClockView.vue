<template>
  <div class="content-clock">
        <div id="clock">
            <ul class="list-group">
                <li class="list-group-item" v-show="date"><strong><i class="ri-calendar-fill"></i></strong> {{ date }}</li>
            </ul> 
            <div id="time" class="animate__animated animate__slideInUp animate__delay-.5s">
				<div><span id="hours">{{ hours }}</span><span>Heures</span></div>
				<div><span id="minutes">{{ minutes }}</span><span>Minutes</span></div>
				<div><span id="seconds">{{ seconds }}</span><span>Secondes</span></div>
			</div>
		</div>
  </div>
</template>

<script>
export default {
    name: 'ClockView',
    data: () => ({
        date: '',
        hours: 0,
        minutes: 0,
        seconds: 0
    }),
    methods: {
        printDate: function () {
            return new Date().toLocaleDateString();
        },          
        setTime() {
            const date = new Date();
            let hours = date.getHours();
            let minutes = date.getMinutes();
            let seconds = date.getSeconds();
            hours = hours <= 9 ? `${hours}`.padStart(2, 0) : hours;
            minutes = minutes <= 9 ? `${minutes}`.padStart(2, 0) : minutes;
            seconds = seconds <= 9 ? `${seconds}`.padStart(2, 0) : seconds;
            this.hours = hours;
            this.minutes = minutes;
            this.seconds = seconds;
        }
    },
    mounted: function () {
        this.date = this.printDate();
        setInterval(() => this.setTime(), 1000)
    },
}
</script>

<style>
.content-clock {
    display: flex;
    align-items: center;
    justify-content: center;
}

#clock {
    margin-bottom: 50px;
}

#clock > ul > li {
    list-style: none;
    margin-bottom: 25px;
    font-family: "Montserrat", sans-serif;
    font-weight: 500;
    font-size: 1.3em;
    color: rgb(63, 102, 186);
}

#clock #time { display: flex; }

#clock #time div {
	position: relative;
	margin: 0 5px;
}

#clock #time div span {
	position: relative;
    border-radius: 10px;
	display: block;
	width: 100px;
	height: 80px;
    background: rgba(48, 179, 236, 0.62);
    box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
    backdrop-filter: blur(5px);
	color: #fff;
	font-weight: 300;
	display: flex;
	justify-content: center;
	align-items: center;
	font-size: 3em;
	z-index: 10;
}

#clock #time div span:nth-child(2) {
	height: 30px;
	font-size: 0.7em;
	letter-spacing: 0.2em;
	font-weight: 500;
	z-index: 9;
	box-shadow: none;
    background: rgba(18, 127, 214, 0.63);
    box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
    backdrop-filter: blur(5px);
	text-transform: uppercase;
}

#clock #time div:last-child span { background-color: #ff006a; }

#clock #time div:last-child span:nth-child(2) { background-color: #ec0062; }
</style>
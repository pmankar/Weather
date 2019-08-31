<template>
	<div id="app" class="container mt-4">
		<!-- header section -->
		<div class="header">
		</div>
		
		<!-- page body  -->
		<div class="body">
			<div v-if="body" class="card border shadow mt-4" style="width: 21rem;">
				<div class="card-body m-3">
					<div class="row">
						<h4 class="card-title">{{ body.name }}</h4>
					</div>
					<div class="row">
						<p><small>{{ (new Date( body.dt * 1000 )).toLocaleTimeString() }}, {{ body.weather[0].description }} </small></p>
					</div>					
					<div class="row">
						<div class="col col-xs-12">
							<p class="display-1 tempC"> {{ Math.round(body.main.temp) }}</p>
						</div>
						<!--<img class="col col-xs-4" :src="'https://openweathermap.org/img/wn/' + body.weather[0].icon + '@2x.png'">
						<b>{{ body.weather[0].main}} </b> <br>
							<small>{{ body.weather[0].description }} </small> <br>
						-->
					</div>
					<div class="row">
						Humidity: {{ body.main.humidity }}% at {{ body.main.pressure }} hpa <br>
						Wind: {{ body.wind.speed }} kmph at {{ body.wind.deg }}°
					</div>
				</div>
				<div class="card-body pt-0">
					<div class="row my-1">
						<div class="col col-xs-6">Min: {{ body.main.temp_min}} °C</div>
						<div class="col col-xs-6">Max: {{ body.main.temp_max}} °C</div>
					</div>
					<div class="row my-1">
						<div class="col col-xs-6">Sunrise: {{ pad((new Date( body.sys.sunrise * 1000 )).getHours()) + ":" + pad((new Date( body.sys.sunrise * 1000 )).getMinutes()) }}</div>
						<div class="col col-xs-6">Sunset: {{ pad((new Date( body.sys.sunset * 1000 )).getHours()) + ":" + pad((new Date( body.sys.sunset * 1000 )).getMinutes()) }}</div>
					</div>
				</div>
			</div>
			<div v-else class="card border shadow mt-4" style="width: 21rem;">
				<div class="card-body p-4">
					Hold on, while the info is being loaded.
				</div>
			</div>
		</div>
		
		<!-- footer section -->
		<footer>
			Powered By: 
				<a href='https://vuejs.org'><img src="./assets/logo.png" title='Vue.js'></a>
				<a href='https://getbootstrap.com'><img src="https://getbootstrap.com/docs/4.3/assets/brand/bootstrap-solid.svg" title='Bootstrap'></a>
				<a href='https://openweathermap.org'><img src="https://openweathermap.org/themes/openweathermap/assets/img/openweather-negative-logo-RGB.png" style="width:50px" title='openweathermap'></a>
		</footer>
	</div>
</template>

<script>
var appid = "1c36c16e8018c18485ac7e2e468df02c"; // Please don"t steal me 
var url = "https://api.openweathermap.org/data/2.5/weather?id=3220838&units=metric&appid=" + appid;

export default {
	data () {
		return {
			header: "Weather in Munich",
			body: null,
			pad: function(a) {return(100+a+"").slice(-2)}
		}
	},
	 mounted() {
		axios.get(url)
			.then(response => {
				this.body = response.data
			})
	}
}
import axios from "axios";

</script>

<style>
body{
	margin-bottom: 50px !important;
}

.tempC::after{
	content:'°C';
	font-size: 3rem;
	position: absolute;
	margin-top: 1rem;
}
footer {
	position: fixed;
	bottom: 0px;
	left: 0px;
	min-height: 30px;
	width:100%;
	background: #ddd;
	padding: 0.5rem;
	text-align: center;
	color: var(--light);
	background: var(--dark);
}

footer a img {
	height: 20px;
	width: 20px;
	position: relative;
	margin-right: 0.5rem;
}
</style>
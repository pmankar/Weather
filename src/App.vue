<template>
	<div id="app" class="container mt-4">
		<!-- header section -->
		<div class="header">
			<h2>{{ header }} </h2>
		</div>
		
		<!-- page body  -->
		<div class="body">
			<div class="card border border-primary shadow mt-4" style="width: 24rem;">
				<div class="card-body pb-0">
					<div class="row">
						<img class="col col-sm-4" :src="'http://openweathermap.org/img/wn/' + body.weather[0].icon + '@2x.png'">
						<div class="col-sm-8"><b> {{ body.main.temp }} °C </b> at {{ body.main.pressure }} hpa<br>
						<b>{{ body.weather[0].main}} </b> <br>
						<small>{{ body.weather[0].description }} </small> <br>
						<small>Last updated: {{ (new Date( body.dt * 1000 )).toLocaleTimeString() }} </small> <br>
						</div>
					</div>
					<hr>
				</div>
				<div class="card-body pt-0">
					<div class="row my-1">
						<div class="col-sm-6">Min: {{ body.main.temp_min}} °C</div>
						<div class="col-sm-6">Max: {{ body.main.temp_max}} °C</div>
					</div>
					<div class="row my-1">
						<div class="col-sm-6">Visibility: {{ ( body.visibility / 1000 ).toFixed(1) }} km</div>
						<div class="col-sm-6">Wind: {{ body.wind.speed }} kmph {{ body.wind.deg ? " at " + body.wind.deg + "°": "" }}</div>
					</div>
					<div class="row my-1">
						<div class="col-sm-6">Min: {{ body.main.temp_min}} °C</div>
						<div class="col-sm-6">Max: {{ body.main.temp_max}} °C</div>
					</div>
					<div class="row my-1">
						<div class="col-sm-6">Sunrise: {{ (new Date( body.sys.sunrise * 1000 )).toLocaleTimeString() }}</div>
						<div class="col-sm-6">Sunset: {{ (new Date( body.sys.sunset * 1000 )).toLocaleTimeString() }}</div>
					</div>
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
var url = "http://api.openweathermap.org/data/2.5/weather?id=3220838&units=metric&appid=" + appid;

  
export default {
	data () {
		return {
			header: "Weather in Munich",
			body: null
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

function getImgURL(){
	return "ok";
}
</script>

<style>

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
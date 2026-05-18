<script>
	import { onMount } from 'svelte';

	export let date;

	let countDate = 0;
	let interval;

	let days = '00';
	let hours = '00';
	let minutes = '00';
	let seconds = '00';

	onMount(() => {

		countDate = new Date(date).getTime();

		updateTimer();

		interval = setInterval(updateTimer, 1000);

		return () => clearInterval(interval);
	});

	function updateTimer() {

		const now = Date.now();
		const gap = countDate - now;

		if (gap <= 0) {
			clearInterval(interval);
			return;
		}

		const second = 1000;
		const minute = second * 60;
		const hour = minute * 60;
		const day = hour * 24;

		days = String(Math.floor(gap / day)).padStart(2, '0');

		hours = String(
			Math.floor((gap % day) / hour)
		).padStart(2, '0');

		minutes = String(
			Math.floor((gap % hour) / minute)
		).padStart(2, '0');

		seconds = String(
			Math.floor((gap % minute) / second)
		).padStart(2, '0');
	}
</script>

<div class="flex flex-wrap items-center justify-center gap-4 md:gap-6">

	<!-- Card -->
	<div class="time-card text-center">
		<div class="glow"></div>

		<h2 class="lg:text-3xl text-xl">{days}</h2>
		<p class=" md:text-sm text-xs">Days</p>
	</div>

	

	<!-- Card -->
	<div class="time-card text-center">
		<div class="glow"></div>

		<h2 class="lg:text-3xl text-xl">{hours}</h2>
		<p class=" md:text-sm text-xs">Hours</p>
	</div>

	
	<!-- Card -->
	<div class="time-card text-center">
		<div class="glow"></div>

		<h2 class="lg:text-3xl text-xl">{minutes}</h2>
		<p class=" md:text-sm text-xs">Minutes</p>
	</div>

	

	<!-- Card -->
	<div class="time-card text-center">
		<div class="glow"></div>

		<h2 class="lg:text-3xl text-xl">{seconds}</h2>
		<p class=" md:text-sm text-xs">Seconds</p>
	</div>

</div>


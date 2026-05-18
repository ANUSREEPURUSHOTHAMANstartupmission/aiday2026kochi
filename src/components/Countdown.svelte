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



<div class="flex items-center justify-center flex-row ">
	<div class="counter w-20 h-24 text-white font-semibold font-heading lg:text-3xl text-xl  flex flex-col items-center justify-center">
		{days}
		<div class="text-base font-light font-sans">Days</div>
	</div>
	<div class=" counter w-20 h-24 text-white font-semibold font-heading lg:text-3xl text-xl  flex flex-col items-center justify-center">
		{hours}
		<div class="text-base font-light font-sans">Hours</div>
	</div>
	<div class="counter w-20 h-24 text-white font-semibold font-heading lg:text-3xl text-xl  flex flex-col items-center justify-center">
		{minutes}
		<div class="text-base font-light font-sans">Mins</div>
	</div>
	<div class="counter w-20 h-24 text-white font-semibold font-heading lg:text-3xl text-xl  flex flex-col items-center justify-center">
		{seconds}
		<div class="text-base font-light font-sans">Secs</div>
	</div>
</div>



<style>
	.time-card {
		position: relative;
		width: 110px;
		height: 130px;
		border-radius: 28px;

		background:
			linear-gradient(
				180deg,
				rgba(255,255,255,0.08),
				rgba(255,255,255,0.03)
			);

		border: 1px solid rgba(255,255,255,0.08);

		backdrop-filter: blur(18px);

		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;

		overflow: hidden;

		box-shadow:
			0 10px 40px rgba(0,0,0,0.35),
			inset 0 1px 1px rgba(255,255,255,0.08);

		transition: all .3s ease;
	}

	.time-card:hover {
		transform: translateY(-5px);
		border-color: rgba(139,92,246,0.4);

		box-shadow:
			0 20px 50px rgba(139,92,246,0.2);
	}

	.time-card h2 {
		font-size: 2rem;
		font-weight: 800;
		line-height: 1;
		color: white;
		z-index: 2;
	}

	.time-card p {
		margin-top: 12px;
		font-size: .75rem;
		letter-spacing: .25em;
		color: rgba(255,255,255,0.7);
		z-index: 2;
	}

	.glow {
		position: absolute;
		top: -40px;
		width: 100px;
		height: 100px;

		background: radial-gradient(
			circle,
			rgba(139,92,246,0.45),
			transparent 70%
		);

		filter: blur(20px);
	}

	@media (max-width: 768px) {

		.time-card {
			width: 85px;
			height: 105px;
			border-radius: 22px;
		}

		.time-card h2 {
			font-size: 2rem;
		}

		.time-card p {
			font-size: .65rem;
		}
	}
</style>
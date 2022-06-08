<svelte:head>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Sora:wght@500&display=swap" rel="stylesheet"> 
</svelte:head>

<script>
	const DATE_PERIOD = "Aug 31, 2022 00:00:00";

    const formatDate = (date) => {
        return date < 10 ? `0${date}` : date
    }

    const calculateDays = (difference) => {
        return formatDate(Math.floor((difference) / (1000 * 60 * 60 * 24)))
    }

    const calculateHours = (difference) => {
        return formatDate(Math.floor(((difference) % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)))
    }

    const calculateMinutes = (difference) => {
        return formatDate(Math.floor(((difference) % (1000 * 60 * 60)) / (1000 * 60)))
    }

    const calculateSeconds = (difference) => {
        return formatDate(Math.floor(((difference) % (1000 * 60)) / 1000))
    }

    const currentDate = new Date()
    const countdownDate = new Date(DATE_PERIOD).getTime();
    const counter = {
        days: calculateDays(countdownDate - currentDate.getTime()),
        hours: calculateHours(countdownDate - currentDate.getTime()),
        minutes: calculateMinutes(countdownDate - currentDate.getTime()),
        seconds: calculateSeconds(countdownDate - currentDate.getTime())
    }
    
    const updateCount = setInterval(() => {
        const today = new Date().getTime()
        const interval = (countdownDate - today)
        counter.days = calculateDays(interval)
        counter.hours = calculateHours(interval)
        counter.minutes = calculateMinutes(interval)
        counter.seconds = calculateSeconds(interval)
    }, 1000)
</script>

<main> 

    <h1 class="font-extrabold text-transparent text-8xl bg-clip-text bg-gradient-to-r from-blue-400 to-pink-600">
        Mental.fy
    </h1>

    <div class="container">
        <div class="flex flex-col items-center justify-center">
            <div class="text-center">
                <h2 class="text-4xl font-bold">
                    <span class="font-extrabold text-transparent text-5xl bg-clip-text bg-gradient-to-r from-purple-400 to-pink-600">{counter.days}</span>
                    <span class="text-5xl text-gray-500 ">{counter.hours}</span>
                    <span class="text-5xl text-gray-500">{counter.minutes}</span>
                    <span class="text-5xl text-gray-500">{counter.seconds}</span>
                </h2>
                <h3 class="text-xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-blue-300 to-pink-300">Until We Launch</h3>
            </div>
        </div>
    </div>
</main>

<style>
    main {
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .container {
        width: 100%;
        max-width: 600px;
        padding: 2rem;
    }

    h1 {
        font-family: 'Sora', sans-serif;
        font-size: 4rem;
        line-height: 1.2;
        text-align: center;
    }

    h2 {
        font-family: 'Sora', sans-serif;
        font-size: 2rem;
        line-height: 1.2;
        text-align: center;
    }
</style>
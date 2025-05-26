<script lang="ts">
  import { onMount, onDestroy } from 'svelte';
  import { calculateTimeLeft, type TimeLeft } from '$lib/countdown';

  export let targetDate: Date;

  let timeLeft: TimeLeft = { days: 0, hours: 0, minutes: 0, seconds: 0 };

  // Menyimpan interval countdown (bisa number atau undefined tergantung browser)
  let intervalId: ReturnType<typeof setInterval>;

  const update = () => {
    timeLeft = calculateTimeLeft(targetDate);
  };

  onMount(() => {
    update();
    intervalId = setInterval(update, 1000);
  });

  onDestroy(() => {
    clearInterval(intervalId);
  });
</script>

<!-- Tampilan countdown -->
<div class="text-lg md:text-2xl">
  <span>{timeLeft.days} hari</span> :
  <span>{timeLeft.hours} jam</span> :
  <span>{timeLeft.minutes} menit</span> :
  <span>{timeLeft.seconds} detik</span>
</div>

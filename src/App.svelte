<!-- JS -->
<script>
  // Moment.js import
  import moment from "moment";

  // Calendar data
  let data = {
		year: moment().year(),				
		month: moment().month(),
		day: moment().date(),
		dayNumberOfWeek: moment().day(),	
		startOfMonthNumberOfWeek: moment().startOf('month').day(),	
		daysInMonth: moment().daysInMonth(),
		daysInMonthPrev: moment().subtract( 1, 'months').daysInMonth(),
		daysInMonthNext: moment().add( 1, 'months').daysInMonth()
	};
	data.weeksInMonth = Math.ceil((data.daysInMonth + data.startOfMonthNumberOfWeek - 1) / 7);

  console.log(data.daysInMonthPrev)

</script>

<!-- HTML -->
<main>

  <div class="container">
		<div class="row mt-5 justify-content-center">
			<h3 class="text-center">{moment().format('YYYY-MM-DD')}</h3>
		</div>
		<div class="row justify-content-center mt-3">
			
			<table class="table table-bordered w-auto">
				<thead>
					<tr>
            {#each ['H', 'K', 'Sz', 'Cs', 'P', 'Szo', 'V'] as nap}
						  <th class="text-center">{nap}</th>
            {/each}
					</tr>
				</thead>
				<tbody>
          {#each Array(data.weeksInMonth) as _, w}
					  <tr class="text-center">
              {#each Array(7) as _, i}
                {@const day = w * 7 + i - data.startOfMonthNumberOfWeek + 2}
                <td class:text-muted={day < 1 || day > data.daysInMonth} 
                    class:fw-bold={day > 0 && day <= data.daysInMonth} 
                    class:text-primary={day == data.day}>
                  {#if day < 1}
                    {data.daysInMonthPrev + day}
                  {:else if day > data.daysInMonth}
                    {day - data.daysInMonth}
                  {:else}  
                    {day}
                  {/if}
                </td>
              {/each}
					  </tr>
          {/each}
				</tbody>
			</table>
		</div>
	</div>
</main>

<!-- CSS
  <style></style>
-->

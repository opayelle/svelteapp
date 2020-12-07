<script>
import { format, parse, toDate, getUnixTime } from 'date-fns'
let dateFormat = "yyyy-MM-dd"
let timeFormat = "HH:mm:ss"

// Input "date"
$: dateText = format(Date.now(), dateFormat)
$: dateTime = format(Date.now(), timeFormat)
$: timestamp = Math.floor(Date.now()/1000)
$: resultFromInputDate = parse(dateText + dateTime, dateFormat + timeFormat, new Date())
$: resultFromTimestamp = toDate(timestamp * 1000)

function onDateChange() {
  resultFromInputDate = parse(dateText + dateTime, dateFormat + timeFormat, new Date())
  timestamp = getUnixTime(resultFromInputDate)
}

function onTimestampChange() {
  resultFromTimestamp = toDate(timestamp * 1000)
  dateText = format(resultFromTimestamp, dateFormat)
  dateTime = format(resultFromTimestamp, timeFormat)
}
</script>

<div>
  <h2>Date &lt;=&gt; timestamp</h2>
  <div> 
    <input type="date" id="dateToConvert" name="dateToConvert" bind:value={dateText} on:input={onDateChange}>
    <input type="time" id="timeToConvert" name="timeToConvert" step="2" bind:value={dateTime} on:input={onDateChange}>
  </div>
  <br/>
  <div>
    <input type="number" name="timestamp" bind:value={timestamp} on:input={onTimestampChange}  />
  </div>
  <br/>
</div>

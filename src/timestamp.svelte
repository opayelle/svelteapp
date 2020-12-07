<script>
import { format, parse, toDate, getUnixTime } from 'date-fns'
let dateFormat = "yyyyMMdd HH:mm:ss"

// Input "date"
$: dateText = format(Date.now(), dateFormat)
$: resultFromInputDate = parse(dateText, dateFormat, new Date())
$: timestampFromInputDate = getUnixTime(resultFromInputDate)

// Input "timestamp"
$: timestamp = getUnixTime(Date.now())
$: resultFromTimestamp = toDate(timestamp * 1000)

</script>
<h2>Date to timestamp</h2>
<div>Date: {resultFromInputDate}</div>
<div>Date: <input type="text" name="date" bind:value={dateText} /></div>
<div>Timestamp: {timestampFromInputDate}</div>

<hr/>
Timestamp to date

<div>Timestamp: <input type="text" name="timestamp" bind:value={timestamp} /></div>
<div>Date: {resultFromTimestamp}</div>

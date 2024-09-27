[[Pagbank]]

https://medium.com/@roscoe.kerby/understanding-cron-expressions-in-java-with-scheduled-annotation-4444658ee90c


`* * * * * *`  
`| | | | | |`  
`| | | | | +-- Year (optional)`  
`| | | | +---- Day of the week (0 - 7, where both 0 and 7 represent Sunday)`  
`| | | +------ Month (1 - 12)`  
`| | +-------- Day of the month (1 - 31)`  
`| +---------- Hour (0 - 23)`  
`+------------ Minute (0 - 59)`

- `* * * * * *`: Runs every minute.
- `0 * * * * *`: Runs every hour.
- `0 0 * * * *`: Runs daily at midnight.
- `0 12 * * * *`: Runs daily at noon.
- `0 0 * * 0 *`: Runs every Sunday at midnight.
- `0 0 1* * *`: Runs every first day of the month.
- `0 0 L * * *`: Runs every last day of the month.
- `0 9 * * 1-5 *`: Runs every weekday (Monday to Friday) at 9:00 am.
- `*/15 * * * * *`: Runs every 15 minutes.
- `0 */5 * * * *`: Runs every 5 hours.
- `0 0 1 1 * *`: Runs every New Year’s Day at midnight.
- `30 * * * * *`: Runs every 30th minute past the hour.
- `30 15 * * 1,3 *`: Runs every Monday and Wednesday at 15:30 pm.

Java Cron Expression

`* * * * * *`  
`| | | | | |`  
`| | | | | +-- day of the week  
`| | | | +---- month(1-12)  
`| | | +------ Day of the month (1 - 12)`  
`| | +-------- Hour (1 - 31)`  
`| +---------- MInute(0 - 23)`  
`+------------ Second(0 - 59)`

	
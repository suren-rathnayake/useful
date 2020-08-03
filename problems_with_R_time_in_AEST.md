I want to convert a character string into AEST 

After reading a csv file, I get something like the following in character from

    tmp <- c("27/05/2015 2:04:11 AM", "19/06/2015 4:53:45 AM")

I use the `lubridate` package to convert to  class `"POSIXct", "POSIXt"` as follows:

    tmp <- dmy_hms(tmp)

The **problem** with this is that these are in UTC

    tmp
    #[1] "2015-05-27 02:04:11 UTC" "2015-06-19 04:53:45 UTC"

and I'd rather have them in AEST.

---
### Attempt 1
Following is not good as it at 10h to the values

    attr(tmp, "tzone") <- "Australia/Queensland"
    tmp
    #[1] "2015-05-27 12:04:11 AEST" "2015-06-19 14:53:45 AEST"

---
### Attempt 2
Following works but with a warning

    attr(tmp, "tzone") <- "AEST"
    tmp
    #[1] "2015-05-27 02:04:11 GMT" "2015-06-19 04:53:45 GMT"
    #Warning messages:
    #1: In as.POSIXlt.POSIXct(x, tz) : unknown timezone 'AEST'
    #2: In as.POSIXlt.POSIXct(x, tz) : unknown timezone 'AEST'


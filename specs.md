  
    recur = "FREQ"=freq *(
                ; either UNTIL or COUNT may appear in a 'recur',
                ; but UNTIL and COUNT MUST NOT occur in the same 'recur'

                ( ";" "UNTIL" "=" enddate ) /
                ( ";" "COUNT" "=" 1*DIGIT ) /

                ; the rest of these keywords are optional,
                ; but MUST NOT occur more than once

                ( ";" "INTERVAL" "=" 1*DIGIT )          /
                ( ";" "BYSECOND" "=" byseclist )        /
                ( ";" "BYMINUTE" "=" byminlist )        /
                ( ";" "BYHOUR" "=" byhrlist )           /
                ( ";" "BYDAY" "=" bywdaylist )          /
                ( ";" "BYMONTHDAY" "=" bymodaylist )    /
                ( ";" "BYYEARDAY" "=" byyrdaylist )     /
                ( ";" "BYWEEKNO" "=" bywknolist )       /
                ( ";" "BYMONTH" "=" bymolist )          /
                ( ";" "BYSETPOS" "=" bysplist )         /
                ( ";" "WKST" "=" weekday )              /
                ( ";" x-name "=" text )
                )

     freq = "SECONDLY" / "MINUTELY" / "HOURLY" / "DAILY" / "WEEKLY" / "MONTHLY" / "YEARLY"
     
     enddate    = date
     enddate    =/ date-time ;An UTC value

     byseclist  = seconds / ( seconds *("," seconds) )
     seconds    = 1DIGIT / 2DIGIT       ;0 to 59

     byminlist  = minutes / ( minutes *("," minutes) )
     minutes    = 1DIGIT / 2DIGIT       ;0 to 59

     byhrlist   = hour / ( hour *("," hour) )
     hour       = 1DIGIT / 2DIGIT       ;0 to 23

     bywdaylist = weekdaynum / ( weekdaynum *("," weekdaynum) )
     weekdaynum = [([plus] ordwk / minus ordwk)] weekday

     plus       = "+"
     minus      = "-"

     ordwk      = 1DIGIT / 2DIGIT       ;1 to 53

     weekday    = "SU" / "MO" / "TU" / "WE" / "TH" / "FR" / "SA"
     ;Corresponding to SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY,
     ;FRIDAY, SATURDAY and SUNDAY days of the week.

     bymodaylist = monthdaynum / ( monthdaynum *("," monthdaynum) )
     monthdaynum = ([plus] ordmoday) / (minus ordmoday)

     ordmoday   = 1DIGIT / 2DIGIT       ;1 to 31

     byyrdaylist = yeardaynum / ( yeardaynum *("," yeardaynum) )
     yeardaynum = ([plus] ordyrday) / (minus ordyrday)

     ordyrday   = 1DIGIT / 2DIGIT / 3DIGIT      ;1 to 366

     bywknolist = weeknum / ( weeknum *("," weeknum) )
     weeknum    = ([plus] ordwk) / (minus ordwk)

     bymolist   = monthnum / ( monthnum *("," monthnum) )
     monthnum   = 1DIGIT / 2DIGIT       ;1 to 12

     bysplist   = setposday / ( setposday *("," setposday) )

     setposday  = yeardaynum
    *If the property permits, multiple "recur" values are specified by a COMMA character (US-ASCII decimal 44)
    *The rule parts are separated from each other by the SEMICOLON character (US-ASCII decimal 59).
    
    FREQ: SECONDLY, MINUTELY, HOURLY, DAILY, WEEKLY, MONTHLY, YEARLY (Mandatory)
    INTERVAL: INT >= 1 (Default: 1)
    UNTIL: UTC DATETIME (Optional)
    COUNT: INT > 0 (Optional)
    BYSECOND: 0 <= INT < 60 (Optional)
    BYMINUTE: 0 <= INT < 60 (Optional)
    BYHOUR: 0 <= INT < 24 (Optional)
    BYDAY: MO, TU, WE, TH, FR, SA, SU (Optional) 
      // +1MO works also as first monday day of the month
      // -1TU works also as last tuesday of the month
    BYMONTHDAY: 1, 2, ....., 31 OR -31, -30, .... , -1 (Optional)
    BYYEARDAY: 1, 2, ....., 366 OR -366, -365, .... , -1 (Optional)
    BYWEEKNO: 1, 2, ....., 53 OR -53, -52, .... , -1 (Optional)
    BYMONTH: 1, 2, ....., 12 (Optional)
    WKST: MO, TU, WE, TH, FR, SA, SU (Default: MO) //Day used to start the week
    EXDATE: UTC DATETIME1, UTC DATETIME2, .... UTC DATETIMEX (Optional)
    

# utl-nice-example-of-alias-columns-in-wps-proc-report
Nice example of alias columns in wps proc report
    %let pgm=utl-nice-example-of-alias-columns-in-wps-proc-report;

    Nice example of alias columns in wps proc report

    github
    http://tinyurl.com/5n83rmda
    https://github.com/rogerjdeangelis/utl-nice-example-of-alias-columns-in-wps-proc-report

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*           |                                                             |                                              */
    /*           |                                                             |                                              */
    /*  SD1.HAVE |       WPS Proc Report                                       |  Trial ABC: Patient Min, Max and Median Age  */
    /*           |                                                             |                                              */
    /*  REC AGE  |  Proc Report Data=sd1.have(obs=100) split="#";              |       Min      Median      Max               */
    /*           |  title "Trial ABC: Patient Minimun, Maximum and Median Age";|  Age(Yrs)     Age(Yrs)   Age(Yrs)            */
    /*  100  37  |   Column                                                    |                                              */
    /*  200  33  |         Age=Age_min                                         |        28           37         49            */
    /*  300  36  |         Age=Age_med                                         |                                              */
    /*  400  42  |         Age=Age_max                                         |                                              */
    /*  500  39  |   ;                                                         |                                              */
    /*  600  33  |  Define Age_min  / min  "Min#Age(Yrs)#"  width=14;          |                                              */
    /*  700  28  |  Define Age_max  / max  "Max#Age(Yrs)#"  width=14;          |                                              */
    /*  800  49  |  Define Age_med  / median "Median#Age(Yrs)#" width=14;      |                                              */
    /*  900  40  |                                                             |                                              */
    /*           |                                                             |                                              */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options validvarname=upcase;
    libname sd1 "d:/sd1";

    data sd1.have;

      do rec=100 to 900 by 100;
         age=int(40*uniform(9876))+10;
         output;
      end;

    run;quit;
    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* SD1.HAVE total obs=9                                                                                                   */
    /*                                                                                                                        */
    /* Obs    REC    AGE                                                                                                      */
    /*                                                                                                                        */
    /*  1     100     37                                                                                                      */
    /*  2     200     33                                                                                                      */
    /*  3     300     36                                                                                                      */
    /*  4     400     42                                                                                                      */
    /*  5     500     39                                                                                                      */
    /*  6     600     33                                                                                                      */
    /*  7     700     28                                                                                                      */
    /*  8     800     49                                                                                                      */
    /*  9     900     40                                                                                                      */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                                                                     _
    __      ___ __  ___   _ __  _ __ ___   ___   _ __ ___ _ __   ___  _ __| |_
    \ \ /\ / / `_ \/ __| | `_ \| `__/ _ \ / __| | `__/ _ \ `_ \ / _ \| `__| __|
     \ V  V /| |_) \__ \ | |_) | | | (_) | (__  | | |  __/ |_) | (_) | |  | |_
      \_/\_/ | .__/|___/ | .__/|_|  \___/ \___| |_|  \___| .__/ \___/|_|   \__|
             |_|         |_|                             |_|
    */

    %utl_submit_wps64x('
    libname sd1 "d:/sd1";
    Proc Report Data=sd1.have(obs=100) split="#";
    title "Trial ABC: Patient Minimun, Maximum and Median Age";
     Column
           Age=Age_min
           Age=Age_med
           Age=Age_max
     ;
    Define Age_min  / min  "Min#Age(Yrs)#"  width=14;
    Define Age_max  / max  "Max#Age(Yrs)#"  width=14;
    Define Age_med  / median "Median#Age(Yrs)#" width=14;
    run;quit;
    ');

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Trial ABC: Patient Minimun, Maximum and Median Age                                                                     */
    /*                                                                                                                        */
    /*         Min      Median Car             Max                                                                            */
    /*    Age(Yrs)        Age(Yrs)        Age(Yrs)                                                                            */
    /*                                                                                                                        */
    /*          28              37              49                                                                            */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

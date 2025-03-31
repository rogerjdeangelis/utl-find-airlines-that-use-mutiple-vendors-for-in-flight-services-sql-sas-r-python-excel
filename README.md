# utl-find-airlines-that-use-mutiple-vendors-for-in-flight-services-sql-sas-r-python-excel
Find airlines that use mutiple vendors for in flight services sql sas r python excel 
    %let pgm=utl-find-airlines-that-use-mutiple-vendors-for-in-flight-services-sql-sas-r-python-excel;

    %stop_submission;

    Find airlines that use mutiple vendors for in flight services sql sas r python excel;

    https://communities.sas.com/t5/SAS-Procedures/Finding-inconsistencies-within-a-group/m-p/841506#M82174


      CONTENTS

          1 sas sql
            ksharp
            https://communities.sas.com/t5/user/viewprofilepage/user-id/18408

          2 sql r python excel
            only r presented same code in python and excel
            see
            https://tinyurl.com/4e6yaap8

    github
    https://tinyurl.com/mr4bf6t2
    https://github.com/rogerjdeangelis/utl-find-airlines-that-use-mutiple-vendors-for-in-flight-services-sql-sas-r-python-excel

    related (use for python and excel solutions to this problem - use same sql code
    github
    https://tinyurl.com/4e6yaap8
    https://github.com/rogerjdeangelis/utl-identify-changes-in-all-variable-values-between-phase1-and-phase2-trials

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*             INPUT                  |        PROCESS                          |   OUTPUT                                */
    /*             =====                  |        =======                          |                                         */
    /*                                    |                                         |                                         */
    /*   PLAN  PRODUCT VENDOR LOCALVENDOR | 1 SAS SQL                               |  PLAN  PRODUCT VENDOR LOCALVENDOR       */
    /*                                    | ==========                              |                                         */
    /*   DELTA  WIFI     NY     ALBANY    |                                         |  DELTA  WIFI     NY     HUDSON          */
    /*   DELTA  WIFI     NY     ALBANY    | proc sql;                               |  DELTA  WIFI     NY     ALBANY          */
    /*   DELTA  WIFI     NY     HUDSON**  |   create                                |  DELTA  WIFI     NY     ALBANY          */
    /*                                    |     table want as                       |                                         */
    /*   TRANS  NUTS     GA     ROSWEL    |   select                                |                                         */
    /*   TRANS  NUTS     GA     ROSWEL    |      Plan                               |                                         */
    /*                                    |     ,Product                            |                                         */
    /*   ** more than one local vendor    |     ,Vendor                             |                                         */
    /*                                    |     ,LocalVendor                        |                                         */
    /*  options validvarname=upcase;      |   from                                  |                                         */
    /*  libname sd1 "d:/sd1";             |      sd1.have                           |                                         */
    /*  data sd1.have;                    |   group                                 |                                         */
    /*    infile datalines truncover;     |      by plan, product                   |                                         */
    /*    input                           |   having                                |                                         */
    /*    (Plan Product Vendor            |      count(distinct                     |                                         */
    /*      LocalVendor) ($);             |      cats(Vendor,LocalVendor))>1        |                                         */
    /*  cards4;                           | ;quit;                                  |                                         */
    /*  DELTA WIFI NY  ALBANY             |                                         |                                         */
    /*  DELTA WIFI NY  ALBANY             |-----------------------------------------------------------------------------------*/
    /*  DELTA WIFI NY  HUDSON             |                                         |                                         */
    /*  TRANS NUTS GA  ROSWEL             | 2 SQL R PYTHON EXCEL                    |                                         */
    /*  TRANS NUTS GA  ROSWEL             | ====================                    |  PLAN  PRODUCT VENDOR LOCALVENDOR       */
    /*  ;;;;                              | for python  excel see                   |                                         */
    /*  run;quit;                         | https://tinyurl.com/4e6yaap8            |  DELTA  WIFI     NY     HUDSON          */
    /*                                    | sqllite does do automatic remerging     |  DELTA  WIFI     NY     ALBANY          */
    /*                                    |                                         |  DELTA  WIFI     NY     ALBANY          */
    /*                                    | %utl_rbeginx;                           |                                         */
    /*                                    | parmcards4;                             |                                         */
    /*                                    | library(haven)                          |                                         */
    /*                                    | library(sqldf)                          |                                         */
    /*                                    | source("c:/oto/fn_tosas9x.R")           |                                         */
    /*                                    | have<-read_sas("d:/sd1/have.sas7bdat")  |                                         */
    /*                                    | have                                    |                                         */
    /*                                    | want <- sqldf('                         |                                         */
    /*                                    |   with                                  |                                         */
    /*                                    |      grp as (                           |                                         */
    /*                                    |   select                                |                                         */
    /*                                    |      Plan                               |                                         */
    /*                                    |     ,Product                            |                                         */
    /*                                    |   from                                  |                                         */
    /*                                    |      have                               |                                         */
    /*                                    |   group                                 |                                         */
    /*                                    |       by plan, product                  |                                         */
    /*                                    |   having                                |                                         */
    /*                                    |       count(distinct                    |                                         */
    /*                                    |         Vendor||LocalVendor)>1 )        |                                         */
    /*                                    |   select                                |                                         */
    /*                                    |      l.Plan                             |                                         */
    /*                                    |     ,l.Product                          |                                         */
    /*                                    |     ,l.Vendor                           |                                         */
    /*                                    |     ,l.LocalVendor                      |                                         */
    /*                                    |   from                                  |                                         */
    /*                                    |     have as l inner join grp as r       |                                         */
    /*                                    |   on                                    |                                         */
    /*                                    |         l. Plan   = r. Plan             |                                         */
    /*                                    |     and l.Product = r.Product           |                                         */
    /*                                    |  ')                                     |                                         */
    /*                                    | print(want)                             |                                         */
    /*                                    | fn_tosas9x(                             |                                         */
    /*                                    |       inp    = want                     |                                         */
    /*                                    |      ,outlib ="d:/sd1/"                 |                                         */
    /*                                    |      ,outdsn ="want"                    |                                         */
    /*                                    |      )                                  |                                         */
    /*                                    | ;;;;                                    |                                         */
    /*                                    | %utl_rendx;                             |                                         */
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
       infile datalines truncover;
       input
       (Plan Product Vendor
         LocalVendor) ($);
     cards4;
     DELTA WIFI NY  ALBANY
     DELTA WIFI NY  ALBANY
     DELTA WIFI NY  HUDSON
     TRANS NUTS GA  ROSWEL
     TRANS NUTS GA  ROSWEL
     ;;;;
     run;quit;

    /**************************************************************************************************************************/
    /* PLAN  PRODUCT VENDOR LOCALVENDOR                                                                                       */
    /*                                                                                                                        */
    /* DELTA  WIFI     NY     ALBANY                                                                                          */
    /* DELTA  WIFI     NY     ALBANY                                                                                          */
    /* DELTA  WIFI     NY     HUDSON**                                                                                        */
    /*                                                                                                                        */
    /* TRANS  NUTS     GA     ROSWEL                                                                                          */
    /* TRANS  NUTS     GA     ROSWEL                                                                                          */
    /*                                                                                                                        */
    /* ** more than one local vendor                                                                                          */
    /**************************************************************************************************************************/

    /*                             _
    / |  ___  __ _ ___   ___  __ _| |
    | | / __|/ _` / __| / __|/ _` | |
    | | \__ \ (_| \__ \ \__ \ (_| | |
    |_| |___/\__,_|___/ |___/\__, |_|
                                |_|
    */

    proc sql;
      create
        table want as
      select
         Plan
        ,Product
        ,Vendor
        ,LocalVendor
      from
         sd1.have
      group
         by plan, product
      having
         count(distinct
         cats(Vendor,LocalVendor))>1
    ;quit;

    /**************************************************************************************************************************/
    /* PLAN  PRODUCT VENDOR LOCALVENDOR                                                                                       */
    /*                                                                                                                        */
    /* DELTA  WIFI     NY     HUDSON                                                                                          */
    /* DELTA  WIFI     NY     ALBANY                                                                                          */
    /* DELTA  WIFI     NY     ALBANY                                                                                          */
    /**************************************************************************************************************************/

    /*___              _                      _   _                                    _
    |___ \   ___  __ _| |  _ __   _ __  _   _| |_| |__   ___  _ __    _____  _____ ___| |
      __) | / __|/ _` | | | `__| | `_ \| | | | __| `_ \ / _ \| `_ \  / _ \ \/ / __/ _ \ |
     / __/  \__ \ (_| | | | |    | |_) | |_| | |_| | | | (_) | | | ||  __/>  < (_|  __/ |
    |_____| |___/\__, |_| |_|    | .__/ \__, |\__|_| |_|\___/|_| |_| \___/_/\_\___\___|_|
                    |_|          |_|    |___/
    */

    %utl_rbeginx;
    parmcards4;
    library(haven)
    library(sqldf)
    source("c:/oto/fn_tosas9x.R")
    have<-read_sas("d:/sd1/have.sas7bdat")
    have
    want <- sqldf('
      with
         grp as (
      select
         Plan
        ,Product
      from
         have
      group
          by plan, product
      having
          count(distinct
            Vendor||LocalVendor)>1 )
      select
         l.Plan
        ,l.Product
        ,l.Vendor
        ,l.LocalVendor
      from
        have as l inner join grp as r
      on
            l. Plan   = r. Plan
        and l.Product = r.Product
     ')
    print(want)
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="want"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.want;
    run;quit;

    /**************************************************************************************************************************/
    /*  ROWNAMES    PLAN     PRODUCT    VENDOR    LOCALVENDOR                                                                 */
    /*                                                                                                                        */
    /*      1       DELTA     WIFI        NY        ALBANY                                                                    */
    /*      2       DELTA     WIFI        NY        ALBANY                                                                    */
    /*      3       DELTA     WIFI        NY        HUDSON                                                                    */
    /**************************************************************************************************************************/

    /*           _ _
      __ _ _   _(_) |_
     / _` | | | | | __|
    | (_| | |_| | | |_
     \__, |\__,_|_|\__|
        |_|
    */

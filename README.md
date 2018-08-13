# utl_another_nice_example_of_dow_loop_rate_of_change_by_group
Another nice example of dow loop rate of change by group.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Another nice example of dow loop rate of change by group

    see
    https://tinyurl.com/y9e9wfcg
    https://github.com/rogerjdeangelis/utl_another_nice_example_of_dow_loop_rate_of_change_by_group

    https://tinyurl.com/ycmg3fdq
    https://communities.sas.com/t5/Base-SAS-Programming/fill-in-the-gaps-between-sequential/m-p/486355

    https://communities.sas.com/t5/user/viewprofilepage/user-id/4877

    INPUT
    =====

    WORK.HAVE total obs=4   |       RULES
                            |       =====     Average
                            |                 Rate of
      ID    MONTH    VAR1   |  ID    MONTH    Change
                            |
       1       4       2    |   1       6       3    3 = (8 - 2)/(6 - 4) =6/2
       1       6       8    |   1       7       3
                            |   1       8       3
                            |
       2       9       0    |   2       9       2    2 = (8 -0 )/(13 - 9) = 8/4
       2      13       8    |   2      10       2
                            |   2      11       2
                            |   2      12       2
                            |   2      13       2

    EXAMPLE OUTPUT
    ---------------

    WORK.WANT total obs=8

      ID    MONTH    RATEOFCHANGE

       1       4           3
       1       5           3
       1       6           3

       2       9           2
       2      10           2
       2      11           2
       2      12           2
       2      13           2


    PROCESS
    =======


    * I made some slight changes;
    data want;

     do until (last.id);

       set have;
       by id;

       if first.id then do;
         _from=month;
         _d1=var1;
       end;

     end;

     RateOfChange=(var1-_d1)/(month-_from);
     mth=month;

     do until (last.id);
       set have;
       by id;

       if first.id then do;
          do month=_from to mth;
            output;
          end;
       end;
     end;

     keep id month RateOfChange;

    run;quit;

    *                _               _       _
     _ __ ___   __ _| | _____     __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|

    ;

    data have;
     input id month var1;
    cards4;
    1 4  2
    1 6  8
    2 9  0
    2 13 8
    ;;;;
    run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    see process

    data want;

     do until (last.id);
       set have;
       by id;

       if first.id then do;
         _from=month;
         _d1=var1;
       end;

       if last.id then do;
         _to=month;
         _d2=var1;
        end;

     RateOfChange=(_d2-_d1)/(_to-_from);

     do until (last.id);
       set have;
       by id;

       if first.id then do;
          do month=_from to _to;
            output;
          end;
       end;

     keep id month RateOfChange;

    run;





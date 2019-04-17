# utl-share-sas-global-macros-across-sessions-and-users
Share SAS global macros across sessions and users
    Share SAS global macros across sessions and users

    github
    https://tinyurl.com/y4yujmlg
    https://github.com/rogerjdeangelis/utl-share-sas-global-macros-across-sessions-and-users


      Somewaat complicated

        1. Open a sas session
        2. Do the following
           libname storemac "d:/sd1";
           options mstored sasmstore=storemac ;

           %macro globals(dummy)/des="sharded global macro variables" store source;
             %global __one __two __tre;

             %let __one=1;
             %let __two=2;
             %let __tre=3;

           %mend globals;

        3. Close the session because SAS has lock on storemac and
           storemac cannot be closed and opened readonly or
           used in another session.

        4. Open two SAS sessions and run the code below

           libname storemac "d:/sd1" access=readonly;
           options mstored sasmstore=storemac ;

           %globals;

           %put &=__one;
           %put &=__two;
           %put &=__tre;


        5. In each session you should see

           __ONE=1
           __TWO=2
           __TRE=3


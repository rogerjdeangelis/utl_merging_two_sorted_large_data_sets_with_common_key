# utl_merging_two_sorted_large_data_sets_with_common_key
Efficiently Merging Two Large Sorted Data Sets With Some Common Variables. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Efficiently Merging Two Large Sorted Data Sets With Some Common Variables

    see
    https://goo.gl/uY4xpk
    https://github.com/rogerjdeangelis/utl_merging_two_sorted_large_data_sets_with_common_key

    For small daatsets like these I like to use a single SQL (join took a little over 4 minutes).
    No need to patition and run parallel tasks.
    Run on my 10 year old desktop.

    NOTE: Table WORK.WANT created, with 120000 rows and 118 columns.

    NOTE: PROCEDURE SQL used (Total process time):
    real time           4:13.13


    see
    https://goo.gl/QyD9XG
    https://communities.sas.com/t5/General-SAS-Programming/Efficiently-Merging-Two-Large-Data-Sets-With-Some-Common/m-p/431464

    INPUT  ( Two datsets

     F._2004  DATASET 46 variables Total Obs 68,000,500
     ====================================================

     F._2004  Middle Observation(34,000,250 ) of f._2004 - Total Obs 68,000,500

      Primary Key  (sorted 45 variables)

                                       VALUE

        YEAR                C  4       2003
        MSA                 C  1       B
        COUNTYCODE          C  2       16
        STATE               C  2       VT
        LOAN_AMOUNT         N  8       27200000


         -- CHARACTER --
        A1                  C 8       12345678
        A2                  C 8       12345678
        A3                  C 8       12345678
        A4                  C 8       12345678
        A5                  C 8       12345678
        A6                  C 8       12345678
        A7                  C 8       12345678
        A8                  C 8       12345678
        A9                  C 8       12345678
        A10                 C 8       12345678
        A11                 C 8       12345678
        A12                 C 8       12345678
        A13                 C 8       12345678
        A14                 C 8       12345678
        A15                 C 8       12345678
        A16                 C 8       12345678
        A17                 C 8       12345678
        A18                 C 8       12345678
        A19                 C 8       12345678
        A20                 C 8       12345678


         -- NUMERIC --
        N1                  N 8       12345678
        N2                  N 8       12345678
        N3                  N 8       12345678
        N4                  N 8       12345678
        N5                  N 8       12345678
        N6                  N 8       12345678
        N7                  N 8       12345678
        N8                  N 8       12345678
        N9                  N 8       12345678
        N10                 N 8       12345678
        N11                 N 8       12345678
        N12                 N 8       12345678
        N13                 N 8       12345678
        N14                 N 8       12345678
        N15                 N 8       12345678
        N16                 N 8       12345678
        N17                 N 8       12345678
        N18                 N 8       12345678
        N19                 N 8       12345678
        N20                 N 8       12345678


      G.C2FINA  dataset 73 varables Total Obs 24,000,000
      ==================================================

       Middle Observation(12000000 ) of g.c2final - Total Obs 24,000,000
                                       VALUE

       RYEAR               C 4       2003
       RMSA                C 1       B
       RCOUNTYCODE         C 2       16
       RSTATE              C 2       VT
       RLOAN_AMOUNT        N 8       27200000

          -- CHARACTER --
        B1                 C 8       12345678
        B2                 C 8       12345678
        B3                 C 8       12345678
        B4                 C 8       12345678
        B5                 C 8       12345678
        B6                 C 8       12345678
        B7                 C 8       12345678
        B8                 C 8       12345678
        B9                 C 8       12345678
        B10                C 8       12345678
        B11                C 8       12345678
        B12                C 8       12345678
        B13                C 8       12345678
        B14                C 8       12345678
        B15                C 8       12345678
        B16                C 8       12345678
        B17                C 8       12345678
        B18                C 8       12345678
        B19                C 8       12345678
        B20                C 8       12345678
        B21                C 8       12345678
        B22                C 8       12345678
        B23                C 8       12345678
        B24                C 8       12345678
        B25                C 8       12345678
        B26                C 8       12345678
        B27                C 8       12345678
        B28                C 8       12345678
        B29                C 8       12345678
        B30                C 8       12345678
        B31                C 8       12345678
        B32                C 8       12345678
        B33                C 8       12345678
        B34                C 8       12345678
        B35                C 8       12345678
        B36                C 8       12345678
        B37                C 8       12345678
        B38                C 8       12345678
        B39                C 8       12345678
        B40                C 8       12345678

         -- NUMERIC --
        M1                 N 8       12345678
        M2                 N 8       12345678
        M3                 N 8       12345678
        M4                 N 8       12345678
        M5                 N 8       12345678
        M6                 N 8       12345678
        M7                 N 8       12345678
        M8                 N 8       12345678
        M9                 N 8       12345678
        M10                N 8       12345678
        M11                N 8       12345678
        M12                N 8       12345678
        M13                N 8       12345678
        M14                N 8       12345678
        M15                N 8       12345678
        M16                N 8       12345678
        M17                N 8       12345678
        M18                N 8       12345678
        M19                N 8       12345678
        M20                N 8       12345678
        M21                N 8       12345678
        M22                N 8       12345678
        M23                N 8       12345678
        M24                N 8       12345678
        M25                N 8       12345678
        M26                N 8       12345678
        M27                N 8       12345678
        M28                N 8       12345678


    PROCESS (All the code)
    ======================

      proc sql;
        create
          table want as
        select
          l.*
         ,r.*
        from
          f._2004    as l
          ,g.c2final as r
        where
          l.Year         = r.rYear         and
          l.MSA          = r.rMSA          and
          l.CountyCode   = r.rCountyCode   and
          l.state        = r.rstate        and
          l.Loan_Amount  = r.rLoan_Amount
      ;quit;

    OUTPUT
    ======

     WORK.WANT 118 variables and 120,000 observations

       Middle Observation(60000 ) of want - Total Obs 120,000

       YEAR             C 4       2003
       MSA              C 1       B
       COUNTYCODE       C 2       16
       STATE            C 2       VT
       LOAN_AMOUNT      N 8       48000

       RYEAR            C 4       2003
       RMSA             C 1       B
       RCOUNTYCODE      C 2       16
       RSTATE           C 2       VT
       RLOAN_AMOUNT     N 8       48000

        -- CHARACTER --
       A1               C 8       12345678
       A2               C 8       12345678
       A3               C 8       12345678
       A4               C 8       12345678
       A5               C 8       12345678
       A6               C 8       12345678
       A7               C 8       12345678
       A8               C 8       12345678
       A9               C 8       12345678
       A10              C 8       12345678
       A11              C 8       12345678
       A12              C 8       12345678
       A13              C 8       12345678
       A14              C 8       12345678
       A15              C 8       12345678
       A16              C 8       12345678
       A17              C 8       12345678
       A18              C 8       12345678
       A19              C 8       12345678
       A20              C 8       12345678
       B1               C 8       12345678
       B2               C 8       12345678
       B3               C 8       12345678
       B4               C 8       12345678
       B5               C 8       12345678
       B6               C 8       12345678
       B7               C 8       12345678
       B8               C 8       12345678
       B9               C 8       12345678
       B10              C 8       12345678
       B11              C 8       12345678
       B12              C 8       12345678
       B13              C 8       12345678
       B14              C 8       12345678
       B15              C 8       12345678
       B16              C 8       12345678
       B17              C 8       12345678
       B18              C 8       12345678
       B19              C 8       12345678
       B20              C 8       12345678
       B21              C 8       12345678
       B22              C 8       12345678
       B23              C 8       12345678
       B24              C 8       12345678
       B25              C 8       12345678
       B26              C 8       12345678
       B27              C 8       12345678
       B28              C 8       12345678
       B29              C 8       12345678
       B30              C 8       12345678
       B31              C 8       12345678
       B32              C 8       12345678
       B33              C 8       12345678
       B34              C 8       12345678
       B35              C 8       12345678
       B36              C 8       12345678
       B37              C 8       12345678
       B38              C 8       12345678
       B39              C 8       12345678
       B40              C 8       12345678


        -- NUMERIC --
       N1               N 8       12345678
       N2               N 8       12345678
       N3               N 8       12345678
       N4               N 8       12345678
       N5               N 8       12345678
       N6               N 8       12345678
       N7               N 8       12345678
       N8               N 8       12345678
       N9               N 8       12345678
       N10              N 8       12345678
       N11              N 8       12345678
       N12              N 8       12345678
       N13              N 8       12345678
       N14              N 8       12345678
       N15              N 8       12345678
       N16              N 8       12345678
       N17              N 8       12345678
       N18              N 8       12345678
       N19              N 8       12345678
       N20              N 8       12345678
       M1               N 8       12345678
       M2               N 8       12345678
       M3               N 8       12345678
       M4               N 8       12345678
       M5               N 8       12345678
       M6               N 8       12345678
       M7               N 8       12345678
       M8               N 8       12345678
       M9               N 8       12345678
       M10              N 8       12345678
       M11              N 8       12345678
       M12              N 8       12345678
       M13              N 8       12345678
       M14              N 8       12345678
       M15              N 8       12345678
       M16              N 8       12345678
       M17              N 8       12345678
       M18              N 8       12345678
       M19              N 8       12345678
       M20              N 8       12345678
       M21              N 8       12345678
       M22              N 8       12345678
       M23              N 8       12345678
       M24              N 8       12345678
       M25              N 8       12345678
       M26              N 8       12345678
       M27              N 8       12345678
       M28              N 8       12345678

    *                _               _       _
     _ __ ___   __ _| | _____     __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|

    ;

    libname f "f:/wrk";
    data f._2004;

       array as[20] $8 a1-a20 (20*'12345678');
       array ns[20] n1-n20 (20*12345678);

       do year='2001','2002','2003','2004','2005';
          do MSA='A','B','C','D';
             do CountyCode='12','13','14','15','16';
                do State='AK','AL','CA','VT','TX';
                   do Loan_Amount=0 to 27200000 by 200;
                     output;
                   end;
                end;
             end;
          end;
       end;

    run;quit;

    proc sort data=f._2004 force;
    by Year MSA CountyCode state Loan_Amount;
    run;quit;


    libname g "g:/wrk";
    data g.c2final;

       array as[40] $8 b1-b40 (40*'12345678');
       array ns[28]    m1-m28 (28*12345678);

       do ryear='2001','2002','2003','2004','2005';
          do rMSA='A','B','C','D';
             do rCountyCode='12','13','14','15','16';
                do rState='AK','AL','CA','VT','TX';
                   do rLoan_Amount=1 to 48000 by 1;
                         output;
                   end;
                end;
             end;
          end;
       end;

    run;quit;

    proc sort data=g.c2final force;
    by rYear rMSA rCountyCode rstate rLoan_Amount;
    run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    proc sql;
      create
        table want as
      select
        l.*
       ,r.*
      from
        f._2004    as l
        ,g.c2final as r
      where
        l.Year         = r.rYear         and
        l.MSA          = r.rMSA          and
        l.CountyCode   = r.rCountyCode   and
        l.state        = r.rstate        and
        l.Loan_Amount  = r.rLoan_Amount
    ;quit;


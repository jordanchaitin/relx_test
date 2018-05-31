=================================================================================
This is a set of instructions to test if Episcina breaks on using the latest relx
=================================================================================
1.  Extract the contents from the tar file and first update the rel/sys.config file     with your postgres database details.
2.  In the main dir relx_test enter the command gmake run
3.  Enter pp_db:simple_query("select 1"). at the erlang prompt and see that it works.
4.  Exit erlang
5.  gmake distclean
6.  Now open erlang.mk and go to line 6710-11.
7.  Comment out the line where the RELX_URL refers to the old relx
8.  Uncomment the line where the RELX_URL refers to the new relx
9.  Save and exit
10. Repeat the steps in 2. An error similar to the one below should be seen

=================================================================================
sample error message
=================================================================================
1> pp_db:simple_query("select 1").
** exception error: timeout
in function  gproc:await/2
   called as gproc:await({n,l,{epna_pool,primary}},10000)
in call from timer:tc/3 (timer.erl, line 197)
in call from epna_pool:get_connection/2 (src/epna_pool.erl, line 86)
in call from pp_db:get_connection/1 (src/pp_db.erl, line 16)
in call from pp_db:simple_query/1 (src/pp_db.erl, line 38) ))))}})"")
~
~

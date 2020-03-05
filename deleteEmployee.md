process before output.
 module status_9006.
*
process after input.
 module user_command_9006.

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_STATUS_9006O01 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  STATUS_9006  OUTPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module status_9006 output.
  set pf-status 'ZSTATUS6'.
  set titlebar 'ZTITLE6'.








endmodule.                 " STATUS_9006  OUTPUT

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_USER_COMMAND_900I07 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  USER_COMMAND_9006  INPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module user_command_9006 input.

  case ok_admin.
    when 'HOME'.
      call screen 9000.
    when 'BACK'.
      call screen 9001.
    when 'DELETE'.
      try .
        zca_project=>agent->delete_persistent(
     i_zemp_id = deleteempid
   ).

commit work.

catch cx_os_object_not_existing.
  message  'USER NOT EXISTS' type 'I'.
endtry.



    when others.
      leave to screen 0.
  endcase.

endmodule.                 " USER_COMMAND_9006  INPUT




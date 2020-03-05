process before output.
 module status_9010.

process after input.
 module user_command_9010.

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_STATUS_9010O01 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  STATUS_9010  OUTPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module status_9010 output.
  set pf-status 'ZSTATUS10'.
  set titlebar 'ZTITLE10'.

    nopension = message.

endmodule.                 " STATUS_9010  OUTPUT

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_USER_COMMAND_901I01 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  USER_COMMAND_9010  INPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module user_command_9010 input.

  case ok_hr.
    when 'HOME'.
      call screen 9000.
    when 'BACK'.
      call screen 9002.
    when others.
      leave to screen 0.
   endcase.

endmodule.                 " USER_COMMAND_9010  INPUT




process before output.
  module status_9001.
*
process after input.
 module user_command_9001.

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_STATUS_9001O01 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  STATUS_9001  OUTPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module status_9001 output.
   set pf-status 'ZSTATUS1'.
   set titlebar 'ZTITLE1'.

endmodule.                 " STATUS_9001  OUTPUT

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_USER_COMMAND_900I02 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  USER_COMMAND_9001  INPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module user_command_9001 input.

  case ok_admin.
    when 'ADD'.
      call screen 9004.
    when 'UPDATE'.
      call screen 9005.
    when 'DELETE'.
      call screen 9006.
    when 'VIEW_ALL'.
      call screen 9007.
    when 'VIEW'.
      call screen 9008.
    when 'HOME'.
      call screen 9000.
    when 'BACK'.
      call screen 9000.

    when others.
      leave to screen 0.
  endcase.

endmodule.                 " USER_COMMAND_9001  INPUT





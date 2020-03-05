process before output.
  module status_9000.
*
process after input.
  module user_command_9000.

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_STATUS_9000O01 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  STATUS_9000  OUTPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module status_9000 output.
   set pf-status 'ZSTATUS'.
   set titlebar 'ZTITLE'.

endmodule.                 " STATUS_9000  OUTPUT

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_USER_COMMAND_900I01 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  USER_COMMAND_9000  INPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module user_command_9000 input.
  case ok_code.
    when 'ADMIN'.
        call screen 9001.
    when 'HR'.
        call screen 9003.
     when 'EMPLOYEE'.
       call screen 9002.
    when others.
      leave to screen 0.
  endcase.

endmodule.                 " USER_COMMAND_9000  INPUT




process before output.
 module status_9003.
*
process after input.
 module user_command_9003.

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_STATUS_9003O01 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  STATUS_9003  OUTPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module status_9003 output.
 set pf-status 'ZSTATUS3'.
 set titlebar 'ZTITLE3'.

endmodule.                 " STATUS_9003  OUTPUT

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_USER_COMMAND_900I03 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  USER_COMMAND_9003  INPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module user_command_9003 input.
  case ok_hr.
    when 'HR_UPDATE'.
      call screen 9005.
      when 'HR_VIEWALL'.
      call screen 9007.
      when 'HR_VIEW'.
      call screen 9008.
    when 'HOME'.
      call screen 9000.
    when 'BACK'.
      call screen 9000.

    when others.
      leave to screen 0.

  endcase.

endmodule.                 " USER_COMMAND_9003  INPUT




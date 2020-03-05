process before output.
 module status_9005.
*
process after input.
 module user_command_9005.

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_STATUS_9005O01 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  STATUS_9005  OUTPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module status_9005 output.
  set pf-status 'ZSTATUS5'.
  set titlebar 'ZTITLE5'.

endmodule.                 " STATUS_9005  OUTPUT

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_USER_COMMAND_900I06 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  USER_COMMAND_9005  INPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module user_command_9005 input.

  case ok_admin.
    when 'HOME'.
      call screen 9000.
    when 'BACK'.
      call screen 9001.
    when 'UPDATE'.
      try.
         data: project_obj type ref to zcl_project.
          project_obj = zca_project=>agent->get_persistent(
                                    i_zemp_id = updateempid
                                   ).
          call method project_obj->set_zemp_salary( updatesalary ).
          commit work.
        catch cx_os_object_not_found.
           message  'USER NOT EXISTS' type 'I'.
    endtry.
  when others.
      leave to screen 0.
  endcase.

endmodule.                 " USER_COMMAND_9005  INPUT




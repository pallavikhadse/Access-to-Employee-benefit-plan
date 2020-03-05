process before output.
 module status_9004.
*
process after input.
 module user_command_9004.

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_STATUS_9004O01 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  STATUS_9004  OUTPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module status_9004 output.
  set pf-status 'ZSTATUS4'.
  set titlebar 'ZTITLE4'.

endmodule.                 " STATUS_9004  OUTPUT

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_USER_COMMAND_900I05 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  USER_COMMAND_9004  INPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module user_command_9004 input.

  case ok_admin.
    when 'HOME'.
      call screen 9000.
    when 'BACK'.
      call screen 9001.

    when 'ADD_EMP'.
      data:
            lv_number_range type znewempid,    "-- Variable to hold Newly generated Number Range
            lv_rc type inri-returncode.            "-- Variable to hold the Return Code
            call function 'NUMBER_GET_NEXT'
  exporting
    nr_range_nr             = '01'                "-- This hold the Newly generated Number
    object                  = 'ZEMPID'       "---- Passing the Number Range Object

  importing
    number                  = lv_number_range "-- Newly generated Number
    returncode              = lv_rc                   "-- The Return Code Number
  exceptions
    interval_not_found      = 1
    number_range_not_intern = 2
    object_not_found        = 3
    quantity_is_0           = 4
    quantity_is_not_1       = 5
    interval_overflow       = 6
    buffer_overflow         = 7
    others                  = 8.
if sy-subrc <> 0.
  message id sy-msgid type sy-msgty number sy-msgno
          with sy-msgv1 sy-msgv2 sy-msgv3 sy-msgv4.
endif.

      try.

          new_emp_agent = zca_project=>agent.
          new_emp = new_emp_agent->create_persistent(
          i_zemp_id = lv_number_range
          i_zemp_firstname = emp_firstname
          i_zemp_lastname = emp_lastname
          i_zemp_address = emp_address
          i_zemp_phone = emp_phone
          i_zemp_dob =  emp_dob
          i_zemp_emailid = emp_emailid
          i_zemp_startdate = emp_startdate
          i_zemp_position = emp_position
          i_zemp_department = emp_department
          i_zemp_salary = emp_salary

          ).

          commit work.
          if sy-subrc = 4.
             message  'USER ALREADY EXISTS' type 'I'.
              endif.

        catch cx_os_object_not_found.
          " Error handling comes here
      endtry.
      call screen 9001.

    when others.
      leave to screen 9000.
  endcase.

endmodule.                 " USER_COMMAND_9004  INPUT




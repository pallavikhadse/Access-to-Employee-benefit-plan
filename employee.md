process before output.
  module status_9002.
*
process after input.
  module user_command_9002.

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_STATUS_9002O01 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  STATUS_9002  OUTPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module status_9002 output.
  set pf-status 'ZSTATUS2'.
  set titlebar 'ZTITLE2'.
    clear : pension,
            insurance,
            special.
     pension = totalval5.
     insurance = message1.
     special = message2.
     pf = message3.
endmodule.                 " STATUS_9002  OUTPUT

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_USER_COMMAND_900I04 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  USER_COMMAND_9002  INPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module user_command_9002 input.
  case ok_employee.
    when 'HOME'.
      clear:zempid,
            pension,
            totalval5,
            insurance,
            special,
            message1,
            message2,
            message3.
      call screen 9000.

    when 'EMPVIEW'.

      data: in_table6 type standard table of zprojectrs,
               row6 type zprojectrs,
               zemp_dob type zempdob,
               zemp_salary type zempsalary,
               newdate type zempdob,
               zemp_firstname type zprojectrs,
               age type integer,
               zempage type integer,
               zsalary type zempsalary,
               totalval1 type decfloat34,
               totalval2 type decfloat34,
               totalval3 type decfloat34,
               totalval4 type decfloat34.



      select * from zprojectrs into table in_table6 where zemp_id = zempid.

      loop at in_table6 into row6.
        newdate = row6-zemp_dob.
        zsalary = row6-zemp_salary.
      endloop.
      if row6-zemp_dob ne 00000000.
      call function 'ZEMPAGE'
        exporting
          zemp_dob = row6-zemp_dob
        importing
          zemp_age = age.
      endif.
      if age ge 60.
        totalval1 = zsalary * 20.
        totalval2 = totalval1 / 100.
        totalval3 = zsalary -  totalval2.
        totalval4 = totalval3 / 12.      ""SAL PER MONTH
        totalval5 = totalval4 / 2.          ""PENSION PER MONTH
        message1 = 'Medical Insurance for family(Self + Spouse) Euro 5000'.
        message2 = 'Special allowance for Employee with Tenure more than 30 Years'.
        message3 = 'Gratuity(PF) 5% of salary for number of working years'.
      else.
        message = 'Currently not eligible for Pension. Pension benefit will be available one year prior to Retirement '.
        call screen 9010.
      endif.

    when others.
      leave to screen 0.
  endcase.

endmodule.                 " USER_COMMAND_9002  INPUT



*&---------------------------------------------------------------------*
*& Module Pool       ZPROJECTRS
*&
*&---------------------------------------------------------------------*
*&
*&
*&---------------------------------------------------------------------*

program  zprojectrs.
data: ok_code type sy-ucomm,
      ok_admin type sy-ucomm,
      ok_employee type sy-ucomm,

      new_emp_agent type ref to zca_project,
      new_emp type ref to zcl_project,
      emp_id type znewempid,
      emp_firstname type zempfirstname,
      emp_lastname type zemplastname,
      emp_address type zempaddress,
      emp_phone type zempphone,
      emp_dob type zempdob,
      emp_emailid type zempemailid,
      emp_startdate type zempstartdate,
      emp_position type zempposition,
      emp_department type zempdepartment,
      emp_salary type zempsalary,

      empage type integer,
      inp_empid type znewempid,
      zemp type znewempid,
      zempview type znewempid,
      zempid type znewempid,
      deleteempid type znewempid,
      updateempid type znewempid,
      updatesalary type zempsalary,
      totalval5 type decfloat34,
      pension type decfloat34,
      nopension type string,
      message type string,
      insurance type string,
      special type string,
      message1 type string,
      message2 type string,
      message3 type string,
      pf type string,
      ok_hr type sy-ucomm.


include zprojectrs_status_9000o01.

include zprojectrs_user_command_900i01.

include zprojectrs_status_9001o01.

include zprojectrs_user_command_900i02.

include zprojectrs_status_9003o01.

include zprojectrs_user_command_900i03.

include zprojectrs_status_9002o01.

include zprojectrs_user_command_900i04.

include zprojectrs_status_9004o01.

include zprojectrs_user_command_900i05.

include zprojectrs_status_9005o01.

include zprojectrs_user_command_900i06.

include zprojectrs_status_9006o01.

include zprojectrs_user_command_900i07.

include zprojectrs_status_9007o01.

include zprojectrs_user_command_900i08.

include zprojectrs_status_9008o01.

include zprojectrs_user_command_900i09.

include zprojectrs_status_9009o01.

include zprojectrs_user_command_900i10.

include zprojectrs_status_9010o01.

include zprojectrs_user_command_901i01.

process before output.
module status_9007.

process after input.
 module user_command_9007.

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_STATUS_9007O01 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  STATUS_9007  OUTPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module status_9007 output.
  set pf-status 'ZSTATUS7'.
  set titlebar 'ZTITLE7'.

data: ls_t type table of zprojectrs,
      row type zprojectrs,
      go_grid type ref to cl_gui_alv_grid,
      go_hr_container type ref to cl_gui_custom_container,
      lt_fcat type lvc_t_fcat,
      ls_fcat type lvc_s_fcat.

  select * from zprojectrs into table ls_t.
  sort ls_t by zemp_id ascending.

  refresh lt_fcat.
  data: lv_pos type i.

  lv_pos = lv_pos + 1.
  ls_fcat-fieldname = 'ZEMP_ID'.
  ls_fcat-coltext = 'EMPLOYEE-ID'.
  ls_fcat-col_pos = lv_pos.
  ls_fcat-outputlen = 3.
  append ls_fcat to lt_fcat.

  lv_pos = lv_pos + 1.
  ls_fcat-fieldname = 'ZEMP_FIRSTNAME'.
  ls_fcat-coltext = 'EMPLOYEE FIRST NAME'.
  ls_fcat-col_pos = lv_pos.
  ls_fcat-outputlen = 20.
  append ls_fcat to lt_fcat.

  lv_pos = lv_pos + 1.
  ls_fcat-fieldname = 'ZEMP_LASTNAME'.
  ls_fcat-coltext = 'EMPLOYEE LAST NAME'.
  ls_fcat-col_pos = lv_pos.
  ls_fcat-outputlen = 20.
  append ls_fcat to lt_fcat.

  lv_pos = lv_pos + 1.
  ls_fcat-fieldname = 'ZEMP_ADDRESS'.
  ls_fcat-coltext = 'ADDRESS'.
  ls_fcat-col_pos = lv_pos.
  ls_fcat-outputlen = 20.
  append ls_fcat to lt_fcat.

  lv_pos = lv_pos + 1.
  ls_fcat-fieldname = 'ZEMP_DOB'.
  ls_fcat-coltext = 'DATE OF BIRTH'.
  ls_fcat-col_pos = lv_pos.
  ls_fcat-outputlen = 20.
  append ls_fcat to lt_fcat.

  lv_pos = lv_pos + 1.
  ls_fcat-fieldname = 'ZEMP_EMAILID'.
  ls_fcat-coltext = 'EMAIL ID'.
  ls_fcat-col_pos = lv_pos.
  ls_fcat-outputlen = 20.
  append ls_fcat to lt_fcat.

  lv_pos = lv_pos + 1.
  ls_fcat-fieldname = 'ZEMP_STARTDATE'.
  ls_fcat-coltext = 'JOINING DATE'.
  ls_fcat-col_pos = lv_pos.
  ls_fcat-outputlen = 20.
  append ls_fcat to lt_fcat.


  lv_pos = lv_pos + 1.
  ls_fcat-fieldname = 'ZEMP_SALARY'.
  ls_fcat-coltext = 'SALARY'.
  ls_fcat-col_pos = lv_pos.
  ls_fcat-outputlen = 20.
  append ls_fcat to lt_fcat.

  lv_pos = lv_pos + 1.
  ls_fcat-fieldname = 'ZEMP_POSITION'.
  ls_fcat-coltext = 'POSITION'.
  ls_fcat-col_pos = lv_pos.
  ls_fcat-outputlen = 20.
  append ls_fcat to lt_fcat.

  lv_pos = lv_pos + 1.
  ls_fcat-fieldname = 'ZEMP_DEPARTMENT'.
  ls_fcat-coltext = 'DEPARTMENT'.
  ls_fcat-col_pos = lv_pos.
  ls_fcat-outputlen = 20.
  append ls_fcat to lt_fcat.


  if go_hr_container is initial.
    create object go_hr_container
      exporting
        container_name = 'Z_EMPLOYEELIST'.
    create object go_grid
      exporting
        i_parent = go_hr_container.
  endif.
  call method go_grid->set_table_for_first_display
    changing
      it_outtab       = ls_t
      it_fieldcatalog = lt_fcat.


endmodule.                 " STATUS_9007  OUTPUT

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_USER_COMMAND_900I08 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  USER_COMMAND_9007  INPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module user_command_9007 input.

  case ok_admin.
     when 'HOME'.
      call screen 9000.
       when 'BACK'.
      call screen 9001.

    when others.
      leave to screen 0.
  endcase.


endmodule.                 " USER_COMMAND_9007  INPUT




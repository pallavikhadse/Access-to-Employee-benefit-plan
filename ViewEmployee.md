process before output.
 module status_9008.
*
process after input.
 module user_command_9008.

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_STATUS_9008O01 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  STATUS_9008  OUTPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module status_9008 output.
  set pf-status 'ZSTATUS8'.
  set titlebar 'ZTITLE8'.


  data:ls_t1 type table of zprojectrs,
      row1 type zprojectrs,
      go_grid1 type ref to cl_gui_alv_grid,
      go_hr_container1 type ref to cl_gui_custom_container,
      lt_fcat1 type lvc_t_fcat,
      ls_fcat1 type lvc_s_fcat.


  select * from zprojectrs into table ls_t1 where zemp_id = zemp.
  sort ls_t1 by zemp_id ascending.

  refresh lt_fcat1.
  data: lv_pos1 type i.

  lv_pos1 = lv_pos1 + 1.
  ls_fcat1-fieldname = 'ZEMP_ID'.
  ls_fcat1-coltext = 'EMPLOYEE-ID'.
  ls_fcat1-col_pos = lv_pos1.
  ls_fcat1-outputlen = 3.
  append ls_fcat1 to lt_fcat1.

  lv_pos1 = lv_pos1 + 1.
  ls_fcat1-fieldname = 'ZEMP_FIRSTNAME'.
  ls_fcat1-coltext = 'EMPLOYEE FIRST NAME'.
  ls_fcat1-col_pos = lv_pos1.
  ls_fcat1-outputlen = 20.
  append ls_fcat1 to lt_fcat1.

  lv_pos1 = lv_pos1 + 1.
  ls_fcat1-fieldname = 'ZEMP_LASTNAME'.
  ls_fcat1-coltext = 'EMPLOYEE LAST NAME'.
  ls_fcat1-col_pos = lv_pos1.
  ls_fcat1-outputlen = 20.
  append ls_fcat1 to lt_fcat1.

  lv_pos1 = lv_pos1 + 1.
  ls_fcat1-fieldname = 'ZEMP_ADDRESS'.
  ls_fcat1-coltext = 'ADDRESS'.
  ls_fcat1-col_pos = lv_pos1.
  ls_fcat1-outputlen = 20.
  append ls_fcat1 to lt_fcat1.

  lv_pos1 = lv_pos1 + 1.
  ls_fcat1-fieldname = 'ZEMP_DOB'.
  ls_fcat1-coltext = 'DATE OF BIRTH'.
  ls_fcat1-col_pos = lv_pos1.
  ls_fcat1-outputlen = 20.
  append ls_fcat1 to lt_fcat1.

  lv_pos1 = lv_pos1 + 1.
  ls_fcat1-fieldname = 'ZEMP_EMAILID'.
  ls_fcat1-coltext = 'EMAIL ID'.
  ls_fcat1-col_pos = lv_pos1.
  ls_fcat1-outputlen = 20.
  append ls_fcat1 to lt_fcat1.

  lv_pos1 = lv_pos1 + 1.
  ls_fcat-fieldname = 'ZEMP_STARTDATE'.
  ls_fcat-coltext = 'JOINING DATE'.
  ls_fcat-col_pos = lv_pos1.
  ls_fcat-outputlen = 20.
  append ls_fcat1 to lt_fcat1.


  lv_pos1 = lv_pos1 + 1.
  ls_fcat1-fieldname = 'ZEMP_SALARY'.
  ls_fcat1-coltext = 'SALARY'.
  ls_fcat1-col_pos = lv_pos1.
  ls_fcat1-outputlen = 20.
  append ls_fcat1 to lt_fcat1.

  lv_pos1 = lv_pos1 + 1.
  ls_fcat1-fieldname = 'ZEMP_POSITION'.
  ls_fcat1-coltext = 'POSITION'.
  ls_fcat1-col_pos = lv_pos1.
  ls_fcat1-outputlen = 20.
  append ls_fcat1 to lt_fcat1.

  lv_pos1 = lv_pos1 + 1.
  ls_fcat1-fieldname = 'ZEMP_DEPARTMENT'.
  ls_fcat1-coltext = 'DEPARTMENT'.
  ls_fcat1-col_pos = lv_pos1.
  ls_fcat1-outputlen = 20.
  append ls_fcat1 to lt_fcat1.


  if go_hr_container1 is initial.
    create object go_hr_container1
      exporting
        container_name = 'Z_EMPSEARCH'.
    create object go_grid1
      exporting
        i_parent = go_hr_container1.
  endif.
  call method go_grid1->set_table_for_first_display
    changing
      it_outtab       = ls_t1
      it_fieldcatalog = lt_fcat1.


endmodule.                 " STATUS_9008  OUTPUT

*----------------------------------------------------------------------*
***INCLUDE ZPROJECTRS_USER_COMMAND_900I09 .
*----------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  USER_COMMAND_9008  INPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
module user_command_9008 input.

case ok_admin.

     when 'HOME'.
      call screen 9000.
      when 'BACK'.
      call screen 9001.
      when 'SEARCH'.

      zemp = inp_empid.

    when others.
      leave to screen 0.
  endcase.







endmodule.                 " USER_COMMAND_9008  INPUT




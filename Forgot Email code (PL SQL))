DECLARE
l_user_name  varchar2(50);
l_password   varchar2(50);
e_error exception;
l_count number(2);
l_app_url varchar2(500);
BEGIN
 
SELECT count(1) INTO l_count
FROM USER_ACCOUNT
WHERE UPPER(EMAIL)=UPPER(:P11_EMAIL);

IF l_count > 0 THEN
SELECT USER_NAME,PASSWORD INTO l_user_name,l_password
FROM USER_ACCOUNT
WHERE UPPER(EMAIL)=UPPER(:P11_EMAIL);
l_app_url:= '<html><body>' || utl_tcp.crlf ||
                   '<p>To login into the appliaction <a href="' ||
                   apex_mail.get_instance_url || 'f?p=14807">Click here</a></p>' || utl_tcp.crlf ||
                   '</body></html>';

APEX_MAIL.SEND(
        p_to        => :P11_EMAIL,
        p_from      => 'iacademy-noreply@oracle.com',
        p_subj      => 'Donate Plasma Account Password reset Notification' ,
        p_body      => '',
        p_body_html => 'Hi'||' '||l_user_name||','|| '<br><br>Please find below details to login.<br>'||
		 '<br>User Name:-'||l_user_name||'<br>Password:-'||l_password||'<br><br>'||l_app_url||'<br>'||'Regards,<br>'||'Plasma Donation Team'
		 );
         APEX_MAIL.PUSH_QUEUE;
ELSE
RAISE e_error;
END IF;

 EXCEPTION 
 WHEN e_error THEN
 RAiSE_APPLICaTION_ERROR(-20001,'Email does not exist,Please enter valid email') ;
 WHEN NO_DATA_FOUND THEN
 RAiSE_APPLICaTION_ERROR(-20001,'Email does not exist.') ;
 WHEN OTHERS THEN
  RAiSE_APPLICaTION_ERROR(SQLCODE,SQLERRM) ;
END;

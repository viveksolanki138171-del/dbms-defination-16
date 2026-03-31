Definition 16:
--calculate salary by fetching salary from emp where deptno =10 with
explicit cursor (USE ROWTYPE variable)
set serveroutput on;
declare
cursor sal_cal is select ename, deptno, basicsal from emp3 where deptno =
10;
xename emp3.ename%type;
xdeptno emp3.deptno%type;
xsal emp3.basicsal%type;
da number;
hra number(10) := 1000;
pf number;
fsalary number;

begin
open sal_cal;
loop
fetch sal_cal into xename, xdeptno, xsal;
exit when sal_cal%notfound;
da := xsal * 0.10;
pf := xsal * 0.12;
fsalary := (xsal + da + hra) - pf;
dbms_output.put_line('employee name : ' || xename);
dbms_output.put_line('department no : ' || xdeptno);
dbms_output.put_line('basic salary : ' || xsal);
dbms_output.put_line('da : ' || da);
dbms_output.put_line('hra : ' || hra);
dbms_output.put_line('pf : ' || pf);
dbms_output.put_line('final salary : ' || fsalary);
dbms_output.put_line('-----------------------');
end loop;
close sal_cal;
end;
/

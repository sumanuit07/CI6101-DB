# CI6101-DB
# CI 6101: Database Design and Management: Practical Approach

DB
- Organized data

Relation > Table
Row > Tuple
Column > Attribute

Operation/Analytical Database

SQL is declarative, not procedural
// บอกว่าอยากได้อะไร? WHAT????

Homework: 10% 
Project: 20%  
Midterm: 35%  เน้น SQL**
Final: 35% 

relational algebra


artificial key or surrogate key < Primary Key ที่ generate จากระบบ
projection operation > เลือกบาง column
selection operation > เลือกบาง แถว

Junction or Linking Table >> ตารางที่ทำให้เป็น many to many
Pin Tab ไม่ให้มันหายไป





cartesian product << join ไม่ where


select *

from person 
join contact2 using(id);  << Using ใช้เฉพาะกรณีที่ pk กับ fk ชื่อเดียวกัน

ลง Anaconda
https://www.continuum.io/downloads

ลง conda



-- Outer Join does not have the following characteristics:

Commutativity  (A op B) = (B op A)

Associativity  (A op B) op C = A op (B op C)



Full Outer join = left, right, union


Scalar subquery = subquery ที่คืนมาค่าเดียว
vector subquery = subquery ที่คืนค่ามาเต็ม


-- Temporary table
create temporary table [table alise] as 
	
select managerid, count(*) as directreports
	
from person
	
group by managerid;



------------------------------

Float เก็บค่าประมาณไม่ควรใช้กับเงิน

Constants
- Inline
- Outline

Not Null
Constants ต้องเป็น External ในกรณีที่มีมากกว่า 1 ฟิลด์



serial << คือ Bigint(20) unsignt, PK, Not null, Auto Increment


ON DELETE 
- RESTRICT (default)
- CASCADE ลบลูกด้วย
- SET NULL เซ็ตลูกเป็น null



------------------------------

Index
เป็น Table อีก 1 ตัวโดยมีโครงสร้างเป็น B-Tree

ถ้ามีเยอะจะทำให้ช้าเพราะมีโอกาสจะต้องปรับโครงสร้างของต้นได้

ถ้า Index มี 2 คอลัมน์ จะดูที่ column แรกก่อน ถ้ามีซ้ำก็ถึงจะดู column ที่ 2


EXPLAIN SELECT count(*) FROM test WHERE fruit = 'Kate';

ต้องทำ index ใน Column ที่เป็นเงื่อนไขในการค้นหาบ่อยๆ


Implicit Indexes  พวกที่ Auto create เช่น FK, Unique Constraint



------------------------------
Alter 

.frm ไฟล์โครงสร้าง
.ibd ไฟล์ข้อมูล

การ alter จะเป็นการสร้างไฟล์ใหม่ แล้ว copy ข้อมูลไปอีกไฟล์ ดังนั้นควรทำทีเดียวถ้าคิดจะ alter 

Create index กับ drop index ใน mysql จะเปลี่ยนเป็น alter table ทำให้ช้าเช่นกัน

-----------------------------------

GRANT


CREATE USER <user>@<host> IDENTIFIED BY <password>;
host > เข้ามาจากเครื่องไหน
Create user [username];
show grants;
grant select on sqldb.employee to john;



select * from mysql.user; -- << grant  user scope
select * from mysql.db; -- << grant globla scope
select * from mysql.tables_priv; -- << grant table scope
select * from mysql.columns_priv; -- << grant column scope
select * from mysql.procs_priv; -- << grant 




GRANT ALL ON *.* TO 'joe'@'localhost' WITH GRANT OPTION; -- root/admin privileges
REVOKE GRANT OPTION ON *.* FROM 'joe'@'localhost';

WITH GRANT OPTION << ให้สิทธิ์ Grant
REVOKE GRANT OPTION << เอาสิทธฺ์ Grant ออก

** Jopiter Notebook


select user(); << who am i


** pk of user is user+host

GRANT ALL 



-------

Stored Routine
- Stored Procedure (associated with a database)
	does not return a value
	invoked using CALL
- Stored Function (associated with a database)
	returns a value
	invoked in an expression
- Triggers (associated with a table)
	“fires” before or after INSERT/UPDATE/DELETE
	Possible actions: correct invalid input, audit/ archieve
	deletes, and set default



เปลี่ยนตัวจบคำสั่ง (บอก Editor)
delimiter //
delimiter ;

---

**Sessions variables**
@sessionVar << 

set @sessionVar = 'xx';
select id into @sessionVar from xxx;
select @sessionVar;

**Local Variable**
DECARE localVar = "xx";
select id into localVar from xxx;
----


Function

delimite //
create function xx(in1 type, in2 type)
return [return type]
begin

	..;
	..;
end//

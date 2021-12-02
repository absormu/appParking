# Rewrite App Parkirng API

## Server
* OpenSUSE Leap 15.3 Server
* Go
* MariaDB/Mysql
* Samba
* NTP

## PM
* Raspberry 
* Raspbian
* Python
* IpCam

## PK
* OS Linux Ringan Mininum ?
* Python
* IpCam

## Pos Office
* Web Base
* VueJS

## Desain Database
* Bikin Uml
* tb_shift
```


CREATE TABLE shifts 
(
	shift_name VARCHAR(50) NOT NULL,
	shift_start_time VARCHAR(50) NOT NULL,
	shift_end_time VARCHAR(50) NOT NULL,
	PRIMARY KEY (shift_name)
) ENGINE = InnoDb;

SELECT * FROM shifts;

INSERT INTO shifts
	(shift_name, shift_start_time,shift_end_time)
VALUES
	('1', '08:00:00','15:59:01'),
	('2', '16:00:00','23:59:01'),
	('3', '00:00:00','07:59:01');

INSERT INTO dbparking.shifts (shift_name,shift_start_time,shift_end_time) VALUES
	 ('S1','2012-01-01 08:00:00','2012-01-01 15:59:00'),
	 ('S2','2012-01-01 16:00:00','2012-01-01 23:59:00'),
	 ('S3','2012-01-02 00:00:00','2012-01-02 07:59:00');
	
TRUNCATE table shifts;

script ini berjalan tapi ada bug di jam:59 misal 09:59:02

SELECT shift_name
FROM shifts
WHERE(shift_start_time < shift_end_time and(shift_start_time <= time(now()) and shift_end_time > time(now())))
OR(shift_start_time > shift_end_time and(shift_start_time <= time(now()) or shift_end_time > time(now())))

SET @keluar = '2021-05-24 15:59:01';   
SELECT shift_name
FROM shifts
WHERE(shift_start_time < shift_end_time and(shift_start_time <= time(@keluar) and shift_end_time > time(@keluar)))
OR(shift_start_time > shift_end_time and(shift_start_time <= time(@keluar) or shift_end_time > time(@keluar)));

-- https://pretagteam.com/question/how-to-get-current-shift-by-current-time-from-mysql-database

SELECT CAST(NOW(3) AS TIME(6));

DELIMITER //

CREATE FUNCTION GetShift(p_Date DATETIME(3))
RETURNS VARCHAR(10)
BEGIN
    DECLARE v_Time time(6) DEFAULT CAST(p_Date AS TIME(6));
    
    RETURN
    CASE WHEN v_Time >= '08:00:00' AND v_Time < '15:59:01' THEN 'SHIFT1'
         WHEN v_Time >= '00:00:00' AND v_Time < '07:59:01' THEN 'SHIFT3'
         ELSE 'SHIFT2' END;
END;
//

DELIMITER ;

SELECT GetShift(NOW(3));

SET @keluar = '2021-05-24 12:15:01';   
SELECT GetShift(@keluar);

-- https://dba.stackexchange.com/questions/228475/how-to-get-current-shift
-- https://dbfiddle.uk/?rdbms=sqlserver_2017&fiddle=b5e18aa705b495bb9879e80407a67d44
-- https://www.sqlines.com/online





```

## Web Service
* Bikin OpenAPI
* Bikin RESTful






Link :

http://sqlfiddle.com/

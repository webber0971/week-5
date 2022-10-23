# week-5

#要求3-1
INSERT INTO MEMBER(NAME,USERNAME,PASSWORD,FOLLOWER_COUNT)
VALUES('TEST','TEST',11,111),
		('TEST2','TEST2',22,222),
        ('TEST3','TEST3',33,333),
        ('TEST4','TEST4',44,444);
        
#要求3-2 取得所有在 member 資料表中的會員資料。
select * from member;
![image](https://user-images.githubusercontent.com/101098094/197385160-f5c06e2b-9ee7-45f1-9870-7bfb83666a79.png)


#3-3 取得所有在 member 資料表中的會員資料，並按照 time 欄位，由進到遠
select * from member order by TIME DESC;
![image](https://user-images.githubusercontent.com/101098094/197385174-89b85ba8-505e-4c34-b170-c0e48c31d3f0.png)


#3-4 取得 member 資料表中第 2 ~ 4 共三筆資料，並按照 time 欄位，由近到遠排序。
select * from member order by TIME DESC limit 1,3;
![image](https://user-images.githubusercontent.com/101098094/197385184-e6aa1fc4-69cc-461d-8c72-208da9952eb4.png)


#3-5 取得欄位 username 是 test 的會員資料。
select * FROM MEMBER WHERE USERNAME = 'TEST';
![image](https://user-images.githubusercontent.com/101098094/197385190-8d36e5f8-502e-4306-be85-36c4b09a8627.png)




#3-6 取得欄位 username 是 test、且欄位 password 也是 test 的資料。
select * FROM MEMBER WHERE USERNAME = 'TEST' AND PASSWORD='TEST';
![image](https://user-images.githubusercontent.com/101098094/197385196-2cb5d4f1-bdae-4801-ae74-4122b0526625.png)

#3-7 UPDATE 指令更新欄位 username 是 test 的會員資料，將資料中的 name 欄位改成 test2。
SET SQL_SAFE_UPDATES = 0;
UPDATE MEMBER SET USERNAME='TEST2' WHERE NAME='TEST';
![image](https://user-images.githubusercontent.com/101098094/197385271-42307386-1b7e-4e25-8402-90ed74b1213e.png)



#4-1 取得 member 資料表中，總共有幾筆資料
SELECT COUNT(*) FROM MEMBER;
![image](https://user-images.githubusercontent.com/101098094/197385282-aaa24fbf-e779-47f6-8f06-867da6712923.png)


#4-2 取得 member 資料表中，所有會員 follower_count 欄位的總和。
SELECT SUM(follower_count) FROM MEMBER;
![image](https://user-images.githubusercontent.com/101098094/197385287-c643f293-ba9c-48fc-a4e6-4e3de60a3e62.png)



#4-3 取得 member 資料表中，所有會員 follower_count 欄位的平均數
SELECT AVG(FOLLOWER_COUNT) FROM MEMBER;
![image](https://user-images.githubusercontent.com/101098094/197385299-735c7b72-5472-4091-b449-e4efd52ab427.png)



#5-1 建立新資料表紀錄留⾔資訊，取名字為 message。
CREATE TABLE MESSAGE1(
	id Int primary key auto_increment comment '獨立編號',
    MEMBER_ID INT NOT null comment '留言者會員編號',
    content varchar(255) NOT null comment '留言內容',
    like_count INT unsigned NOT NULL default 0 COMMENT '按讚的數量',
    time datetime NOT NULL default current_timestamp COMMENT '留言時間'
);

INSERT INTO MESSAGE(MEMBER_ID,CONTENT,LIKE_COUNT) VALUES(1,'EKIWEJ',4);
INSERT INTO MESSAGE(MEMBER_ID,CONTENT,LIKE_COUNT) VALUES(1,'EKIWEJ',6);
INSERT INTO MESSAGE(MEMBER_ID,CONTENT,LIKE_COUNT) VALUES(1,'EKIwwWEJ',6);

SELECT * FROM MESSAGE;
![image](https://user-images.githubusercontent.com/101098094/197385315-12f83b67-a6b1-4c06-b0c4-e83f2a58ccaf.png)

#5-2 使用 SELECT 搭配 JOIN 語法，取得所有留言，結果須包含留言者會員的姓名。
SELECT NAME , content FROM MEMBER INNER JOIN MESSAGE ON MEMBER.ID=MESSAGE.MEMBER_ID;
![image](https://user-images.githubusercontent.com/101098094/197385325-9323f80e-9c73-4077-8278-cbfdefa360ee.png)

#5-3 使用 SELECT 搭配 JOIN 語法，取得 member 資料表中欄位 username 是 test 的所有留言，資料中須包含留言者會員的姓名。
SELECT NAME, USERNAME , content FROM MEMBER INNER JOIN MESSAGE ON MEMBER.ID=MESSAGE.MEMBER_ID where USERNAME='TEST';
![image](https://user-images.githubusercontent.com/101098094/197385330-418e59b9-22c7-43fe-98d3-ce84bab1fe03.png)

#5-4 使用 SELECT、SQL Aggregate Functions 搭配 JOIN 語法，取得 member 資料表中欄位 username 是 test 的所有留言平均按讚數。
SELECT AVG(like_count) FROM MEMBER INNER JOIN MESSAGE ON MEMBER.ID=MESSAGE.MEMBER_ID where USERNAME='TEST';
![image](https://user-images.githubusercontent.com/101098094/197385343-5508c950-f878-4314-8688-c32c7dfd8ed1.png)


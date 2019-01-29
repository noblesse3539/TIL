# SQLite3

우분투에서 기본적으로 사용할 수 있는 오픈소스 데이터베이스.



## 1. 실행하기

```powershell
$ sqlite3
```



### 1-1. csv 파일을 불러오기

```sqlite
.import hellodb.csv examples
SELECT * FROM EXAMPLES;
```

### 1-2. 레코드들을 좀 이쁘게 출력시키기 위해 설정!!!

```sqlite
.headers on
.mode column
SELECT * FROM examples;
```



## 2. 데이터베이스 만들기

```powershell
$ sqlite3 tutorial.sqlite3
```

```sqlite
sqlite> .databases
```



> SQL의 여러 문장을 실행할 땐 .sql 파일을 만들어 .read 파일이름.sql 을 하여 실행한다!!


# PostgreSQL

## PSQL

* 사용자 조회

	* ```select * from pg_shadow;```


* 비밀번호 변경

	* ```alter user dodotdo with password 'ektenekt25';```

* Create User
	* ```create user username [[with] options [...]] where option can be;```
	* ```create user test2 password 'test2';```
	
* 대기중 쿼리 조회
	* ```
	select * from pg_stat_activity where datname='dodotdo';
	``` 
	
* 대기 중인 쿼리 Clear
	* ```
	SELECT
 pg_terminate_backend (pg_stat_activity.pid)
FROM
 pg_stat_activity
WHERE
 pg_stat_activity.datname = 'dodotdo';
```



## GUI PostgreSQL Tool : Postico

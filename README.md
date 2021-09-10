# 발견 문제점
## 1. 실행 오류
***오류 구문***
> org.springframework.beans.factory.UnsatisfiedDependencyException

스프링 배우면서 거의 매일 봤던 오류라 어노테이션이 되어있지 않거나 xml 파일에 문제가 있음을 알고 xml 파일을 확인하여 수정함.

<br>

> **원인** : WriteDAO.xml 에서 `<!-- view.do -->` 부분 resultType 경로 문제

```
com.lec.spring.WriteDTO
-> com.lec.spring.domain.WriteDTO
```

<br>

---

## 2. 삭제 오류
***오류 구문***
> java.sql.SQLSyntaxErrorException: Unknown column 'uid' in 'where clause'

sql 구문에서 오류 발생

<br>

> **원인** : WriteDAO.xml 에서 delete 구문 컬럼명 오류

```sql
WHERE uid = #{uid}
-> WHERE wr_uid #{uid}
```

<br>

---

## 3. 수정 오류
***오류 구문***
> Failed to convert value of type 'java.lang.String' to required type 'int'; nested exception is java.lang.NumberFormatException: For input string: ""

int를 요구하는건 viewcnt밖에 없는 걸로 알아서 해당 부분을 살펴봤는데 문제될 게 없었음.

'수정 성공'이 뜬 뒤 url 부분을 살펴보면 `http://localhost:8093/board/view.do?uid=` 이렇게 되어있음

<br>

> **원인** : updateOk.do 파일에서 올바른 uid 값이 넘겨지지 않음
 
```jsp
view.do?uid=${uid}
-> view.do?uid=${param.uid}
```
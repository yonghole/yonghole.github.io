---
title: "[데이터베이스] 데이터 베이스 강의 3: Querying Relational Databases "
date: 2021-03-16 04:33:02
categories: Database
---
# 데이터베이스 강의3: Querying Relational Databases

### Steps in creating and using a (relational) database

1. Design schema; create using DDL // SQL → CREATE TABLE
2. "Bulk load" initial data // Tuple들을 insert
3. Repeat : execute queries and modifications

### Ad-hoc queries in high-level language

→ All students with **GPA > 3.7** applying to Stanford and MIT only

→ All engineering departments in CA with < 500 applicants

→ College with highest average accept rate over last 5 years

- 조건을 표현하기 쉬운 경우도, 어려운 경우도 있다.
- 어떤 경우에는 DBMS가 효율적으로 실행하기 편리하고, 어떤 경우에는 어렵다.
- Query Language(DML) 는 데이터를 modify 하는데도 사용된다.
    - Query (retrieve)
    - Querying & Modifying

### Queries return relations ("compositonal", "closed")

→ Query 는 realation을 반환한다. 

→ 다른 개념으로 넘어가지 않고 그 개념 안에서 처리가 되기 때문에 closed 라고 표현한다. 

### Query Languages

- Relational Algebra
    - formal → 구현이 안되어 있다.
- SQL
    - Actual / implemented

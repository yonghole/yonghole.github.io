---
title: "[데이터베이스] 데이터 베이스 강의 2: Relational Databases "
date: 2021-03-16 04:19:02
categories: Database
---
# 데이터베이스 강의2: The Relational Model

## The Relational Model

- 대부분의 주요 상용화된 데이터베이스 시스템에서 사용된다.
- 매우 간단한 모델
- High-level languages 들과 query를 주고 받는다.
- 효율적인 구현을 가졌다.

re : retrieve

wr: modify (insert,delete,update)

### Concepts

- Schema = structural description of relations(table) in database
- Instance = actual contents at given point in time
- Database = set of named relations (or tables)
    - 각 relation들은 attribute(columns)들의 set을 가지고 있다.
    - 각 tuple(row) 는 각 attribute에 대한 값을 가지고 있다.
    - 각 attribute는 type(domain)을 가지고 있다.

        String, int, etc...

![Untitled](https://user-images.githubusercontent.com/55180768/111209017-d10ebc00-860e-11eb-8501-6ef227d83d78.png)


- NULL - special value for "unknown" or "undefined"
    - undefined : 해당 값을 정의할 수 없음. 정의 할 수 없는 경우가 어색하지 않다.
    - unknown : 어떤 값이 들어가야 하지만 아무것도 들어가지 않은 경우.

- Key - attribute whose value is unique in each tuple or set of attributes whose combined values are unique
    - Relation에서 값이 모두 unique 한 attribute조합을 선택한 경우
    - Tuple이 모든 attribute에서 값이 다른 경우(의 key)를 이야기한다.
    - 예를 들어, 위의 Student table에서 ID와 name을 골랐을 때 중복되는 tuple이 존재하지 않는다면 (ID,name)은 Key가 된다.

![Untitled 1](https://user-images.githubusercontent.com/55180768/111209022-d2d87f80-860e-11eb-84ee-c1e200b3fee1.png)

    - 하지만 만약  다음과 같은 상황이라면 ID,name을 골랐을 때 중복되는 tuple이 생기기 때문에 Key가 될 수 없다.
    - 위 테이블에서 ID와 name 이 중복되어도, (ID,name,GPA) 까지 선택한다면 unique한 tuple이 되기 때문에 (ID,name,GPA)는 Key가 된다.

    ### Creating relations (tables) in SQL

    ```sql
    create table Student(ID, name, GPA, photo)

    create table College(name string, state char(2), enrollment integer)
    ```

    ###

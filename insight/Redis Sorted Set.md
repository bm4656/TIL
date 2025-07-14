### ✅ Sorted Set

- 순위표/랭킹 구현에 사용
- 특정인의 순위 알 수 있음

### ✅ Skip List

Sorted Set 구현에 사용한 자료 구조는 Skip List

![image.png](https://github-production-user-asset-6210df.s3.amazonaws.com/65716445/466106819-d759be08-e333-4f81-9e87-1db7b77ee69b.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20250714%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20250714T163301Z&X-Amz-Expires=300&X-Amz-Signature=da6bccd69e75e285e80edae119bded5ed870fcdd776c9941d2c4e1ef4982b2f7&X-Amz-SignedHeaders=host)

- 연결 리스트가 계층을 구성함 → 0, 1, 2 레벨
- 각 연결 리스트는 값을 순서대로 가짐
- 0 레벨: 전체 값을 가짐
- 상위 레벨: 하위 노드에서 일부 노드만 포함

**검색 - 30 찾기**
- 만약 0레벨처럼 단일 연결 리스트 구조라면 앞에서부터 순차적으로 검색할 것이다.

![image.png](https://private-user-images.githubusercontent.com/65716445/466107832-7374edcf-adbc-4dad-ad34-4518f24e7978.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTI1MTE0MjMsIm5iZiI6MTc1MjUxMTEyMywicGF0aCI6Ii82NTcxNjQ0NS80NjYxMDc4MzItNzM3NGVkY2YtYWRiYy00ZGFkLWFkMzQtNDUxOGYyNGU3OTc4LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA3MTQlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNzE0VDE2Mzg0M1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTM2YmY4Y2JlNDFjYjYwNmIwMGIzMmRjMDZhNjJmY2FjMzMyODJkZTY3OTQzMmIzMWViZTg5MDkyYTZkNGRmMjMmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.ONUgUJ4LMWENUUXkkW1pJvxljbgdGsnKjcJkKj5fgnY)

- 계층 구조를 가지고 있는 Skip List는 가장 최상위 레벨에서부터 시작한다.

```tsx
- 2레벨 HEAD 노드에서 다음노드 확인 → 40, 30보다 크군 더이상 진행 X, 한 칸 내려감

- 1레벨 HEAD 노드에서 다음노드 확인 → 20, 30보다 작군, 다음노드 확인 → 40, 30보다 크군 더이상 진행 X, 한 칸 내려감

- 0레벨 20노드에서 다음노드 확인 → 30이 있네!
```

- 삽입과 삭제도 비슷한 방식으로 자리를 찾아간다.
- 평균 O(log n)의 시간복잡도를 가진다.

**값 70의 랭킹은?**

![image.png](https://private-user-images.githubusercontent.com/65716445/466107907-9c73deeb-b4a9-4610-a798-c3e8574adfb0.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTI1MTE0MjMsIm5iZiI6MTc1MjUxMTEyMywicGF0aCI6Ii82NTcxNjQ0NS80NjYxMDc5MDctOWM3M2RlZWItYjRhOS00NjEwLWE3OTgtYzNlODU3NGFkZmIwLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA3MTQlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNzE0VDE2Mzg0M1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTZiNTNmMjcxNDZiOThmYTI2NTY2NjY4N2Q3YzRlNjdmNTk2YTVjYzliNDY5NTQ1MDQ0ZDEyYWY0NWUwYzNhMjQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.aLBzGNjn0wSfm16GSUCCfU_42tGMQ0IU82-OSgmb5q0)

- 그냥 0레벨에서 순서대로 찾으면 O(n)
- Skip List에서는 랭킹을 찾기 위해서 새로운 정보를 하나 추가한다.

![image.png](https://private-user-images.githubusercontent.com/65716445/466107949-dcaa08c5-98a6-4251-9b2d-2c113a444c77.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTI1MTE0MjMsIm5iZiI6MTc1MjUxMTEyMywicGF0aCI6Ii82NTcxNjQ0NS80NjYxMDc5NDktZGNhYTA4YzUtOThhNi00MjUxLTliMmQtMmMxMTNhNDQ0Yzc3LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA3MTQlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNzE0VDE2Mzg0M1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTcxZDg4NTQxMTljMmU3ZTVkYmZlZDk3Zjk0Mjc0Mjk3NjUxOGQxNGQxOTZjYzlhOWU5YTdjOThkMjQ5MmE2NDEmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.vjxIZXUwRfTM6gEsjtCI9HyihTyxs4kGOr2_V81REfs)

- **각 노드간의 간격(칸)을 추가한다. → SPAN**

![image.png](https://private-user-images.githubusercontent.com/65716445/466108004-31908331-4d60-4509-8ff5-8f71a41afe00.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTI1MTE0MjMsIm5iZiI6MTc1MjUxMTEyMywicGF0aCI6Ii82NTcxNjQ0NS80NjYxMDgwMDQtMzE5MDgzMzEtNGQ2MC00NTA5LThmZjUtOGY3MWE0MWFmZTAwLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA3MTQlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNzE0VDE2Mzg0M1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTk5NGFmNGUyMWNkMDBkYmFkMzhmM2IzYjFlYjI2Mzk1YzM3YTY2OTgxNmM2NDMxYzgzODM3ZGQzMTM0ODAwMTAmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.2JJ96XKBTuk6A99MgAayUXVJ7OhevVDXkYz-L8hMWRw)

- 동일하게 최상위 레벨부터 시작한다.
- 이런식으로 O(log n)의 시간복잡도로 랭킹을 구할 수 있다.

**키 c의 랭킹은?**

![image.png](https://private-user-images.githubusercontent.com/65716445/466108037-838282af-78a8-4528-9d50-a0e8b90a01e8.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTI1MTE0MjMsIm5iZiI6MTc1MjUxMTEyMywicGF0aCI6Ii82NTcxNjQ0NS80NjYxMDgwMzctODM4MjgyYWYtNzhhOC00NTI4LTlkNTAtYTBlOGI5MGEwMWU4LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA3MTQlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNzE0VDE2Mzg0M1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWU3ZTJjMDNjYjA3OGVlYTMyMjcwZGIxODcyZDZkMWRjM2VmNTk0ODQzNDNjYzlhOWE3YThjYjY0MmRkOWZkYjQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.dtDYdPKsSJ06ZTLWSZlrNR5dfkxAtEQREcAlfTeVh6U)

- 해시테이블로 (키, 값) 쌍을 유지
- 먼저 c에 해당하는 값을 구하고, 랭킹을 찾아간다.

### ✅ **정리**

**Redis Sorted Set = Skip List + Hashtable**

- 랭킹을 구하기 위해 내부적으로 부가정보인 SPAN 값을 관리한다.
- 단점 → 계층 구조에 따른 메모리 사용량 증가

[🔗 출처 링크](https://www.youtube.com/watch?v=-titFXvd5xE)
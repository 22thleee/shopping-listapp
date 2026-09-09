# 🛒 shopping-listapp

[Supabase](https://supabase.com) 데이터베이스에 자동 저장되는 간단한 쇼핑 리스트 웹앱입니다. 별도의 빌드나 서버 없이 단일 HTML 파일로 동작합니다.

## 기능

- 아이템 추가 / 삭제
- 체크(구매 완료) 표시 및 취소선
- 체크된 항목 일괄 삭제
- 남은 항목 / 전체 항목 개수 표시
- Supabase 데이터베이스에 저장되어 어느 기기에서 접속해도 같은 목록 유지
- 라이트 / 다크 모드 자동 대응

## 사용 방법

`index.html` 파일을 브라우저에서 열면 됩니다.

```
open index.html
```

`index.html` 상단의 `SUPABASE_URL` / `SUPABASE_KEY` 상수를 본인의 Supabase 프로젝트 값으로 교체하세요.

### 데이터베이스 스키마

```sql
create table public.shopping_items (
  id uuid primary key default gen_random_uuid(),
  text text not null check (char_length(text) between 1 and 100),
  checked boolean not null default false,
  created_at timestamptz not null default now()
);

alter table public.shopping_items enable row level security;
-- 로그인 없는 공개 앱이므로 anon 역할에 select / insert / update / delete 정책을 허용합니다.
```

## 기술 스택

- 순수 HTML / CSS / JavaScript
- [@supabase/supabase-js](https://github.com/supabase/supabase-js) (ESM CDN)

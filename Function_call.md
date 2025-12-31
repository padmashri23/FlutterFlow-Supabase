### Create RPC function and call the function to join two tables via Postman:

## What is an RPC function?
- An RPC function is a stored procedure or function defined inside your PostgreSQL database.
- It lets you run server-side logic (SQL or PL/pgSQL) by calling a single function name with parameters.
- With Supabase, you can call these functions remotely from your app using `supabase.rpc(...)` or the REST RPC endpoint.

---

## Why use RPC functions?
- Encapsulate complex queries and business logic on the server (fewer round-trips).
- Keep sensitive logic or calculations in the database, not on the client.
- Reuse logic across different clients (web, mobile, server).
- Sometimes faster for complex joins/aggregations because work runs close to the data.    

---

## auth schema:

<img width="1917" height="608" alt="image" src="https://github.com/user-attachments/assets/8aa3a05a-2635-4ea5-b826-43d27b630c36" />

## public schema:

## Post table:
 <img width="1916" height="592" alt="image" src="https://github.com/user-attachments/assets/d87e5179-ebf3-4472-b1bb-2310cf9f635e" />

 ## User table:
 <img width="1512" height="511" alt="image" src="https://github.com/user-attachments/assets/02007688-774c-4cce-b0e1-bf33058fb8bd" />

 ### Creating rpc function:
 ```pgsql
CREATE FUNCTION public.get_posts_with_users(payload json)
RETURNS SETOF json
LANGUAGE sql
STABLE
SECURITY DEFINER
AS $$
  SELECT json_build_object(
    'post_id', p.id,
    'title', p.title,
    'body', p.body,
    'created_at', p.created_at,
    'user_id', u.id,
    'first_name', u.first_name,
    'last_name', u.last_name,
    'email', u.email
  )
  FROM public.posts p
  JOIN public.users u
    ON p."user" = u.id
  ORDER BY p.created_at DESC;
$$;
``` 

### Enable access (RLS / Permissions):
```pgsql
GRANT EXECUTE ON FUNCTION public.get_posts_with_users() TO anon;
GRANT EXECUTE ON FUNCTION public.get_posts_with_users() TO authenticated;
```

### Store the variables and values:

<img width="1347" height="865" alt="image" src="https://github.com/user-attachments/assets/70e97a5e-350e-45c5-b5a8-1abf58692309" />

###  Set request type - Post:

<img width="1345" height="577" alt="image" src="https://github.com/user-attachments/assets/ce728890-65cc-4336-9478-af9081e797c2" />
<img width="1315" height="537" alt="image" src="https://github.com/user-attachments/assets/d7374331-cc70-430f-b4c4-6c4e75b5d6d8" />

### Result: Calling & testing it in Postman:
<img width="658" height="820" alt="image" src="https://github.com/user-attachments/assets/b7e73cd5-2deb-4412-9b45-edf6ba955754" />



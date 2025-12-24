### RLS policy with different edge cases:                          

### Created user JWT:
<img width="1915" height="1031" alt="image" src="https://github.com/user-attachments/assets/6d548f6b-d1e5-451c-9f21-234254b254f3" />

### RLS Select policy(auth.uid() = user_id) with where clause:
<img width="1919" height="967" alt="image" src="https://github.com/user-attachments/assets/bc4e6e55-a3ab-4f71-80ed-e7ca5ca22603" />

// API fetched only the currently logged in user to-do's:

### RLS Select policy(true) without where clause:
<img width="1917" height="953" alt="image" src="https://github.com/user-attachments/assets/b06e4aff-30bc-46e2-8767-97be8a2692ec" />

### RLS Select policy(true) with where clause:
<img width="1910" height="964" alt="image" src="https://github.com/user-attachments/assets/139b88b8-bde9-4649-ada9-4e3f47de01b8" />

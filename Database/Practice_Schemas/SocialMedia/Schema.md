# Practice Schema: Social Media Feed

Social media systems require high read speeds and handle complex relationships (the "Graph" problem).

## Tables

### 1. Users & Profiles
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    bio TEXT,
    avatar_url TEXT
);

CREATE TABLE follows (
    follower_id INT REFERENCES users(id),
    followed_id INT REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (follower_id, followed_id)
);
```

### 2. Posts & Interactions
```sql
CREATE TABLE posts (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    content TEXT NOT NULL,
    image_url TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE likes (
    user_id INT REFERENCES users(id),
    post_id INT REFERENCES posts(id),
    PRIMARY KEY (user_id, post_id)
);
```

## Scaling the Feed

### 1. The Fan-out Problem
When a user with 1 million followers posts, how do you show it to all followers?
- **Pull Model:** When a follower opens the app, the DB finds all posts from people they follow. (Slow for users following many people).
- **Push Model:** When a celebrity posts, their post is "pushed" (copied) into the pre-computed feed of all 1 million followers. (Extremely memory intensive).
- **Hybrid:** Push for small users, Pull for celebrities.

### 2. Practice Query: "My Feed"
"Show me the latest 20 posts from people I follow."
```sql
SELECT p.*, u.username
FROM posts p
JOIN users u ON p.user_id = u.id
JOIN follows f ON f.followed_id = p.user_id
WHERE f.follower_id = 123 -- My ID
ORDER BY p.created_at DESC
LIMIT 20;
```

### 3. Optimization
- **Index:** `CREATE INDEX idx_posts_user_created ON posts (user_id, created_at DESC);`
- **Caching:** Store the "Latest 50 posts" for every active user in **Redis** (List data type) for instant loading.
- **Denormalization:** Store `likes_count` directly on the `posts` table to avoid joining the `likes` table every time a feed is loaded.
    - *Update Rule:* `UPDATE posts SET likes_count = likes_count + 1 WHERE id = 456;` (Use triggers or application logic).
    - *Risk:* Data can become out of sync. Use a periodic "reconciler" background job.

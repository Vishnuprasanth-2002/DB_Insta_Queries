# Create database Instaclone

- To create database, CREATE DATABASE instaclone
- To connect the database, \c instaclone
## Create table

CREATE TABLE users(user_id SERIAL PRIMARY KEY NOT NULL, name VARCHAR NOT NULL);

CREATE TABLE posts(post_id SERIAL PRIMARY KEY NOT NULL,
post_content VARCHAR NOT NULL,
post_date DATE NOT NULL DEFAULT CURRENT_DATE,
user_id SERIAL REFERENCES users(user_id));

CREATE TABLE likes(like_id SERIAL PRIMARY KEY NOT NULL, post_id SERIAL REFERENCES posts(post_id),
user_id SERIAL REFERENCES users(user_id))

## Insert datas
INSERT INTO users(name) VALUES('Edina'),('Colin'),('Glenda'),('Paula');

INSERT INTO posts(post_content, user_id) VALUES('craft',1),('sale',1),('design',1),('tips',1),('lesson',1);
INSERT INTO posts(post_content, user_id) VALUES('animal',2),('cartoon',2),('gift',2),('meme',2),('craft',2);
INSERT INTO posts(post_content, user_id) VALUES('forest',3),('bikesale',3),('book',3),('award',3),('comedy',3);
INSERT INTO posts(post_content, user_id) VALUES('gold',4),('awarness',4),('Experiments',4),('landsale',4),('tricks',4);

INSERT INTO likes(post_id, user_id) VALUES(13, 3),(13,4),(13,1),(13,2),(14,1),(14,2),(15,4),(15,2),
(17,3),(17,1),(19,3),(19,2),(1,4),(1,3),(4,3),(4,4),(4,2),(7,3),(7,4),(7,1),(7,2),(8,4),
(8,1),(9,4),(9,1),(9,3)

## task

- 1. list all users `SELECT * from users;`

- 2. list all posts `SELECT * from posts`

- 3. List posts that are liked by colin `select posts.post_content as liked_By_Colin from posts left join likes on posts.post_id = likes.post_id where likes.user_id = 2;`

- 4. As a Glenda, she wants to know who are all liked her post book. `select users.name as glendas_post_book_liked_by from users inner join likes on users.user_id=likes.user_id where likes.post_id=13;`

- 5. Edina needs to know the post count which are liked by others. `SELECT COUNT(DISTINCT posts.post_id) liked_posts_count FROM posts inner join likes on posts.post_id=likes.post_id where posts.user_id = 1;`

- 6. Paula needs to check the count of awarness and trickes likes count, here awarness id is 17 and trickes id is 20.`SELECT posts.post_content, COUNT(likes.like_id) FROM posts LEFT JOIN likes ON posts.post_id = likes.post_id WHERE posts.post_id IN (17, 20) GROUP BY posts.post_content;`

- 7. List Posts of Edina which has likes and also not liked posts.
`SELECT posts.postcontent as PostOfEdina FROM posts where posts.userid = 1;`

- 8. Search all users posts with Text "sal"

The LIKE operator is case sensitive, if you want to do a case insensitive search, use the ILIKE operator instead.

`SELECT * FROM posts WHERE posts.postcontent ILIKE '%sal%';`

- 9. Get the count of colin posts
`SELECT COUNT(posts.postid) AS no_of_colin_post FROM posts WHERE  posts.userid=2;`

- 10. Get count of likes for the post cartoon. user colin
`instaclone=# select COUNT(likes.likeid) AS cartoon_likes from likes where likes.postid = 7;`

11. Get the maximum likes posts.
`instaclone=# select postid, count(postid) from likes GROUP BY postid HAVING COUNT(postid)>1 order by count(postid) desc limit 2;`
- 12. In Edina, sort posts by title in forward.
      post content is ordered by ascending order for the user edina.
`instaclone=# select * from posts where userid=1 ORDER BY postcontent;`

- 13. In Paula, sort post by date backward.
`instaclone=# select * from posts where userid=4 ORDER BY postdate DESC;`

- 14. Filter today posted posts.
`instaclone=# select * from posts where postdate= 'today';`
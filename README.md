# Create database Instaclone

- To create database, CREATE DATABASE instaclone
- To connect the database, \c instaclone
- Now, add the database in the dbeaver, with the instaclone database name.
- In this database, we are going to create the tables for users, posts, likes.
  - To create users table, CREATE TABLE users(userid SERIAL PRIMARY KEY NOT NULL, username VARCHAR NOT NULL);
  - To create posts table, CREATE TABLE posts(postid SERIAL PRIMARY KEY NOT NULL, postcontent VARCHAR NOT NULL, postdate DATE NOT NULL DEFAULT CURRENT_DATE, userid SERIAL REFERENCES users(userid));
  - To create likes table, CREATE TABLE likes(likeid SERIAL PRIMARY KEY NOT NULL, postid SERIAL REFERENCES posts(postid),userid SERIAL REFERENCES users(userid))
- To insert the information into the table use the command,
  - INSERT INTO users(username) VALUES('Edina'),('Colin'),('Glenda'),('Paula')
  - 1-Edina, 2-Colin, 3-Glenda, 4-Paula
  - INSERT INTO posts(postcontent, userid) VALUES('craft',1),('sale',1),('design',1),('tips',1),('lesson',1)
  - 1-Crafts-1, 2-sale-1, 3-design, 4-tips, 5-lesson, 6-animal, 7-cartoon, 8-gift, 9-meme, 10-craft, 11-forest, 12-bikesale, 13-book, 14-award, 15-comedy, 16-gold, 17-awarness, 18-Experiments, 19-landsale, 20-tricks.
  - INSERT INTO likes(postid, userid) VALUES(13, 3),(13,4),(13,1),(13,2),(14,1),(14,2),(15,4),(15,2),(17,3),(17,1),(19,3),(19,2),(1,4),(1,3),(4,3),(4,4),(4,2),(7,3),(7,4),(7,1),(7,2),(8,4),(8,1),(9,4),(9,1),(9,3)

## task

- 1. list all users `SELECT * from users;`

- 2. list all posts `SELECT * from posts`

- 3. List posts that are liked by colin `select posts.postcontent as likedByColin from posts left join likes on posts.postid = likes.postid where likes.userid = 2;`

- 4. As a Glenda, she wants to know who are all liked her post book. `select users.username as liked_glenda_post from users inner join likes on users.userid=likes.userid where likes.postid=13;`

- 5. Edina needs to know the post count which are liked by others. `SELECT COUNT(DISTINCT posts.postid) FROM posts inner join likes on posts.postid=likes.postid where posts.userid = 1;`

- 6. Paula needs to check the count of awarness and trickes likes count, here awarness id is 17 and trickes id is 20.`SELECT COUNT(likes.likeid) FROM likes where likes.postid = 17 or likes.postid=20;`

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
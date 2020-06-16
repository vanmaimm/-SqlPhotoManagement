# Tạo table
```
CREATE TABLE users (
  	id int NOT NULL AUTO_INCREMENT PRIMARY KEY,
	email VARCHAR(50),
	password VARCHAR(50),
	role VARCHAR(50),
	created_at DATETIME,
	updated_at DATETIME     
);

CREATE TABLE categories(
	id int NOT NULL AUTO_INCREMENT PRIMARY KEY,
	name VARCHAR(50),
	created_at DATETIME,
	updated_at DATETIME 
);

CREATE TABLE photos(
	id int NOT NULL AUTO_INCREMENT PRIMARY KEY,
	title VARCHAR(100),
	category_id INT,
	image VARCHAR(100),
	created_at DATETIME,
	updated_at DATETIME,
	FOREIGN KEY (category_id) REFERENCES categories(id)
);

CREATE TABLE tags(
	id int NOT NULL AUTO_INCREMENT PRIMARY KEY,
	name VARCHAR(50),
	created_at DATETIME,
	updated_at DATETIME 
);

CREATE TABLE taggale(
	tag_id int,
  	photo_id int,
	created_at DATETIME,
	updated_at DATETIME,
	FOREIGN KEY (tag_id) REFERENCES tags(id),
  	FOREIGN KEY (photo_id) REFERENCES photos(id),
  	PRIMARY KEY (tag_id,photo_id)
);

CREATE TABLE photo_descriptions(
	id int NOT NULL,
	content VARCHAR(50),
	created_at DATETIME,
	updated_at DATETIME,
	FOREIGN KEY (id) REFERENCES photos(id),
	PRIMARY KEY (id)
);
```
# Insert Data
```
INSERT INTO users (email,password,role)
VALUES ('van.mai@gmail.com','van123','user'),
	('admin','admin','admin');
       
INSERT INTO categories (name)
VALUES ('love'),
	('life');
       
INSERT INTO photos (title,category_id,image)
VALUES ('Beauty and Monster',1,'beautiful.png'),
	('Body language is important',2,'book.png');
       
INSERT INTO tags (name)
VALUES ('Lovely'),
     ('Cute'),
     ('Happy'),
     ('Smart');
       
INSERT INTO taggale (tag_id,photo_id)
VALUES (1,1), 
	(2,1),
       (3,2),
       (4,2),
       (3,1);
       
INSERT INTO photo_descriptions (id,content)
VALUES (1,'The girl has found her love');
```
# Querry
```
SELECT 	p.title,
	c.name ,
	p.image,
	(SELECT pd.content
        FROM photo_descriptions pd 
        WHERE pd.photo_id = p.id) AS  content, 
    	(SELECT GROUP_CONCAT(t.name)
        FROM tags t, taggable tg
        WHERE tg.tag_id = t.id AND tg.photo_id = p.id  ) AS  tags     
FROM photos p 
INNER JOIN categories c
ON p.category_id = c.id ;
```
# COPY from Mr.Linh
## CREATE
```
CREATE TABLE `categories` (
  `id` bigint PRIMARY KEY AUTO_INCREMENT,
  `name` varchar(50) ,
  `created_at` timestamp NOT NULL DEFAULT current_timestamp(),
  `updated_at` timestamp NOT NULL DEFAULT current_timestamp()
);

CREATE TABLE `photos` (
  `id` bigint PRIMARY KEY AUTO_INCREMENT,
  `title` varchar(100) ,
  `category_id` bigint,
  `image` varchar(100),
  `created_at` timestamp NOT NULL DEFAULT current_timestamp(),
  `updated_at` timestamp NOT NULL DEFAULT current_timestamp(),

  FOREIGN KEY (`category_id`) REFERENCES `categories` (`id`) ON DELETE CASCADE
);

CREATE TABLE `photo_descriptions` (
  `photo_id` bigint PRIMARY KEY,
  `content` varchar(100),
  `created_at` timestamp NOT NULL DEFAULT current_timestamp(),
  `updated_at` timestamp NOT NULL DEFAULT current_timestamp(),

  FOREIGN KEY (`photo_id`) REFERENCES `photos` (`id`) ON DELETE CASCADE
);

CREATE TABLE `tags` (
  `id` bigint PRIMARY KEY AUTO_INCREMENT,
  `name` varchar(50),
  `created_at` timestamp NOT NULL DEFAULT current_timestamp(),
  `updated_at` timestamp NOT NULL DEFAULT current_timestamp()
);

CREATE TABLE `taggable` (
  `tag_id` bigint,
  `photo_id` bigint,
  `created_at` timestamp NOT NULL DEFAULT current_timestamp(),
  `updated_at` timestamp NOT NULL DEFAULT current_timestamp(),

  FOREIGN KEY (`photo_id`) REFERENCES `photos` (`id`) ON DELETE CASCADE,
  FOREIGN KEY (`tag_id`) REFERENCES `tags` (`id`) ON DELETE CASCADE
);

CREATE TABLE `users` (
  `id` bigint PRIMARY KEY AUTO_INCREMENT,
  `email` varchar(50),
  `password` varchar(255),
  `role` varchar(50),

  `created_at` timestamp NOT NULL DEFAULT current_timestamp(),
  `updated_at` timestamp NOT NULL DEFAULT current_timestamp()
);

```
## INSERT
```
insert into categories(`name`) values ('Friend'), ('Family');
insert into photos(`title`,`category_id`,`image`) values ('T1',1,'image1'), ('T2',1,'image2');
insert into photo_descriptions(`photo_id`,`content`) values (1,'content1'), (2,'content2');
insert into tags(`name`) values ('house'), ('building'), ('beach'), ('forest');
insert into users(`email`,`password`,`role`) values ('admin@gmail.com','123','admin'), ('nam@gmail.com', 'abc', 'user');
insert into taggable(`tag_id`,`photo_id`) values (1,1) ,(1,2), (3,2), (2,1), (2,2);

```

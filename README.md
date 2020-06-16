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

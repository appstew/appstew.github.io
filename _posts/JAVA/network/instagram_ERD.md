- https://dbdiagram.io/d
```java
table users {
  id varchar [pk]
  img varchar
}

table post {
  id int [pk]
  user_id int
  user_img varchar
  img varchar
  text varchar
  like int
}

Ref: users.id > post.user_id
Ref: users.img > post.user_img
Ref: like.count > post.like


table hashtag {
  post_text int
  comment_text varchar
}

Ref: post.text > hashtag.post_text
Ref: comment.text > hashtag.comment_text


table comment {
  id int [pk]
  user_id int
  user_img varchar
  text varchar
  like int 
}

Ref: users.id > comment.user_id
Ref: users.img > comment.user_img

table follow {
  user_id int 
  user_img varchar 
  follow_count int
}

Ref: users.id > follow.user_id
Ref: users.img > follow.user_img

table follower {
  user_id varchar 
  user_img varchar 
  follower_count int
}

Ref: users.id > follower.user_id
Ref: users.img > follower.user_img

table like {
  user_id int
  count int
}

Ref: users.id > like.user_id
```
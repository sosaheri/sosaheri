---
layout: post
title: "D7 Laravel Relations"
date: 2022-07-04 14:30:00 +0400
categories: Laravel
---

### Laravel Relations

One to Many relationship will use when one table associated with multiple tables. For example, a post may have multiple comments. one to many eloquent relationship in laravel 6, laravel 7, laravel 8 and laravel 9 example.

So in this tutorial, you can understand how to create migration with a foreign key schema for one to many relationships, use sync with a pivot table, create records, get all data, delete, update and everything related to one to many relationships.

In this example, I will create a "posts" table and "comments" table. both tables are connected with each other. now we will create one to many relationships with each other by using the laravel Eloquent Model. We will first create database migration, then model, retrieve records and then how to create records too. So you can also see database table structure on below screen.

One to Many Relationship will use "hasMany()" and "belongsTo()" for relation.


Create Migrations:

Now we have to create migration of "posts" and "comments" table. we will also add foreign key with posts table. so let's create like as below:

posts table migration:

Schema::create('posts', function (Blueprint $table) {

    $table->increments('id');

    $table->string("name");

    $table->timestamps();

});

comments table migration:

Schema::create('comments', function (Blueprint $table) {

    $table->increments('id');

    $table->integer('post_id')->unsigned();

    $table->string("comment");

    $table->timestamps();

    $table->foreign('post_id')->references('id')->on('posts')

        ->onDelete('cascade');

});

Create Models:

Here, we will create Post and Comment table model. we will also use "hasMany()" and "belongsTo()" for relationship of both model.

Post Model:

<?php


namespace App;


use Illuminate\Database\Eloquent\Model;


class Post extends Model
{
    /**
     * Get the comments for the blog post.
     */
    public function comments()
    {
        return $this->hasMany(Comment::class);
    }
}

Comment Model:

<?php


namespace App;


use Illuminate\Database\Eloquent\Model;


class Comment extends Model
{
    /**
     * Get the post that owns the comment.
     */
    public function post()
    {
        return $this->belongsTo(Post::class);
    }
}

Retrieve Records:

$post = Post::find(1);
 
$comments = $post->comments;
 
dd($comments);
$comment = Comment::find(1);
 
$post = $comment->post;
 
dd($post);
Create Records:

$post = Post::find(1);
 
$comment = new Comment;
$comment->comment = "Hi ItSolutionStuff.com";
 
$post = $post->comments()->save($comment);

$post = Post::find(1);
 
$comment1 = new Comment;
$comment1->comment = "Hi ItSolutionStuff.com Comment 1";
 
$comment2 = new Comment;
$comment2->comment = "Hi ItSolutionStuff.com Comment 2";
 
$post = $post->comments()->saveMany([$comment1, $comment2]);

$comment = Comment::find(1);
$post = Post::find(2);
 
$comment->post()->associate($post)->save();




<script src="https://utteranc.es/client.js"
repo="sosaheri/sosaheri"
issue-term="pathname"
theme="github-light"
crossorigin="anonymous"
async>
</script>
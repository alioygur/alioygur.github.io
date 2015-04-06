---
layout: post
title: Laravel 4 Eloquent Accessors & Mutators tips tricks
categories: 
- laravel
---

Laravel 4 Eloquent ORM have a nice feature [Accessors & Mutators](http://laravel.com/docs/eloquent#accessors-and-mutators)

___

**What is this?**

that is like hook. You can define a hook on set/get.

**Let's define a Accessor**

    <?php

    /**
     * Post Model
     */
    class Post extends Eloquent 
    {
        /**
         * Replace newline to <br> on get
         * 
         * @param  string $value raw string
         * @return string modified string
         */
        public function getBodyAttribute($value)
        {
            return nl2br($value);
        }
    }

**Let's define a Mutator**

    <?php

    /**
     * Post Model
     */
    class Post extends Eloquent 
    {
        /**
         * strip html tags on set
         * 
         * @param string $value
         * @return void
         */
        public function setBodyAttribute($value)
        {
            $this->attributes['body'] = strip_tags($value);
        }
    }
    // End of file
    ?>

**Bonus**

When i do when i need raw data ? We may need it while editing.

    <textarea name="body"><?php $post->getOriginal("body") ?></textarea>

Can i define attribute which not exists on table

Yes Ofcourse! You can define like this

    <?php

    /**
     * UserProfile Model
     */
    class UserProfile extends Eloquent
    {
        /**
         * Get user fullname
         * You can access like this $model->full_name;
         * 
         * @return string
         */
        public function getFullNameAttribute()
        {
            return $this->firstname . ' ' . $this->lastname;
        }
    }
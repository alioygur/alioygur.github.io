---
layout: post
title: laravel4 redirect tips & tricks
---

laravel have have nice redirect options like `Redirect::guest` and `Redirect::intended`

The `Redirect::intended` create a new redirect response to the previously intended location.

**Here is source code**

    <?php    
    /**
    * Create a new redirect response to the previously intended location.
    *
    * @param  string  $default
    * @param  int     $status
    * @param  array   $headers
    * @param  bool    $secure
    * @return \Illuminate\Http\RedirectResponse
    */
    public function intended($default, $status = 302, $headers = array(), $secure = null)
    {
        $path = $this->session->get('url.intended', $default);
    
        $this->session->forget('url.intended');
    
        return $this->to($path, $status, $headers, $secure);
    }

The `Redirect::guest` create a new redirect response, while putting the current URL in the session.

**Here is source code**

    <?php          
    /**
    * Create a new redirect response, while putting the current URL in the session.
    *
    * @param  string  $path
    * @param  int     $status
    * @param  array   $headers
    * @param  bool    $secure
    * @return \Illuminate\Http\RedirectResponse
    */
    public function guest($path, $status = 302, $headers = array(), $secure = null)
    {
        $this->session->put('url.intended', $this->generator->full());
    
        return $this->to($path, $status, $headers, $secure);
    }

This functions use usually redirect the user to the URL they were trying to access before being caught by the authentication filter.

**Bonus**

if you using ajax on form processing, You can use `getTargetUrl()`

    <?php
    Route::post("auth/login", function()
    {
        // ... login process
    
        return Response::json(array(
            "location" => Redirect::intended("path/to/default")->getTargetUrl()
        ));
    });
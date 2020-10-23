# slim2-csrf
Simple Implementation of CSRF in Slim2 Framework


Getting Started
===================================

Download via composer with this command

  composer require cruxoid/slim2-csrf
  
Setting Up Reference
====================================

You might be having slim initiated like the following

```
$app = new \Slim\Slim(array(
        'templates.path' => './app/templates',
        'view' => new \Slim\Views\Twig(),
        'cookies.encrypt' => true,
               
       )    
);

```
Add the following line

```
$app->add( new  Cruxoid\Middleware\CsrfMiddleware);
```

You are all set, now head back to your twig template and add the following inside forms

```
<form action="/process" method="POST">
 <input type="hidden" class="form-control" name="{{csrf_key}}" value="{{csrf_token}}"/>
  
  Favorite color: <input type="text" name="favoriteColor">
  <button type="submit">Submit</button>
</form>

```
Validating CSRF Token
====================================

Validate post form data that contains CSRF Token aginst session data i.e.

```
 $csrf_token = $_POST['csrf_token'];
 $session_csrf_token = $_SESSION['csrf_token'];

if($csrf_token == $session_csrf_token){
//successfully token match, proceed with the form submission
} else {
//CSRF Voilated, error!!
}
```

You are all set!

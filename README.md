# Pagination for Wordpress
 > It's an extension kit for our theme https://github.com/hieu-pv/nf-theme and have use "illuminate/pagination" package of Symfony.
 
<a name="installation"></a>
##### Step 1: Install 
```
Updating ...
```

<a name="configuration"></a>
##### Step 2: Use
> Open `config/app.php` and register the required service provider.
```php
$paginator = new Paginator($data, $current_url, $current_page, $name_paging);
```

- Example:
```php
    /**
    * http://url?trang=1
    */
   
    global $wp;
    $page = 1;
    if(isset($_GET['trang']) && !empty($_GET['trang'])) {
        $page = $_GET['trang'];
    }

    $current_url = home_url(add_query_arg([], $wp->request));
    $user_id     = get_current_user_id();

    $all_notify  = User::where('user_id', $user_id)->orderBy('ID', 'DESC')->paginate(4,['*'], 'trang', $page)->setPageName("trang");


    $paginator = new Paginator($all_notify, $current_url, $page,'trang');
```

- Show paginator on html template
```php
<div>
	<?php $paginator->links(); ?>
</div>
```
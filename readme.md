# 安装过程

1. 2025/10/24 -- mysqli系列函数发生变化，校验更加严格，原有db不存在时逻辑会异常退出。直接替换。两处使用wp-db.php，均改为6.9版本的class-wpdb.php。
2. 2025/10/24 -- 删除调用wp_magic_quotes()的函数，原有get_magic_quotes_gpc函数在php8中被取消。
3. 2025/10/24 -- class-wpdb.php的函数check_database_version()调用了6.7才增加的新函数wp_get_wp_version()，改回原来的直接使用global $wp_version

# 静态解析

1. 2025/10/27 -- 为一些类追加#[ReturnTypeWillChange]属性。
2. 2025/10/27 -- 为一些类追加#[AllowDynamicProperties]属性。

# 运行错误

## login过程

1. 2025/10/27 -- wp_strip_all_tags()函数完全替换成6.x版本。
2. 2025/10/27 -- wp_signon()中$credentials的初始化不再是简单的array()，这会造成wp_authenticate()中直接用null的类型作trim，这在php8里不允许。
3. 2025/10/27 -- _wp_delete_tax_menu_item不能在第一个参数$object_id后面给默认值。

## wp-admin
### Home
1. 2025/10/28 -- http_build_query() 第二个参，从null改成'' -- cURL.php on line 327
2. 2025/10/28 -- setcookie() 第五个参，从null改成'' -- option.php on line 919,920
3. 2025/10/28 -- version_compare第一个参增加非null判断。 -- \wp-admin\includes\update.php  on line 608
4. 2025/10/28 -- compact()使用前要求每个变量都已经被定义。增加$groupby赋初始值。 -- class-wp-comment-query.php on line 459
5. 2025/10/28 -- 去掉\wp-includes\comment.php get_comment第一个参数前面的取地址符。这会导致\wp-includes\class-wp-comment-query.php on line 460的警告。

### Updates
1. 2025/10/29 -- http_build_query() 第二个参，从null改成'' -- \wp-includes\update.php on line 341

### All Posts
1. 2025/10/29 -- compact()使用前要求每个变量都已经被定义。增加$post_status，$perm，$order，$orderby赋初始值。 -- \wp-admin\includes\post.php:1080

### New Post
1. 2025/10/29 -- compact()使用前要求每个变量都已经被定义。导入6.9的$new_postarr取值小方法。此处另有从6.9获得的小改动。 -- \wp-includes\post.php on line 3482
2. 2025/10/29 -- 输入参使用前强转成string类型，将null变成空字符串。 -- wp-includes\formatting.php on line 4383


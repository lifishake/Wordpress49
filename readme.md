# 安装过程

1. 2025/10/24-- mysqli系列函数发生变化，校验更加严格，原有db不存在时逻辑会异常退出。直接替换。两处使用wp-db.php，均改为6.9版本的class-wpdb.php。
2. 2025/10/24-- 删除调用wp_magic_quotes()的函数，原有get_magic_quotes_gpc函数在php8中被取消。
3. 2025/10/24-- class-wpdb.php的函数check_database_version()调用了6.7才增加的新函数wp_get_wp_version()，改回原来的直接使用global $wp_version

# 静态解析

1. 2025/10/27-- 为一些类追加#[ReturnTypeWillChange]属性。
2. 2025/10/27-- 为一些类追加#[AllowDynamicProperties]属性。

# 运行错误

## login过程

1. 2025/10/27-- wp_strip_all_tags()函数完全替换成6.x版本。
2. 2025/10/27-- wp_signon()中$credentials的初始化不再是简单的array()，这会造成wp_authenticate()中直接用null的类型作trim，这在php8里不允许。
3. 2025/10/27-- _wp_delete_tax_menu_item不能在第一个参数$object_id后面给默认值。

# 安装过程
1. 2025/10/24-- mysqli系列函数发生变化，校验更加严格，原有db不存在时逻辑会异常退出。直接替换。两处使用wp-db.php，均改为6.9版本的class-wpdb.php。
2. 2025/10/24-- 删除调用wp_magic_quotes()的函数，原有get_magic_quotes_gpc函数在php8中被取消。
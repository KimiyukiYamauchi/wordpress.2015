# wordpressとphpその1

## 記事のタイトルと本文の表示

### テンプレートタグ

```
<?php if(have_posts()): while(have_posts()): the_post(); ?>

<?php the_title(); ?>

<?php the_content(); ?>

<?php endwhile; endif; ?>
```

### <?php ~ ?>の記述をまとめる

```
<?php

if(have_posts()):
	while(have_posts()):
		the_post();
		the_title();
		the_content();
	endwhile;
endif;

?>
```

### if ~　endif、while ~ endwhileを{ ~ }に変更

```
<?php

if(have_posts()){
	while(have_posts()){
		the_post(); // ループのための処理(wordpressの関数)
		the_title(); // タイトルの表示(wordpressの関数)
		the_content(); // 本文の表示(wordpressの関数)
	}
}

?>
```
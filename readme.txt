WordPressのプラグインです。
ですがテーマのfuncions.phpに記述しても同じ結果が得られます。
このコードはカテゴリーにテキスト色と背景色のカスタムフィールドを追加します。
カラー値の入力はテキストフィールドで直接入力できる他にカラーピッカーでも行えます。
テキストフィールドには16進数以外の文字は入力できません（多分）。
また、入力された値をもとにその場で配色を確認できます。

入力された値をテンプレートファイル内で使うときは
$term_data = get_option('term_'.カテゴリーID);
とし、
文字色は　$term_data['textcolor']
背景色は　$term_data['bgcolor']
となります。

サンプルコード（ループ内で）
$cats = get_the_category();
if ( $cats && ! is_wp_error( $cats ) ) : // 取得できたら
	foreach ( $cats as $cat ) { // 配列で戻ってきているのでループを回す
		$term_data = get_option('term_'.intval($cat->term_id));
		$term_bgcolor = ( empty( $term_data['bgcolor'] ) ) ? '#666' : $term_data['bgcolor'];
		$term_txcolor = ( empty( $term_data['textcolor'] ) ) ? '#fff' : $term_data['textcolor'];
		echo '<a href="'.get_term_link( $cat ).'" style="background-color: '.esc_attr($term_bgcolor).'; color: '.esc_attr($term_txcolor).';">'.$cat->name."</a> ";
	}
endif;

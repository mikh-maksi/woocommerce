# woocommerce
## Підключення верстки під плагін WooCommerce.
Woocommerce має наступні основні елементи відображення:
* Каталог товарів
* Сторінка товару
* Кошик
* Сторінка чекауту
* Сторінка "Дякую"

Також важливом в цілому є сторінка авторизації WordPress.  

Розглянемо основні елементи.
Сторінка товару:
* Основний файл \templates\single-product.php

В ньому ми маємо наступні хуки та елементи:
* Хук: woocommerce_before_main_content , елементи: woocommerce_output_content_wrapper - 10, woocommerce_breadcrumb - 20
* Цикл WordPress із підключенням шаблону контенту single-product
* Хук: woocommerce_after_main_content, елементи: woocommerce_output_content_wrapper_end - 10
* Хук: woocommerce_sidebar, елемент woocommerce_get_sidebar - 10


Основний цикл WordPress підключає файл:
**content-single-product.php**:
* Хук: woocommerce_before_single_product, елементи: woocommerce_output_all_notices - 10
* За необхідності пароля - вивод пароля: get_the_password_form
* блок із id
* Хук: woocommerce_before_single_product_summary, елементи: woocommerce_show_product_sale_flash, woocommerce_show_product_images

* 	<div class="summary entry-summary">
* Хук: woocommerce_single_product_summary, елементи: woocommerce_template_single_title, woocommerce_template_single_rating, woocommerce_template_single_price, woocommerce_template_single_excerpt, woocommerce_template_single_add_to_cart, woocommerce_template_single_meta, woocommerce_template_single_sharing, WC_Structured_Data::generate_product_data()
* Хук: woocommerce_after_single_product_summary, елементи: woocommerce_output_product_data_tabs, woocommerce_upsell_display, woocommerce_output_related_products
* Хук: woocommerce_after_single_product

# Плагін frequently-bought-together
Цей плагін дозволяє виводити декілька товарів разом.
Основний файл плагіна: wpc-frequently-bought-together.php
Задача по роботі із плагіном - виявити основні класи і їх вже переоформити, прописав потрібні стилі.

Класи:  
* Основна обертка (в тому числі по ціну внизу списку): woobt-wrap woobt-layout-default woobt-wrap-147 woobt-wrap-responsive
* Обертка товарів: woobt-products woobt-products-layout-default woobt-products-147
* Класи картки основного товару: woobt-product woobt-product-this
* Класи картки додаткових товарів: woobt-product woobt-product-this
* Елементи товару:
* * woobt-choose - чекбокс
* * woobt-thumb - картинка
* * woobt-title - назва
* * woobt-price - ціна

? Як підключити CSS спеціально під ці стилі?
Підключаємо до основного файлу style.css через імпорт: 

## Сторінка Чекауту.
Шаблон знаходиться за адресою: woocommerce/checkout/form-checkout.php  
Основна задача - підключити стилі, які вже створені на стандартну сторінку чекауту (бо поля для продажів створює сам WordPress)

## Використання API
Включаємо підтрику API для необхідного типу (lesson)

```
## Додаємо підтримку REST API для вже наявного типу запису
add_filter( 'register_post_type_args', 'my_custom_post_type_rest_support', 10, 2 );
function my_custom_post_type_rest_support( $args, $post_type ) {

	// переконаємось, що це наш тип запису
	if ( $post_type === 'lesson' ) {
		$args['show_in_rest']          = true;
		$args['rest_base']             = 'lesson';
		$args['rest_controller_class'] = 'WP_REST_Posts_Controller';
	}

	return $args;
}

```


Робимо запит:
https://www.course.innovations.kh.ua/wp-json/wp/v2/lesson/256

_links | wp:featuredmedia | 0 | href

"https://www.course.innovations.kh.ua/wp-json/wp/v2/media/318"

За цим посиланням отримаємо адресу картинки:

source_url : "https://www.course.innovations.kh.ua/wp-content/uploads/2023/07/image-409223145.png"


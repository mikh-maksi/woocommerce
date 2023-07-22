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
# -Tuto-R-glage-des-erreurs-PhpMyAdmin
[Tuto] Réglage des erreurs PhpMyAdmin

Réglage des erreurs PHPMYADMIN
Voici les erreurs que nous allons régler

Warning in ./libraries/sql.lib.php#613
error Notice in ./libraries/DisplayResults.php#1226

 La solution est de remplacer la ligne 613 du fichier /usr/share/phpmyadmin/libraries/sql.lib.php :
```
|| (count($analyzed_sql_results['select_expr'] == 1)

par

|| (count($analyzed_sql_results['select_expr']) == 1
Néanmoins, une erreur du même type peut persister lorsque l'on veut utiliser les fonction Import / Export. Il faut alors remplacer la ligne 551 du fichier /usr/share/phpmyadmin/libraries/plugin_interface.lib.php

       if ($options != null && count($options) > 0) {
par

       if ($options != null && count((array)$options) > 0) {
```
Ensuite restart quand meme le serveur apache2 : service apache2 restart

 

L'erreur final à régler /usr/share/phpmyadmin//libraries/DisplayResults.php         Ligne 1226

 


#remplacer sa
```
list($order_link, $sorted_header_html)
    = $this->_getOrderLinkAndSortedHeaderHtml(
        $fields_meta[$i], $sort_expression,
        $sort_expression_nodirection, $i, $unsorted_sql_query,
        $session_max_rows, $comments,
        $sort_direction, $col_visib,
        $col_visib[$j]
    );
```
#par sa
```
list($order_link, $sorted_header_html)
    = $this->_getOrderLinkAndSortedHeaderHtml(
        $fields_meta[$i], $sort_expression,
        $sort_expression_nodirection, $i, $unsorted_sql_query,
        $session_max_rows, $comments,
        $sort_direction, $col_visib,
        isset($col_visib[$j]) ? $col_visib[$j] : false
    );
```
Voila nous avons régler les erreurs PHPmyadmin 

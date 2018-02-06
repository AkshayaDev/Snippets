# Snippets
	/**
	* Updating parent on term edit screen
	*/
	add_filter('wp_update_term_parent','test_func',10,5);
	function test_func($parent, $term_id, $taxonomy, $parsed_args, $args) {
		return 19;
	}

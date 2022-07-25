# LoginRegister

Sir pls go read me to take the login and register PHP code

<--------------------------------------------------------------------------------------------------------------------------->
Login PHP Code connect to database

<?php

if ($_SERVER['REQUEST_METHOD']=='POST') {

    $email = $_POST['email'];
    $password = $_POST['password'];

    $dbc = mysqli_connect('localhost', 'root', '');
    mysqli_select_db($dbc, 'stopsmoking');

    $sql = "SELECT * FROM user WHERE email='$email' ";

    if ($r = mysqli_query($dbc, $sql)) {
		if (mysqli_num_rows($r) > 0) {
		//retrieve and print every record
			while ($row = mysqli_fetch_array($r)) {
				$response[0]['error'] = 0;
		$response[0]['message'] = "Welcome Login ";
		}
    }
		else {
            $response[0]['error'] = 1;
			$response[0]['message'] = "User not found.";
		}
		
	}
	else {
		$response[0]['error'] = 1;
		$response[0]['message'] = "Fail to display because " . mysqli_error($dbc) . "The query was: " . $query;
	}

	echo  json_encode($response);
}


?>

<--------------------------------------------------------------------------------------------------------------------------->

Register PHP Code connect to database

<?php
 
if ($_SERVER['REQUEST_METHOD']=='POST'){
 
    $name = $_POST['name'];
    $email = $_POST['email'];
    $password = $_POST['password'];
    $amt_cigarette = $_POST['amt_cigarette'];
    $price_cigarette = $_POST['price_cigarette'];
 
    $password = password_hash($password, PASSWORD_DEFAULT);

    $conn = mysqli_connect("localhost", "root", "", "stopsmoking");
 
    $sql = "INSERT INTO user (name, email, password, amt_cigarette, price_cigarette) VALUES ('$name', '$email', '$password', '$amt_cigarette', '$price_cigarette')";
 
    if (mysqli_query($conn, $sql)) {
   
        echo "Success! Congratulation your account has been register!";
        mysqli_close($conn);

    }else{

        echo "Fail to registration your account!";
        mysqli_close($conn);

    }
 
}
?>

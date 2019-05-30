# REGIS_LOGIN
<!DOCTYPE html>
<html>
<head>
  /** A Regform.html file**/
	<title>Registration Form</title>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"></script>
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"></script>
	<script src="https://use.fontawesome.com/releases/v5.6.1/js/all.js"></script>

	<link rel="stylesheet" href="formstyle.css">
</head>

<body>
/** FOR REGISTRATION **/
<div class="container-fliud">
<form class="main-form" action="processreg.php" method="POST">
	<h2>Sign Up</h2>
<!-- First name -->
  <div class="form-row">
	<div class="form-group col-md-6">
	  <label for="lastname">First Name</label>
	  <input type="text" name="firstname" class="form-control" required="true" placeholder="Enter first name" />
	</div>
<!-- Last Name -->
	<div class="form-group col-md-6">
	  <label for="lastname">Last Name</label>
  	  <input type="text" name="lastname" class="form-control" required="true" placeholder="Enter last name" />
	</div>
  </div>
<!-- Email -->
  <div class="form-row">
	<div class="form-group col-sm-12">
	  <label for="email">Email</label>
	  <input type="email" name="email" class="form-control" required="true" placeholder="Enter email address" />
	</div>
  </div>
<!-- Password -->
  <div class="form-row">
    <div class="form-group col-sm-12">
      <label for="password">Password</label>
      <input type="password" name="password" class="form-control" required="true" placeholder="Enter password" />
      <small>Enter a combination of at least six numbers, letters & punctuation marks (like! and &).</small>
    </div>
  </div>
<!-- Username -->
  <div class="form-row">
    <div class="form-group col-sm-12">
      <label for="username">Username</label>
      <input type="text" name="username" class="form-control" required="true" placeholder="Enter username" />
    </div>
  </div>
<!-- Gender -->
  <div class="form-row">
  	<label for="gender" class="radio-inline col-sm-4">Gender: </label>
	<div class="form-group col-sm-3">
	  <input type="radio" name="gender" value="F" checked="true" />Female<br/>
	  <input type="radio" name="gender" value="M" checked="true" />Male
<!--<div class="form-group col-sm-3">
	<select name="gender" class="form-control">
		<option value="male">Male</option>
		<option value="female">Female</option>
	</select>
	</div> -->
	</div>
  </div>
<!-- Date of Birth -->
  <div class="form-row">
  	<label for="dob" class="col-sm-4 col-form-label">Date of Birth:</label>
  	<div class="form-group col-md-6">
  	  <input type="date" name="dob" class="form-control">
  	</div>
  </div>
<!-- Secret word -->
  <div class="form-row">
    <div class="form-group col-sm-12">
      <label for="secretword">Secret Word</label>
      <input type="text" name="secretword" class="form-control" required="true" placeholder="Enter secret word" />
    </div>
  </div>

<!-- Submit and Reset buttons -->
  <input type="submit" name="signup-submit" class="btn btn-outline-success">
  <a href="loginform.html" class="btn btn-outline-primary">Login</a>

<!-- <input class="btn btn-outline-primary" type="reset" value="Reset"> -->
  <!--
  <div class="form-row">
  	<div class="form-group btn-inline col-sm-1 ">
	  <button type="submit" class="btn btn-outline-success">Submit</button>
	  <input class="btn btn-outline-primary" type="reset" value="Reset">
	</div>
  </div>
  -->
</form>
</body>
</html>

/** Process.php file **/

<?php
	$servername = "localhost";
	$username = "root";
	$password = "";
	$dbname = "gwdb";

// CREATE CONNECTION
	$conn = mysqli_connect($servername, $username, $password, $dbname);

/* // CHECK CONNECTION
	if (!$conn) {
   		die("Connection failed: " .mysqli_connect_error());
	}
	echo "Connected successfully";
*/

/* //CREATE DATABASE 
$sql = "CREATE DATABASE gwdb";
if (mysqli_query($conn, $sql)) {
    echo "Database created successfully";
} else {
    echo "Error creating database: " . mysqli_error($conn);
}
*/

/* //SQL TO CREATE A TABLE 
$sql = "CREATE TABLE Regtb (
id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY, 
FirstName VARCHAR(30) NOT NULL,
LastName VARCHAR(30) NOT NULL,
Email VARCHAR(50) NOT NULL,
Username VARCHAR(30) NOT NULL,
Password VARCHAR(20),
Gender Char(1),
Birth_Date DATE,
SecretWord VARCHAR(20) NOT NULL
)"; 
if (mysqli_query($conn, $sql)) {
    echo "Table Regtb created successfully";
} else {
    echo "Error creating table: " . mysqli_error($conn);
} */

//TO INSERT DATA INTO MYSQL
if(isset($_POST['signup-submit'])){
		$firstname = $_POST['firstname'];
		$lastname  = $_POST['lastname'];
		$email     = $_POST['email'];
		$username  = $_POST['username'];
		$password  = $_POST['password'];
		$gender    = $_POST['gender'];
		$dob       = $_POST['dob'];
		$secretword= $_POST['secretword'];

		//var_dump($_POST);

	$sql = "INSERT INTO Regtb (FirstName, LastName, Email, Username, Password, Gender, Birth_Date, SecretWord)
		VALUES('$firstname', '$lastname', '$email', '$username', '$password', '$gender', '$dob', '$secretword')";

	if(mysqli_query($conn, $sql)) 
	{
    	echo "New record created successfully";
	} 
	else 
	{
    	echo "Error: " . $sql . "<br>" .mysqli_error($conn);
	}
mysqli_close($conn);
}
?>

/*** Login.php file ***/

<!DOCTYPE html>
<html>
<head>
	<title>Login Form</title>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"></script>
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"></script>
	<script src="https://use.fontawesome.com/releases/v5.6.1/js/all.js"></script>

	<link rel="stylesheet" href="formstyle.css">
</head>
<body>
<form>
	<div class="container">
	  <form class="main-form" action="loginprocess.php" method="POST">
	    <h2>Login</h2>
 	<!-- Username -->
  	    <div class="form-row">
   		  <div class="form-group col-sm-12">
            <label for="username">Username</label>
            <input type="text" name="uname" class="form-control" required="true" placeholder="Enter username" />
          </div>
        </div>
    <!-- Password -->
  		<div class="form-row">
    	  <div class="form-group col-sm-12">
      		<label for="password">Password</label>
      		<input type="password" name="pword" class="form-control" required="true" placeholder="Enter password" />
    	  </div>
  		</div>
	<!-- Login & SignUp buttons -->
		<button type="submit" class="btn btn-outline-success" name="login-submit">Login</button>
  		<a href="regform.html" class="btn btn-outline-primary">Sign Up</a>
    </div>
</form>
</body>
</html>

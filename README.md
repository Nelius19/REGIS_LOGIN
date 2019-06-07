/****** Regisform.html *****/

<!DOCTYPE html>
<html>
<head>
	<title>Registration Form</title>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"></script>
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"></script>
	<script src="https://use.fontawesome.com/releases/v5.7.0/js/all.js"></script>

	<link rel="stylesheet" href="regformstyle.css">
</head>
<body>
<div class="container-fluid">
<form action="regformprocess.php" method="POST">
	<h3>Sign Up</h3>
<!-- First Name -->
  <div class="form-row">
	<div class="form-group col-md-6">
		<label for="firstname">First Name</label>
		<input type="text" name="firstname" class="form-control" required="true" placeholder="Enter first name"/>
	</div>
<!-- Last Name -->
	<div class="form-group col-md-6">
		<label for="Lastname">Last Name</label>
		<input type="text" name="lastname" class="form-control" required="true" placeholder="Enter last name"/>
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
  	  <input type="date" name="dob" class="form-control" required="true">
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
  <button type="submit" class="btn btn-outline-success" name="signup-submit">SIGNUP</button>
  <a href="loginform.html" class="btn btn-outline-primary">Login</a>
</form>
</div>
</body>
</html>

/******** Regformprocess.php ********/
<?php
	$servername = "localhost";
	$username = "root";
	$password = "";
	$dbname = "gwdb";

// CREATE CONNECTION
	$conn = mysqli_connect($servername, $username, $password, $dbname);

// CHECK CONNECTION
	if (!$conn) {
   		die("Connection failed: " .mysqli_connect_error());
	}
	echo "Connected successfully";

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

// TO INSERT DATA INTO MYSQL
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

/**** Regformstyle.css *****/
/* REGISTRATION FORM CSS */
body{
	background-image: url(img/img5.jpg);
	width: 100%;
	height: 100vh;
	color: #fff;
	font-family: fantasy;
	}
h3{
	text-align: center;
	padding-bottom: 1rem;
	}
.container-fluid{
	text-transform: uppercase;
	text-shadow: .1rem .1rem .5rem black;
	font-size: .8rem;
	width: 30rem;
	margin-top: 1vh; /* margin-top: 2vh; */
	border: 0rem solid #fff; /* .1rem */
	padding: 1.8rem;
	-webkit-box-shadow: 1px 4px 26px 11px rgba(0,0,0,0.75);
	-moz-box-shadow: 1px 4px 26px 11px rgba(0,0,0,0.75);
	box-shadow: 1px 4px 26px 11px rgba(0,0,0,0.75);
	}

/**** Loginform.html ****/
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
	<script src="https://use.fontawesome.com/releases/v5.7.0/js/all.js"></script>

	<link rel="stylesheet" href="loginformstyle.css">
</head>
<body>
<div class="container">
<form action="loginformprocess.php" method="POST">
	<h3>Login</h3>
 	<!-- Username -->
  	<div class="form-row">
   		<div class="form-group col-sm-12">
          <label for="username">Username</label>
          <i class="fas fa-user"></i>
          <input type="text" name="uname" class="form-control" required="true" placeholder="Enter username" />
        </div>
    </div>
    <!-- Password -->
  	<div class="form-row">
     	<div class="form-group col-sm-12">
      	  <label for="password">Password</label>
      	  <i class="fas fa-lock"></i>
      	  <input type="password" name="pword" class="form-control" required="true" placeholder="Enter password" />
    	</div>
  	</div>
	<!-- Login & SignUp buttons -->
		<button type="submit" class="btn btn-outline-success" name="login-submit">LOGIN</button>
  		<a href="regform.html" class="btn btn-outline-primary">Sign Up</a>
</form>
</div>
</body>
</html>


/**** Loginformprocess.php ****/
<?php
	$servername = "localhost";
	$username = "root";
	$password = "";
	$dbname = "gwdb";

// CREATE CONNECTION
	$conn = mysqli_connect($servername, $username, $password, $dbname);

/*// CHECK CONNECTION 
	if (!$conn) {
   		die("Connection failed: " .mysqli_connect_error());
	}
	echo "Connected successfully";
*/

if(isset($_POST['login-submit'])) {
	$name = $_POST['uname'];
	$pass = $_POST['pword'];

	$sql = "SELECT * FROM regtb WHERE Username='$name'&& Password='$pass'";

	$result = mysqli_query($conn, $sql);
	if(mysqli_num_rows($result) > 0)
	{
		header('location:dashboard.php');
	}
	else{
		header('location:loginform.html');
	}
}
?>

/* LOGIN FORM CSS */ //Loinform.css
body{
	background-image: url(img/img5.jpg);
	width: 100%;
	height: 100vh;
	color: #fff;
	font-family: fantasy;
	}
h3{
	text-align: center;
	padding-bottom: 1rem;
	}
.container{
	text-transform: uppercase;
	text-shadow: .1rem .1rem .5rem black;
	font-size: 1rem;
	width: 31rem;
	margin-top: 15vh; /* margin-top: 2vh; */
	border: 0rem solid #fff; /* .1rem */
	padding: 4rem;
	-webkit-box-shadow: 1px 4px 26px 11px rgba(0,0,0,0.75);
	-moz-box-shadow: 1px 4px 26px 11px rgba(0,0,0,0.75);
	box-shadow: 1px 4px 26px 11px rgba(0,0,0,0.75);
	}


/***** Dashboard.php ******/
<?php
	session_start();
?>
<!DOCTYPE html>
<html lang="en-US">
<head>
	<title>Welcome</title>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"></script>
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"></script>
	<script src="https://use.fontawesome.com/releases/v5.7.0/js/all.js"></script>

	<link rel="stylesheet" type="text/css" href="dboard.css">
	
</head>
<body>
<div class="container">
<form action="dboard.php" method="POST">  <!-- use if statement in the code to display... -->
<nav class="navbar navbar-expand-md navbar-dark bg-dark fixed-top">
	<ul class="navbar-nav">
		<li class="nav-item">
			<a class="nav-name">Dashboard Order</a>
		</li>
	</ul>
	<ul class="navbar-nav ml-auto">
		<?php
			echo $_SESSION['user']; 
		?>
		<button type="submit" name="logout-submit" class="btn btn-warning btn-md">
			<i class="fas fa-sign-out-alt"></i>Logout
		</button>
		</li>
	</ul>
</nav>
	<!-- For Large Pizza -->	<!-- class="inline col-md-5" align the input field on top of each other. -->
	<div class="form-row">
		<h3>Quantity</h3>
		<div class="form-group col-md-10">
		  <label for="pizzalarge" class="inline col-md-6">Large Pizza (ksh. 1,000):</label> 
		  <input type="number" name="LPNumber" min="0" max="1000">
		</div>
	</div>

	<!-- For Medium Pizza -->
	<div class="form-row">
		<div class="form-group col-md-10">
		  <label for="pizzamedium" class="inline col-md-6">Medium Pizza (ksh. 700):</label>
		  <input type="number" name="MPNumber" min="0" max="1000">
		</div>
	</div>

	<!-- For Small Pizza -->
	<div class="form-row">
		<div class="form-group col-md-10">
		  <label for="pizzasmall" class="inline col-md-6">Small Pizza (ksh. 400):</label>
		  <input type="number" name="SPNumber" min="0" max="1000">
		</div>
	</div>

	<!-- Extra Topping area -->
		<h3><u>Extra Toppings</u></h3>
		<input type="radio" name="topping" value="meat">Meat Toppings (ksh. 150)<br/>
		<input type="radio" name="topping" value="vegetable">Vegetable Toppings (ksh. 100)<br/>
		<input type="radio" name="topping" value="none">No Toppings (ksh. 0)

	<!-- Donation part -->
	<div class="button1 form-row">
   		<div class="form-group col-md-11">
			<label for="donation" class="inline col-md-4">Feed a Hungry Child Today?</label><br/>
			<input type="checkbox" name="donn" value="donate">Donate ksh 200
		</div>
	</div>

	<!-- Submit Order and Reset buttons -->
	<div class="button2 form-row">
	    <div class="form-group col-md-11">
	    	<button type="submit" class="btn btn-outline-primary" name="order-submit">ORDER</button>
			<button type="reset" class="btn btn-outline-success" name="reset">RESET</button>
	    </div>
	</div>
</form>
</div>
</body>
</html>

/*** dboard.php ***/
<?php
	session_start();

if(isset($_POST['logout-submit'])) 
	{
		unset($_SESSION['user']);
		unset($_SESSION['access']);
		session_destroy();
		header("location: loginform.html");
	}

// Variable and values
	$largepizza = 1000;
	$mediumpizza = 700;
	$smallpizza = 400;
	$meattopping = 150;
	$vegetopping = 100;
	$nonetopping = 0;
	$donors = 200;
	$total1 = "0";
	$total2 = "0";
	$total3 = "0";
	$final  = "0";
	$final1 = "0";
	$final2 = "0";
	$final3 = "0";


if(isset($_POST['order-submit']))
{
	$LPNumber = $_POST['LPNumber'];
	$MPNumber = $_POST['MPNumber'];
	$SPNumber = $_POST['SPNumber'];
	$topping  = $_POST['topping'];
	$donation = $_POST['donn'];

	//For Order
	if ($LPNumber > 0 || $MPNumber > 0 || $SPNumber > 0)
	{
		echo "Thank You For Your Order.<br/><br/>";
		echo "Order Details:<br/>";

		$total1 = $LPNumber * $largepizza;
		echo "$LPNumber x Large pizza = $total1 <br/>";
		$total2 = $MPNumber * $mediumpizza;
		echo "$MPNumber x Medium pizza = $total2 <br/>";
		$total3 = $SPNumber * $smallpizza;
		echo "$SPNumber x Small pizza = $total3 <br/>";
	
		$total = $LPNumber + $MPNumber + $SPNumber;

		echo "<br/>Extra Toppings";
	}
	//For Toppings
	if ($topping == "meat") 
	{
		echo "<br/>Meat Topping<br/>";
		$final1 = $total * $meattopping;
		echo "$total x Extra Toppings = $final1<br/><br/>";
	}
	elseif ($topping == "vegetable") 
	{
		echo "<br/>Vegetable Topping<br/>";
		$final2 = $total * $vegetopping;
		echo "$total x Extra Toppings = $final2<br/><br/>";
	}
	elseif ($topping == "none") 
	{
		echo "<br/>No Topping<br/>";
		$final3 = $total * $nonetopping;
		echo "$total x Extra Toppings = $final3<br/><br/>";
	}
	else
		echo "Please select a topping";

	///For Donation
	if ($donation == "donate") 
	{
		echo "Bless your kind soul for your 200 ksh donation!<br/>";
		$final = $total1 + $total2 + $total3 + $final1 + $final2 + $final3 + $donors;
		echo "Total is: $final";
	}

	elseif ($donation != "donate") 
	{
		$final = $total1 + $total2 + $total3 + $final1 + $final2 + $final3;
		echo "Total is: $final";
	}
	else
		echo "error";
}
?>

/**dboard.css**/

.navbar{
	font-weight: 700;
	text-shadow: 2px 2px 4px #000000;
	text-transform: uppercase;
	height: 2rem;
	background: rgba(0, 0, 0, .6)!important;
	}
.navbar-dark{
	color: gold;
	}
.btn-warning{
	text-transform: uppercase;
	text-shadow: 2px 2px 4px #000000;
	font-weight: 500;
	color: white;
	border: 0rem;
	margin-left: 2rem; /* Will increase the space between the name and logout button in the navbar */
	padding-top: .1rem;
	padding-bottom: .1rem;
	padding-left: .1rem;
	padding: right: .1rem;
	-webkit-animation: mymove 15s infinite;
	animation: mymove 15s infinite;s
	}
	@-webkit-keyframes mymove {
  	from {background-color: gold;}
  	to {background-color: green;}
  	}
/* Standard syntax */
	@keyframes mymove {
  	from {background-color: yellow;}
  	to {background-color: green;}
	}
h3{
	font-family: serif;
	padding-left: 15rem;
	}
.container{
	font-weight: 500;
	text-transform: uppercase;
	margin-top: 8vh;
	width: 50rem;
	color: #000000;
	border: .1rem solid #73AD21;
	padding: 1.2rem;
	}
.button1{
	text-align: center;
	}
.button2{
	margin-top: 1rem; /* Will put space between the button */
	padding-right: 1rem;
	}

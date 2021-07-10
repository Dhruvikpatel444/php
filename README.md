# php login
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">

    <title>Client Login</title>
  </head>
  <body>
    <?php
      $con = mysqli_connect("localhost","root","","student");
      session_start();
      if(isset($_POST['submit']))
      {
        $email = $_POST['email'];
        $mobile = $_POST['mobile'];
        
        $insert = mysqli_query($con,"SELECT * FROM `register` WHERE `email`='$email' AND `mobile`='$mobile' AND `status`='1'");
        
        $count = mysqli_num_rows($insert);
        if($count > 0)
        {
         $row = mysqli_fetch_array($insert);
          $_SESSION['email'] = $row['email'];
          $_SESSION['mobile'] = $row['mobile'];
          echo "<script>window.location.href='admin.php'</script>";          
        }
        else
        {
          echo "FAIL";
        }


        /*if($insert)
        {
          echo "Successfully Inserted Data";
        }
        else
        {
          echo "Insert Fail";
        }*/
      }
      echo $_SESSION['email'];
    ?>
    <section class="container mt-5 py-5 border">
      <h1 style="text-align: center;">Login</h1>
      <hr>
      <form method="POST">
        <div class="row mb-3">
          <label for="inputEmail3" class="col-sm-2 col-form-label">Email</label>
          <div class="col-sm-10">
            <input type="email" name="email" class="form-control" id="inputEmail3" required="">
          </div>
        </div>
        <div class="row mb-3">
          <label for="inputPassword3" class="col-sm-2 col-form-label">Password</label>
          <div class="col-sm-10">
            <input type="password" name="mobile" class="form-control" id="inputPassword3" required="Please enter strong password.!!">
          </div>
        </div>
        <div style="margin-left: 500px; margin-top: 50px;">
          <button type="submit" name="submit" class="btn btn-primary">Sign in</button>
          <a href="logout.php" class="btn btn-primary">Logout</a>
        </div>
        <div style="margin-left: 520px; margin-top: 20px;">
          <a href="forgotpass.php"><span>Forgot Password</span></a>
        </div>      
      </form>
    </section>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>

    
  </body>
</html>
#register php
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">

    <title>School Register</title>
  </head>
  <body>
    <?php
      $con = mysqli_connect("localhost","root","","student");
      if(isset($_POST['submit']))
      {
        $fname = $_POST['fname'];
        $lname = $_POST['lname'];
        $mname = $_POST['mname'];
        $email = $_POST['email'];
        $mobile = $_POST['mobile'];
        $address = $_POST['address'];
        $dob = $_POST['dob'];
        $gender = $_POST['gender'];
        $course = $_POST['course'];
        
        $insert = mysqli_query($con,"INSERT INTO `register`(`fname`,`lname`,`mname`,`email`,`mobile`,`address`,`gender`,`course`,`dob`) VALUES ('$fname','$lname','$mname','$email','$mobile','$address','$gender','$course','$dob')");

        /*if($insert)
        {
          echo "Successfully Inserted Data";
        }
        else
        {
          echo "Insert Fail";
        }*/
      }
    ?>
    <section class="container border mt-5 py-5">
      <h1 style="text-align: center;">Register</h1>
      <hr>
      <form method="POST">
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">First Name</label>
          <input type="text" name="fname" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
        </div>
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">Last Name</label>
          <input type="text" name="lname" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
        </div>
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">Middle Name</label>
          <input type="text" name="mname" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
        </div>
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">Email</label>
          <input type="email" name="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
        </div>
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">Mobile No.</label>
          <input type="text" name="mobile" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
        </div>
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">Address</label>
          <input type="text" name="address" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
        </div>
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">Date of Birth</label>
          <input type="date" name="dob" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
        </div>
        <div class="input-group mb-3">
          <label class="input-group-text" for="inputGroupSelect01">Course</label>
          <select class="form-select" name="course" id="inputGroupSelect01">
            <option selected>Choose...</option>
            <option value="BCA sem-1">BCA sem-1</option>
            <option value="BCOM sem-1">BCOM sem-1</option>
            <option value="BBA sem-1">BBA sem-1</option>
            <option value="MCA sem-3">MCA sem-3</option>
            <option value="MCOM sem-3">MCOM sem-3</option>
            <option value="MBA sem-1">MBA sem-1</option>
          </select>
        </div>

        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">Gender</label>
          &nbsp; &nbsp; &nbsp;

          <div class="form-check form-check-inline">
            <input class="form-check-input" type="radio" name="gender" id="inlineRadio1" value="Male">
            <label class="form-check-label" for="inlineRadio1">MALE</label>
          </div>
          <div class="form-check form-check-inline">
            <input class="form-check-input" type="radio" name="gender" id="inlineRadio2" value="Female">
            <label class="form-check-label" for="inlineRadio2">FEMALE</label>
          </div>
        </div>

        <button type="submit" name="submit" class="btn btn-primary">Submit</button>
      </form>

    </section>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>

  </body>
</html>
#logout php
<?php
     $con = mysqli_connect("localhost","root","","student");
      session_start();
      session_destroy();
      echo "<script>window.location.href='login.php'</script>";
?>
# forgot password php

<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">

    <title>Forgot Password</title>
  </head>
  <body>
    <?php
      $con = mysqli_connect("localhost","root","","student");
      if(isset($_POST['submit']))
      {
        $email = $_POST['email'];
        
        $insert = mysqli_query($con,"SELECT * FROM `register` WHERE `email`='$email' AND `status`='1'");
        
        $count = mysqli_num_rows($insert);
        if($count > 0)
        {
         $row = mysqli_fetch_array($insert);
          $_SESSION['email'] = $row['email'];
          echo "<script>window.location.href='resetpass.php'</script>";          
        }
        else
        {
          echo "FAIL";
        }


        /*if($insert)
        {
          echo "Successfully Inserted Data";
        }
        else
        {
          echo "Insert Fail";
        }*/
      }
      echo $_SESSION['email'];
    ?>
    
    <section id="" class="page-section pad-0">
      <div class="container relative pad-0 border mt-5 py5">
        <div class="m0w1180p">         
          <div class="tac" style="margin-left:400px;">
            <div style="width:380px;">
              <div class="title_bg">
                <div class="fll">
                  <h1 class="fll white" style="text-align: center;">Forgot Password</h1>
                  <hr>
                </div>
              </div>
            </div>
            <div class="clear "></div>
          </div>
        </div>                 
        <div class="m0w1180p">
          <div style="background:#FFF; width:380px!important; overflow:auto; height:auto; margin-left:400px; padding:20px;">
            <h5 class="" style="line-height:22px; text-align: center;">Kindly enter your email id in below given box to receive password reset instruction on your mail.</h5>    
            <br>
            <form id="formID" class="formular" method="post" onsubmit="return validateFormOnSubmit1(this)" action="">    
              <table width="100%" border="0" cellspacing="0" cellpadding="0">
                <tbody>
                  <tr>
                    <td width="100%" >
                      <strong>Enter your Email Address:</strong>
                      <input type="text" name="email" id="emailaddress" style="border:1px solid #CCC; background-color:#fff; height:35px; margin-bottom:5px; width:94%"></td>
                  </tr>
                  <tr>
                    <td>
                      <div style="margin-left: 120px; margin-top: 30px;">
                        <button type="submit" name="submit" class="btn btn-primary">submit</button>
                      </div>
                    </td>
                  </tr>
                </tbody>
              </table>
            </form><br><br>
          </div>
        </div>
      </div>
    </section>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>

    
  </body>
</html>
#reset password php
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">

    <title>Resect Password</title>
  </head>
  <body>
    <?php
      $con = mysqli_connect("localhost","root","","student");
      if(isset($_POST['submit']))
      {
        $email = $_POST['email'];
        $dob = $_POST['dob'];
        $mobile = $_POST['mobile'];
        
        $insert = mysqli_query($con,"SELECT * FROM `register` WHERE `email`='$email' AND `dob`='$dob'");
        
        $count = mysqli_num_rows($insert);
        if($count > 0)
        {
         $update = mysqli_query($con,"UPDATE `register` SET `mobile`='$mobile' WHERE `email`='$email' AND `dob`='$dob'");
          echo "<script>window.location.href='login.php'</script>";          
        }
        else
        {
          echo "FAIL";
        }
      }
      echo $_SESSION['email'];
    ?>
    
    <section id="" class="page-section pad-0 mt-5 py-5">
      <div class="container relative pad-0">         
        <form method="POST">
          <table class="table table-success table-striped">
            <thead>
                <h1 style="text-align: center;"><strong>Reset Password</strong></h1>
                <hr>
            </thead>
            <tbody>
              <tr>
                <td class="table-success">
                  <p><strong>Enter Email Id :</strong></p>
                </td>
                <td class="table-success">
                  <input type="email" name="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
                </td>
              </tr>
              <tr>
                <td class="table-success">
                  <p><strong>Enter Your Date of Birth :</strong></p>
                </td>
                <td class="table-success">
                  <input type="Date" name="dob" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
                </td>
              </tr>
              <tr>
                <td class="table-success">
                  <p><strong>Enter New Password :</strong></p>
                </td>
                <td class="table-success">
                  <input type="password" class="form-control validate[required] text-input" id="exampleInputEmail1" aria-describedby="emailHelp">
                </td>
              </tr>
              <tr>
                <td class="table-success">
                  <p><strong>Confirm Password :</strong></p>
                </td>
                <td class="table-success">
                  <input type="password" name="mobile" class="form-control validate[required,equals[password]] text-input" id="exampleInputEmail1" aria-describedby="emailHelp">
                </td>
              </tr>
            </tbody>
          </table>
          <div style="margin-left: 500px; margin-top: 30px;">
            <button type="submit" name="submit" class="btn btn-primary">submit</button>
          </div>
        </form>  
      </div>
    </section>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>

    
  </body>
</html>
# students list 
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">

    <title>Selected Student</title>
  </head>
  <body>
    <section class="container mt-5 py-5 ">
      <h1 style="text-align: center;">Selected Student Data</h1>
      <table class="table table-dark table-hover">
        <thead>
          <tr>
            <th scope="col">Sr.no</th>
            <th scope="col">Last Name</th>
            <th scope="col">First Name </th>
            <th scope="col">Middle Name</th>
            <th scope="col">Email</th>
            <th scope="col">Mobile No.</th>
            <th scope="col">Address</th>
            <th scope="col">Course</th>
            <th scope="col">Gender</th>
            <th scope="col">Date of Birth</th>
          </tr>
        </thead>
        <tbody>
          <?php
            $con = mysqli_connect("localhost","root","","student");
            $sel = mysqli_query($con,"SELECT * FROM `register` WHERE `status`='1'");
            $no = 0;
            while($row = mysqli_fetch_array($sel))
            {
              $no = $no + 1;
            
          ?>
          <tr>
            <th scope="row"><?php echo $no ?></th>
            <td><?php echo $row['lname']; ?></td>
            <td><?php echo $row['fname']; ?></td>
            <td><?php echo $row['mname']; ?></td>
            <td><?php echo $row['email']; ?></td>
            <td><?php echo $row['mobile']; ?></td>
            <td><?php echo $row['address']; ?></td>
            <td><?php echo $row['course']; ?></td>
            <td><?php echo $row['gender']; ?></td>
            <td><?php echo $row['dob']; ?></td>
          
          </tr>
        <?php } ?>
        </tbody>
      </table>
    </section>
    
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
  </body>
</html>
#pyramid php
<?php
// Php code to demonstrate
// star pattern

// Function to demonstrate
// printing pattern
function pypart($n)
{
    
    // Outer loop to handle number
    // of rowsn in this case
    for ($i = 0; $i < $n; $i++)
    {
        
        // inner loop to handle
        // number of columns
        // values changing acc.
        // to outer loop
        for($j = 0; $j <= $i; $j++ )
        {
            
            // Printing stars
            echo "* ";
        }

        // ending line after
        // each row
        echo "\n";
    }
}

    // Driver Code
    $n = 5;
    pypart($n);
?>
/*OUTPUT
* 
* * 
* * * 
* * * * 
* * * * * 
*/
<?php
// PHP code to demonstrate
// star pattern

// Function to demonstrate
// printing pattern
function pypart2($n)
{
    for ($i = 1; $i <= $n; $i++) {
        for ($j = 1; $j <= $n; $j++) {
            if($j<=($n-$i)){
                echo " "." ";
                
            }else {
                echo "* ";
            }
            
        }
        echo PHP_EOL;
    }
}

    // Driver Code
    $n = 5;
    pypart2($n);

?>
/*output
        * 
      * * 
    * * * 
  * * * * 
* * * * * 
*/
<?php
// PHP code to demonstrate
// star pattern

// Function to demonstrate
// printing pattern
function triangle($n)
{
    
    // number of spaces
    $k = 2 * $n - 2;

    // outer loop to handle
    // number of rows
    // n in this case
    for ($i = 0; $i < $n; $i++)
    {
        
        // inner loop to handle
        // number spaces
        // values changing acc.
        // to requirement
        for ($j = 0; $j < $k; $j++)
            echo " ";

        // decrementing k after
        // each loop
        $k = $k - 1;

        // inner loop to handle
        // number of columns
        // values changing acc.
        // to outer loop
        for ($j = 0; $j <= $i; $j++ )
        {
            
            // printing stars
            echo "* ";
        }

        // ending line after
        // each row
        echo "\n";
    }
}

    // Driver Code
    $n = 5;
    triangle($n);
    
?>
/*
    * 
   * * 
  * * * 
 * * * * 
* * * * * 
*/
<?php
    // code
// PHP code to demonstrate
// star pattern 2

// Function to demonstrate
// printing pattern 2
function triangle_pattern($len){
$string="*";
$pyramid_str="";
$mid_point=ceil($len/2);
for($i=1;$i<=$mid_point;$i++){
    for($j = 1; $j <= $i; ++$j) {
        $pyramid_str.=$string." ";
    }
    $pyramid_str.="\r\n";
}

for($i=$mid_point;$i>=1;$i--){
    for($j = 1; $j < $i; ++$j) {
        $pyramid_str.=$string." ";
    }
    $pyramid_str.="\r\n";
}

return $pyramid_str;
}
echo triangle_pattern(9);
?>
/*
* 
* * 
* * * 
* * * * 
* * * * * 
* * * * 
* * * 
* * 
* 
*/
<?php
// PHP code to demonstrate
// printing pattern of numbers

// Function to demonstrate
// printing pattern
function numpat($n)
{
    
    // initializing starting number
    $num = 1;

    // outer loop to handle
    // number of rows
    // n in this case
    for ($i = 0; $i < $n; $i++)
    {

        // inner loop to handle
        // number of columns
        // values changing acc.
        // to outer loop
        for ($j = 0; $j <= $i; $j++ )
        {
            
            // printing number
            echo $num." ";
        }
        
            // incrementing number
            // at each column
            $num = $num + 1;

        // ending line after
        // each row
        echo "\n";
    }
}

    // Driver Code
    $n = 5;
    numpat($n);

?>
/*
1 
2 2 
3 3 3 
4 4 4 4 
5 5 5 5 5
*/
<?php
// PHP code to demonstrate
// printing pattern of numbers

// Function to demonstrate
// printing pattern
function numpat($n)
{
    
    // initialising starting
    // number
    $num = 1;

    // outer loop to handle
    // number of rows
    // n in this case
    for ($i = 0; $i < $n; $i++)
    {
        
        // inner loop to handle
        // number of columns
        // values changing acc.
        // to outer loop
        for ($j = 0; $j <= $i; $j++ )
        {
            
            // printing number
            echo $num." ";

            // incrementing number
            // at each column
            $num = $num + 1;
        }

        // ending line after
        // each row
        echo "\n";
    }
}

    // Driver Code
    $n = 5;
    numpat($n);

?>
/*
1 
2 3 
4 5 6 
7 8 9 10 
11 12 13 14 15 
*/
<?php
// PHP code to demonstrate printing
// pattern of alphabets

// Function to demonstrate
// printing pattern
function alphapat($n)
{
    
    // initializing value
    // corresponding to 'A'
    // ASCII value
    $num = 65;

    // outer loop to handle
    // number of rows
    // n in this case
    for ($i = 0; $i < $n; $i++)
    {
        
        // inner loop to handle
        // number of columns
        // values changing acc.
        // to outer loop
        for ($j = 0; $j <= $i; $j++ )
        {
            
            // explicitly converting
            // to char
            $ch = chr($num);

            // printing char value
            echo $ch." ";
        }

        // incrementing number
        $num = $num + 1;

        // ending line after
        // each row
        echo "\n";
    }
}

    // Driver Code
    $n = 5;
    alphapat($n);
    
?>
/*
A 
B B 
C C C 
D D D D 
E E E E E
*/
<?php
// PHP code to demonstrate printing
// pattern of alphabets

// Function to demonstrate
// printing pattern
function contalpha($n)
{
    
    // initializing value
    // corresponding to 'A'
    // ASCII value
    $num = 65;

    // outer loop to handle
    // number of rows
    // n in this case
    for ($i = 0; $i < $n; $i++)
    {
        
        // inner loop to handle
        // number of columns
        // values changing acc.
        // to outer loop
        for ($j = 0; $j <= $i; $j++ )
        {
            
            // explicitely converting
            // to char
            $ch = chr($num);

            // printing char value
            echo $ch." ";

            // incrementing number
            // at each column
            $num = $num + 1;
        }

        // ending line after each row
        echo "\n";
    }
}

    // Driver Code
    $n = 5;
    contalpha($n);
    
?>
/*
A 
B C 
D E F 
G H I J 
K L M N O 
*/

<!DOCTYPE html>
<html>
  <head>
    <title>Registration Form</title>
    <style>
      /* Center the title */
      h1 {
        text-align: center;
        color: #00BFFF; /* blue color */
      }
      /* Center the submit button */
      input[type="submit"] {
        margin: 0 auto;
        width: 150px;
        height: 50px;
        font-size: 20px;
        display: block;
        margin: 30px auto;
        background-color:#00bfff;
        color:white;
      }
      /* Use Grid layout to separate title and rest of the form */
      body {
        display: grid;
        grid-template-columns: 1fr;
        grid-template-rows: auto 1fr;
        height: 100vh;
        margin: 0;
      }
      /* Add background color for title */
      .title {
        background-color: #F2F2F2; /* light gray color */
        padding: 20px;
      }
      /* Add space and background color between fields */
      .field {
        margin: 60px 0;
        padding: 10px;
        background-color: transparent; /* light gray color */
      }
      form {
        text-align:center;
      }
    </style>
  </head>
  <body>
    <div class="title">
      <h1>DEJMO FITNESS</h1>
    </div>
    <div>
      <form action="/register" method="POST">
        <div class="field">
          <label for="firstname">First Name:</label>
          <input type="text" id="firstname" name="firstname" required>
        </div>
        <div class="field">
          <label for="lastname">Last Name:</label>
          <input type="text" id="lastname" name="lastname" required>
        </div>
        <div class="field">
          <label for="email">Email:</label>
          <input type="email" id="email" name="email" required>
        </div>
        <div class="field">
          <label for="password">Password:</label>
          <input type="password" id="password" name="password" required>
        </div>
        <div class="field">
          <label for="dob">DOB:</label>
          <input type="date" id="dob" name="dob" required>
        </div>
        <div class="field">
          <label for="phone">Phone:</label>
          <input type="tel" id="phone" name="phone" required>
        </div>
        <div class="field">
          <input type="submit" value="Submit">
        </div>
      </form>
    </div>
  </body>
</html>
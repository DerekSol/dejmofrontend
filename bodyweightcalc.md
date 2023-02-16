<html>
<head>
	<title>Weight Tracker</title>
	<style>
		table, th, td {
			border: 1px solid black;
			border-collapse: collapse;
			padding: 5px;
		}
		th {
			background-color: #f2f2f2;
		}
	</style>
</head>
<body>
	<h1>Weight Tracker</h1>
	<form id="myForm">
		<label for="name">Name:</label>
		<input type="text" id="name" name="name"><br>

		<label for="weight">Weight:</label>
		<input type="number" id="weight" name="weight"><br>

		<label for="date">Date:</label>
		<input type="date" id="date" name="date"><br>

		<input type="button" value="Add" onclick="addRow()">
	</form>
	<br>
	<table id="myTable">
		<tr>
			<th>Name</th>
			<th>Weight</th>
			<th>Date</th>
			<th>Action</th>
		</tr>
	</table>
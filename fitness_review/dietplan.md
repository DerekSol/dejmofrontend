<!DOCTYPE html>
<html>
<head>
    <title>Personalized Diet Plan Generator</title>
</head>
<body>
    <h1>Personalized Diet Plan Generator</h1>
    <form>
        <label for="weight_goal">Weight goal:</label>
        <select id="weight_goal" name="weight_goal">
            <option value="lose">Lose weight</option>
            <option value="gain">Gain weight</option>
            <option value="maintain">Maintain weight</option>
        </select>
        <br>
        <label for="current_weight">Current weight:</label>
        <input type="number" id="current_weight" name="current_weight">
        <br>
        <label for="height">Height:</label>
        <input type="number" id="height" name="height">
        <br>
        <label for="age">Age:</label>
        <input type="number" id="age" name="age">
        <br>
        <label for="gender">Gender:</label>
        <select id="gender" name="gender">
            <option value="male">Male</option>
            <option value="female">Female</option>
        </select>
        <br>
        <button type="button" onclick="generateDiet()">Generate Diet Plan</button>
    </form>

    <div id="output"></div>

    <script src="script.js"></script>
</body>
</html>



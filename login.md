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

    <script>
        function generateDiet() {
            const weight_goal = document.getElementById('weight_goal').value;
            const current_weight = document.getElementById('current_weight').value;
            const height = document.getElementById('height').value;
            const age = document.getElementById('age').value;
            const gender = document.getElementById('gender').value;

            fetch('/generate_diet', {
                method: 'POST',
                body: JSON.stringify({weight_goal, current_weight, height, age, gender}),
                headers: {'Content-Type': 'application/json'}
            })
            .then(response => response.json())
            .then(data => {
                let output = '<h2>Diet Plan</h2>';
                output += '<h3>Breakfast</h3>';
                for (const [food, info] of Object.entries(data.breakfast)) {
                    output += '<p>' + food + ': ' + info.quantity + ' ' + info.unit + '</p>';
                }
                output += '<h3>Lunch</h3>';
                for (const [food, info] of Object.entries(data.lunch)) {
                    output += '<p>' + food + ': ' + info.quantity + ' ' + info.unit + '</p>';
                }
                output += '<h3>Dinner</h3>';
                for (const [food, info] of Object.entries(data.dinner)) {
                    output += '<p>' + food + ': ' + info.quantity + ' ' + info.unit + '</p>';
                }
                output += '<h3>Snack</h3>';
                for (const [food, info] of Object.entries(data.snack)) {
                    output += '<p>' + food + ': ' + info.quantity + ' ' + info.unit + '</p>';
                }
                document.getElementById('output').innerHTML = output;
            })
            .catch(error => console.error('Error:', error));
        }
    </script>
</body>
</html>

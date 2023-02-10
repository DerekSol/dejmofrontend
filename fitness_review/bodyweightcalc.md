<html>
    <head>
        <title>Body Weight Loss Calculator</title>
    </head>
    <body>
        <h1>Body Weight Loss Calculator</h1>
        <form>
            <h3>Personal Information:</h3>
            <p>
                <label>Gender:</label>
                <select id="gender" name="gender">
                    <option value="male">Male</option>
                    <option value="female">Female</option>
                </select>
            </p>
            <p>
                <label>Age:</label>
                <input type="number" id="age" name="age">
            </p>
            <p>
                <label>Weight (LBS):</label>
                <input type="number" id="weight" name="weight">
            </p>
            <p>
                <label>Height (IN):</label>
                <input type="number" id="height" name="height">
            </p>
            <p>
                <label>Activity Level:</label>
                <select id="activity_level" name="activity_level">
                    <option value="not active">Not Active</option>
                    <option value="sedentary">Sedentary</option>
                    <option value="lightly active">Lightly Active</option>
                    <option value="moderately active">Moderately Active</option>
                    <option value="very active">Very Active</option>
                    <option value="extra active">Extra Active</option>
                </select>
            </p>
            <p>
                <label>Goal Weight (LBS):</label>
                <input type="number" id="goal_weight" name="goal_weight">
            </p>
            <br>
            <input type="submit" value="Calculate Macros" onclick="calculateMacros()">
        </form>
        <div id="output"></div>
    </body>
    <script>
        function calculateMacros() {
            // get the values of each input field
            let gender = document.getElementById("gender").value;
            let age = document.getElementById("age").value;
            let weight = document.getElementById("weight").value;
            let height = document.getElementById("height").value;
            let activity_level = document.getElementById("activity_level").value;
            let workout_preference = document.getElementById("workout_preference").value;
            let goal_weight = document.getElementById("goal_weight").value;

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
                <select name="gender">
                    <option value="male">Male</option>
                    <option value="female">Female</option>
                </select>
            </p>
            <p>
                <label>Age:</label>
                <input type="number" name="age">
            </p>
            <p>
                <label>Weight (LBS):</label>
                <input type="number" name="weight">
            </p>
            <p>
                <label>Height (IN):</label>
                <input type="number" name="height">
            </p>
            <p>
                <label>Activity Level:</label>
                <select name="activity_level">
                    <option value="not active">Not Active</option>
                    <option value="sedentary">Sedentary</option>
                    <option value="lightly active">Lightly Active</option>
                    <option value="moderately active">Moderately Active</option>
                    <option value="very active">Very Active</option>
                    <option value="extra active">Extra Active</option>
                </select>
            </p>
            <br>
            <input type="submit" value="Calculate Macros">
        </form>
    </body>
</html>

<style>
  .search-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    padding: 20px;
  }
  .search-input {
    width: 300px;
    height: 50px;
    border: none;
    border-radius: 25px;
    padding: 0 20px;
    font-size: 20px;
    margin-right: 20px;
  }
  .search-button {
    width: 150px;
    height: 50px;
    background-color: #46CEE3;
    color: white;
    border: none;
    border-radius: 25px;
    font-size: 20px;
    cursor: pointer;
  }
</style>
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
            <p>
                <label>Workout Preference:</label>
                <select name="workout_preference">
                    <option value="Cardio"></option>
                    <option value="Lifting"></option>
                    <option value="Calisthenics"></option>
            </p>
            <p>
                <label>Goal Weight (LBS):</label>
                <input type="number" name="goal_weight">
            </p>
            <br>
            <input type="submit" value="Calculate Macroscq">
        </form>
    </body>
</html>
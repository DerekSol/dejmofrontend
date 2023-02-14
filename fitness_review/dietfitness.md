<html lang="en">
<head>
    <title>Diet Fitness</title>
</head>
<body>
    <h1>Diet Fitness</h1>
    <i>Enter your username to get started</i>
    <input placeholder="Username" id="user" />
    <p>If you already have saved diets, enter your username above and hit "load diets"</p>
    <button onclick="loadDiets()">Load Diets</button>

    <hr />
    <div id="existingDiets">
    </div>
    <div id="dietBox">
        <div>
    <h2>Add a diet</h2>
    <form id="adiet">
        <input placeholder="Diet Name" id="diet_name" />
        <input placeholder="Calories" id="calories" />
        <input placeholder="Protein" id="protein" />
        <input placeholder="Fat" id="fat" />
        <input placeholder="Carbs" id="carbs" />
        <textarea placeholder="Extra Notes" id="extra_notes"></textarea>
        <input type="submit" />
    </form>

</div>
<div id="previewDiet">
    <h2>Preview Diet</h2>
    <p id="DietName">Diet Name: N/A</p>
    <p id="Calories">Calories: N/A</p>
    <p id="Protein">Protein: N/A</p>
    <p id="Fat">Fat: N/A</p>
    <p id="Carbs">Carbs: N/A</p>
    <p id="ExtraNotes">Extra Notes: N/A</p>
    <button onclick="deleteDiet()">Delete Diet</button>
</div>
</div>

</body>

<script>
    let dietLoader = {}
    let currentDiet = -1
    // change in AWS
    const url = "http://localhost:8086/diet?"

    const previewDiet = (diet) => {
        document.getElementById("DietName").innerHTML = "Diet Name: " + diet.diet_name
        document.getElementById("Calories").innerHTML = "Calories: " + diet.calories
        document.getElementById("Protein").innerHTML = "Protein: " + diet.protein + " grams"
        document.getElementById("Fat").innerHTML = "Fat: " + diet.protein + " grams"
        document.getElementById("Carbs").innerHTML = "Carbs: " + diet.protein + " grams"
        document.getElementById("ExtraNotes").innerHTML = "Extra Notes:\n" + diet.extra_notes
        currentDiet = diet.id
    }

    const loadDiets = () => {
        const user = document.getElementById("user").value
        if (user === "") {alert("Invalid username!"); return}
        try {
        fetch(url + new URLSearchParams({username: user})).then(data => data.json()).then(json => {
            document.getElementById("existingDiets").innerHTML = ""
            
            json.forEach(diet => {
                const button = document.createElement("button")
                button.innerHTML = diet.diet_name
                dietLoader[diet.id] = JSON.parse(JSON.stringify(diet))
                button.onclick = () => previewDiet(dietLoader[diet.id])
                document.getElementById("existingDiets").appendChild(button)
            })

            localStorage.setItem("user", user)
        })
    } catch {
        alert("Username not found!")
    }
    }

    const deleteDiet = () => {
        if (currentDiet < 0) {
            alert("invalid diet!")
            return
        }

        fetch(url, {
            method: 'DELETE',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({id: currentDiet})
        }).then(() => {
            alert("Success, deleted!")
            loadDiets()
        })
    }

    document.getElementById("adiet").addEventListener("submit", (e) => {
        e.preventDefault();
        e.stopImmediatePropagation();
        const fields = [
            "diet_name",
            "user",
            "calories",
            "protein",
            "fat",
            "carbs",
            "extra_notes"
        ]
        const values = fields.map((f) => document.getElementById(f).value)
        if (values.indexOf("") !== -1) {
            alert("Please fill out all the fields!")
            return
        }

        const zip = (a, b) => a.map((k, i) => [k, b[i]]);
        const dict = Object.fromEntries(
            zip(
                fields.map(f => f.toLowerCase()), 
                values
            )
        )
        dict["username"] = dict["user"]
        delete dict["user"]
        dict["calories"] = parseInt(dict["calories"])
        dict["protein"] = parseInt(dict["protein"])
        dict["fat"] = parseInt(dict["fat"])
        dict["carbs"] = parseInt(dict["carbs"])

        fetch(url, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(dict)
        }).then((data) =>data.json()).then(data => {
            previewDiet(data)
            loadDiets()
        })
    })

    const maybeUser = localStorage.getItem("user")
    if (maybeUser !== null) {
        document.getElementById("user").value = maybeUser
        loadDiets()
    }
</script>

<style>
    input, textarea {
        display: block;
        width: 400px;

        background-color: white;
        outline: none;
        border: 1px solid brown;
        padding: 4px;
        margin: 6px 0px;
        font-size: 18px;
    }

    hr {
        margin-top: 20px;
    }

    #existingDiets {
        display: flex;
        gap: 15px;
        margin-bottom: 15px;
    }

    button {
        background-color: #ffcc00;
        outline: none;
        border: 1px solid #ffcc00;
        color: black;
        padding: 6px;
        font-size: 18px;
        transition: all 0.1s linear;
    }

    button:hover {
        background-color: #aa8800;
        border: 1px solid #aa8800;
        transform: translateY(-5px);
    }

    #dietBox {
        display: flex;
        flex-direction: row;
        gap: 40px
    }

    #previewDiet > p {
        margin: 4px 0px;
        font-size: 18px;
    }
</style>
</html>

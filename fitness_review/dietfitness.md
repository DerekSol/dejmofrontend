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
    <button id="update" type="submit">Update Diet</button>

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
    const baseurl = "http://127.0.0.1:8086/api/diets/";

    const previewDiet = (diet) => {
        document.getElementById("DietName").innerHTML = "Diet Name: " + diet.diet_name
        document.getElementById("Calories").innerHTML = "Calories: " + diet.calories
        document.getElementById("Protein").innerHTML = "Protein: " + diet.protein + " grams"
        document.getElementById("Fat").innerHTML = "Fat: " + diet.fat + " grams"
        document.getElementById("Carbs").innerHTML = "Carbs: " + diet.carbs + " grams"
        document.getElementById("ExtraNotes").innerHTML = "Extra Notes:\n" + diet.extra_notes
        currentDiet = diet.id
    }

    const loadDiets = () => {
        const user = document.getElementById("user").value
        const url = baseurl+user;
        if (user === "") {alert("Invalid username!"); return}
        try {
        fetch(url, {
            username : user
        }).then(data => data.json()).then(json => {
            document.getElementById("existingDiets").innerHTML = ""
            
            console.log(json)
            json.forEach(diet => {
                const button = document.createElement("button")
                button.innerHTML = diet.diet_name
                dietLoader[diet.id] = JSON.parse(JSON.stringify(diet))
                button.onclick = () => previewDiet(dietLoader[diet.id])
                document.getElementById("existingDiets").appendChild(button)
            })

            localStorage.setItem("user", user) //Used for redundancy in case user is undefined
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
        url = baseurl+'delete/'+currentDiet
        fetch(url, {
            method: 'DELETE',
            headers: {
                'Content-Type': 'application/json'
            }
        }).then(() => {
            alert("Success, deleted!")
            loadDiets()
        })
    }

    document.getElementById("adiet").addEventListener("submit", async (e) => { //post
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
        const url = 'http://127.0.0.1:8086/api/diets/post'
        const rawResponse = await fetch(url, {
            method: 'POST',
            body: JSON.stringify(dict),
            headers : {
                'Content-Type':'application/json'
            },
            data: {}
  });
  const content = await rawResponse.json();

  console.log(content);
    })

    const maybeUser = localStorage.getItem("user")
    if (maybeUser !== null) {
        document.getElementById("user").value = maybeUser
        loadDiets()
    }
document.getElementById("update").addEventListener("click", async (e) => { //put
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
        // content["message"]
        const dict = {}
        for (let i = 0; i < values.length; i++){
            if (values[i] != ""){
                dict[fields[i]] = values[i]
            }
        }
        // define url
        const user = document.getElementById("user").value
        const diet = document.getElementById("diet_name").value
        const url = "http://127.0.0.1:8086/api/diets/"+user+"_"+diet
        console.log(url)
        const rawResponse = await fetch(url, {
            method: 'PUT',
            body: JSON.stringify({"update" : dict}),
            headers : {
                'Content-Type':'application/json'
            },
            data: {}
        });
        const content = await rawResponse.json();
        if (content["message"] === "There is nothing like this!"){
            alert("There is nothing like this!")
        }
        else if(content["message"] === "Action Complete!"){
            alert("Action Complete!")
        }
        console.log(content);
})

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


**I have a 404 error when requesting openAI API**

>There could be a few reasons why you're seeing a 404 error when requesting the OpenAI API. Here are a few things you could try:
>
>1. Make sure that you're using the correct API endpoint and that you've entered it correctly in your code. The endpoint for the text-davinci-003 model is https://api.openai.com/v1/text-davinci-003/generate.
>2. Make sure that you have a valid API key and that you're including it in the request as the Authorization header. You can find your API key in the OpenAI API dashboard.
>3. Make sure that you're using the correct prompt parameter. The prompt should be a string containing the text you'd like the model to generate. For example, to generate a cocktail recipe with vodka as the base alcohol, you might use a prompt like Cocktail recipe with vodka.
>4. Make sure that you're using a supported model. The text-davinci-003 model supports generating up to 1024 tokens of text. If you're generating more than this, you might see a 404 error.
>
>I hope these suggestions are helpful! Let me know if you have any other questions or if you're still experiencing issues with the API.

---

**Can you modify the code to add Autorization header for my API key**


>Certainly! Here is the modified code that includes the Authorization header with your API key:
>
>```javascript
><html>
><head>
>  <title>The Cocktail Codex</title>
>  <link rel="icon" type="image/png" href="icon.png">
></head>
><body>
>  <h1>The Cocktail Codex</h1>
>  <h2>Randomly generated, expertly crafted</h2>
>  <div id="alcohol-buttons">
>    <button onclick="generateCocktail('vodka')">Vodka</button>
>    <button onclick="generateCocktail('rum')">Rum</button>
>    <button onclick="generateCocktail('gin')">Gin</button>
>    <button onclick="generateCocktail('tequila')">Tequila</button>
>  </div>
>  <div id="cocktail-recipe">
>    <!-- This div will be populated with the cocktail recipe -->
>  </div>
>  <div id="cocktail-image">
>    <!-- This div will be populated with the cocktail image -->
>  </div>
>  <script>
>    function generateCocktail(baseAlcohol) {
>      // Request a cocktail recipe from the OpenAI API
>      const recipeResponse = fetch(`https://api.openai.com/v1/text-davinci-003/generate?>prompt=Cocktail%20recipe%20with%20${baseAlcohol}&max_tokens=1024`, {
>        headers: {
>          'Authorization': 'Bearer YOUR_API_KEY'
>        }
>      });
>      recipeResponse
>        .then(response => response.json())
>        .then(recipe => {
>          // Extract the cocktail name and instructions from the recipe
>          const cocktailName = recipe.data.slice(0, recipe.data.indexOf('\n'));
>          const instructions = recipe.data.slice(recipe.data.indexOf('\n'));
>          // Display the cocktail name and instructions in the "cocktail-recipe" div
>          const recipeDiv = document.getElementById('cocktail-recipe');
>          recipeDiv.innerHTML = `<h3>${cocktailName}</h3><p>${instructions}</p>`;
>          // Request a cocktail image from the DALL-E API
>          const imageResponse = fetch(`https://api.openai.com/v1/images/generate?model=image-alpha-001&>prompt=${cocktailName}`, {
>            headers: {
>              'Authorization': 'Bearer YOUR_API_KEY'
>            }
>          });
>          imageResponse
>            .then(response => response.json())
>            .then(image => {
>              // Display the cocktail image in the "cocktail-image" div
>              const imageDiv = document.getElementById('cocktail-image');
>              imageDiv.innerHTML = `<img src="${image.data.url}" alt="${cocktailName}">`;
>            });
>        });
>    }
>  </script>
></body>
></html>
>```
>Be sure to replace YOUR_API_KEY with your actual API key.
>
>I hope this helps! Let me know if you have any other

---

**Modify the code to request OpenAI API and DALL-E API with XMLHttpRequest and POST**

Certainly! Here is the modified code that uses XMLHttpRequest and POST to request the OpenAI API:

>```javascript
><html>
><head>
>  <title>The Cocktail Codex</title>
>  <link rel="icon" type="image/png" href="icon.png">
></head>
><body>
>  <h1>The Cocktail Codex</h1>
>  <h2>Randomly generated, expertly crafted</h2>
>  <div id="alcohol-buttons">
>    <button onclick="generateCocktail('vodka')">Vodka</button>
>    <button onclick="generateCocktail('rum')">Rum</button>
>    <button onclick="generateCocktail('gin')">Gin</button>
>    <button onclick="generateCocktail('tequila')">Tequila</button>
>  </div>
>  <div id="cocktail-recipe">
>    <!-- This div will be populated with the cocktail recipe -->
>  </div>
>  <div id="cocktail-image">
>    <!-- This div will be populated with the cocktail image -->
>  </div>
>  <script>
>    function generateCocktail(baseAlcohol) {
>      // Create a new XMLHttpRequest object
>      const xhr = new XMLHttpRequest();
>      // Set the request method and endpoint
>      xhr.open('POST', 'https://api.openai.com/v1/text-davinci-003/generate');
>      // Set the request headers
>      xhr.setRequestHeader('Content-Type', 'application/json');
>      xhr.setRequestHeader('Authorization', 'Bearer YOUR_API_KEY');
>      // Set the request body
>      xhr.send(JSON.stringify({
>        prompt: `Cocktail recipe with ${baseAlcohol}`,
>        max_tokens: 1024
>      }));
>      // Handle the response
>      xhr.onload = function() {
>        if (xhr.status === 200) {
>          // Extract the cocktail name and instructions from the response
>          const cocktailName = xhr.response.data.slice(0, xhr.response.data.indexOf('\n'));
>          const instructions = xhr.response.data.slice(xhr.response.data.indexOf('\n'));
>          // Display the cocktail name and instructions in the "cocktail-recipe" div
>          const recipeDiv = document.getElementById('cocktail-recipe');
>          recipeDiv.innerHTML = `<h3>${cocktailName}</h3><p>${instructions}</p>`;
>          // Request a cocktail image from the DALL-E API
>          const imageResponse = new XMLHttpRequest();
>          imageResponse.open('POST', 'https://api.openai.com/v1/images/generate');
>          imageResponse.setRequestHeader('Content-Type', 'application/json');
>          imageResponse.setRequestHeader('Authorization', 'Bearer YOUR_API_KEY');
>          imageResponse.send(JSON.stringify({
>            model: 'image-alpha-001',
>            prompt: cocktailName
>          }));
>          imageResponse.onload = function() {
>            if (imageResponse.status === 200) {
>              // Display the cocktail image in the "cocktail-image" div
>              const imageDiv = document.getElementById('cocktail-image');
>              imageDiv.innerHTML = `<img src="${imageResponse.response.data.url}" alt="${cocktailName}">`;
>            }
>          }
>        };
>    }
>    }
>  </script>
></body>
></html>
>```

---

**NOTE : At this stage, we understood that ChatGPT had no clue about the OpenAI API interfaces changes that occured after 2021.**
**We decided to take back control, and manually modified the code.**
**Human made modifications are tagged with the following comment in the code (5 modifications, 7 lines)**
```javascript
// ;) Human Note :
```
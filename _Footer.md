```js
app.get("/", function(request, response){
   response.render("index.ejs", {list: "lists"});
});
```
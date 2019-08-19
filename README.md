# firebase-realtime-database-jsoneditor

This webapp is based off https://github.com/josdejong/jsoneditor

Modified to edit firebase real time db with additional options available
  - Sorting 
  - Find by ID
  - Query filtering 
  - Seraching 
  - Duplicate objects
  - Insert objects
  - Change types
  - and more
  
# Usage

Make the necessary changes to index.hmtl
  - Add firebase config
  - Moidify  [name_of_your_root] to match your json root in firebase realtime db
  
# Docs

Find the api docs for jsoneditor.js at https://github.com/josdejong/jsoneditor/blob/master/docs/api.md
 
```html
<!DOCTYPE HTML>
<html>
<head>
    <!-- when using the mode "code", it's important to specify charset utf-8 -->
    <meta http-equiv="Content-Type" content="text/html;charset=utf-8">

    <link href="jsoneditor.min.css" rel="stylesheet" type="text/css">
    <link href="custom.css" rel="stylesheet" type="text/css">
    <script src="jsoneditor.min.js"></script>
    <!-- Firebase App (the core Firebase SDK) is always required and must be listed first -->
    <script src="https://www.gstatic.com/firebasejs/6.0.2/firebase-app.js"></script>

    <!-- Add Firebase products that you want to use -->
    <script src="https://www.gstatic.com/firebasejs/6.0.2/firebase-auth.js"></script>
    <script src="https://www.gstatic.com/firebasejs/6.0.2/firebase-database.js"></script>
    <script>
        var firebaseConfig = {
           //TODO , Add Firebase config here
        };
    
        // Initialize Firebase
        firebase.initializeApp(firebaseConfig);
    </script>
</head>
<body>
    <div id="jsoneditor" style="width: 100%; height: 900px;"></div>

    <script>
        // create the editor
        var container = document.getElementById("jsoneditor");
        var options = {
            
            //Fires when any of the the json in the json edidor changes
            onChangeJSON: function(json){
                
                /* chnage  [name_of_your_root] to match your json root in firebase realtime db*/
                
                firebase.database().ref('/name_of_your_root').set(json);
            },

            onChangeText: function(jsonString){
                // Do something with the raw json
            }
        };

        var json = {}
        
        
         /* chnage  [name_of_your_root] to match your json root in firebase realtime db*/

        var rootRef = firebase.database().ref('/name_of_your_root');
        rootRef.once('value').then (function(snapshot) {
            
            json = snapshot.val()
            console.log(json)
            if(json){
                var editor = new JSONEditor(container, options, json);
                        
                // get json
                var json = editor.get();
            }
        });
            
    </script>
</body>
</html>
```

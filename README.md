
![Alt](https://www.media3.net/img/m3/m3-logo.png)|
|--|
## Synopsis
This session shall demonstrate the capabilities of Azure Cognitive Services - an API that leverages AI and ML to provide sentiment analysis, entity recognition, auto-translator, text-to-speech, speech translation, and many more services.


## Related links
[AI / Cognitive Services](https://cfsummit.adobeevents.com/attendease/networking/experience/bbe5ed14-8b56-41f1-831f-95f61ae709c0/3f61fb74-7a03-4593-ad0a-b373112cf62d)<br />
 [Media3 Github](https://github.com/Media3-Technologies)

## Javascript with Postman 
###### All of these examples are not performed in a single request but are working examples through out the entire collection. 
```javascript
// SET THE JSON RESPONSE
var  jsonData  =  pm.response.json();

// SET REQUEST VARIABLES
pm.environment.set("authorization_endpoint", jsonData.authorization_endpoint);
pm.environment.set("token_endpoint", jsonData.token_endpoint );

// AUTHENTICATION VARIABLES
pm.environment.set("access_token", jsonData.access_token );
pm.environment.set("refresh_token", jsonData.refresh_token );
```



## Setting the global variables
```javascript
var  template  =  `<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
	<table class="table table-striped">
		<tr>
			<th>Name</th>
			<th>Kind</th>
			<th>Email</th>
			<th>Endpoint</th>
			<th>ID</th>
		</tr>
		{{#each response.value}}
		<tr id=row_{{@key}} onClick="handleClick(this.id)">
			<td id={{@key}}>{{count}}</td>
			<td id={{@key}}>{{name}}</td>
			<td>{{kind}}</td>
			<td>{{properties.endpoint}}</td>
			<td id={{@key}} colspan="3">{{id}}</td>
		</tr>
		{{/each}}
	</table>`;


var  jsonData  =  pm.response.json();
var  activeAccountIndex  =  6;
pm.globals.set("activeAccount", jsonData.value[activeAccountIndex].id);

 
for( i  =  1; i  <  jsonData.value.length; i  ++ )
{
	/* * 
  I USED A NAMING SCHEMA WITH EITHER 
  CFSUMMIT- OR CFSUMMIT AT THE BEGINNING 
  AND CHOSE TO REMOVE IT AND MATCH THE NAME OF THE COGNITIVE SERVICE
	* */
  var  cleanedName  =  jsonData.value[i].name.replace( "cfsummit-","" );
	cleanedName  =  cleanedName.replace( "cfsummit","" );
	cleanedName  =  cleanedName.replace( "-","_" );
	pm.globals.set( cleanedName  +  "_endpoint" ,jsonData.value[i].properties.endpoint );
	pm.globals.set( cleanedName  +  "_resourceId" ,jsonData.value[i].id );
}

  
  
  

pm.visualizer.set(template, {
	response: pm.response.json()
});
```

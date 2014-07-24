# Coggle API Javascript Client
[![NPM version](https://badge.fury.io/js/coggle.svg)](http://badge.fury.io/js/coggle)

## Basic Use
See [coggle-issue-importer](http://github.com/coggle/coggle-issue-importer) or
[coggle-opml-importer](http://github.com/coggle/coggle-opml-importer) for
complete example applications, including authentication.

```bash
npm install coggle
```

```js
var CoggleApi = require('coggle');

var coggle = new CoggleApi({
  token:user_access_token
});

coggle.createDiagram(
    "My New Coggle"
    function(err, diagram){
        if(err)
            throw err;
        console.log("created diagram!", diagram);
    }
);
```


# API Documentation


##Class `CoggleApi`
The Coggle API client.

###Constructor
Create a new instance of the Coggle API client.

Example:
```js
new CoggleApi({token:user_auth_token})
```
Parameters:
  * **`options`** type: `Object`  
     Possible Options:
  * **`token`**, **required**: API user authentication token

###Method `createDiagram()`
Create a new Coggle diagram.

Parameters:
  * **`title`** type: `String`  
     Title for the created diagram.
  * **`callback`** type: `Function`  
     Callback accepting (Error, CoggleApiDiagram)

##Class `CoggleApiDiagram`
Coggle API Diagram object.

###Constructor
Create a new instance of a Coggle API Diagram object.

Parameters:
  * **`coggle_api`** type: `CoggleApi`  
     The API client used for accessing this diagram.
  * **`diagram_resource`** type: `Object`  
     Diagram Resource object, with at least `_id` and `title` fields

###Method `webUrl()`
Return the web URL for accessing this diagram.


###Method `getNodes()`
Get all of the nodes (branch elements) in a Diagram.

Parameters:
  * **`callback`** type: `Function`  
     Callback accepting (Error, [Array of CoggleApiNode])

##Class `CoggleApiNode`
Coggle API Node object, which represents individual parts("nodes") of the branches in a Coggle diagarm

###Constructor
Create a new instance of a Coggle API Node object.

Parameters:
  * **`coggle_api_diagram`** type: `CoggleApiDiagram`  
     The Diagram in which this node belongs.
  * **`node_resource`** type: `Object`  
     Node Resource object, with at least `_id` (`String`), `text` (`String`), and `offset` (`{x:Number, y:Number}`) fields.

###Method `addChild()`
Add a child to this item. The child is positioned relative to this item, and will move when you move this item.

Parameters:
  * **`text`** Text to add for the item.
  * **`offset`** type: `Object: {x:Number, y:Number}`  
     Offset of the new item from this one. The `x` coordinate is along the branch direction, the `y` coordinate is vertically down from the top of the document.
  * **`callback`** type: `Function`  
     Callback accepting (Error, CoggleApiNode)

###Method `update()`
Update the properties of this node

Parameters:
  * **`properties`** type: `Object: {text:String, offset:{x:Number, y:Number}, parent:String}`  
     Omitted properties are unmodified.
  * **`callback`** type: `Function`  
     Callback accepting (Error, CoggleApiNode)

###Method `setText()`
Set the text of this node.

Parameters:
  * **`text`** type: `String`  
     New text to set
  * **`callback`** type: `Function`  
     Callback accepting (Error, CoggleApiNode)

###Method `move()`
Move this node to a new offset relative to its parent.

Parameters:
  * **`offset`** type: `Object {x:Number, y:Number}`  
     New position to set
  * **`callback`** type: `Function`  
     Callback accepting (Error, CoggleApiNode)

###Method `remove()`
Remove this node, and all nodes descended from it.

Parameters:
  * **`callback`** type: `Function`  
     Callback accepting (Error)





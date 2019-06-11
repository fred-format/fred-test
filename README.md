# fred-test
A language agnostic test suite for FRED parsers.

It defines two groups of tests, invalid FRED Documents and valid
FRED Documents. 

Invalid tests have invalid
examples of FRED and parsers
should reject these documents.

Valid test have valid examples of FRED and an expected output as a JSON.

Parsers should accept these documents and also output the expected JSON. This output format is described below.

## JSON Encoding


* FRED Values corresponds to specific JSON Object 
    * ``{ "tag" : tagName, "meta" : metaData, "type": typeName, "value": value }``
    * typeName is the FRED types names
    * value is a JSON String, JSON Array or JSON Object representing the FRED Value. Can also be null.
    * tagName is a JSON String representing the FRED Tag
    * metaData is a JSON Array in the format
        * ``[{nameMeta : valueMeta}, {}, ...]``
        * nameMeta is a JSON String representing the metaName
        * valueMeta is ``{ "type": typeName, "value": value }``


### Example of JSON encoding

FRED Data
```
People (visible=1) [
    Person {
        name : "Richard"
        birth-date : 1997-12-08T12:32:45Z
        age : 21
    }
    Person {
        name : "Lucas"
        birth-date : 1997-08-07T02:46:15Z
        age : 21
    }
    Person {
        name : "Alax"
        birth-date : 1997-12-06T02:46:15Z
        age : 21
    }
]
```

JSON Data encoded
```
{
    "tag" : "People",
    "meta" : [{ "visible" : {"type" : "string", "value" : "1"} }],
    "type" : "array",
    "value" : [
        {
            "tag" : "Person", 
            "meta" : null, 
            "type" : "object",
            "value" : {
                "name" : {"tag" : null, "meta" : null, "type" : "string", "value" : "Richard"},
                "birth-date" : {"tag" : null, "meta" : null,"type" : "date", "value" : "1997-12-08T12:32:45Z"},
                "age" : { "tag" : null, "meta" : null, "type" : "string", "value" : "21"}
            }
        },
        {
            "tag" : "Person", 
            "meta" : null, 
            "type" : "object",
            "value" : {
                "name" : {"tag" : null, "meta" : null, "type" : "string", "value" : "Lucas"},
                "birth-date" : {"tag" : null, "meta" : null,"type" : "date", "value" : "1997-08-07T02:46:15Z"},
                "age" : { "tag" : null, "meta" : null, "type" : "string", "value" : "21"}
            }
        }
        {
            "tag" : "Person", 
            "meta" : null, 
            "type" : "object",
            "value" : {
                "name" : {"tag" : null, "meta" : null, "type" : "string", "value" : "Alax"},
                "birth-date" : {"tag" : null, "meta" : null,"type" : "date", "value" : "1997-12-06T02:46:15Z"},
                "age" : { "tag" : null, "meta" : null, "type" : "string", "value" : "21"}
            }
        }
    ]
}
```

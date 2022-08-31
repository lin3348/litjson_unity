### fork from litjson，modify the ToJson method for dump object purpose
* support exporting unity object to json with circulate reference
* support unity base type, for example Vector2, Vector3, Ray etc
* support custom filter type for ToJson method

### usage
```
      JsonWriter jw = new JsonWriter();
      jw.PrettyPrint = true;
      jw.IsRecyleRef = true;
      
      JsonMapper.ToJson(dataObject, jw, new List<Type>(){ typeof(YourClassThatDontBeSerialized) });
      var saveJsonStr = jw.TextWriter.ToString();
      
      // support utf-8 char
      var reg = new System.Text.RegularExpressions.Regex(@"(?i)\\[uU]([0-9a-f]{4})");
      saveJsonStr = reg.Replace(saveJsonStr, delegate (System.Text.RegularExpressions.Match m)
      {
          return ((char)System.Convert.ToInt32(m.Groups[1].Value, 16)).ToString();
      });
```

### How do I set the validations to continue even if there is an error, or to stop the first time an error is encountered?
* Use the CascadeMode. [See here](https://github.com/JeremySkinner/FluentValidation/wiki/Configuring-a-Validator#setting-the-cascade-mode)
* Or create an extension with "severity" [like this person did](https://fluentvalidation.codeplex.com/discussions/355890), so that only failures of validations with a certain "severity" stop the execution, while other failures allow the continuation of testing.   

### How do I get a list of all the rules per property that has been set
* use the following code in you validator: 

```C#
    public string AllRules()  
    {  
        string rules = "";  
        var d = this.CreateDescriptor();  
  
        foreach (var member in d.GetMembersWithValidators())  
            foreach (var rule in member)  
                rules += "property:" + member.Key + " validation:" + rule +  Environment.NewLine;  
        return rules;  
    }
```

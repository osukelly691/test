# FAQ - Frequently Asked Questions

### How do I set the validations to continue even if there is an error, or to stop the first time an error is encountered?
* Use the CascadeMode. [See here](https://github.com/JeremySkinner/FluentValidation/wiki/Configuring-a-Validator#setting-the-cascade-mode)
* Or create an extension with "severity" [like this person did](https://fluentvalidation.codeplex.com/discussions/355890), so that only failures of validations with a certain "severity" stop the execution, while other failures allow the continuation of testing.   

### How do I get a list of all the rules per property that has been set
* use the following code in you validator: 

```C#
    using FluentValidation.Internal;

    //... class definition with some rules defined during construction and then:

    public List<string>AllRules()
    {           
        var rules = new List<string>();
        var descriptor = this.CreateDescriptor();
        foreach( var member in descriptor.GetMembersWithValidators()  )
            foreach( var validationRule in descriptor.GetRulesForMember(member.Key)  )
            {
                var rule = (PropertyRule)validationRule; // cast 
                foreach( var validator  in rule.Validators )
                    rules.Add(
                        string.Format("validator:{0} | display:{1} | property:{2} | member:{3} | expression:{4}", 
                                            validator.ToString().Replace("FluentValidation.Validators.",""),
                                            rule.PropertyName,
                                            rule.GetDisplayName(),
                                            rule.Member,
                                            rule.Expression));
            }
        return rules;
    }

```

# Generic Entity Base

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=26TY9QLTDWDSE&lc=US&item_name=leandroberti&item_number=github&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donate_SM%2egif%3aNonHosted)

This is a template for creating entity models.

By using this template, we end up with the need to duplicate entity properties in view models that represent them.
The great advantage of this is that we exterminate the maintenance nightmare that usually entails in having to remember to mirror changes to the entity to its view models.


## How it works?

Using the power of interfaces, we create a entity base model that can be inherited from.

To help us a litle bit more, we implement those interfaces into two abstract classes `Entity` and `Entity<T>`.
The first must be used for entities with composite primary key and the seconde one shall be used for entities with single primary key where the gereric type `<T>` will be the primary key type.

All the properties of both abstract classes are virtual and can be overrided if needed.
A good example of this kind of need is: we dont't want store one of those properties into database, and to acomplish this, we need mark this property with `[NotMapped]` attribute.

## How to use this extension?

Here is a entity with composite primary key:

```C#
public class MyEntityWitCompositeKey : Entity
{
    public int EntityFirstCompsiteKey { get; set; }
    public int EntitySecondCompsiteKey { get; set; }

    [NotMapped]
    public override DateTime ModifiedDate { get; set; }

    public override object GetId()
    {
        return new object[] { EntityFirstCompsiteKey, EntitySecondCompsiteKey };
    }
}
```

And a entity with `integer` primary key

```C#
public class MyEntity : Entity<int>
{
    public override int Id { get; set; }

    [NotMapped]
    public override string ModifiedBy { get; set; }
}
```

## Where to get this extension?

You can install this extension direct from:

[![Nuget](https://img.shields.io/badge/nuget-v1.1.0-blue.svg)](https://www.nuget.org/packages/LMB.GenericEntityBase/)

Or instal with Package Manager Console

```C#
Install-Package LMB.GenericEntityBase
```

Or you can download this github project and copy the `Entity.cs` file, along with all interfaces files, direct into your project.

# Donations

**If you enjoy this work, please consider supporting me for developing and maintaining this (and others) templates.**

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=26TY9QLTDWDSE&lc=US&item_name=leandroberti&item_number=github&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donate_SM%2egif%3aNonHosted)

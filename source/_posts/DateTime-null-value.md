---
title: DateTime null value
date: 2020-11-23 12:24:32
tags:
  - .Net
  - C#
  - null value
category: .Net
author: Xavier
---

# NULL value for DateTime

For normal DateTimes, if you don't initialize them at all then they will match DateTime.MinValue, because it is a value type rather than a reference type.

You can also use a nullable DateTime, like this:

```CSharp
DateTime? MyNullableDate;
```

Or longer version:

```CSharp
Nullable<DateTime> MyNullableDate;
```

And, finally, there's a built in way to reference the default of any type. This returns null for reference types, but for our DateTime example it will return the same as DateTime.MinValue:

```CSharp
default(DateTime)
```

or, in more recent versions of C#,

```CSharp
default
```

And you can check the value with:

```CSharp
if (dt.HasValue)
{
  // Do something with dt.Value
}
```

Or you can use it like:

```CSharp
DateTime dt2 = dt ?? DateTime.MinValue;
```

You can read more here:
http://msdn.microsoft.com/en-us/library/b3h38hb0.aspx
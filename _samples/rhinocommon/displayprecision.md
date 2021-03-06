---
layout: code-sample
author:
platforms: ['Cross-Platform']
apis: ['RhinoCommon']
languages: ['C#', 'Python', 'VB.NET']
title: Changing Display Precision
keywords: ['changing', 'display', 'precision']
categories: ['Other']
description:
order: 1
---

```cs
partial class Examples
{
  public static Result DisplayPrecision(RhinoDoc doc)
  {
    var gi = new GetInteger();
    gi.SetCommandPrompt("New display precision");
    gi.SetDefaultInteger(doc.ModelDistanceDisplayPrecision);
    gi.SetLowerLimit(0, false);
    gi.SetUpperLimit(7, false);
    gi.Get();
    if (gi.CommandResult() != Result.Success)
      return gi.CommandResult();
    var distance_display_precision = gi.Number();

    if (distance_display_precision != doc.ModelDistanceDisplayPrecision)
      doc.ModelDistanceDisplayPrecision = distance_display_precision;

    return Result.Success;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Partial Friend Class Examples
  Public Shared Function DisplayPrecision(ByVal doc As RhinoDoc) As Result
	Dim gi = New GetInteger()
	gi.SetCommandPrompt("New display precision")
	gi.SetDefaultInteger(doc.ModelDistanceDisplayPrecision)
	gi.SetLowerLimit(0, False)
	gi.SetUpperLimit(7, False)
	gi.Get()
	If gi.CommandResult() <> Result.Success Then
	  Return gi.CommandResult()
	End If
	Dim distance_display_precision = gi.Number()

	If distance_display_precision IsNot doc.ModelDistanceDisplayPrecision Then
	  doc.ModelDistanceDisplayPrecision = distance_display_precision
	End If

	Return Result.Success
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
from Rhino import *
from Rhino.Input.Custom import *
from Rhino.Commands import *
from scriptcontext import doc
import rhinoscriptsyntax as rs

def RunCommand():
  distance_display_precision = rs.GetInteger("Display precision",
    doc.ModelDistanceDisplayPrecision, 0, 7)
  if distance_display_precision == None: return Result.Nothing

  if distance_display_precision <> doc.ModelDistanceDisplayPrecision:
    doc.ModelDistanceDisplayPrecision = distance_display_precision

  return Result.Success

if __name__ ==  "__main__":
  RunCommand()
```
{: #py .tab-pane .fade .in}


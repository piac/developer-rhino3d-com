---
layout: code-sample
author:
platforms: ['Cross-Platform']
apis: ['RhinoCommon']
languages: ['C#', 'Python', 'VB.NET']
title: Read Dimension Text
keywords: ['read', 'dimension', 'text']
categories: ['Other']
description:
order: 1
---

```cs
partial class Examples
{
  public static Result ReadDimensionText(RhinoDoc doc)
  {
    var go = new GetObject();
    go.SetCommandPrompt("Select annotation");
    go.GeometryFilter = ObjectType.Annotation;
    go.Get();
    if (go.CommandResult() != Result.Success) 
      return Result.Failure;
    var annotation = go.Object(0).Object() as AnnotationObjectBase;
    if (annotation == null)
      return Result.Failure;

    RhinoApp.WriteLine("Annotation text = {0}", annotation.DisplayText);

    return Result.Success;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Partial Friend Class Examples
  Public Shared Function ReadDimensionText(ByVal doc As RhinoDoc) As Result
	Dim go = New GetObject()
	go.SetCommandPrompt("Select annotation")
	go.GeometryFilter = ObjectType.Annotation
	go.Get()
	If go.CommandResult() <> Result.Success Then
	  Return Result.Failure
	End If
	Dim annotation = TryCast(go.Object(0).Object(), AnnotationObjectBase)
	If annotation Is Nothing Then
	  Return Result.Failure
	End If

	RhinoApp.WriteLine("Annotation text = {0}", annotation.DisplayText)

	Return Result.Success
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
from Rhino import *
from Rhino.DocObjects import *
from Rhino.Commands import *
from Rhino.Input.Custom import *
import rhinoscriptsyntax as rs

def RunCommand():
  go = GetObject()
  go.SetCommandPrompt("Select annotation")
  go.GeometryFilter = ObjectType.Annotation
  go.Get()
  if go.CommandResult() <> Result.Success:
    return Result.Failure
  annotation = go.Object(0).Object()
  if annotation == None or not isinstance(annotation, AnnotationObjectBase):
    return Result.Failure

  print "Annotation text = {0}".format(annotation.DisplayText)

  return Result.Success

if __name__ == "__main__":
  RunCommand()
```
{: #py .tab-pane .fade .in}


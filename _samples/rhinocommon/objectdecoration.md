---
layout: code-sample
author:
platforms: ['Cross-Platform']
apis: ['RhinoCommon']
languages: ['C#', 'Python', 'VB.NET']
title: Adding Arrowheads to Curves
keywords: ['adding', 'arrowheads', 'curves']
categories: ['Adding Objects', 'Curves']
description:
order: 1
---

```cs
partial class Examples
{
  public static Rhino.Commands.Result ObjectDecoration(Rhino.RhinoDoc doc)
  {
    // Define a line
    var line = new Rhino.Geometry.Line(new Rhino.Geometry.Point3d(0, 0, 0), new Rhino.Geometry.Point3d(10, 0, 0));

    // Make a copy of Rhino's default object attributes
    var attribs = doc.CreateDefaultAttributes();

    // Modify the object decoration style
    attribs.ObjectDecoration = Rhino.DocObjects.ObjectDecoration.BothArrowhead;

    // Create a new curve object with our attributes
    doc.Objects.AddLine(line, attribs);
    doc.Views.Redraw();

    return Rhino.Commands.Result.Success;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Partial Friend Class Examples
  Public Shared Function ObjectDecoration(ByVal doc As Rhino.RhinoDoc) As Rhino.Commands.Result
	' Define a line
	Dim line = New Rhino.Geometry.Line(New Rhino.Geometry.Point3d(0, 0, 0), New Rhino.Geometry.Point3d(10, 0, 0))

	' Make a copy of Rhino's default object attributes
	Dim attribs = doc.CreateDefaultAttributes()

	' Modify the object decoration style
	attribs.ObjectDecoration = Rhino.DocObjects.ObjectDecoration.BothArrowhead

	' Create a new curve object with our attributes
	doc.Objects.AddLine(line, attribs)
	doc.Views.Redraw()

	Return Rhino.Commands.Result.Success
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
import Rhino
import scriptcontext

def ObjectDecoration():
    # Define a line
    line = Rhino.Geometry.Line(Rhino.Geometry.Point3d(0, 0, 0), Rhino.Geometry.Point3d(10, 0, 0))

    # Make a copy of Rhino's default object attributes
    attribs = scriptcontext.doc.CreateDefaultAttributes()

    # Modify the object decoration style
    attribs.ObjectDecoration = Rhino.DocObjects.ObjectDecoration.BothArrowhead

    # Create a new curve object with our attributes
    scriptcontext.doc.Objects.AddLine(line, attribs)
    scriptcontext.doc.Views.Redraw()

if __name__ == "__main__":
    ObjectDecoration()
```
{: #py .tab-pane .fade .in}


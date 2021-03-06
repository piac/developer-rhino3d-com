---
layout: code-sample
author:
platforms: ['Cross-Platform']
apis: ['RhinoCommon']
languages: ['C#', 'Python', 'VB.NET']
title: Add Torus
keywords: ['add', 'torus']
categories: ['Adding Objects']
description:
order: 1
---

```cs
partial class Examples
{
  public static Rhino.Commands.Result AddTorus(Rhino.RhinoDoc doc)
  {
    const double major_radius = 4.0;
    const double minor_radius = 2.0;

    Rhino.Geometry.Plane plane = Rhino.Geometry.Plane.WorldXY;
    Rhino.Geometry.Torus torus = new Rhino.Geometry.Torus(plane, major_radius, minor_radius);
    Rhino.Geometry.RevSurface revsrf = torus.ToRevSurface();
    if (doc.Objects.AddSurface(revsrf) != Guid.Empty)
    {
      doc.Views.Redraw();
      return Rhino.Commands.Result.Success;
    }
    return Rhino.Commands.Result.Failure;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Partial Friend Class Examples
  Public Shared Function AddTorus(ByVal doc As Rhino.RhinoDoc) As Rhino.Commands.Result
	Const major_radius As Double = 4.0
	Const minor_radius As Double = 2.0

	Dim plane As Rhino.Geometry.Plane = Rhino.Geometry.Plane.WorldXY
	Dim torus As New Rhino.Geometry.Torus(plane, major_radius, minor_radius)
	Dim revsrf As Rhino.Geometry.RevSurface = torus.ToRevSurface()
	If doc.Objects.AddSurface(revsrf) <> Guid.Empty Then
	  doc.Views.Redraw()
	  Return Rhino.Commands.Result.Success
	End If
	Return Rhino.Commands.Result.Failure
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
import Rhino
import scriptcontext
import System.Guid

def AddTorus():
    major_radius = 4.0
    minor_radius = 2.0

    plane = Rhino.Geometry.Plane.WorldXY
    torus = Rhino.Geometry.Torus(plane, major_radius, minor_radius)
    revsrf = torus.ToRevSurface()

    if scriptcontext.doc.Objects.AddSurface(revsrf)!=System.Guid.Empty:
        scriptcontext.doc.Views.Redraw()
        return Rhino.Commands.Result.Success
    return Rhino.Commands.Result.Failure


if __name__=="__main__":
    AddTorus()
```
{: #py .tab-pane .fade .in}


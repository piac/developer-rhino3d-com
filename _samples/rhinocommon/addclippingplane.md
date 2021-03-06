---
layout: code-sample
author:
platforms: ['Cross-Platform']
apis: ['RhinoCommon']
languages: ['C#', 'Python', 'VB.NET']
title: Add Clipping Plane
keywords: ['add', 'clipping', 'plane']
categories: ['Adding Objects']
description:
order: 1
---

```cs
partial class Examples
{
  public static Rhino.Commands.Result AddClippingPlane(Rhino.RhinoDoc doc)
  {
    // Define the corners of the clipping plane
    Rhino.Geometry.Point3d[] corners;
    Rhino.Commands.Result rc = Rhino.Input.RhinoGet.GetRectangle(out corners);
    if (rc != Rhino.Commands.Result.Success)
      return rc;

    // Get the active view
    Rhino.Display.RhinoView view = doc.Views.ActiveView;
    if (view == null)
      return Rhino.Commands.Result.Failure;

    Rhino.Geometry.Point3d p0 = corners[0];
    Rhino.Geometry.Point3d p1 = corners[1];
    Rhino.Geometry.Point3d p3 = corners[3];

    // Create a plane from the corner points
    Rhino.Geometry.Plane plane = new Rhino.Geometry.Plane(p0, p1, p3);

    // Add a clipping plane object to the document
    Guid id = doc.Objects.AddClippingPlane(plane, p0.DistanceTo(p1), p0.DistanceTo(p3), view.ActiveViewportID);
    if (id != Guid.Empty)
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
  Public Shared Function AddClippingPlane(ByVal doc As Rhino.RhinoDoc) As Rhino.Commands.Result
	' Define the corners of the clipping plane
	Dim corners() As Rhino.Geometry.Point3d = Nothing
	Dim rc As Rhino.Commands.Result = Rhino.Input.RhinoGet.GetRectangle(corners)
	If rc IsNot Rhino.Commands.Result.Success Then
	  Return rc
	End If

	' Get the active view
	Dim view As Rhino.Display.RhinoView = doc.Views.ActiveView
	If view Is Nothing Then
	  Return Rhino.Commands.Result.Failure
	End If

	Dim p0 As Rhino.Geometry.Point3d = corners(0)
	Dim p1 As Rhino.Geometry.Point3d = corners(1)
	Dim p3 As Rhino.Geometry.Point3d = corners(3)

	' Create a plane from the corner points
	Dim plane As New Rhino.Geometry.Plane(p0, p1, p3)

	' Add a clipping plane object to the document
	Dim id As Guid = doc.Objects.AddClippingPlane(plane, p0.DistanceTo(p1), p0.DistanceTo(p3), view.ActiveViewportID)
	If id <> Guid.Empty Then
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

def AddClippingPlane():
    # Define the corners of the clipping plane
    rc, corners = Rhino.Input.RhinoGet.GetRectangle()
    if rc!=Rhino.Commands.Result.Success: return rc

    # Get the active view
    view = scriptcontext.doc.Views.ActiveView
    if view is None: return Rhino.Commands.Result.Failure

    p0, p1, p2, p3 = corners
    # Create a plane from the corner points
    plane = Rhino.Geometry.Plane(p0, p1, p3)

    # Add a clipping plane object to the document
    id = scriptcontext.doc.Objects.AddClippingPlane(plane, p0.DistanceTo(p1), p0.DistanceTo(p3), view.ActiveViewportID)
    if id!=System.Guid.Empty:
        scriptcontext.doc.Views.Redraw()
        return Rhino.Commands.Result.Success
    return Rhino.Commands.Result.Failure

if __name__=="__main__":
    AddClippingPlane()
```
{: #py .tab-pane .fade .in}


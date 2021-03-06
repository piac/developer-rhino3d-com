---
layout: code-sample
author:
platforms: ['Cross-Platform']
apis: ['RhinoCommon']
languages: ['C#', 'Python', 'VB.NET']
title: Add a layout with a detail view
keywords: ['add', 'layout', 'with', 'detail', 'view']
categories: ['Adding Objects', 'Viewports and Views']
description:
order: 1
---

```cs
partial class Examples
{
  /// <summary>
  /// Generate a layout with a single detail view that zooms to a list of objects
  /// </summary>
  /// <param name="doc"></param>
  /// <returns></returns>
  public static Rhino.Commands.Result AddLayout(Rhino.RhinoDoc doc)
  {
    doc.PageUnitSystem = Rhino.UnitSystem.Millimeters;
    var page_views = doc.Views.GetPageViews();
    int page_number = (page_views==null) ? 1 : page_views.Length + 1;
    var pageview = doc.Views.AddPageView(string.Format("A0_{0}",page_number), 1189, 841);
    if( pageview!=null )
    {
      Rhino.Geometry.Point2d top_left = new Rhino.Geometry.Point2d(20,821);
      Rhino.Geometry.Point2d bottom_right = new Rhino.Geometry.Point2d(1169, 20);
      var detail = pageview.AddDetailView("ModelView", top_left, bottom_right, Rhino.Display.DefinedViewportProjection.Top);
      if (detail != null)
      {
        pageview.SetActiveDetail(detail.Id);
        detail.Viewport.ZoomExtents();
        detail.DetailGeometry.IsProjectionLocked = true;
        detail.DetailGeometry.SetScale(1, doc.ModelUnitSystem, 10, doc.PageUnitSystem);
        // Commit changes tells the document to replace the document's detail object
        // with the modified one that we just adjusted
        detail.CommitChanges();
      }
      pageview.SetPageAsActive();
      doc.Views.ActiveView = pageview;
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
  ''' <summary>
  ''' Generate a layout with a single detail view that zooms to a list of objects
  ''' </summary>
  ''' <param name="doc"></param>
  ''' <returns></returns>
  Public Shared Function AddLayout(ByVal doc As Rhino.RhinoDoc) As Rhino.Commands.Result
	doc.PageUnitSystem = Rhino.UnitSystem.Millimeters
	Dim page_views = doc.Views.GetPageViews()
	Dim page_number As Integer = If(page_views Is Nothing, 1, page_views.Length + 1)
	Dim pageview = doc.Views.AddPageView(String.Format("A0_{0}",page_number), 1189, 841)
	If pageview IsNot Nothing Then
	  Dim top_left As New Rhino.Geometry.Point2d(20,821)
	  Dim bottom_right As New Rhino.Geometry.Point2d(1169, 20)
	  Dim detail = pageview.AddDetailView("ModelView", top_left, bottom_right, Rhino.Display.DefinedViewportProjection.Top)
	  If detail IsNot Nothing Then
		pageview.SetActiveDetail(detail.Id)
		detail.Viewport.ZoomExtents()
		detail.DetailGeometry.IsProjectionLocked = True
		detail.DetailGeometry.SetScale(1, doc.ModelUnitSystem, 10, doc.PageUnitSystem)
		' Commit changes tells the document to replace the document's detail object
		' with the modified one that we just adjusted
		detail.CommitChanges()
	  End If
	  pageview.SetPageAsActive()
	  doc.Views.ActiveView = pageview
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

# Generate a layout with a single detail view that zooms
# to a list of objects
def AddLayout():
    scriptcontext.doc.PageUnitSystem = Rhino.UnitSystem.Millimeters
    page_views = scriptcontext.doc.Views.GetPageViews()
    page_number = 1
    if page_views: page_number = len(page_views) + 1
    pageview = scriptcontext.doc.Views.AddPageView("A0_{0}".format(page_number), 1189, 841)
    if pageview:
        top_left = Rhino.Geometry.Point2d(20,821)
        bottom_right = Rhino.Geometry.Point2d(1169, 20)
        detail = pageview.AddDetailView("ModelView", top_left, bottom_right, Rhino.Display.DefinedViewportProjection.Top)
        if detail:
            pageview.SetActiveDetail(detail.Id)
            detail.Viewport.ZoomExtents()
            detail.DetailGeometry.IsProjectionLocked = True
            detail.DetailGeometry.SetScale(1, scriptcontext.doc.ModelUnitSystem, 10, scriptcontext.doc.PageUnitSystem)
            # Commit changes tells the document to replace the document's detail object
            # with the modified one that we just adjusted
            detail.CommitChanges()
        pageview.SetPageAsActive()
        scriptcontext.doc.Views.ActiveView = pageview
        scriptcontext.doc.Views.Redraw()

if __name__=="__main__":
    AddLayout()
```
{: #py .tab-pane .fade .in}


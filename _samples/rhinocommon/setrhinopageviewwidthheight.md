---
layout: code-sample
author:
platforms: ['Cross-Platform']
apis: ['RhinoCommon']
languages: ['C#', 'Python', 'VB.NET']
title: Set RhinoPageView Width and Height
keywords: ['rhinopageview', 'width', 'height']
categories: ['Other']
description:
order: 1
---

```cs
partial class Examples
{
  public static Result SetRhinoPageViewWidthAndHeight(RhinoDoc doc)
  {
    var width = 1189;
    var height = 841;
    var page_views = doc.Views.GetPageViews();
    int page_number = (page_views==null) ? 1 : page_views.Length + 1;
    var pageview = doc.Views.AddPageView(string.Format("A0_{0}",page_number), width, height);

    int new_width = width;
    var rc = RhinoGet.GetInteger("new width", false, ref new_width);
    if (rc != Result.Success || new_width <= 0) return rc;

    int new_height = height;
    rc = RhinoGet.GetInteger("new height", false, ref new_height);
    if (rc != Result.Success || new_height <= 0) return rc;

    pageview.PageWidth = new_width;
    pageview.PageHeight = new_height;
    doc.Views.Redraw();
    return Result.Success;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Partial Friend Class Examples
  Public Shared Function SetRhinoPageViewWidthAndHeight(ByVal doc As RhinoDoc) As Result
	Dim width = 1189
	Dim height = 841
	Dim page_views = doc.Views.GetPageViews()
	Dim page_number As Integer = If(page_views Is Nothing, 1, page_views.Length + 1)
	Dim pageview = doc.Views.AddPageView(String.Format("A0_{0}",page_number), width, height)

	Dim new_width As Integer = width
	Dim rc = RhinoGet.GetInteger("new width", False, new_width)
	If rc IsNot Result.Success OrElse new_width <= 0 Then
		Return rc
	End If

	Dim new_height As Integer = height
	rc = RhinoGet.GetInteger("new height", False, new_height)
	If rc IsNot Result.Success OrElse new_height <= 0 Then
		Return rc
	End If

	pageview.PageWidth = new_width
	pageview.PageHeight = new_height
	doc.Views.Redraw()
	Return Result.Success
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
from Rhino import *
from Rhino.Commands import *
from Rhino.Input import *
from scriptcontext import doc

def RunCommand():
  width = 1189
  height = 841
  page_views = doc.Views.GetPageViews()
  page_number = 1 if page_views==None else page_views.Length + 1
  pageview = doc.Views.AddPageView("A0_{0}".format(page_number), width, height)

  new_width = width
  rc, new_width = RhinoGet.GetInteger("new width", False, new_width)
  if rc != Result.Success or new_width <= 0: return rc

  new_height = height
  rc, new_height = RhinoGet.GetInteger("new height", False, new_height)
  if rc != Result.Success or new_height <= 0: return rc

  pageview.PageWidth = new_width
  pageview.PageHeight = new_height
  doc.Views.Redraw()
  return Result.Success

if __name__ == "__main__":
  RunCommand()
```
{: #py .tab-pane .fade .in}


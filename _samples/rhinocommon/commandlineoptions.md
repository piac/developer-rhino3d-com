---
layout: code-sample
author:
platforms: ['Cross-Platform']
apis: ['RhinoCommon']
languages: ['C#', 'Python', 'VB.NET']
title: Add Command Line Options
keywords: ['add', 'command', 'line', 'options']
categories: ['Adding Objects']
description:
order: 1
---

```cs
partial class Examples
{
  public static Rhino.Commands.Result CommandLineOptions(Rhino.RhinoDoc doc)
  {
    // For this example we will use a GetPoint class, but all of the custom
    // "Get" classes support command line options.
    Rhino.Input.Custom.GetPoint gp = new Rhino.Input.Custom.GetPoint();
    gp.SetCommandPrompt("GetPoint with options");

    // set up the options
    Rhino.Input.Custom.OptionInteger intOption = new Rhino.Input.Custom.OptionInteger(1, 1, 99);
    Rhino.Input.Custom.OptionDouble dblOption = new Rhino.Input.Custom.OptionDouble(2.2, 0, 99.9);
    Rhino.Input.Custom.OptionToggle boolOption = new Rhino.Input.Custom.OptionToggle(true, "Off", "On");
    string[] listValues = new string[] { "Item0", "Item1", "Item2", "Item3", "Item4" };

    gp.AddOptionInteger("Integer", ref intOption);
    gp.AddOptionDouble("Double", ref dblOption);
    gp.AddOptionToggle("Boolean", ref boolOption);
    int listIndex = 3;
    int opList = gp.AddOptionList("List", listValues, listIndex);

    while (true)
    {
      // perform the get operation. This will prompt the user to input a point, but also
      // allow for command line options defined above
      Rhino.Input.GetResult get_rc = gp.Get();
      if (gp.CommandResult() != Rhino.Commands.Result.Success)
        return gp.CommandResult();

      if (get_rc == Rhino.Input.GetResult.Point)
      {
        doc.Objects.AddPoint(gp.Point());
        doc.Views.Redraw();
        Rhino.RhinoApp.WriteLine("Command line option values are");
        Rhino.RhinoApp.WriteLine(" Integer = {0}", intOption.CurrentValue);
        Rhino.RhinoApp.WriteLine(" Double = {0}", dblOption.CurrentValue);
        Rhino.RhinoApp.WriteLine(" Boolean = {0}", boolOption.CurrentValue);
        Rhino.RhinoApp.WriteLine(" List = {0}", listValues[listIndex]);
      }
      else if (get_rc == Rhino.Input.GetResult.Option)
      {
        if (gp.OptionIndex() == opList)
          listIndex = gp.Option().CurrentListOptionIndex;
        continue;
      }
      break;
    }
    return Rhino.Commands.Result.Success;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Partial Friend Class Examples
  Public Shared Function CommandLineOptions(ByVal doc As Rhino.RhinoDoc) As Rhino.Commands.Result
	' For this example we will use a GetPoint class, but all of the custom
	' "Get" classes support command line options.
	Dim gp As New Rhino.Input.Custom.GetPoint()
	gp.SetCommandPrompt("GetPoint with options")

	' set up the options
	Dim intOption As New Rhino.Input.Custom.OptionInteger(1, 1, 99)
	Dim dblOption As New Rhino.Input.Custom.OptionDouble(2.2, 0, 99.9)
	Dim boolOption As New Rhino.Input.Custom.OptionToggle(True, "Off", "On")
	Dim listValues() As String = { "Item0", "Item1", "Item2", "Item3", "Item4" }

	gp.AddOptionInteger("Integer", intOption)
	gp.AddOptionDouble("Double", dblOption)
	gp.AddOptionToggle("Boolean", boolOption)
	Dim listIndex As Integer = 3
	Dim opList As Integer = gp.AddOptionList("List", listValues, listIndex)

	Do
	  ' perform the get operation. This will prompt the user to input a point, but also
	  ' allow for command line options defined above
	  Dim get_rc As Rhino.Input.GetResult = gp.Get()
	  If gp.CommandResult() <> Rhino.Commands.Result.Success Then
		Return gp.CommandResult()
	  End If

	  If get_rc Is Rhino.Input.GetResult.Point Then
		doc.Objects.AddPoint(gp.Point())
		doc.Views.Redraw()
		Rhino.RhinoApp.WriteLine("Command line option values are")
		Rhino.RhinoApp.WriteLine(" Integer = {0}", intOption.CurrentValue)
		Rhino.RhinoApp.WriteLine(" Double = {0}", dblOption.CurrentValue)
		Rhino.RhinoApp.WriteLine(" Boolean = {0}", boolOption.CurrentValue)
		Rhino.RhinoApp.WriteLine(" List = {0}", listValues(listIndex))
	  ElseIf get_rc Is Rhino.Input.GetResult.Option Then
		If gp.OptionIndex() = opList Then
		  listIndex = gp.Option().CurrentListOptionIndex
		End If
		Continue Do
	  End If
	  Exit Do
	Loop
	Return Rhino.Commands.Result.Success
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
import Rhino
import scriptcontext

def CommandLineOptions():
    # For this example we will use a GetPoint class, but all of the custom
    # "Get" classes support command line options.
    gp = Rhino.Input.Custom.GetPoint()
    gp.SetCommandPrompt("GetPoint with options")
    
    # set up the options
    intOption = Rhino.Input.Custom.OptionInteger(1, 1, 99)
    dblOption = Rhino.Input.Custom.OptionDouble(2.2, 0, 99.9)
    boolOption = Rhino.Input.Custom.OptionToggle(True, "Off", "On")
    listValues = "Item0", "Item1", "Item2", "Item3", "Item4"
    
    gp.AddOptionInteger("Integer", intOption)
    gp.AddOptionDouble("Double", dblOption)
    gp.AddOptionToggle("Boolean", boolOption)
    listIndex = 3
    opList = gp.AddOptionList("List", listValues, listIndex)
    while True:
        # perform the get operation. This will prompt the user to
        # input a point, but also allow for command line options
        # defined above
        get_rc = gp.Get()
        if gp.CommandResult()!=Rhino.Commands.Result.Success:
            return gp.CommandResult()
        if get_rc==Rhino.Input.GetResult.Point:
            point = gp.Point()
            scriptcontext.doc.Objects.AddPoint(point)
            scriptcontext.doc.Views.Redraw()
            print "Command line option values are"
            print " Integer =", intOption.CurrentValue
            print " Double =", dblOption.CurrentValue
            print " Boolean =", boolOption.CurrentValue
            print " List =", listValues[listIndex]
        elif get_rc==Rhino.Input.GetResult.Option:
            if gp.OptionIndex()==opList:
              listIndex = gp.Option().CurrentListOptionIndex
            continue
        break
    return Rhino.Commands.Result.Success


if __name__ == "__main__":
    CommandLineOptions()

```
{: #py .tab-pane .fade .in}


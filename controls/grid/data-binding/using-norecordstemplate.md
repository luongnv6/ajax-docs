---
title: Using NoRecordsTemplate
page_title: Using NoRecordsTemplate | UI for ASP.NET AJAX Documentation
description: Using NoRecordsTemplate
slug: grid/data-binding/using-norecordstemplate
tags: using,norecordstemplate
published: True
position: 3
---

# Using NoRecordsTemplate



## 

Each __GridTableView__ has a property __NoRecordsTemplate__. This property defines a template that will be displayed if there are no records in the assigned __DataSource__.

There are cases in which you may want to show an empty grid rather than this template. There is a boolean property __EnableNoRecordsTemplate__ which defines whether __GridTableView__ will use the defined __NoRecordsTemplate__ or not.

The __NoRecordsTemplate__ should be populated for each detail table (in case of hierarchical grids) in the __DetailTableDataBind__ event.

You can control the visibility of thetable/NoRecordsTemplate controls by using corresponding Controls(0), Controls(1) of each __GridTableView__. This should happen after it was data-bound.

````ASPNET
	  <telerik:RadGrid ID="RadGrid1" runat="server">
	    <MasterTableView>
	      <NoRecordsTemplate>
	        <div>
	          There are no records to display</div>
	      </NoRecordsTemplate>
	    </MasterTableView>
	  </telerik:RadGrid>
````



__Define NoRecordsTemplate programmatically__

You need to design your custom class (holding the set of controls for the __NoRecordsTemplate__) which implements the __ITemplate__ interface. Then you can assign an instance of this class to the __NoRecordsTemplate__ of the corresponding __GridTableView__.

The example below shows how to embed MS Label in the NoRecordsTemplate of the MasterTableView at runtime:

>tabbedCode

````C#
	
	protected RadGrid RadGrid1;
	
	public class MyNoRecordsTemplate : ITemplate
	{
	       Label NoRecordsLabel;
	        public void System.Web.UI.ITemplate.InstantiateIn(System.Web.UI.Control container)
	        {
	            NoRecordsLabel = new Label();
	            NoRecordsLabel.ID = "NoRecordsLabel";
	            NoRecordsLabel.BackColor = System.Drawing.Color.Orange;
	            NoRecordsLabel.BorderWidth = Unit.Pixel(1);
	            NoRecordsLabel.BorderColor = System.Drawing.Color.Brown;
	            NoRecordsLabel.Text = "No data to display";
	            container.Controls.Add(NoRecordsLabel);
	        }
	}
	protected override void OnInit(EventArgs e)
	{
	        base.OnInit(e);
	        PopulateGrid1OnPageInit();
	}
	protected void PopulateGrid1OnPageInit()
	{
	        RadGrid RadGrid1 = new RadGrid();
	        RadGrid1.ID = "RadGrid1";
	        RadGrid1.MasterTableView.AutoGenerateColumns = false;
	        RadGrid1.DataSource = new Object [0];
	        RadGrid1.EnableAJAX = true;
	        RadGrid1.MasterTableView.AllowPaging = true;
	        RadGrid1.MasterTableView.NoRecordsTemplate = new MyNoRecordsTemplate();
	
	        RadGrid1.PagerStyle.Mode = GridPagerMode.NumericPages;
	        RadGrid1.AllowSorting = true;
	      //runtime column definitions
	}
	          
````



````VB.NET
	    Public Class NoRecordsTemplate
	        Implements ITemplate
	
	        Public Sub InstantiateIn(ByVal container As System.Web.UI.Control) Implements System.Web.UI.ITemplate.InstantiateIn
	            Dim NoRecordsLabel As New Label()
	            With NoRecordsLabel
	                .ID = "NoRecordsLabel"
	                .BackColor = System.Drawing.Color.Orange
	                .BorderWidth = Unit.Pixel(1)
	                .BorderColor = System.Drawing.Color.Brown
	                .Text = "No data to display"
	            End With
	            container.Controls.Add(NoRecordsLabel)
	        End Sub
	    End Class
	
	    Protected Overloads Overrides Sub OnInit(ByVal e As EventArgs) Handles MyBase.OnInit
	        MyBase.OnInit(e)
	        PopulateGrid1OnPageInit()
	    End Sub
	
	    Protected Sub PopulateGrid1OnPageInit()
	        Dim RadGrid1 As New RadGrid()
	        RadGrid1.ID = "RadGrid1"
	        RadGrid1.MasterTableView.AutoGenerateColumns = False
	        RadGrid1.DataSource = New Object() {}
	        RadGrid1.EnableAJAX = True
	        RadGrid1.MasterTableView.AllowPaging = True
	        RadGrid1.MasterTableView.NoRecordsTemplate = New MyNoRecordsTemplate()
	        RadGrid1.PagerStyle.Mode = GridPagerMode.NumericPages
	        RadGrid1.AllowSorting = True
	        'runtime column definitions
	    End Sub
````


>end

Detailed information about how to create templates programmatically you can find in the __MSDN__: [http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dv_vstechart/html/vstechart.asp](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dv_vstechart/html/vbtchcreatingwebservercontroltemplatesprogrammatically.asp)
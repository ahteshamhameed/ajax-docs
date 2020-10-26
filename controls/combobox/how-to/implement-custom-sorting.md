---
title: Implement Custom Sorting
page_title: Implement Custom Sorting | RadComboBox for ASP.NET AJAX Documentation
description: Implement Custom Sorting
slug: combobox/how-to/implement-custom-sorting
tags: implement,custom,sorting
published: True
position: 3
---

# Implement Custom Sorting



## Sorting items by Value

By default, **RadComboBox** sorts items by their **Text** property. This article will show you how to implement custom sorting - the items will be sorted by their **Value** property.

For this purpose, we will use the **IComparer** interface which exposes a method that compares two objects.

Here are the two steps that you need to perform:

1. Create a class that implements **IComparer** for your custom sorting:



````C#
	     
public class SortComboItemsByValue : IComparer
{
   public int Compare(object x, object y)
   {
	   RadComboBoxItem p1 = new RadComboBoxItem();
	   RadComboBoxItem p2 = new RadComboBoxItem();
	   if (x is RadComboBoxItem)
		   p1 = x as RadComboBoxItem;
	   else
		   throw new ArgumentException("Object is not of type RadComboBoxItem.");
	   if (y is RadComboBoxItem)
		   p2 = y as RadComboBoxItem;
	   else
		   throw new ArgumentException("Object is not of type RadComboBoxItem.");
	   int cmp = 0;
	   if (p1.ComboBoxParent.Sort == RadComboBoxSort.Ascending)
	   {
		   //here we compare the Values of the items
		   cmp = String.Compare(p1.Value, p2.Value, !p1.ComboBoxParent.SortCaseSensitive);
	   }
	   if (p1.ComboBoxParent.Sort == RadComboBoxSort.Descending)
	   {
		   //here we compare the Values of the items
		   cmp = String.Compare(p1.Value, p2.Value, !p1.ComboBoxParent.SortCaseSensitive) * -1;
	   }
	   return cmp;
   }
} 			
````
````VB.NET
		
Public Class SortComboItemsByValue
	Implements IComparer
	Public Function Compare(ByVal x As Object, ByVal y As Object) As Integer Implements IComparer.Compare
		Dim p1 As New RadComboBoxItem()
		Dim p2 As New RadComboBoxItem()
		If TypeOf x Is RadComboBoxItem Then
			p1 = TryCast(x, RadComboBoxItem)
		Else
			Throw New ArgumentException("Object is not of type RadComboBoxItem.")
		End If
		If TypeOf y Is RadComboBoxItem Then
			p2 = TryCast(y, RadComboBoxItem)
		Else
			Throw New ArgumentException("Object is not of type RadComboBoxItem.")
		End If
		Dim cmp As Integer = 0
		If p1.ComboBoxParent.Sort = RadComboBoxSort.Ascending Then
			'here we compare the Values of the items
			cmp = [String].Compare(p1.Value, p2.Value, Not p1.ComboBoxParent.SortCaseSensitive)
		End If
		If p1.ComboBoxParent.Sort = RadComboBoxSort.Descending Then
			'here we compare the Values of the items
			cmp = [String].Compare(p1.Value, p2.Value, Not p1.ComboBoxParent.SortCaseSensitive) * -1
		End If
		Return cmp
	End Function
End Class
	
````


2. Call the overloaded **SortItems** or **Items.Sort** methods passing your IComparer as a parameter:



````C#
	     
RadComboBox2.Sort = RadComboBoxSort.Ascending;
RadComboBox2.SortItems(new SortComboItemsByValue());
				
````
````VB.NET
	
RadComboBox2.Sort = RadComboBoxSort.Ascending
RadComboBox2.SortItems(New SortComboItemsByValue())
	
````


That's it. Now the combobox items will be sorted by their **Values** instead of Text.

## Custom sorting with checked items on top

When using RadComboBox with enabled checkbox, common issue is how to bring the checked items on top of the sorted dropdown. This can be achieved by adding additional check in the custom comparer class from the sample above

Sample declaration:

````ASPX
<telerik:RadComboBox runat="server" AutoPostBack="true" OnItemChecked="RadComboBox1_ItemChecked" ID="RadComboBox1" CheckBoxes="true">
    <Items>
        <telerik:RadComboBoxItem Text="Item 1" Value="1" />
        <telerik:RadComboBoxItem Text="Item 2" Value="2" />
        <telerik:RadComboBoxItem Text="Item 3" Value="3" />
        <telerik:RadComboBoxItem Text="Item 4" Value="4" />
        <telerik:RadComboBoxItem Text="Item 5" Value="5" />
        <telerik:RadComboBoxItem Text="Item 6" Value="6" />
    </Items>
</telerik:RadComboBox>
````

Code-behind:

````C#
protected void Page_Load(object sender, EventArgs e)
{
    RadComboBox1.Sort = RadComboBoxSort.Ascending;
    RadComboBox1.SortItems(new SortCheckedComboItemsFirst());
}
public class SortCheckedComboItemsFirst : IComparer
{
    public int Compare(object x, object y)
    {
        RadComboBoxItem p1 = new RadComboBoxItem();
        RadComboBoxItem p2 = new RadComboBoxItem();
        if (x is RadComboBoxItem)
            p1 = x as RadComboBoxItem;
        else
            throw new ArgumentException("Object is not of type RadComboBoxItem.");
        if (y is RadComboBoxItem)
            p2 = y as RadComboBoxItem;
        else
            throw new ArgumentException("Object is not of type RadComboBoxItem.");
        int cmp = 0;

        if (p1.Checked)
        {
            if (p2.Checked == false)
            {
                return -1;
            }
            // uncomment for skipping the sorting of the checked items
            //else
            //{                   
            //    return 1;
            //}
        }
        else if (p2.Checked)
        {
            return 1;
        }

        if (p1.ComboBoxParent.Sort == RadComboBoxSort.Ascending)
        {
            //here we compare the Values of the items
            cmp = String.Compare(p1.Value, p2.Value, !p1.ComboBoxParent.SortCaseSensitive);
        }
        if (p1.ComboBoxParent.Sort == RadComboBoxSort.Descending)
        {
            //here we compare the Values of the items
            cmp = String.Compare(p1.Value, p2.Value, !p1.ComboBoxParent.SortCaseSensitive) * -1;
        }
        return cmp;
    }
}

protected void RadComboBox1_ItemChecked(object sender, RadComboBoxItemEventArgs e)
{

}
````
````VB.NET
Protected Sub Page_Load(ByVal sender As Object, ByVal e As EventArgs) Handles Me.Load
    RadComboBox1.Sort = RadComboBoxSort.Ascending
    RadComboBox1.SortItems(New SortCheckedComboItemsFirst())
End Sub

Public Class SortCheckedComboItemsFirst
    Implements IComparer
    Public Function Compare(ByVal x As Object, ByVal y As Object) As Integer Implements IComparer.Compare
        Dim p1 As New RadComboBoxItem()
        Dim p2 As New RadComboBoxItem()

        If TypeOf x Is RadComboBoxItem Then
            p1 = TryCast(x, RadComboBoxItem)
        Else
            Throw New ArgumentException("Object is not of type RadComboBoxItem.")
        End If

        If TypeOf y Is RadComboBoxItem Then
            p2 = TryCast(y, RadComboBoxItem)
        Else
            Throw New ArgumentException("Object is not of type RadComboBoxItem.")
        End If

        Dim cmp As Integer = 0

        If p1.Checked Then

            If p2.Checked = False Then
                Return -1
			'uncomment for skipping the sorting of the checked items
			'Else
			'   Return 1
            End If
        ElseIf p2.Checked Then
            Return 1
        End If

        If p1.ComboBoxParent.Sort = RadComboBoxSort.Ascending Then
            'here we compare the Values of the items
            cmp = [String].Compare(p1.Value, p2.Value, Not p1.ComboBoxParent.SortCaseSensitive)
        End If
        If p1.ComboBoxParent.Sort = RadComboBoxSort.Descending Then
            'here we compare the Values of the items
            cmp = [String].Compare(p1.Value, p2.Value, Not p1.ComboBoxParent.SortCaseSensitive) * -1
        End If
        Return cmp
    End Function
End Class

Protected Sub RadComboBox1_ItemChecked(sender As Object, e As RadComboBoxItemEventArgs)

End Sub
````
 

# See Also

 * [Sorting]({%slug combobox/functionality/sorting%})
